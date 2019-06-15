# Command Line Tool


### Creating a new wallet
 For security reasons the cryptographic materials are stored encryped by providing a password.

To do this, run:

```
zeroc wallet init
```

You will then be prompted to enter a password. This password will be used to encrypt your mnemonics of your wallet. Wallet files are stored

Platform	Value	Example
Linux	$XDG_DATA_HOME or $HOME/.local/share/zeroc	/home/alice/.local/share
macOS	$HOME/Library/Application Support/zeroc	/Users/Alice/Library/Application Support
Windows	{FOLDERID_LocalAppData}\zeroc	C:\Users\Alice\AppData\Local\zeroc

### Creating a new account

```
zeroc wallet gen-account -n <ACCOUNT NAME>
```

### Show accounts list

```
zeroc wallet list
```

### Recover a wallet from mnemonic

```
zeroc wallet recover
```
You will then be prompted to enter a password.

### Change current account

```
zeroc wallet change-account -a <ACCOUNT NAME>
```

### Get an account's balance

```
zeroc wallet get-balance
```

### Setup for zk-proving

```
zeroc snark setup
```

### send

```
zeroc send
```
You will then be prompted to enter a transferred amount and a destination address.
