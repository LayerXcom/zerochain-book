# Turotial: Confidential payment

This tutorial will explain the basic confidential transfer on Zerochain. Alice has the **encrypted** balance of 10,000 coins and sends **encrypted** 100 coins to you. The encrypted fee will be subtracted from her balance. (By default, a base fee parameter is set to 1.) So, Alice's balance will be 9,899 coins and you will get the 100 coins. All operations are done encrypted by ElGamal encryption and zk-SNARKs.

In this tutorial, we assumed you've already done the all installation explained [previous section](ch01-01-installation.md).

### 1. Install ZFace
First of all, you need to install [ZFace](ch02-00-zface.md) to interact with Zerochain. ZFace is basically a low-level wallet core and cryptographic tools for Zerochain.

```
cargo install --force --path zface
```

Then, you can use CLI powerd by ZFace.

### 2. Wallet creation
Create a new zerochain wallet.

```
zface wallet init
```

You will then be prompted to enter a wallet password and a initial account name.
**Please, note carefully the following mnemonic words. They will be needed to recover your wallet.**

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/60558171-34957f00-9d83-11e9-9094-e446cb9b2ce7.png" width="900px">
</div>

### 3. Run Zerochain nodes
Run a Zerochain node in other terminal screen. `--dev` flag is for specifying development mode.

```
./target/release/zerochain --dev
```

If you want to clear your old chain's history:
```
./target/release/zerochain purge-chain --dev
```

### 4. Interacting with Zerochain

##### 4-1. Transfer initial minted coins to your account
When you initialize your Zerochain, a specific Alice account has initial minted 10,000 coins (of course, it is encrypted). You can transfer the encrypted coins from Alice to your just generated account by `debug` command.

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

##### 4-3. Confidential payment between your accounts
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

- Transfer encrypted coins to your new account
```
zface tx send -t <ADDRESS> -a <AMOUNT>
```
It's Done!