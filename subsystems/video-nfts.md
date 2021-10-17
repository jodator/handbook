---
description: >-
  Video ownership, as distinct from authorship, is a transferable title
  represented as a Non-Fungible Token (NFT). These transfers can occur through
  non-intermediated auction, purchases or standing sell
---

# NFTs

## Preamble

This article will later be incorporated into the [content-directory.md](content-directory.md "mention") document at a later time.

## Introduction

A passionate follower of some creator or topic may find significant value in being able to associated themselves with related creative content. They key is that the association is very public and visible, and thereby allows the owner to signal to their community and related audiences something about who they are, the resources they have - financial, social and human, in the latter for example by having discerning taste or judgement. This behavior is already very prevalent in lots of social arenas in the off-line world, in particular among collectors. People collect stamps, coins, art, cars, sneakers, etc., and motivations span:

1. inherent enjoyment in collecting anything durable, sort of like a hobby, where you also get to curate a collection
2. a tasteful way to demonstrate you have access to resources like time, money and information
3. showing you have good judgement and taste
4. owning a piece of history in some way
5. making a good investment

Video NFTs play into all of these objectives, and arguably substantially amplify your ability to achieve those goals through the following

* **More public:** you and your assets are visible for everyone to see, and is a highly entertaining and viral medium, e.g. unlike a painting hanging on a wall in your house.
* **More financial:** anyone can bid on and buy your assets 24/7/365, giving you increased liquidity and greater price discovery. This makes it particularly valuable to be early, with good judgement, before something goes viral or gains attention, and perhaps even makes it valuable to be able to market something and make it valuable.

Hence the name of the game here is really to empower the owner to be visible as the owner, to support all these goals, and to make it easy to transact in this ownership. For the creator the value is in monetising the exclusive ownership status over their content.

**Critically, owning a video, in the sense described herein, is not a claim on the intellectual property, revenue or any other rivalrous property of using the actual content itself.**

## Concepts

### NFT Owner

An NFT Owner refers to one among two distinct varieties of possible owners of a given NFT, and they are

* **ChannelOwner:** This means that whomever owns the channel in which the video to whicht he NFT corresponds, is also the owner of the NFT.
* **Member:** This means that a given specified member owns the video.

Notice that curator groups, curators or the content directory lead cannot directly own an NFT, only by owning the channel. This also implies that, as will be seen further down, neither of these actors can participate as possible beneficiaries of an NFT, for example as bidders, buyer or offer recipients.

### Auction Type

An _Auction Type_ refers to one among the two distinct varieties of auctions which can be used to reallocate ownership of an NFT, hence it is either

* **English:** An _English Auction_ is an auction where the highest bid, above some possibly set _reservation price_, is maintained and updated over time until some block in the future, called the _finalization block._
* **Open:** An _Open Auction_ is an auction which operates the same way as an English auction, except that there is no predefined duration, hence no finalization block. For this reason there is a _bid locking duration_, which is the number of blocks which must pass from the time a bid is submitted until the bidder can withdraw the bid if it is not accepted by the current owner.

In both kinds of auctions, there is the concept of a _buy now_ price, which if set, means that if any bid matches this amount at any time, the auction is automatically concluded in favour of this bid.

### Bid

A _bid_ represents a binding financial commitment from a member to aquire ownership of an NFT from the current owner at a given price in an auction, and it is defined by

* **Bidder:** The identifier of the member who is making the bid.
* **Account:** The identifier for the account which holds the committed funds, which will be encumbered by a reservation for a slong as the bid exists.
* **Amount:** The balance of funds comitted in the bid.
* **MadeAtBlock:** The block number in which the bid was created. 

Notice that only members can be bidders, no other kind of actor.

### Auction

An _auction_ represents the structured process through which the current owner can transfer ownership of an NFT through an open non-intermediated bidding process, and it is defined by the following

* **Reservation Price:** The minimum balance required for amount of any bid to be valid.
* **Type:** The [#auction-type](video-nfts.md#auction-type "mention") representing what type of auction this is.
* **Minimal Bid Step:** The minimum difference in amount between two consecutive bids in order for the new bid to be valid.
* **Last Bid:** If present, is the last [#bid](video-nfts.md#bid "mention")which was successfully submitted.
* **Starts At:** The block after which point it becomes possible to submit bids in the auction.
* **Whitelist:** The set, which if non-empty, contains the set of members who are permitted to submit bids in the auction.

### Content Actor: we will see!



* Curator(CuratorGroupId, CuratorId)
* Member(MemberId)
* Lead

xxx

### Transactional Status

The transactional _status_ of an NFT represents the state of current opportunities to change the ownership, and it has the following distinct varieties

* **Idle:** There is no currently available opportunity, and the only relevant action is to transition to noe of the other three other statuses.
* **Offered:** The current owner has extended an offer for a specific other member, called the _beneficiary_ to acquire ownership of the NFT, possibly for some require payment. In this status, the beneficiary can at any time accept the offer, which results in title transfer, or the current owner can withdraw the offer, which results in returning to the idle status.
* **Auction:** There is a currently active auction of some kind, as represented by an [#auction](video-nfts.md#auction "mention").
* **Buy Now:** Anyone can instantly become the owner by paying a given amount. The owner can change the status back to idle at any time.

The ...



### NFT

An _NFT_ represents ownership title over video, and it is defined by the following information

* **Owner:** The [#nft-owner](video-nfts.md#nft-owner "mention")representing the current owner.
* **Status: The **[#transactional-status](video-nfts.md#transactional-status "mention") representing the state of the NFT currently.
* **Royalty:** If set, it specifies the fraction of the paid value of later transactions which must accrue to the issuer.

## Parameters

The following mutable parameters.

| Name                      | Type          | Description                                    |
| ------------------------- | ------------- | ---------------------------------------------- |
| `MinRoundTime`            | `BlockNumber` | Min auction round time.                        |
| `MaxRoundTime`            | `BlockNumber` | Max auction round time.                        |
| `MinBidLockDuration`      | `BlockNumber` | Min bid lock duration.                         |
| `MaxBidLockDuration`      | `BlockNumber` | Max bid lock duration.                         |
| `MinStartingPrice`        | `Balance`     | Min auction staring price.                     |
| `MinCreatorRoyalty`       | `Perbill`     | Min creator royalty percentage.                |
| `MaxCreatorRoyalty`       | `Perbill`     | Max creator royalty percentage.                |
| `MinBidStep`              | `Balance`     | Min auction bid step.                          |
| `MaxBidStep`              | `Balance`     | Max auction bid step.                          |
| `AuctionFeePercentag`     | `Perbill`     | Auction platform fee percentage.               |
| `AuctionStartsAtMaxDelta` | `BlockNumber` | Max delta between current block and starts at. |

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

| Name             | Description                                                               | Value     |
| ---------------- | ------------------------------------------------------------------------- | --------- |
| `INVITE_LOCK_ID` | The identifier value for the lock applied to root account of a new member | `fill-in` |
| `xxx`            |                                                                           | `fill-in` |

## Extrinsics

### Issue NFT

**Parameters**

| `actor`    | The `ContentActor` attempting to issue the NFT.                |
| ---------- | -------------------------------------------------------------- |
| `video_id` | Video on which NFT is to be issued.                            |
| `royalty`  | If present, the royalty for all future auctions                |
| `metadata` | The raw metadata for the issuance.                             |
| `to`       | If present, the member who should be set as the initial owner. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Offer NFT

**Parameters**

| Name       | Description                                                               |
| ---------- | ------------------------------------------------------------------------- |
| `video_id` | The video corresponding to the NFT for which offer is to be made.         |
| `owner_id` | `ContentActor`  identifying caller.                                       |
| `to`       | The beneficiary member of the offer.                                      |
| `price`    | If present, the amount which must be paid by beneficiary to accept offer. |

#### Conditions

* WIP.

#### Effect

* WIP.



### Cancel Offer

**Parameters**

| `owner_id` | `ContentActor` identifying the caller.                            |
| ---------- | ----------------------------------------------------------------- |
| `video_id` | The video corresponding to the NFT for which offer is to be made. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Accept Offer

**Parameters**

| Name           | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| `video_id`     | The video corresponding to the NFT for which offer is to be made. |
| `recipient_id` | Identifier of beneficiary.                                        |

#### Conditions

* WIP.

#### Effect

* WIP.

### Sell NFT

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Buy NFT

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Start NFT Auction

**Parameters**

| Name               | Description                                                                                                   |
| ------------------ | ------------------------------------------------------------------------------------------------------------- |
| `auctioneer`       | ContentActor who owns NFT.                                                                                    |
| `video_id`         | Video identifier for video to which NFT corresponds.                                                          |
| `auction_type`     | AuctionType designating what kind of auction should be used.                                                  |
| `starting_price`   | Balance that sets lower bound for first valid bid amount.                                                     |
| `minimal_bid_step` | Balance that sets lower bound for how much each new bid must exceed last valid bid amount, if it exists.      |
| `buy_now_price`    | If provided, the Balance at which one would instantly be able to buy the NFT.                                 |
| `starts_at`        | If provided, the BlockNumber at which it becomes possible to bid in the auction or buy now.                   |
| `whitelist`        | Set of membership identifiers which, at leats one is provided, restricts bidders or buyers to be among these. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Cancel NFT Auction

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Make Bid

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Cancel Open Auction Bid

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.

### Complete NFT Auction

**Parameters**

| Name           | Description                       |
| -------------- | --------------------------------- |
| `root_account` | To be root account of membership. |

#### Conditions

* WIP.

#### Effect

* WIP.
