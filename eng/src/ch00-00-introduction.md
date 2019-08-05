# Introduction

This documentation helps developers understand the core concepts of Zerochain and walks through the steps required to build a Zerochain node and send confidential transactions using Zerochain’s module.

Zerochain is a generic, privacy-protecting layer on top of Substrate. It provides substrate modules and a toolkit for protecting the user's identity and sensitive data that is stored on chain.
Zerochain protocol (v1) combines with solutions of the Zether and Zcash toolchain and of course Substrate.
- Zether is a high-level privacy scheme which takes an account-based approach.
- The Zcash toolchain is a Zero-knowledge proving system with elliptic curve operations.
- Substrate is a blockchain layer which provides core components such as P2P networking, database, and a consensus engine.

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/59009598-33972d80-8869-11e9-922b-1f86e18455a8.png" width="500px">
</div>

The first goal of Zerochain is to provide a secure and efficient confidential and anonymous payment protocol for fungible assets. This requirements are that
- Transferred amounts are private.
- Each account balance is private.
- Identities of transactors are private.

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/54678399-6d00ac80-4b48-11e9-9c8d-d1ec2b668761.png" width="500px">
</div>

Core features of Zerochain are
- Efficient computational cost of zk-proofs and verification.
- Auditability for each account.
- Storage friendly confidentiality from the point of view of both the wallet and blockchain.

More precisely
- In general, computational costs tend to be huge for zero-knowledge proofs. Zerochain uses pre-processing zk-SNARKS which is a kind of ZK proving systems that has low computational cost and small proof size. There are, however, some trade-offs.
- Statements in zk-SNARK are based on the Zether protocol so that computational cost of the proof is less than other privacy-protecting protocols.
- Users can allow auditors to observe account balances by using a viewing key but auditors cannot use the key to spend the user's money.
- Zerochain's wallet doesn't need to run either full node or light client. It can simply send transactions using an RPC API.
- Zerochain is an account-based blockchain so it can avoid UTXO accumulation and minimize storage.
