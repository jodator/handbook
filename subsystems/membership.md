# Membership

## TODO

* fix issue with cretidting invited users, and adding lock, mention lock somewhere. also explain that changing out controller account is best way to escape lock later.
* Add account hierarcht ide in here? or somewhere else?

## Introduction

A membership is a representation of an actor on the platform, and it they exist to serve the following purposes

* **Profile:** A membership has an associated rich profile that includes information that support presenting the actor in a human friendly way in applications, much more so than raw accounts
* **Reputation:** Facilitates the consolidation of all activity under one stable identifier, allowing an actor to invest in the reputation of a membership through prolonged participation with good conduct. This gives honest and competent actors a practical way to signal quality, and this quality signal is a key screening parameter allowing entry into more important and sensitive activities. While nothing technically prevents an actor from registering for multiple memberships, the value of doing a range of activities under one membership should be greater than having it fragmented, since reputation, in essence, increases with the length and scope of the history of consistent good conduct.
* **Recovery:** By binding other roles and activities to a membership, it becomes possible to recover control of those roles even if accounts used to authenticate for those roles are lost. \(Rewrite & update, expand\)

It's important to be aware that a membership is not an account, but a higher level concept that involves accounts for authentication.

The membership subsystem is responsible for storing and managing all memberships on the platform, as well as enabling the creation of new memberships, and the terms under which this may happen.

## Concepts

### Membership

A membership includes the following in the blockchain state:

* **Id:** A unique immutable non-negative integer identifying the member, automatically assigned when membership is created.
* **Root Account:** A required account that is used only to update the controller account. Need not be unique across members, but in practice probably will be.
* **Controller Account:** A required account that is used to authenticate as the member, both in this and other parts of the platform. Need not be unique across members, but in practice probably will be.
* **Name:** Hash of a mutable human readable mutable string.
* **Handle:** Hash of a unique mutable string handle.
* **Invites:** A mutable non-negative integer that represents how many invitations this member has.
* **Verified:** A mutable boolean indicator that reflects whether the implied real world identity in the profile corresponds to the true actor behind the membership.
* **Avatar:** Hash of a mutable URI for an avatar image.
* **About:** Hash of a mutable human readable text description.
* **Founding Member**: A signifier that this member holds some specific historical significance to the launch of the platform. This value will be stored in the chain state when mainnet launches, but for now, since we want to grant founding member status on an ongoing member through a SUDO call, this is in history.
* **Staking Accounts:** A set of accounts that have been bound to this membership for the purpose of holding staked funds. One account can only be used to stake for at most two separate purposes simultaneously, and one of them has to be an election related purpose, i.e. voting or council candidacy. One account can only be a staking account for a single member, and once associated in this way, it cannot be deassociated and associated with another member.

### Membership Working Group

The membership subsystem has a working group. The purpose of the group is to effectively distribute invitation quotas and verified status. The lead has the extra task of refreshing the quotas to workers, which they can in turn then distribute to other members. Workers are referred to as _membership evangelists_.

## State

The system holds the following important on-chain state variables

* All memberships.
* The identifier value for the next membership to be created.
* The price of a membership.
* The referral cut of the membership price diverted to a referrer when buying a membership.
* The default number of invitations set for a new bought membership.
* The total invites budget from which the lead can distribute invitations to other members.
* The next block where the total invites budget will be set to some new specific value.

## Constants

**TBD.**

## Operation

These are the operations possible in this subsystem.

### Buying a Membership

Buying a membership requires an account holder to provide

* Root account
* Controller account
* Name
* Handle
* Avatar URI
* About field
* An optional membership listed as the referrer.

The originating account must have sufficient balance to cover the current membership price. The new membership will

* not be verified
* not be a founding member
* get an id equal to the current next id value
* get an invitation count equal to the current default value

If a referrer is listed, then some share of the price is diverted into the controller account of that member. The remaining membership price is burned.

### Invite Member

A member, signing with the controller account, with a non-zero number of invites may create a new member, providing the same inputs as when a membership is bought, resulting in a reduction in the invites value if successful. The main difference to a bought membership is that the invitation count is zero.

### Update Profile

A member, signing with the controller account, may update one or more of the following

* Name
* Handle
* Avatar URI
* About field

### Transfer Invites

A member can transfer part of invitation budget to another member.

### Update Accounts

A member, signing with the root account, can update the root or controller accounts, or both.

### Update Verified Status

A evangelist or lead can update the verified status of a member to a new value.

### Bind Staking Account

Binds a given account, which is signer, to a given membership, provided the account is not already bound to some other membership.

