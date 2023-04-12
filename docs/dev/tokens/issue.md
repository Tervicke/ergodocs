# Issuing a token

> 🔗 From [EIP-0004](eip4.md)

Ergo supports custom tokens as **first-class citizens**.

- A special [register](registers.md) `R2` of a [box](box.md) contains (tokenId -> amount) pairs.
- A box can contain **at most 255 secondary tokens**. 
- However, there are also some indirect limits: 
    - A box can be no more than 4 kilobytes
    - Tokens add to the computational cost of the transaction.

## Examples

- [Mint a token with Fleet SDK](https://fleet-sdk.github.io/docs/transaction-building#step-4-2-mint-a-token)

## Resources

- [Token category on sigmaverse.io](https://sigmaverse.io/all-projects/?category=Tokens)
- [Ergo Token Minter](https://thierrym1212.github.io/tokenminter/index.html) or [CYTI](https://thierrym1212.github.io/cyti/index.html) which uses a Use CYTI minable smart contract to choose your token ID.
- [ergoutils.org](https://ergoutils.org/#/token)
- [Video Tutorial](https://www.youtube.com/watch?v=I3R6_PceM1k)



