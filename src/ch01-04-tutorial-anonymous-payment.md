# Tutorial: Anonymous payments

In this tutorial, we'll explain how you can send transactions in an anonymous manner. We provide a special Substrate module called [`anonymous-balances`](https://github.com/LayerXcom/zero-chain/tree/master/modules/anonymous-balances) module. User's coins managed in the `anonymous-balances` modules are encrypted in the same way as `encrypted-balances` module. To get an anonimous features, more precisely obfuscating features, some dummy addresses are added to a target address set in a transaction, so that an actual recipient address and dummy addresses cannot be distinguishable from the other people perspective.

For following the tutorial, we expect you to already install ZFace, create your wallet, and run Zerochain, see [the section1~3 in this page](ch01-02-tutorial-confidential-payment.md).

### 1. Mint 100 encrypted coins
You can mint your encrypted coins by the following commands. This issue method isn't anonymous way but confidential way.

```
./target/release/zface tx anonymous-issue -a 100
```

### 2. Send an anonymous transaction
Let's transfer 20 encrypted-coins to the address `5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i`(This address is depending on your wallet account). Some dummy addresses are automatically added to the transaction so that other people cannot see where it came from and went to.

```
./target/release/zface tx anonymous-send -a 20 -i 0 -t 5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i
```

### 3. Check your current balance

You just transferred 20 assets to other address, so you're supposed to have 80 assets.

```
./target/release/zface wallet anonymous-balance
```
