# ZFace: An interface for interacting with Zerochain
(WIP)

ZFace is a low-level wallet core and cryptographic tools for Zerochain.

In this section, we explained the usage of CLI tools powered by ZFace. The CLI tool has mainly four subcommands which is explained later.
- snark: Operations around zk-SNARKs
- wallet: Operations around wallet
- tx: Operatipons around sending transactions to Zerochain
- debug: Debugging and testing commands

### Creating a new wallet
For security reasons, the cryptographic materials are stored encryped by providing a password.

To do this, run:

```
./target/release/zface wallet init
```

You will then be prompted to enter a password. This password will be used to encrypt your mnemonics of your wallet. Wallet files are stored in zface directory located in the following path.

|Platform | Value | Example |
|---|---|---|
| Linux | $XDG_DATA_HOME or $HOME/.local/share/zface | /home/alice/.local/share/zface |
| macOS | $HOME/Library/Application Support/zface | /Users/Alice/Library/Application Support/zface |
| Windows | {FOLDERID_LocalAppData}\zface | C:\Users\Alice\AppData\Local\zface |


### Add a account
You can add a new account into your wallet.

```
./target/release/zface wallet add-account
```

### Show accounts list
It will show your accounts in your wallet.

```
./target/release/zface wallet list
```

### Change default account

```
./target/release/zface wallet change-account -n <ACCOUNT_NAME>
```

### Recover a wallet from mnemonic
(TODO)
```
./target/release/zface wallet recover
```

You will then be prompted to enter a mnemonic to recover your wallet.

### Get balances
- Getting your current balance from `encrypted-balances` module
```
./target/release/zface wallet balance
```

- Getting your curernt balance from `encrypted-balances` module
```
./target/release/zface wallet asset-balance -i <ASSET_ID>
```

- Getting your curernt balance from `anonymous-balances` module
```
./target/release/zface wallet anonymous-balance
```

### Setup for zk-proving
Generating a proving key and verifying key of zk-SNARKs.
```
./target/release/zface snark setup
```

### send
- Submit a transaction to call `confidential_transfer` function in `encrypted-balances` module.
```
./target/release/zface tx send -t <RECIPIENT_ADDRESS> -a <AMOUNT>
```

- Submit a transaction to call `issue` function in `encrypted-assets` module.
```
./target/release/zface tx asset-issue -a <AMOUNT>
```

- Submit a transaction to call `asset_transfer` function in `encrypted-assets` module.
```
./target/release/zface tx asset-send -t <RECIPIENT_ADDRESS> -a <AMOUNT> -i <ASSET_ID>
```

- Submit a transaction to call `burn` function in `encrypted-assets` module.
```
./target/release/zface tx asset-burn -i <ASSET_ID>
```

- Submit a transaction to call `issue` function in `anonymous-balances` module.
```
./target/release/zface tx anonymous-issue -a <AMOUNT>
```

- Submit a transaction to call `anonymous_transfer` function in `anonymous-balances` module.
```
./target/release/zface tx anonymous-send -t <RECIPIENT_ADDRESS> -a <AMOUNT>
```

### Manage encrypted assets
- Issue new encrypted assets
```
./target/release/zface tx asset-issue -a <AMOUNT>
```

- Send encrypted assets
```
./target/release/zface tx asset-transfer -t <RECIPIENT_ADDRESS> -a <AMOUNT> -i <ASSET_ID>
```

- Burn encrypted assets
```
./target/release/zface tx asset-burn -i <ASSET_ID>
```

## Test for debugging

### Print key components
```
./target/release/zface debug key-init
```

### Send tx for debuggin
```
./target/release/zface debug send -s <SENDER_SEED> -t <RECPIENT_ADDRESS> -a <AMOUNT>
```

### Print transaction components
```
./target/release/zface debug print-tx
```
