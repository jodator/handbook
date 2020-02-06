---
description: Learn more about these fundamental components of our current testnet system.
---

# Keys and Addresses

### What Are Keys and Addresses?

Addresses \(also known as accounts\) on Joystream are the most basic representation of an identity on the platform.

Keys and their resultant addresses \(accounts\) are more basic than memberships as they have no information intrinsically attached to them. For this reason their permissions within the governance hierarchy of the platform are strictly limited.

A key without a membership can:

* Send and receive testJOY funds
* Set a memo

A key without an associated membership cannot do things such as:

* Stand as a candidate for council elections
* Vote in council elections
* Make proposals to be voted on by the council
* Upload multimedia content
* Make posts in the platform forum

### Creating and Managing Keys

Our current testnet allows participants to generate keys from a mnemonic or raw seed. Users can choose between two encryption systems for generating the key from the seed. These are `Edwards (ed25519)` and `Schnorrkel/Ristretto x25519 (sr25519)`.

`sr25519` is based on the same underlying Curve25519 as its EdDSA counterpart, `ed25519`. However, it uses Schnorr signatures instead of the EdDSA scheme. 

`sr25519` signatures bring some benefits over the ECDSA/EdDSA schemes. For example, Schnorr allows for native multisignature through signature aggregation while also being more efficient and retaining the same feature set and security assumptions.

If you would like to validate, the `session` key needs to use `ed25519` cryptography.

The private key, seed or mnemonic phrase should never be shared with anybody as these give access to your funds. 

### Different Types Of Key

Roles such as the `Validator` require users to manage a selection of keys, where each key is dedicated to a specific purpose. While in our Acropolis testnet only three keys were required to be a Validator, in Rome, five are needed.

#### `Stash Key`

The stash key is typically where a participant's wealth on the platform is stored. In most cases the stash key should only ever have to sign one message in order to assign the controller account. Once this is done, the controller account can act on behalf of the stash key.

#### `Controller Key`

The controller key acts on behalf of the stash key. It can perform actions with the "weight" of the stash key behind it.

#### `Session Key`

Session keys are specific to the validator role and have a variety of purposes linked to the activities of validators on the network. For Rome, two new session keys will be added.

You can read more about `validators` and their `session keys` in our handbook section dedicated to them.

### The Subkey Utility

You can use Substrate's [command line utility](https://github.com/paritytech/substrate/), `subkey`, to generate accounts, inspect keys, sign messages and transactions as well as to verify signatures.

#### Generate an account <a id="user-content-generate-a-random-account"></a>

This will generate a mnemonic phrase and provide you with the corresponding seed, public key, and address of a new account.

```text
subkey generate
```

#### Inspect a key <a id="user-content-inspecting-a-key"></a>

You can inspect a given parameter \(mnemonic, seed, public key, or address\) and `subkey` will output the corresponding public key and the address.

```text
subkey inspect <mnemonic,seed,pubkey,address>

OUTPUT:
  Public key (hex): 0x461edcf1ba99e43f50dec4bdeb3d1a2cf521ad7c3cd0eeee5cd3314e50fd424c
  Address (SS58): 5DeeNqcAcaHDSed2HYnqMDK7JHcvxZ5QUE9EKmjc5snvU6wF
```

#### Signing <a id="user-content-signing"></a>

```text
echo -n <msg> | subkey sign <seed,mnemonic>

OUTPUT:
a69da4a6ccbf81dbbbfad235fa12cf8528c18012b991ae89214de8d20d29c1280576ced6eb38b7406d1b7e03231df6dd4a5257546ddad13259356e1c3adfb509
```

#### Verifying a signature <a id="user-content-verifying-a-signature"></a>

```text
echo -n <msg> | subkey verify <sig> <address>

OUTPUT:
Signature verifies correctly.
```

#### Signing a transaction <a id="user-content-signing-a-transaction"></a>

```text
subkey sign-transaction \
	--call <call-as-hex> \
	--nonce 0 \
	--suri <secret-uri> \
	--password <password> \
	--prior-block-hash <prior-block-hash-as-hex>
```

### Vanity Addresses

Because Polkadot and Joystream testnet addresses are formatted in the same way, you can use the page [here](https://polkadot.js.org/apps/#/accounts/vanity) to generate a vanity address for Joystream.

Alternatively, using the subkey utility mentioned above, you could simply do:

```text
subkey vanity <string>
```

The longer the string you would like to be part of your address, the longer the process will take.

### Account Balances

Participants should be aware that balances attached to addresses can be held in different states, including:

* **`available`**: funds that are available for any transaction.
* **`bonded`**: funds currently locked for validating or nominating
* **`unbonding`**: funds that are being unbonded \(will be redeemable after the bonding period has passed\)

### Memberships And Keys

For the moment, memberships can only be linked to one key/address. Read more on this [here](memberships/).



