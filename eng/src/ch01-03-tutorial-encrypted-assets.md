# Turotial: Encrypted fungible assets

In this tutorial, we'll exlapin how you can manage your encrypted fungible assets in Zerochan. We provide a special substrate module called [`encrypted-assets`](https://github.com/LayerXcom/zero-chain/tree/master/modules/encrypted-assets) module in order to mint, burn, and transfer encrypted assets. These assets are encrypted on-chain, so no-one can see the actual amounts without its decryption key. Each assets has an unique `asset-id` to be managed as separated assets.

We expect you to install ZFace, setup zk-SNARKs parameters, run Zerochain nodes and create your wallet following [the section1~3 in this page](ch01-02-tutorial-confidential-payment.md).

### 1. Mint 100 encrypted coins

You can mint your encrypted assets by the following commands. The amount is specified `100` and the asset-id is automatically determined as a unique number. You can fetch the asset-id by the event.

```
zface tx asset-issue -a 100
```

### 2. Transfer encrypted asset

Let's transfer 20 encrypted-coins to the address `5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i`. The asset-id of initial minted assets is `0`, so you need to specify it.

```
zface tx asset-transfer -a 20 -i 0 -t 5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i
```

### 3. Check your current balance of encrypted assets

You just transfer 20 assets to other addresss, so you're supposed to have 80 assets.

```
zface wallet asset-balance -i 0
```

### 4. Burn encrypted asset

To burn your encrypted assets, just specify the asset-id and then destroy the assets.

```
zface tx asset-burn -i 0
```
