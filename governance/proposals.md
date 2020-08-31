---
description: >-
  The proposal system is the way changes to the platform state and policy are
  suggested, discussed, voted on by the council, and finalized as accepted or
  rejected.
---

# Proposals

## Introduction

A proposal is a motion to change the state or policy of the system in some way. There are a wide variety of such proposal types, each type having a different

* set of required input parameter values
* requirements and risks of proposing
* barrier for getting accepted
* delay to being put into motion when accepted

The reason for this differentiation across types is because different proposals have very different effects, and carry very different risks of failure or abuse. The proposal system has the responsibility of coordinating the different actors involved in the lifetime of a proposal, from submission to finalization.

## Actors

The relevant actors in the proposal system are

* **Proposer:** A member that has submitted an instance of a specific proposal type. A given member can submit multiple proposals at once, or over time.
* **Council Members:** They are tasked with voting on proposals, which determines whether the proposals are accepted or not, as well as discussing a proposal with the proposer, and leaving a rationale for their vote.

## Concepts

### Proposal Type

A proposal type is a parametrized intention to have some effect on the platform. The set of proposal types will increase considerably in the future, and the current types are listed below. 

#### Constants

All proposal types have constant values for a shared set of parameters that are common across all types, thee are called _proposal constants._ The name and semantics of each constant is listed in the table below.

| **Name** | Shorthand | Description |
| :--- | :---: | :--- |
| **Voting Period** | VP | Maximum number of blocks where one can vote. |
| **Grace Period** | GP | Number of blocks after a proposal is approved until it has its effect. |
| **Approval Quorum** | AQ | Number of votes required to be cast before a proposal can be approved, although this is not a sufficient condition for approval. |
| **Approval Threshold** | AT | Minimum percentage of approval votes as a share of  all cast votes that result in approval. |
| **Slashing Quorum** | SQ | Minimum votes required to be cast before a proposal can be slashed, lead to slashing the stake of the proposer. |
| **Slashing Threshold** | ST | Minimum percentage of cast votes as share  that slash relative to those that vote approve, abstain or reject.  |
| **Proposal Stake** | PS | Minimum stake required to create a proposal of this type. |

#### Parameters: General & Specific

Whenever a proposal of a given type is created, the proposer must provide values for a set of parameters. The parameters fall into one of two categories: _general_ and _type-specific_. Each parameter will also have some constraint on the valid range of values. The general proposal parameters are

* **Proposer:** Member identifier of the proposer.
* **Title:** A human readable title.
* **Rationale:** A human readable description text that is intended to hold the rationale for the proposal should be accepted. It is expected that some social convention will emerge on the appropriate encoding of this text, for example markdown, that would facilitate consistent input and display across client applications.
* **Staking Account:** The account that holds the funds that will be locked for staking, if required.

The type-specific parameters for each proposal type are listed with the proposals below.

### Proposal

A proposal is defined by the following information

* **Type:** Which type of proposal this is.
* **General Parameters:** Values for general proposal parameters.
* **Type-Specific Parameters:** Values for type-specific proposal parameters.
* **State:**  xxxx
* **Discussion:** xxx

mmmmmm

**States and Outcomes**

Below is a list of the states a proposal can be in, and what each of them means:

* `Active` - the proposal can be voted on, and no resolution has been made
* `Grace Period` - the proposal has been approved, and is awaiting execution
* `Executed` - the proposal was approved, and, after a potential `Grace Period`, executed on chain
* `Execution Failed` - the proposal was approved, and, after a potential `Grace Period`, attempted to be executed on chain. For some reason, the execution failed
* `Rejected` - the proposal was rejected by the council
* `Slashed` - the proposal was rejected, and the stake of proposer was slashed by the council
* `Expired` - the council members did not reach consensus and the proposal expired without any action. This can be the result of insufficient voter turnout, or disagreement between the council members

### Vote

A voter can choose between the following outcomes:

* `Approve` - approving the proposed action
* `Reject` - reject the proposed action
* `Slash` - reject the proposed action, and slash the stake of the proposer
* `Abstain` - abstain from voting



### Discussion

xxxxx

## General Proposals

This section includes proposals that concern the platform as whole in terms  intended effect and type-specific parameters.

### Signal

#### Parameters

| Name | Description |
| :--- | :--- |
| Signal | The actual human readable signaling text. |

Note that the distinction between this signal text parameter and the rationale parameter is that the rationale is the _why_ and this signal is the _what._

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

There is no direct effect of this proposal, its utility is purely for social coordination of matters outside of the direct state of the blockchain state.

### Runtime Upgrade

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

The block after this proposal is executed will follow the rules of the runtime captured in the provided Wasm blob.

### Funding Requests

#### Parameters

| Name | Description |
| :--- | :--- |
| Amount | The amount of tokens requested |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

In general, this proposal will include an amount, and a beneficiary. This can be used in to fund development, pay winners of competitions, bonus payments for a role, or anything else that requires minting new tokens to a specific individual or group.

### Set Election Parameters

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

As the Council will see a significantly increased workload, there may be need to change the some of the Election cycle parameters. This proposal allows the Council to vote on expanding the Council seats, increase or decrease the length of the Voting process, or the minimum stakes required to participate. If this proposal is voted through, a change of these parameters will not be activated until the next election cycle, to avoid the current Council making changes benefitting themselves.

### Add Working Group Leader Opening

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

This proposal allows an opening for a Storage Lead to be created. When editing the "Opening schema", you must ensure your changes still returns a valid JSON schema. This determines what information is collected from candidates. Note that the reward specified is not binding, and is only determined when the Fill Working Group Leader Opening proposal is made \(and approved\).

### Begin Review Working Group Leader Application

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

This simply sets the opening for Storage Lead to the "in review" status, meaning no further applications can be accepted. It is required to move on to the `Fill Working Group Leader Opening` proposal.

### Fill Working Group Leader Opening

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

If the Opening is in the "Review Stage", use this proposal to propose a specific Lead. The Council can now vote, and, if approved, this will be the new Lead.

Note that there can be multiple proposals of this type at the same time, so multiple candidates can be considered simultaneously. However, once one is approved, the others will fail.

### Set Working Group Mint Capacity

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

This effectively acts as a budget for the working group \(currently referring to the Storage Working Group\). The Storage Lead will be unable to spend more than the limit established by this proposal.

### Slash Working Group Leader Stake

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

To punish or warn the Storage Lead for not performing their job correctly, they can be slashed partially or fully without firing them using this proposal type.

### Decrease Working Group Leader Stake

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

This proposal type allows decreasing the stake of the Storage Lead.

### Set Working Group Leader Reward

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

This proposal allows for changing the reward for the Storage Lead if it appears too little or too much. Note that only the amount can be changed, not the frequency.

### Terminate Working Group Leader Role

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

If for whatever reason the Storage Lead needs to be removed from their post \(and potentially slashed\), this is the proposal type which needs to be voted on.

## Validation Proposals

### Set Max Validator Count

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

The Validators are rewarded for producing blocks, and will share the rewards that are minted each era \(target 3600 blocks\). This reward is calculated based on the total issuance, and the amount of tJOY staked by the pool of Validators relative to the total issuance. A higher number means smaller rewards for each individual Validator, but set to low and the network grinds to a halt.

## Content Directory Proposals

### Set Content Curator Lead

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

The Content Curator Lead is the first implementation of the concept of Group Leads on the platform. These will in general be responsible for hiring, firing, rewarding and training the group they are leading. They are hired by the council, and will be given a budget to perform their role satisfactory, without inflating the supply more than necessary.

This means they have to answer to the users if they fail in their task. In this particular case, all members can propose to:

* Set a Lead if there are none currently occupying the role
* Fire the existing Lead, without setting a new one
* Replace the existing Lead, with a specified new member

If the proposal is voted through, the change will occur immediately.

### Set Content Working Group Mint Capacity

#### Parameters

| Name | Description |
| :--- | :--- |
| Wasm blob | The raw Webassembly object to be used as the new runtime. |

#### Constants

| Constant | Value |
| :--- | :--- |
| Voting Period |  |
| Grace Period |  |
| Approval Quorum |  |
| Approvial Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

To avoid the Lead paying themselves too much, or frivolous spending in general, the Lead can only spend as much as the Mint Capacity. Effectively, a budget for their spending. Once the Mint runs out, recurring rewards for the Content Curators \(including themselves\) will be frozen.

If the Lead, or anyone else, wants to replenish or drain the existing Mint, a proposal can be made. If voted in, the new Capacity proposed will be set immediately.

## State

x

x

x

## Constants



Here are the values of these parameters for each proposal

| Proposal | VP | GP | AQ | AT | SQ | ST | PS |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Runtime Upgrade | 1230 | 12301 | 45 | 21 | 10 | 5 | 100,00,00 |
| c |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |

Max proposal at any given time.



## Operation

xxxddd

### General

discuss

vote

withdraw



### General Proposals

#### Text/signal Proposal

Although no action will happen if such a proposal is voted through, it provides a way for user to request changes, propose improvements, complaint about something, and in general voice their opinion on a matter. This will open a discussion, and Council Member can signal their approval or rejection through a vote. This can be used to notify the platform developers about key feature missing, highlight a topic of controversy, etc.

#### Runtime Upgrade

As before, upgrading the runtime can be proposed by any member, and voted in by the Council. This is a critical proposal that, if a "bad" runtime is proposed and voted in, can kill the blockchain.

#### Funding Requests

In general, this proposal will include an amount, and a beneficiary. This can be used in to fund development, pay winners of competitions, bonus payments for a role, or anything else that requires minting new tokens to a specific individual or group.

#### Set Election Parameters

As the Council will see a significantly increased workload, there may be need to change the some of the Election cycle parameters. This proposal allows the Council to vote on expanding the Council seats, increase or decrease the length of the Voting process, or the minimum stakes required to participate. If this proposal is voted through, a change of these parameters will not be activated until the next election cycle, to avoid the current Council making changes benefitting themselves.

#### Add Working Group Leader Opening

This proposal allows an opening for a Storage Lead to be created. When editing the "Opening schema", you must ensure your changes still returns a valid JSON schema. This determines what information is collected from candidates. Note that the reward specified is not binding, and is only determined when the Fill Working Group Leader Opening proposal is made \(and approved\).

#### Begin Review Working Group Leader Application

This simply sets the opening for Storage Lead to the "in review" status, meaning no further applications can be accepted. It is required to move on to the `Fill Working Group Leader Opening` proposal.

#### Fill Working Group Leader Opening

If the Opening is in the "Review Stage", use this proposal to propose a specific Lead. The Council can now vote, and, if approved, this will be the new Lead.

Note that there can be multiple proposals of this type at the same time, so multiple candidates can be considered simultaneously. However, once one is approved, the others will fail.

#### Set Working Group Mint Capacity

This effectively acts as a budget for the working group \(currently referring to the Storage Working Group\). The Storage Lead will be unable to spend more than the limit established by this proposal.

#### Slash Working Group Leader Stake

To punish or warn the Storage Lead for not performing their job correctly, they can be slashed partially or fully without firing them using this proposal type.

#### Decrease Working Group Leader Stake

This proposal type allows decreasing the stake of the Storage Lead.

#### Set Working Group Leader Reward

This proposal allows for changing the reward for the Storage Lead if it appears too little or too much. Note that only the amount can be changed, not the frequency.

#### Terminate Working Group Leader Role

If for whatever reason the Storage Lead needs to be removed from their post \(and potentially slashed\), this is the proposal type which needs to be voted on.

### Validation Proposals

#### Set Max Validator Count

The Validators are rewarded for producing blocks, and will share the rewards that are minted each era \(target 3600 blocks\). This reward is calculated based on the total issuance, and the amount of tJOY staked by the pool of Validators relative to the total issuance. A higher number means smaller rewards for each individual Validator, but set to low and the network grinds to a halt.

### Content Directory Proposals

#### Set Content Curator Lead

The Content Curator Lead is the first implementation of the concept of Group Leads on the platform. These will in general be responsible for hiring, firing, rewarding and training the group they are leading. They are hired by the council, and will be given a budget to perform their role satisfactory, without inflating the supply more than necessary.

This means they have to answer to the users if they fail in their task. In this particular case, all members can propose to:

* Set a Lead if there are none currently occupying the role
* Fire the existing Lead, without setting a new one
* Replace the existing Lead, with a specified new member

If the proposal is voted through, the change will occur immediately.

#### Set Content Working Group Mint Capacity

To avoid the Lead paying themselves too much, or frivolous spending in general, the Lead can only spend as much as the Mint Capacity. Effectively, a budget for their spending. Once the Mint runs out, recurring rewards for the Content Curators \(including themselves\) will be frozen.

If the Lead, or anyone else, wants to replenish or drain the existing Mint, a proposal can be made. If voted in, the new Capacity proposed will be set immediately.

## Examples

Suppose there are currently 20 members of the council. A proposal to set max validator count is made, where the parameters below apply:

| Proposal Parameters | Value |
| :---: | :---: |
| `voting_period` | 43,200 |
| `grace_period` | 0 |
| `approval_quorum_percentage` | 50% |
| `approval_threshold_percentage` | 75% |
| `slashing_quorum_percentage` | 60% |
| `slashing_threshold_percentage` | 80% |
| `required_stake` | 25,000 |

A member puts up the required stake of 25,000 tJOY, and the proposal goes the `active` stage at block height 100,000.

**Voting Scenario A**

The votes come in, until we have:

* 6 `Approve`
* 0 `Reject`
* 0 `Slash`
* 0 `Abstain`

At this point, the `Approval Quorum` parameter is fulfilled \(100%&gt;75% approval\), but there are still to few votes cast to fullfill the `Approval Threshold` \(at 30%&lt;50%\).

A few more votes are cast:

* 6 `Approve`
* 1 `Reject`
* 1 `Slash`
* 1 `Abstain`

At this point, neither the `Approval Quorum` parameter \(67%&lt;75% approval\), nor the `Approval Threshold` \(at 45%&lt;50%\), is fulfilled.

Another vote comes in:

* 6 `Approve`
* 2 `Reject`
* 1 `Slash`
* 1 `Abstain`

At this point, `Approval Quorum` parameter \(60%&lt;75% approval\) is not fulfilled, whereas the `Approval Threshold` \(50%\), is now fulfilled.

A few more votes are cast:

* 8 `Approve`
* 2 `Reject`
* 1 `Slash`
* 1 `Abstain`

At this point, `Approval Quorum` parameter \(67%&lt;75% approval\)\) is not fulfilled, whereas the `Approval Threshold` \(50%\), is now fulfilled.

A final vote for `Approve` is cast, and the

