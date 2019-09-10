# Turotial: Encrypted fungible assets

In this tutorial, we'll exlapin how you can manage your encrypted fungible assets in Zerochan. We provide a special substrate module called [`encrypted-assets`](https://github.com/LayerXcom/zero-chain/tree/master/modules/encrypted-assets) module in order to mint, burn, and transfer encrypted assets. These assets are encrypted on-chain, so no-one can see the actual amounts without its decryption key. Each assets has an unique `asset-id` to be managed as separated assets.

We expect you to install ZFace, create your wallet, and run Zerochain following [the section1~3 in this page](ch01-02-tutorial-confidential-payment.md).

### 1. Mint 100 encrypted coins

You can mint your encrypted assets by the following commands. The amount is specified `100` and the asset-id is automatically determined as a unique number. You can fetch the asset-id by the event.

```
zface tx asset-issue -a 100
```

### 2. Transfer encrypted asset

Let's transfer 20 encrypted-coins to the address `5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i`(This address is depending on your wallet account). The asset-id of initial minted assets is `0`, so you need to specify it.

```
zface tx asset-send -a 20 -i 0 -t 5DC4kJ84b4KfVyddcFMYfy5skTJWVtxtWRETZo2i4nh8Ao1i
```

### 3. Check your current balance of encrypted assets

You just transferred 20 assets to other address and are subtracted 1 assets as fee, so you're supposed to have 79 assets.

```
zface wallet asset-balance -i 0
```

### 4. Burn encrypted asset

To burn your encrypted assets, just specify the asset-id and then destroy the assets.

```
zface tx asset-burn -i 0
```
