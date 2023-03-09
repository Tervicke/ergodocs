Another popular use-case of Ethereum is an Initial Coin Offering (ICO) contract. An ICO mirrors an Initial Public Offering (IPO) and provides a mechanism for a project to collect funding in some tokens and then issue “shares” (in the form of some other tokens) to investors.

Generally, an ICO comprises of 3 stages:

- [**Funding**](#funding): During this period, investors are allowed to fund the project.
- [**Issuance**](#issuance): A new asset token is created and issued to investors.
- [**Withdrawal**](#withdrawal): Investors can withdraw their newly issued tokens.

Our ICO contract is quite complex compared to the previous examples since it involves multiple stages and parties. The number of investors may run into thousands, and the naive solution would store this data in the contract, as in the [ERC-20 standard](https://theethereum.wiki/w/index.php/ERC20_Token_Standard).

Unlike Ethereum, Ergo does not permit storing large datasets in a contract. Rather, we store only a 40-bytes header of (a key, value) dictionary authenticated like a Merkle tree [13](https://eprint.iacr.org/2016/994). To access some elements in the dictionary or to modify it, a spending transaction should provide lookup or modification proofs. This allows a contract to authenticate large datasets using very little storage and memory.

## Funding

The project initiates the ICO by creating a box with the guard script given below. The box also contains an authenticating value for an empty dictionary of (investor, balance) pairs in R5, where an investor is the hash of a script that will guard the box with the withdrawn tokens (once the funding period ends).

```scala
// check if the index of the current input is 0
val selfIndexIsZero = INPUTS(0).id == SELF.id

// get the AVL tree proof from a register
val proof = getVar[Coll[Byte]](1).get

// collect pk and value of all inputs, except for the first one
val toAdd = INPUTS.slice(1, INPUTS.size).map({(b: Box) =>
    val pk = b.R4[Coll[Byte]].get
    val value = longToByteArray(b.value)
    (pk, value)
})

// insert the collected inputs into the AVL tree, using the proof
val modifiedTree = SELF.R5[AvlTree].get.insert(toAdd, proof).get

// get the expected AVL tree from the first output
val expectedTree = OUTPUTS(0).R5[AvlTree].get

// check if the self output is correct by comparing the script
// if the current height is less than 2000, compare the script to the current box
// otherwise, compare the script to the issuance script
val selfOutputCorrect =
    if (HEIGHT < 2000) OUTPUTS(0).propositionBytes == SELF.propositionBytes
    else OUTPUTS(0).propositionBytes == issuanceScript

// check if there is only one output and if the self output is correct
val outputsCorrect = OUTPUTS.size == 1 && selfOutputCorrect

// check if the index is 0, outputs are correct, and the expected tree matches the modified tree
selfIndexIsZero && outputsCorrect && modifiedTree == expectedTree

```

The first funding transaction spends this box and creates a box with the same script and updated data. Further funding transactions spend the box created from the previous funding transaction. The box checks that it is the first input of each funding transaction, which must have other input from investors. The investor inputs contain a hash of the withdrawal script in register R4. The script also checks (via proofs) that hashes and monetary values of the investing inputs are correctly added to the dictionary of the new box, which must be the only output with the correct amount of ergs (we ignore fee in this example). 

In this stage, which lasts until height 2,000, withdrawals are not permitted, and ergs can only be put into the project. The first transaction with a height of 2,000 or more should keep the same data but change the output's script, called issuanceScript, described next.

## Issuance

This stage requires only one transaction to get to the next stage (the withdrawal stage). The spending transaction makes the following modifications. Firstly, it changes the list of allowed operations on the dictionary from "inserts only" to "removals only". Secondly, the contract checks that the proper amount of ICO tokens are issued. In Ergo, each transaction can issue at most one new kind of token, with the (unique) identifier of the first input box. The issuance contract checks that a new token is issued with an amount equal to the nano-ergs collected till now. Thirdly, the contract checks that a spending transaction is indeed re-creating the box with the guard script corresponding to the next stage, the withdrawal stage. Finally, the contract checks that the spending transaction has two outputs (one for the project tokens and one for the ergs withdrawn by the project). The complete script is given below.

```scala
// Get the open and closed trees
val openTree = SELF.R5[AvlTree].get
val closedTree = OUTPUTS(0).R5[AvlTree].get

// Check that the digests, key lengths and values are the same
val correctDigest = openTree.digest == closedTree.digest
val correctKeyLength = openTree.keyLength == closedTree.keyLength
val correctValue = openTree.valueLengthOpt == closedTree.valueLengthOpt

// Check that the closed tree is a remove-only tree
val removeOnlyTree = closedTree.enabledOperations == 4

// Check that the token IDs and amounts are correct
val tokenId: Coll[Byte] = INPUTS(0).id
val tokenIssued = OUTPUTS(0).tokens(0)._2
val correctTokenNumber = OUTPUTS(0).tokens.size == 1 && OUTPUTS(1).tokens.size == 0
val correctTokenIssued = SELF.value == tokenIssued
val correctTokenId = OUTPUTS(0).R4[Coll[Byte]].get == tokenId && OUTPUTS(0).tokens(0)._1 == tokenId

// Check that the values have been preserved, the state has changed and the project public key is correct
val valuePreserved = OUTPUTS.size == 2 && correctTokenNumber && correctTokenIssued && correctTokenId
val stateChanged = OUTPUTS(0).propositionBytes == withdrawScript
val projectPubKey = SELF.R5[Coll[Byte]].get == projectPubKeyHash
val treeIsCorrect = correctDigest && correctValue && correctKeyLength && removeOnlyTree

// Check if the tree is correct, the values have been preserved and the state has changed
val stateIsCorrect = projectPubKey && treeIsCorrect && valuePreserved && stateChanged

```

## Withdrawal

Investors can now withdraw ICO tokens under a guard script whose hash is stored in the dictionary. Withdrawals are made in batches of N. A withdrawing transaction, thus, has N + 1 outputs; the first output carries over the withdrawal sub-contract and balance tokens, and the remaining N outputs have guard scripts and token values as per the dictionary. The contract requires two proofs for the dictionary elements: one proving that values to be withdrawn are indeed in the dictionary, and the second proving that the resulting dictionary does not have the withdrawn values. 

The complete script called `withdrawScript` is given below:

```scala
// Get removeProof and lookupProof
val removeProof = getVar[Coll[Byte]](2).get
val lookupProof = getVar[Coll[Byte]](3).get

// Get withdraw indexes and tokenId
val withdrawIndexes = getVar[Coll[Int]](4).get
val tokenId: Coll[Byte] = SELF.R4[Coll[Byte]].get

// Map over withdrawIndexes and find tokenIds
val withdrawals = withdrawIndexes.map({(idx: Int) =>
    val b = OUTPUTS(idx)
    if (b.tokens(0)._1 == tokenId)
        (blake2b256(b.propositionBytes), b.tokens(0)._2)
    else
        (blake2b256(b.propositionBytes), 0L)
    })

// Get withdrawValues and calculate the total amount withdrawn
val withdrawValues = withdrawals.map({(t: (Coll[Byte], Long)) => t._2})
val total = withdrawValues.fold(0L, {(l1: Long, l2: Long) => l1 + l2 })

// Get list of nodes to remove and removed values
val toRemove = withdrawals.map({(t: (Coll[Byte], Long)) => t._1})
val initialTree = SELF.R5[AvlTree].get
val removedValues = initialTree.getMany(toRemove, lookupProof).map(
    {(o: Option[Coll[Byte]]) => byteArrayToLong(o.get)}
    )

// Check if removedValues equals withdrawValues
val valuesCorrect = removedValues == withdrawValues

// Remove nodes and check if the outTree is correct
val modifiedTree = initialTree.remove(toRemove, removeProof).get
val outTreeCorrect = OUTPUTS(0).R5[AvlTree].get == modifiedTree

// Check if the tokenIds and amounts are correct
val selfTokenCorrect = SELF.tokens(0)._1 == tokenId
val outTokenCorrect = OUTPUTS(0).tokens(0)._1 == tokenId
val outTokenCorrectAmt = OUTPUTS(0).tokens(0)._2 + total == SELF.tokens(0)._2
val tokenPreserved = selfTokenCorrect && outTokenCorrect && outTokenCorrectAmt

// Check if the SELF and OUTPUTS are correct
val selfOutputCorrect = OUTPUTS(0).propositionBytes == SELF.propositionBytes
val outTreeCorrect = OUTPUTS(0).R5[AvlTree].get == modifiedTree

// Check if everything is correct
valuesCorrect && outTreeCorrect && selfOutputCorrect && tokenPreserved
```

Note that the above ICO example contains many simplifications. For instance, we don’t consider fees when spending the project box. 
Additionally, the project does not self-destruct after the withdrawal stage. We refer the reader to [14](https://ergoplatform.org/en/blog/2019_04_10-ico-example/) for the full example.