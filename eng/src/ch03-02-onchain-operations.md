# On-chain operations
(TODO)




## Subtracting encrypted fees

Fees are subtracted from sender's encrypted balance based on `transaction_base_fee` storage key in the `conf_transfer` module.
`transaction_base_fee` is set to `1` by default in [chain_spec.rs](https://github.com/LayerXcom/zero-chain/blob/67655966f3dd067011ea4fd215f128784b53ffd0/src/chain_spec.rs#L136).
