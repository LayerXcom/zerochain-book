# On-chain operations
In the basic confidential payment scheme in [conf_transfer module](https://github.com/LayerXcom/zero-chain/blob/master/core/proofs/src/circuit/confidential_transfer.rs), there is one public dispatchable function `confidential_transfer`. It takes some parameters such as a zero-knowledege proof, some ciphertexts and addresses.
In this function, mainly three internal functions are called.

First one is `roll_over` function for pending transfers which is explained later. `roll_over` allows us to send transactions asynchronously and protect from front-running attacks. We roll over an account in an epoch when the first message from this account is received, so one message rolls over only one account. To achieve this, we define a separate (internal) method for rolling over, and the first thing every other method does is to call this method.

Second one is `validate_proof` function for varifying zk proofs. (For more details: [Statements in circuit](ch03-03-statement-in-circuit.md))

Last one is mutating storage to add encrypted coins to recipient's encrypted balance and subtract it from sender's encrypted balance.

## Pending transfer
Zerochain uses a pending transfer strategy to prevent from front-running attacks. This attack is that a malicious attacker can watch Alice's transaction and his transaction gets processed first, then Alice's transaction will be rejected because the proof will not be valid anymore. More precisely, Alice's encrypted balance is updated, so public input to `validate_proof` parameter is no longer correct.

To solve this problems, we have `encrypted_balance` and `pending_transfer` mappings to store account's balances on-chain. `encrypted_balanace` is a actual balance mapping and `pending_transfer` is like a temporary storage in order to store incoming payments.

Let's think a simple case that Alice sends encrypted 5 coins to Bob. The encrypted 5 coins will be stored Bob's `pending_transfer` at first, not affect Bob's `encrypted_balance`. In the next time when someone sends coins to Bob or Bob sends coins to someone, `rollover` function will be invoked and balances are transferred from `pending_transfer` map to `encrypted_balance` map.

More details in Section 3.1: https://crypto.stanford.edu/~buenz/papers/zether.pdf

## Subtracting encrypted fees

Fees are subtracted from sender's encrypted balance based on `transaction_base_fee` storage key in the `conf_transfer` module.
`transaction_base_fee` is set to `1` by default in [chain_spec.rs](https://github.com/LayerXcom/zero-chain/blob/67655966f3dd067011ea4fd215f128784b53ffd0/src/chain_spec.rs#L136).
