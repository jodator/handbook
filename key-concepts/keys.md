---
description: Learn more about these fundamental components of our current testnet system.
---

# Keys

## What Are Keys, Addresses and Accounts?

Accounts are the most basic representation of actor\(s\) on the platform. They are formally represented by unique human-readable addresses, which are themselves generated from their respective private keys. Each account can only be represented by one address, and a single key from which this address is derived.

Accounts are essentially anonymous as they have no identifying information intrinsically attached to them. For this reason their permissions within the governance hierarchy of the platform are strictly limited. Keys play the role of "signing" for accounts when some action is performed on the network.

An account is currently limited to three basic functions:

* Sending and receiving tJOY funds
* Functions relating to being a `Validator` \(see below\)
* Setting a memo for testnet compensation or some other defined purpose

## Creating and Managing Keys

Our current testnet allows participants to generate keys from a mnemonic or raw seed. Users can choose between two encryption systems for generating the key from the seed. These are `Edwards (ed25519)` and `Schnorrkel/Ristretto x25519 (sr25519)`.

`sr25519` is based on the same underlying Curve25519 as its EdDSA counterpart, `ed25519`. However, it uses Schnorr signatures instead of the EdDSA scheme.

`sr25519` signatures bring some benefits over the ECDSA/EdDSA schemes. For example, Schnorr allows for native multisignature through signature aggregation while also being more efficient and retaining the same feature set and security assumptions.

If you would like to validate, the `session` key needs to use `ed25519` cryptography.

The private key, seed or mnemonic phrase should never be shared with anybody as these give access to your funds.

