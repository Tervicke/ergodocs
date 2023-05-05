# Sigma Rust

[sigma-rust](https://github.com/ergoplatform/sigma-rust) is an alternative and simple implementation of ErgoTree interpreter and transaction-building tools. 

See [Architecture](https://github.com/ergoplatform/sigma-rust/blob/develop/docs/architecture.md) for high-level overview.

## Contributing
There is a labelled issues tab on [sigma-rust](https://github.com/ergoplatform/sigma-rust/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) that anyone can pick up.  If you are working on something, leave a comment, so others know. `@greenhat` is ready to assist with anyone interested [on Discord](https://discord.gg/Q86PNMwRsu).




## Crates

[ergoscript-compiler](https://github.com/ergoplatform/sigma-rust/tree/develop/ergoscript-compiler) [![Latest Version](https://img.shields.io/crates/v/ergoscript-compiler.svg)](https://crates.io/crates/ergoscript-compiler) [![Documentation](https://docs.rs/ergoscript-compiler/badge.svg)](https://docs.rs/crate/ergoscript-compiler)

ErgoScript compiler. 

[ergotree-ir](https://github.com/ergoplatform/sigma-rust/tree/develop/ergotree-ir) [![Latest Version](https://img.shields.io/crates/v/ergotree-ir.svg)](https://crates.io/crates/ergotree-ir) [![Documentation](https://docs.rs/ergotree-ir/badge.svg)](https://docs.rs/crate/ergotree-ir)

ErgoTree IR and serialization.

[ergotree-interpreter](https://github.com/ergoplatform/sigma-rust/tree/develop/ergotree-interpreter) [![Latest Version](https://img.shields.io/crates/v/ergotree-interpreter.svg)](https://crates.io/crates/ergotree-interpreter) [![Documentation](https://docs.rs/ergotree-interpreter/badge.svg)](https://docs.rs/crate/ergotree-interpreter)

ErgoTree interpreter.

[ergo-lib](https://github.com/ergoplatform/sigma-rust/tree/develop/ergo-lib) [![Latest Version](https://img.shields.io/crates/v/ergo-lib.svg)](https://crates.io/crates/ergo-lib) [![Documentation](https://docs.rs/ergo-lib/badge.svg)](https://docs.rs/crate/ergo-lib)

Chain types (transactions, boxes, etc.), JSON serialization, box selection for tx inputs, tx creation and signing.

[sigma-ser](https://github.com/ergoplatform/sigma-rust/tree/develop/sigma-ser) [![Latest Version](https://img.shields.io/crates/v/sigma-ser.svg)](https://crates.io/crates/sigma-ser) [![Documentation](https://docs.rs/sigma-ser/badge.svg)](https://docs.rs/crate/sigma-ser)

Ergo binary serialization primitives.

Bindings:

- [ergo-lib-wasm(Wasm)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-wasm) [![Latest Version](https://img.shields.io/crates/v/ergo-lib-wasm.svg)](https://crates.io/crates/ergo-lib-wasm) [![Documentation](https://docs.rs/ergo-lib-wasm/badge.svg)](https://docs.rs/crate/ergo-lib-wasm) 
- [ergo-lib-wasm-browser(JS/TS)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-wasm) [![Latest version](https://img.shields.io/npm/v/ergo-lib-wasm-browser)](https://www.npmjs.com/package/ergo-lib-wasm-browser)
- [ergo-lib-wasm-nodejs(JS/TS)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-wasm) [![Latest version](https://img.shields.io/npm/v/ergo-lib-wasm-nodejs)](https://www.npmjs.com/package/ergo-lib-wasm-nodejs)
- [ergo-lib-ios(Swift)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-ios)
- [ergo-lib-jni(Java)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-jni) [![Latest Version](https://img.shields.io/crates/v/ergo-lib-jni.svg)](https://crates.io/crates/ergo-lib-jni) [![Documentation](https://docs.rs/ergo-lib-jni/badge.svg)](https://docs.rs/crate/ergo-lib-jni)
- [ergo-lib-c (C)](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-c) [![Latest Version](https://img.shields.io/crates/v/ergo-lib-c.svg)](https://crates.io/crates/ergo-lib-c) [![Documentation](https://docs.rs/ergo-lib-c/badge.svg)](https://docs.rs/crate/ergo-lib-c)
- [sigma_rb(Ruby)](https://github.com/thedlop/sigma_rb)[![Gem Version](https://badge.fury.io/rb/sigma_rb.svg)](https://badge.fury.io/rb/sigma_rb)

## Usage Examples
To get better understanding on how to use it in your project check out how its being used in the following projects:

- [Ergo Headless dApp Framework](https://github.com/Emurgo/ergo-headless-dapp-framework);
- [Ergo Node Interface Library](https://github.com/Emurgo/ergo-node-interface);
- [Oracle Core](https://github.com/ergoplatform/oracle-core);
- [AgeUSD Stablecoin Protocol](https://github.com/Emurgo/age-usd);
- [Ergo SDK](https://github.com/ergolabs/ergo-sdk-js) (Wasm bindings);
- [Yoroi wallet](https://github.com/Emurgo/yoroi-frontend) (Wasm bindings);
- [Ergo Desktop Wallet](https://github.com/ErgoWallet/ergowallet-desktop) (Wasm bindings);
- [Create transaction demo](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-wasm/examples/create-transaction-demo) (TS)
- [Address generation demo](https://github.com/ergoplatform/sigma-rust/tree/develop/bindings/ergo-lib-wasm/examples/address-generation-demo) (TS)

Also take a look at tests where various usage scenarios were implemented.


## Tools


::cards::

[
  {
    "title": "🔗 Ergo Utilities",
    "content": "simplify writing off-chain code in Rust.",
    "url": "https://github.com/robkorn/ergo-utilities-rust/"
  },

]

::/cards::