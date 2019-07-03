# Turotial: Confidential payment

This tutorial will explain the basic confidential transfer on Zerochain. Alice has the **encrypted** balance of 10,000 coins and sends **encrypted** 100 coins to you. The encrypted fee will be subtracted from her balance. (By default, a base fee parameter is set to 1.) So, Alice's balance will be 9,899 coins and you will get the 100 coins. All operations are done encrypted by ElGamal encryption and zk-SNARKs.

Currently, there are two ways to interact with Zerochain.

- CLI (**recommended**)
- Browser

Browser UI is not maintenanced well, so might not be working. It is recommended to use with CLI.

In this tutorial, we assumed you've already done the all installation explained [previous section](ch01-01-installation.md).

### 1. Initial setup
First of all, you need to install [ZFace](ch02-00-zface.md) to interact with Zerochain. ZFace is basically a low-level wallet core and cryptographic tools for Zerochain.

##### 1-1. Install ZFace (In the root zerochain directory)
```
cargo install --force --path zface
```

Then, you can use CLI powerd by ZFace. Next thing you need to do for inisital setup is a preparation of zk-SNARKs parameters.

##### 1-2. Setup for zk-SNARKs

Generating a proving key and verifying key of zk-SNARKs, which are used for confidential payments.

```
zface snark setup
```

### 2. Run Zerochain nodes
Run a Zerochain node in other terminal screen. `--dev` flag is for specifying development mode.

```
./target/release/zerochain --dev
```

If you want to clear your old chain's history:
```
./target/release/zerochain purge-chain --dev
```

### 3. Wallet creation
Create a new zerochainc wallet.

```
wallet init
```

You will then be prompted to enter a wallet password and a initial account name.
**Please, note carefully the following mnemonic words. They will be needed to recover your wallet.**

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/60558171-34957f00-9d83-11e9-9094-e446cb9b2ce7.png" width="900px">
</div>

### 4. Interacting with Zerochain

##### 4-1. Transfer initial minted coins to your account
When you initialize your Zerochain, a specific Alice account has initial minted 10,000 coins (of couse, it is encrypted). You can transfer the encrypted coins from Alice to your just generated account by `debug` command.

```
zface debug send -t <YOUR ADDRESS> -a <AMOUNT>
```

For example, the following command can transfer 100 coins to `5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i` address. The address is depending on your account. Please copy and pasted printed-out address.

```
zface debug send -t 5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i -a 100
```


##### 4-2. Check your balanace
If the transferring coins was done successfully, your account should have 100 coins. You can check the balance by

```
zface wallet balance
```

You will then be prompted to enter your passoword.

It's Done!

### 4-3. (Advanced) Confidential payment between your accounts
You also can transfer encypted coins to your other your account by the following commands.

- Create other your account
```
zface wallet add-account
```

- Check your accounts list
```
zface wallet list
```

- Change default account to your first account who has 100 coins
```
zface wallet change-account -n <ACCOUNT_NAME>
```

- Transfer encrypted coins
```
zface tx send -t <ADDRESS> -a <AMOUNT>
```

### Browser

1. Setup for zkSNARKs from CLI
- Get the proving key and the veifying key for zk-SNARKs
```
zface snark setup
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
zeroc debug print-tx
```

- For more information (if you want to set the customized amount and address)
```
zeroc debug print-tx --help
```

5. Fill out the form:

You can send the transaction from firefox browser.

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/54687970-228b2a00-4b60-11e9-8c26-fdfbbb3a17d8.png" width="1100px">
</div>
