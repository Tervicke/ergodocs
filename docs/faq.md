# FAQ

This page aims to provide a background on Ergo and answers to some of the most frequently asked questions. 

## Background

- Ergo is currently available on the following [wallets](https://ergoplatform.org/en/wallets/) and [exchanges](https://ergoplatform.org/en/exchanges/). 
- The development roadmap can be seen [here](https://ergoplatform.org/en/ecosystem/#Roadmap).
- To see the applications currently running on Ergo, check out [sigmaverse.io](https://sigmaverse.io/).
- To read about Ergo from a less technical perspective, visit [ergonaut.space](https://ergonaut.space/en/home). 
- If you want to mine, see the [Miners Handbook](https://ergonaut.space/en/Guides/Mining).

### Why '*Ergo*'? 

Ergo means "therefore" in Latin but "work" in Greek. This is also a play on the fact that the cryptocurrency's design is ***ergo***nomical.

### How does it differ from Bitcoin?

The Ergo project is a cryptocurrency that builds upon the same UTXO model as Bitcoin but extends its functionality with additional features. Ergo allows for more complex programmability by providing access to the entire spending transaction and the block solution in the execution context. This enables the creation of Turing-complete contracts and the implementation of contractual money, where digital coins can be explicitly bound to a contract in the form of executable code.

## What is contractual money?

Contractual money is digital money that is bound to a contract in the form of executable code, which enforces specific rules and conditions for its usage. This is in contrast to traditional money, where contracts are external to the money itself and may be in the form of laws, corporate terms, or informal agreements. Contractual money allows for more precise control over how the money is spent and can be used to implement various use cases, such as microcredit systems or local exchange trading systems.


### What is the *Ergo Foundation*?


The [Ergo Foundation](https://ergoplatform.org/en/foundation/) is a community-driven entity focused on:

  - Promoting non-breaking development of Ergo Platform protocol;
  - Promoting the widespread adoption and use of Ergo Platform and its native token (ERG);
  - Developing the ecosystem around the Ergo Platform;
  - Promoting the use of Ergo Platform and blockchain technology for social good;
  - Supporting truly decentralised infrastructure and;
  - Supporting privacy as a basic human right.


To fund development, promotion, events, and any other activities which may advance the platform, Ergo has in place a Treasury, which will receive **4.43%** of the Ergs released during emission. During the first two years post‐mainnet launch, the Treasury received 7.5 Ergs per block. 

### What is the [Emission Schedule](https://ergoplatform.org/en/blog/2019_05_20-curve/)?

Ergo has a maximum supply of **97,739,925** Ergs, to be completed by 2045. The block reward lowers to 3ERG in 2026. You can see this emission schedule on [ergo.watch](https://ergo.watch/emission)

### When was Ergo launched?

Mainnet July 2019. Before this, there was *Ergo-First-Year-Token*

**What is EFYT?**

Ergo-First-Year-Token was airdropped and distributed on Waves DEX starting with a 100,000 EFYT airdrop in May 2017. EFYT served the dual purposes of helping build an early community of stakeholders and enthusiasts for Ergo and raising a small number of funds for the platform before launch to fund development, promotion etc. EFYT is strictly a Waves token and is not the same as an Erg; the Ergo mainnet native token is mined after Ergo's mainnet launch.

The max supply of EFYT is 1,970,945.0. This is 10% of the first year of Ergo token emission and the same number of Ergs that the Treasury will receive, meaning that the Treasury will have received 1,970,945.0 Ergs during year 1, sufficient to swap the max supply of EFYT for Erg.

### Why 97,739,924?

> A pre-agreed smart contract controls emission in Ergo, so we tried to have a simple enough emission curve with the total limited supply being close to 100M (and emission to be done in 8-10 years).

The max supply is simply the amount needed to create the initial genesis state: 

- A box with proof-of-no-premine (1 ERG)
- [Foundation treasury](https://explorer.ergoplatform.com/en/addresses/4L1ktFSzm3SH1UioDuUf5hyaraHird4D2dEACwQ1qHGjSKtA6KaNvSzRCZXZGf9jkfNAEC1SrYaZmCuvb2BKiXk5zW9xuvrXFT7FdNe2KqbymiZvo5UQLAm5jQY8ZBRhTZ4AFtZa1UF5nd4aofwPiL7YkJuyiL5hDHMZL1ZnyL746tHmRYMjAhCgE7d698dRhkdSeVy) (4,330,791.5 ERG)
- [Miner Reward Box](https://explorer.ergoplatform.com/en/addresses/2Z4YBkDsDvQj8BX7xiySFewjitqp2ge9c99jfes2whbtKitZTxdBYqbrVZUvZvKv6aqn9by4kp3LE1c26LCyosFnVnm6b6U1JYvWpYmL2ZnixJbXLjWAWuBThV1D6dLpqZJYQHYDznJCk49g5TUiS4q8khpag2aNmHwREV7JSsypHdHLgJT7MGaw51aJfNubyzSKxZ4AJXFS27EfXwyCLzW1K6GVqwkJtCoPvrcLqmqwacAWJPkmh78nke9H4oT88XmSbRt2n9aWZjosiZCafZ4osUDxmZcc5QVEeTWn8drSraY3eFKe8Mu9MSCcVU) with the required ERG for 2,080,800 Blocks according to the emission schedule until rewards equal 0 and storage rent and EIP-27-reemission-box takes over (93,409,132 ERG). 

The treasury box is protected by a vesting smart contract that ensures an initial unlocked amount and then only releases an amount of ERG that provides funds for 2.5 years (never exceeding 10% of the circulating supply). All of this results in these specific amounts.

In total, this happens to be 97,739,924.5 ERG.

For proof-of-no-premine, the pre-genesis state in Ergo contains block hashes from Bitcoin and Eth and also headlines from the Guardian, Vedomosti and Xinhua around the moment of launch, which can be seen in [mainnet.conf](https://github.com/ergoplatform/ergo/blob/1935c95560a30b19cdb52c1a291e8a389ba63c97/src/main/resources/mainnet.conf#L11)

```scala
   /**
    * Generates a genesis box that contains proofs of no premine.
    * This is a long-living box with special bytes in registers.
    * @param chainSettings Chain settings of the Ergo network
    * @return The genesis box with the given properties
    */
  private def noPremineBox(chainSettings: ChainSettings): ErgoBox = {
    // create a map of ErgoBox non-mandatory registers with the premine proofs
    val proofsBytes = chainSettings.noPremineProof.map(b => ByteArrayConstant(b.getBytes("UTF-8")))
    val proofs = ErgoBox.nonMandatoryRegisters.zip(proofsBytes).toMap
    // create a genesis box with a value of CoinsInOneErgo, a proposition script of FalseLeaf, an empty tokens sequence, and the premine proofs in non-mandatory registers
    createGenesisBox(EmissionRules.CoinsInOneErgo, Constants.FalseLeaf, Seq.empty, proofs)
  }

```

```JSON
 {
"boxId": "b8ce8cfe331e5eadfb0783bdc375c94413433f65e1e45857d71550d42e4d83bd",
"value": 1000000000,
"ergoTree": "10010100d17300",
"assets": [],
"creationHeight": 0,
"additionalRegisters": {
  "R5": "0e42307864303761393732393334363864393133326335613261646162326535326132333030396536373938363038653437623064323632336337653365393233343633",
  "R6": "0e464272657869743a20626f746820546f727920736964657320706c617920646f776e207269736b206f66206e6f2d6465616c20616674657220627573696e65737320616c61726d",
  "R8": "0e45d094d0b8d0b2d0b8d0b4d0b5d0bdd0b4d18b20d0a7d0a2d09fd09720d0b2d18bd180d0b0d181d182d183d18220d0bdd0b02033332520d0bdd0b020d0b0d0bad186d0b8d18e",
  "R7": "0e54e8bfb0e8af84efbc9ae5b9b3e8a1a1e38081e68c81e7bbade38081e58c85e5aeb9e28094e28094e696b0e697b6e4bba3e5ba94e5afb9e585a8e79083e58c96e68c91e68898e79a84e4b8ade59bbde4b98be98193",
  "R4": "0e4030303030303030303030303030303030303031346332653265376533336435316165376536366636636362363934326333343337313237623336633333373437"
}
```
The code for the emission schedule can be found [here](https://github.com/ergoplatform/ergo/blob/e6086e23ecd45f1e01a3e4c0344f003cec1a5b11/src/test/scala/org/ergoplatform/mining/ErgoMinerPropSpec.scala#L24)




## Discussions

### Why Scala? 

Ergo's primary language is Scala. Similarly, the scripting language used by Ergo, ErgoScript, is also based on Scala, but the off-chain code can be written in any language. Developers have access to a growing selection of tools and Software Development Kits (SDKs) for JVM, Rust and JS/TS.


Scala has several features that set it apart from other JVM languages. 

- Firstly, it is truly cross-platform, as the same code can run on JVM and JavaScript natively. This is a feature that is not found in many other languages. 
- Additionally, key ecosystem libraries for Scala support all platforms, and the popularity of Scala.js and Scala-native is increasing. 
- Another advantage of Scala is its conciseness, both in terms of syntax and conceptual level. 
- Despite its high-level nature, Scala can also be more efficient than similar Java code due to its ability to use primitive unboxed types, and the ability of the Scala compiler to perform code specialization. 
- Furthermore, Scala is multi-paradigm, allowing for the combination of OOP, FP, and LP, making it suitable for a wide range of domains. 
- Lastly, Scala3 brings even more powerful features such as metaprogramming and tools for zero-cost abstractions.

### What about energy consumption? 

- [Proof of Work, Energy & Ergo](https://ergoplatform.org/en/blog/2022-03-29-proof-of-work-energy-and-ergo/)

### Why was non-outsourceability turned off?

Autolykos v1 originally had non-outsourceability built-in to prevent mining pools on Ergo. However, it became apparent that it's only possible to avoid pools with smart contracts. So, they  (the miners) turned it off so that not only larger players could take advantage of the loophole. Ergo is now focusing on memory hardness to keep mining as fair as possible, which should help prevent ASICs mining at least. There are also some improvements for pooling, e.g. Stratum 2 protocol. 


> ["Bypassing Non-Outsourceable Proof-of-Work Schemes Using Collateralized Smart Contracts"](https://ia.cr/2020/044) was presented by Alex Chepurnoy at the WTSC workshop associated with Financial Cryptography and Data Security 2020 in Malaysia
{.is-info}


- It's also discussed here on 'Unblocked with Robert Kornacki' [(14:45)](https://www.youtube.com/watch?v=2sbTMrQwWOw&feature=youtu.be)

Mining pools have certain benefits just now being exposed by Ergo, like more equitable token distribution for dApps/ projects. This is now available to miners on GETBLOK.io, using the world's first *working* SmartPools/subpooling system.

### What about 51% Attacks?

Mining pools offer a buffer against network attacks as the hash rate is distributed across thousands of individual miners.

The memory hardened aspect of ergo also makes this attack vector more expensive as there is no ASIC support to rent. With the collective rentable rigs, there are more viable paths to a 51% attack. In theory, someone could build a massive GPU farm to try to launch such an attack. If a bad actor can rent a warehouse of ASIC and mine on a small chain with 51% attacks is a viable option.

Usually, this attack is made for profit, and massive dumping occurs on an exchange as it is occurring. The attacker will dump tokens on a business and then "double-spend" them back into their wallet. The current exchange situation doesn't provide the liquidity for a viable offramp, and the rentable ASIC support isn't an option. 

Other coins like Ethereum classic are a bad comparisons, as they shared the same mining algorithm as Eth. One could buy more than 100% of the hash rate of eth classic on NiceHash, and it's not the same case for Ergo. Ergo also believes in the 'Good Miner' principle; in the case of Bitcoin - it was a good thing 51% existed. 

### How fast is Ergo?

TPS (Transactions Per Second) is not a useful metric. On Ergo Reference Node v.5, TPS is estimated to be a minimum of 47.5 tx/s. However, transactions can happen in three scaling layers or levels:

- L0: Ergo Reference Nodes, which can be bootstrapped using NiPoPoWs proofs and UTXO set snapshots.
- L1: Ergo has extensions that allow for a wide variety of scaling solutions such as Sharding, Hydra, or BitcoinNG-style macroblocks.
- L2 (off-chain): Ergo should be compatible with the Lightning Network, Rainbow Network, and many more. The implementation here will depend on the needs of the applications being built on Ergo.

The general idea is that many transactions can happen in L1 or L2 and these transactions can be bundled and settled on the L0 layer of the Ergo blockchain using a single transaction. Thanks to the high flexibility of ErgoScript programming model, many different protocols are possible, each one solving scalability problem in a specific domain (like simple payment transactions).
Ergo blockchain can be thought as common settlement layer for many L1/L2 protocols and applications.

See the [scaling](scaling.md) page for more information.

## Is Proof of Useful Work being considered?

While Proof of Useful Work is an interesting idea, it is still in its research phase. Ergo is open to implementing new ideas. But, a radical change to its consensus mechanism that requires a hard fork would likely be outside the scope and resources of Ergo's small core development team and limited budget.


## How can I stake my Erg?

Ergo is a PoW (**Proof of Work**) coin, not a PoS (**Proof of Stake**), which means that blocks are validated by miners, not by stakes; therefore, you can't stake Erg directly.

However, it is possible to earn some yield from your ERG in combination with Ergo in liquidity pools, tokenisation of dApps, trading bots, lending platforms, and other mechanisms. 

You can 'stake' native tokens on Ergo in some form (on ergopad.io *live*, Night Owl Casino *soon*, ErgoMixer *soon*,+ more)  

For more info on earning off your Erg, look at the [Yield guide](https://ergonaut.space/en/Guides/yield).


## Quantum 

The development of practical quantum computers remains a subject of speculation, and their exact timeline is unclear. In anticipation of this potential threat, various post-quantum (PQ) digital signature schemes have been proposed, such as Lamport signatures. However, these PQ schemes often face limitations in terms of efficiency, thorough study, and standardization.

Ergo employs an efficient class of zero-knowledge proofs known as sigma-protocols, but the known post-quantum alternatives are still considered exotic and impractical for widespread use. As a result, it may be premature to implement any concrete changes to address the potential risks posed by quantum computing.

In the event of a crypto-disaster—such as the development of an efficient quantum computer, number-theoretical attacks on elliptic curves, or other unforeseen vulnerabilities—transitioning to a blockchain with robust post-quantum security measures would be the best course of action. 

Until the threat of quantum computing becomes more imminent or tangible, it may be more productive to focus on monitoring developments in the field, exploring potential post-quantum solutions, and considering strategies for smoothly transitioning to a more secure blockchain in the event of a crypto-disaster.

- [Quantum Computing and Resistance | Ergo Clips](https://www.youtube.com/watch?v=A5SJy7c3bfs&ab_channel=ErgoClips)

## EIPs

### What is Ergo's approach to Forking?

- **Velvet-Fork**: Only requires a minority of nodes to upgrade. Introduced by the NiPoPoW paper, the key idea is that you can use the scheme even if only some blocks in the chain include the interlink structure and allows for "gradual deployment" without harming the miners that haven't upgraded to the new rules. In this way, it acts similar to a soft fork in that clients that upgrade to new rules are still compatible with those that don't. 
- **Soft-fork**'s require some nodes to upgrade. Our recent re-emission Soft-Fork EIP37 was possible as it's enforced on miner nodes only via protocol rules. These can be approved with 90% support from miners. 
- **Hard-Fork** Requires all nodes to upgrade. 

Ergo follows a soft-forkability approach --- if a supermajority (90%+) of the network accepts a new feature, it is activated; however, old nodes that do not upgrade continue to operate normally and skip over this feature validation. Disruptive hard forks should be avoided in Ergo unless critical. 

### [EIP-0027](https://github.com/ergoplatform/eips/blob/master/eip-0027.md)

With the updated emission schedule described, re-emission (with 3 ERG re-emission rewards per block) would be enough for 4,566,336 blocks (~17.38 years).

### EIP-0037

The original Difficulty Adjustment Algorithm for Ergo worked well in most cases, including huge price drops, 100x initial difficulty misestimation during mainnet launch, and so on. However, the previous simplified and limitless version of the algorithm is bumpy. A big influx of mining hash rate over multiple epochs, especially with super-linear hash rate growth over time, may result in a huge difficulty spike. Similarly, a few slow epochs may cause a huge drop. Also, for dapps and other applications, it would be desirable to make difficulty readjustment more reactive (previously, readjustment takes place every 1024 blocks, and eight epochs, so about two weeks normally, are considered).

This was resolved with the [EIP-37](https://github.com/ergoplatform/eips/pull/79). 

EIP37 is a hard fork which makes the difficulty adjustment more reactive by shortening epoch length, amplifying the weight of the last epoch and some limits on difficulty changes. 
The 'epoch length' is to be set to 128 blocks. 
It calculates the difficulty in two ways according to the past eight epochs of 128 blocks each.
Then it takes an average from classic and predictive difficulties and limits the change so that the test can never be changed by more than 50% per epoch.


Broader conversations about [difficulty adjustments on ergoforum](https://www.ergoforum.org/t/diff-adjustment-potential-design-tradeoffs/3875)

