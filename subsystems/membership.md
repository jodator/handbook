
# Membership

## Introduction

The membership subsystem is responsible for storing and managing all memberships on the platform, as well as enabling the creation of new memberships, and the terms under which this may happen. A membership is a representation of an actor on the platform, and it they exist to serve the following purposes

- **Profile:** A membership has an associated rich profile that includes information that support presenting the actor in a human friendly way in applications, much more so than raw accounts
- **Reputation:** Facilitates the consolidation of all activity under one stable identifier, allowing an actor to invest in the reputation of a membership through prolonged participation with good conduct. This gives honest and competent actors a practical way to signal quality, and this quality signal is a key screening parameter allowing entry into more important and sensitive activities. While nothing technically prevents an actor from registering for multiple memberships, the value of doing a range of activities under one membership should be greater than having it fragmented, since reputation, in essence, increases with the length and scope of the history of consistent good conduct.
- **Recovery:** By binding other roles and activities to a membership, it becomes possible to recover control of those roles even if accounts used to authenticate for those roles are lost.

It's important to be aware that a membership is not an account, but a higher level concept that involves accounts for authentication.

## Concepts

### Membership

A membership includes the following in the blockchain state:

- **Id:** A unique immutable non-negative integer identifying the member, automatically assigned when membership is created.
- **Root Account:** A required account that is used only to update the controller account. Need not be unique across members, but in practice probably will be.
- **Controller Account:** A required account that is used to authenticate as the member, both in this and other parts of the platform. Need not be unique across members, but in practice probably will be.
- **Handle:** Hash of a unique mutable string handle.
- **Invites:** A non-negative integer that represents how many invitations this member has.

Moreover, the blockchain history also includes a most recent value of the following:

- **Avatar:** URI for an avatar image.
- **About:** Human readable text description.
- **Founding Member**: A signifier that this member holds some specific historical significance to the launch of the platform. This value will be stored in the chain state when mainnet launches, but for now, since we want to grant founding member status on an ongoing member through a SUDO call, this is in history.
- **Rank/score**: Gamification of level? ()

### Membership Working Group

....

### Roles

The membership subsystem includes

#### Lead

A designated member, who also would be the lead in the working group corres

....stuff around lead giving out invites...
... all other stuff that screeners do

#### Screener

... gives out invites to others


## State

- #memberships ever
- memberships
- total invite budget
- membership price
- referral cut amount
- default invites value

## Constants

... add here

## Operation

...

### Buying a Membership

A platform membership can be obtained by registering for one. There is a small fee \(in tJOY\) associated with this to prevent spam registrations. This is currently `100 JOY`.

All of the memberships from the Acropolis testnet have been migrated across to the Rome testnet and given a starting balance \(at the genesis block\) of `2000 JOY`.  For this reason, participants in Acropolis will not need to register again.

params: default invites value

### Invite Member

A member with a non-zero number of invites may create a new member, providign the same inputs as when a membershpi is bought, resulting in a reduction in the invites value if successful. The main difference to a bought membership

### Grant Invites

...

### Update Profile

- change about text
- change change handle (es)
- update controlelr account
- udate root account

### Update Accounts

...

### Tether Account

bind accounts? to it.. to be used for staking, unbind?



## Proposals

....
