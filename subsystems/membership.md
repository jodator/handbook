
# Membership

## Introduction

A membership is a representation of an actor on the platform, and it they exist to serve the following purposes

- **Profile:** A membership has an associated rich profile that includes information that support presenting the actor in a human friendly way in applications, much more so than raw accounts
- **Reputation:** Facilitates the consolidation of all activity under one stable identifier, allowing an actor to invest in the reputation of a membership through prolonged participation with good conduct. This gives honest and competent actors a practical way to signal quality, and this quality signal is a key screening parameter allowing entry into more important and sensitive activities. While nothing technically prevents an actor from registering for multiple memberships, the value of doing a range of activities under one membership should be greater than having it fragmented, since reputation, in essence, increases with the length and scope of the history of consistent good conduct.
- **Authentication:** By binding other accounts to a membership up front, it becomes easy for the actor to indirectly authenticate control over those accounts with a single updatable key later.
- **Recovery:** By binding other roles and activities to a membership, it becomes possible to recover control of those roles even if accounts used to authenticate for those roles are lost.

It's important to be aware that a membership is not an account, but a higher level concept that involves accounts for authentication.

## Memberships

A membership includes the following in the blockchain:

- **Id:** A unique immutable non-negative integer identifying the member.
- **Root Account:** A required account that is used only to update the controller account. Need not be unique across member, but in practice probably will be.
- **Controller Account:** A required account that is used to authenticate as the member, both in this and other parts of the platform. Need not be unique across members, but in practice probably will be.
- **Tethered Accounts:** A list of accounts that have been associated with the membership.
...... uniqueness? remove, after tethered? (Perhaps this needs to be changed??)
- **Handle:** A unique string handle.
- **Avatar:** An optional URI for an avatar image.
- **About:** An optional human readable text description.
- **Invites** A non-negative integer that represents how many invitations this member has.

## Lead

....stuff around lead giving out invites...

## Actions

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
- change change handle
- update controlelr account
- udate root account

### Update Accounts

...

### Tether Account

bind accounts? to it.. to be used for staking, unbind?

### Constants

... add here
