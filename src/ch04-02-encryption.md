# Encryption scheme

All transferred amounts and account balances are encrypted in Zerochain, but you have to compute(add or sub) these with encrypted at the time of the payment.

Zerochain achieves it by using the special encryption algorithm called “Additive homomorphic encryption”. As you can guess from the name, it can compute the addition(or subtraction) with encrypted. More specifically, Zerochain uses “Lifted-ElGamal encryption” to get efficient encryption and additive homomorphic property. (You can think it’s like Pedersen commitment in terms of additive homomorphic property, but Lifted-Elgamal is an asymmetric key encryption algorithm, not a commitment.)

## Encryption

You can compute the ciphertext like bellow.

ciphertext:

<div align="left">
<img src="https://user-images.githubusercontent.com/20852667/59552793-3e1e9900-8fc6-11e9-9227-2eaba1eaf862.png" width="150px">
</div>


where v: transferred amount, r: pseudorandomness, G: generator point, s: secret key (the corresponding public key: sG)

## Decryption

You can decrypt it by using the given ciphertext and secret key.

<div align="left">
<img src="https://user-images.githubusercontent.com/20852667/59552795-437be380-8fc6-11e9-9e3c-0f26d1556443.png" width="250px">
</div>

Then, you realize you have to solve the discrete logarithm problem to get the amount “v”. Practically, “v” would be just a small bits integer (like 32bits) and vG(v=1,2,…) are computed in advance. (On the other hand, the secret key “s” and pseudorandom “r” will be a huge number so that one cannot solve the discrete logarithm.)

The decryption of Lifted-ElGamal is not efficient like this, but we chose it as an encryption algorithm in Zerochain due to the efficient encryption and the good compatibility with zero-knowledge proof.

## Additive homomorphic

Let’s think the case the user has encrypted 10 coins as his balance, then is transferred encrypted 5 coins. That is the addition of ciphertext with v = 10 as balance and v’ = 5 as amount.

<div align="left">
<img src="https://user-images.githubusercontent.com/20852667/59552799-4971c480-8fc6-11e9-9f44-0647b47102cb.png" width="600px">
</div>

This is the same form as the ciphertext you see above. You can get the amount “15” by using secret key “s” in the same way. All the additions of ciphertext are computed on-chain at the time of updating the balance.
