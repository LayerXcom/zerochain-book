# Key components

<div align="center">
<img src="https://user-images.githubusercontent.com/20852667/59552701-57731580-8fc5-11e9-8bee-ccf12e0cb051.png" width="600px">
</div>

These arrows are one-way. For example, you cannot derive a spending key from a decryption key, but you can derive a decryption key from a spending key.

These bunch of keypairs allow us to get a auditability, zk-proofs delegation and hide a signer's identity.

This key components scheme is modified and simplified version of zcash sapling's one to be compatible with Zerochain.


### Signing key
Every time you sign a transaction, a re-randomized signing key will be generated so that a signature will be different from the previous one. It helps to make it quite difficult to distinguish the sender's address because the signature of the same sender is no longer same.

### Decryption key
A decryption key works as a viewing key which allows only this key's owener to see the encrypted balance which is  stored on-chain.

If you pass your decryption key to auditors, they can see your current balance, but cannot spend your coins of course.

### Encryption key
Encryption key is a public key can be used to encrypt all transferred amounts and balances.
