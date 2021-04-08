---
description: >-
  A compendium of useful extrinsics for the runtime that doesn't fit into other subsystem
---

# Joystream Utility

### Introduction

Joystream utility is the place where different extrinsics that doesn't exactly fit into other modules will go. Many of the extrinsics here are only called by proposals and will be documented there.

## Extrinsics

### Burn Account Tokens

**Parameters**

| Name | Description |
| :--- | :--- |
| `amount` | Tokens to be burned |

#### Conditions

* Signer has at least `amount` free balance.
* `amount` is non-zero.

#### Effect

Signer's balance is lowered by `amount` of tokens and so it the total issuance.
