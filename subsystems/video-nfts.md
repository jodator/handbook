# NFTs

## Introduction

This article will be incorporated into the `Content Directory` article later.

## Concepts

### Auction Type

* English: ..
* Open: ...

### Content Actor

* Curator\(CuratorGroupId, CuratorId\)
* Member\(MemberId\)
* Lead

### Buy Now

xxxx

### NFT Status

xxx



## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

| Name | Description | Value |
| :--- | :--- | :--- |
| `INVITE_LOCK_ID` | The identifier value for the lock applied to root account of a new member | `fill-in` |
| `xxx` |  | `fill-in` |

## Extrinsics

### Issue NFT

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Offer NFT

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx



### Cancel Offer

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Accept NFT

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Sell NFT

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Buy NFT

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Start NFT Auction

**Parameters**

| Name | Description |
| :--- | :--- |
| `auctioneer` | ContentActor who owns NFT. |
| `video_id` | Video identifier for video to which NFT corresponds. |
| `auction_type` | AuctionType designating what kind of auction should be used. |
| `starting_price` | Balance that sets lower bound for first valid bid amount. |
| `minimal_bid_step` | Balance that sets lower bound for how much each new bid must exceed last valid bid amount, if it exists. |
| `buy_now_price` | If provided, the Balance at which one would instantly be able to buy the NFT. |
| `starts_at` | If provided, the BlockNumber at which it becomes possible to bid in the auction or buy now. |
| `whitelist` | Set of membership identifiers which, at leats one is provided, restricts bidders or buyers to be among these. |

#### Conditions

* `video_id` corresponds to to existing video `video` .
* `video` 
* signer

#### Effect

* A nexxx

### Cancel NFT Auction

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Make Bid

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Cancel Open Auction Bid

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

### Complete NFT Auction

**Parameters**

| Name | Description |
| :--- | :--- |
| `root_account` | To be root account of membership. |

#### Conditions

* Frexx

#### Effect

* A nexxx

