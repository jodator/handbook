---
description: An introduction to the subkey utility
---

# The Subkey Utility

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

