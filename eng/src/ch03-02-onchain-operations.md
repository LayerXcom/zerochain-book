# On-chain operations
In the basic confidential payment scheme in [conf_transfer module](https://github.com/LayerXcom/zero-chain/blob/master/runtime/src/conf_transfer.rs), there is one public callable function `confidential_transfer`. It takes some parameters such as a zero-knowledege proof, some ciphertexts and addresses.
In this function, mainly three internal functions are called. First one is `roll_over` function for pending transfers which is explained later. Second one is `validate_proof` function for varifying zk proofs. (For more details: [Statements in circuit](ch03-03-statement-in-circuit.md)) Last one is mutating storage to add encrypted coins to recipient's encrypted balance and subtract it from sender's encrypted balance.


## Pending transfer
Zerochain uses a pending transfer strategy to prevent from front-running attacks. We have `encrypted_balance` and `pending_transfer` mappings to store account's balances on-chain. `encrypted_balanace` is a actual balance mapping and `pending_transfer` is like a temporary storage in order to store incoming payments.

```
alice_encrypyed_balance => 0x00
alice_pending_transfer => 0x3ad1..
```

Let's think a simple case that alice sends encrypted 5 coins to bob. The encrypted 5 coins will be stored bob's `pending_transfer` at first, not affect bob's `encrypted_balance`. In the next time when someone sends coins to bob or bob sends coins to someone, `rollover` function will be invoked and balances are transferred from `pending_transfer` map to `encrypted_balance` map. `rollover` function can work correctly if the current block height is over a previous epoch. Epoch is a term for the range of block height. A rollover to same address shouldn't be occured twice in a epoch to prevent from front-running attacks. If it can occur, a malicious attacker can watch transactions and


## Subtracting encrypted fees

Fees are subtracted from sender's encrypted balance based on `transaction_base_fee` storage key in the `conf_transfer` module.
`transaction_base_fee` is set to `1` by default in [chain_spec.rs](https://github.com/LayerXcom/zero-chain/blob/67655966f3dd067011ea4fd215f128784b53ffd0/src/chain_spec.rs#L136).
