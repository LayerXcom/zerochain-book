# Turotial: Confidential payment

This tutorial will explain the basic confidential transfer on Zerochain. Alice has the **encrypted** balance of 100 coins and sends **encrypted** 10 coins to Bob. So, Alice's balance will be 90 coins and Bob will get the 10 coins. All operations are done encrypted by ElGamal encryption and zk-SNARKs.

(First of all, make sure zerochain is running by [the following way](ch01-01-installation.md).)

Currently, there are two ways to interact with Zerochain.

- CLI (recommended)
- Browser

Browser UI is not maintenanced well, so might not be working. It is recommended to use with CLI.

### zeroc: Zerochain CLI

zeroc is a command-line utility which can interact with Zerochain.

#### Initial setup

- Install zeroc
```
cargo install --force --path zeroc
```

- Setup for zk-SNARKs

Generating a proving key and verifying key of zk-SNARKs, which are used for confidential payments.

```
zeroc setup
```

#### Interacting with Zerochain

- Generate key pairs

Generate random key pairs(seed, decryption key, and encryption key(public key)).
Alice's and Bob's key pairs are fixed and Alice already has some coins.

```
zeroc init
```

- Send transaction for confidential payment
```
zeroc send -a <AMOUNT> -s <Sender's SEED> -to <Recipient's PUBLIC KEY>
```

In the case, Alice sends 10 coins to Bob...

```
zeroc send -a 10 -s 416c696365202020202020202020202020202020202020202020202020202020 -to 45e66da531088b55dcb3b273ca825454d79d2d1d5c4fa2ba4a12c1fa1ccd6389
```

- Get balance

Get a decrypyed balance using the user's decryption key.

```
zeroc balance -d <DECRYPTION KEY>
```

To get alice's balance...

```
zeroc balance -d b0451b0bfab2830a75216779e010e0bfd2e6d0b4e4b1270dfcdfd0d538509e02
```

### Browser

1. Setup for zkSNARKs from CLI
- Get the proving key and the veifying key for zk-SNARKs
```
./target/release/zero-chain-cli setup
```

2. Run the nodes
```
./target/release/zero-chain --dev
```
- If you want to clear your old chain's history:
```
./target/release/zero-chain purge-chain --dev
```

3. Run the UI apps

The UI repository is here:
https://github.com/LayerXcom/zero-chain-ui

4. Generate the transaction from CLI
- Generate the transaction components (Computing a zero-knowledge proofs and an encryption)
```
./target/release/zero-chain-cli generate-tx
```

- For more information (if you want to set the customized amount and address)
```
./target/release/zero-chain-cli generate-tx --help
```

5. Fill out the form:

You can send the transaction from firefox browser.

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/54687970-228b2a00-4b60-11e9-8c26-fdfbbb3a17d8.png" width="1100px">
</div>
