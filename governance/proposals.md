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

### Vote

Each council member can submit at most one vote per proposal, and it includes the following:

* **Rationale:** A human readable description of why they are voting as they are.
* **Type:** There three types
  * **Approve:** Proposal should be approved.
  * **Reject:** Proposal should be rejected. Additionally, it can be expressed whether it should be slashed as part of the rejection.
  * **Abstain:** Voter has no position on outcome.

### Proposal Type

A proposal type is a parametrized intention to have some effect on the platform. The set of proposal types will increase considerably in the future, and the current types are listed below. 

#### Constants

All proposal types have constant values for a shared set of parameters that are common across all types, thee are called _proposal constants._ The name and semantics of each constant is listed in the table below.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:center">Shorthand</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Voting Period</b>
      </td>
      <td style="text-align:center">VP</td>
      <td style="text-align:left">
        <p>Maximum number of blocks where one can vote.</p>
        <p>Integer no less than 1.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Gracing Limit</b>
      </td>
      <td style="text-align:center">GL</td>
      <td style="text-align:left">
        <p>Minimum number of blocks that must pass after a
          <br />proposal is approved until it has its intended effect.</p>
        <p>Integer no less than 0.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Approval Quorum</b>
      </td>
      <td style="text-align:center">AQ</td>
      <td style="text-align:left">
        <p>Number of votes cast below which the proposal cannot be approved.</p>
        <p>Integer no less than 1.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Approval Threshold</b>
      </td>
      <td style="text-align:center">AT</td>
      <td style="text-align:left">
        <p>Minimum percentage of approval votes as a share of
          <br />all cast votes that result in approval.</p>
        <p>Integer in [0, 100].</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Slashing Quorum</b>
      </td>
      <td style="text-align:center">SQ</td>
      <td style="text-align:left">
        <p>Number of votes cast below which the proposal
          <br />cannot be slashed.</p>
        <p>Integer no less than 1.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Slashing Threshold</b>
      </td>
      <td style="text-align:center">ST</td>
      <td style="text-align:left">
        <p>Minimum percentage of cast votes as share that slash relative
          <br />to those that vote approve, abstain or reject.</p>
        <p>Integer in [0, 100].</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Stake</b>
      </td>
      <td style="text-align:center">S</td>
      <td style="text-align:left">
        <p>Exact stake required to create a proposal of this type.</p>
        <p>Integer no less than 0.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Constitutionality</b>
      </td>
      <td style="text-align:center">C</td>
      <td style="text-align:left">The number of councils in that must approve the proposal
        <br />in a row before it has its intended effect.
        <br />Integer no less than 1.</td>
    </tr>
  </tbody>
</table>

#### Parameters: General & Specific

Whenever a proposal of a given type is created, the proposer must provide values for a set of parameters. The parameters fall into one of two categories: _general_ and _type-specific_. Each parameter will also have some constraint on the valid range of values. The general proposal parameters are

* **Proposer:** Member identifier of the proposer.
* **Title:** A human readable title.
* **Rationale:** A human readable description text that is intended to hold the rationale for the proposal should be accepted. It is expected that some social convention will emerge on the appropriate encoding of this text, for example markdown, that would facilitate consistent input and display across client applications.
* **Trigger:** An optional block number where the proposal is to be executed.
* **Staking Account:** The account that holds the funds that will be locked for staking, if required.

The type-specific parameters for each proposal type are listed with the proposals below.

#### Creation Conditions

When a proposal is submitted, a set of conditions on the values of the input parameters \(only\) are evaluated, these are called _creation conditions_, and creating the proposal fails if they are not satisfied. These are things like for example respecting the upper bound on the amount of money you are asking for in a spending proposal. Importantly, these checks are _pure_, they only depend on parameters, not the state of the system.

#### Execution Conditions

A proposal may be approved, and at some point the actual business logic that embodies its intended effect has to be executed. This is always much later than when the proposal was first created, and it may very well be possible to have a proposal which originally looked would have had its intended effect to no longer be applicable because the state of he system has changed in the intermediate. An example could be that a funding proposal requires more money than the council currently can spend due to other spending that may have occurred since the proposal was approved. These conditions are called _execution conditions_, and importantly, they are not checked at any time prior to execution of this business logic.

### Proposal

A proposal is defined by the following information

* **Type:** Which type of proposal this is.
* **General Parameters:** Values for general proposal parameters.
* **Type-Specific Parameters:** Values for type-specific proposal parameters.
* **Stage:**  The life-cycle stage of a proposal, as defined precisely in the next section.
* **Votes:** The set of votes currently associated with the proposal.
* **Council Approvals:** How many prior councils have approved the proposal, starts at 0.
* **Discussion:** A single threaded discussion about the proposal, as defined in the discussion section.

**Stage**

Below is a list of the stages a proposal can be in, and what each of them mean:

* **Deciding:** Initial stage for all successfully created proposals. This is the only stage where votes submitted can actually impact the outcome. Lasts for up to VP blocks from when stage begins. When a vote is submitted it is evaluated as such:  


  * If AQ and AT will be satisfied regardless of what additional votes will arrive, then increment council approvals counter. If counter now is C then transition to gracing stage, otherwise  transition to dormant stage.
  * If SQ and ST will be satisfied, and AQ and AT will not, regardless of what additional votes arrive, then slash full stake and transition to the rejected stage.

  
  If VP blocks pass while still in this stage, apply normal checks for approval and slashing in order, with same transition and side-effect rules as the two above. If neither are satisfied, transition to rejected stage and slash rejection fee \(see [Proposals](proposals.md#constants-1)\).

* **Dormant:** Was approved by current council, but requires further approvals to satisfy constitutionality requirement. Transitions to deciding stage when next council is elected.
* **Gracing:** Is awaiting execution for until trigger block, or GL blocks since start of period if no trigger was provided. When this duration is over, the execution conditions are checked, if they are satisfied the proposal transitions to the execution succeeded stage, if they are not, it transitions to the execution failed stage. 
* **Vetoed:** Was halted by SUDO, nothing further can happen. This is removed at mainnet.
* **Execution Succeeded:** Execution succeeded, nothing further can happen.
* **Execution Failed:** Execution failed due to unsatisfied execution conditions, nothing further can happen.
* **Rejected:** Was not approved, nothing further can happen.

It useful to designate any proposal in the stages deciding, dormant or gracing, as an _active proposal_, and any other proposal is said to be an _inactive proposal._

Two extra transition rules are worth bearing in mind

* If number of blocks since decision stage starting is less than VP, then votes can still be submitted, but they have no impact on any outcome when outside of decision stage.
* For any active proposal, SUDO can initiate veto, which results in transition to vetoed stage.

The stages and transitions, excluding SUDO dynamics, are summarized in the image below.

![Stages and transitions in life-cycle of a proposal.](../.gitbook/assets/proposal_2-1-.png)

### Discussion

A single threaded discussion is opened for each successfully created discussion. A thread can be in two modes, open or closed. In open mode, any member can post a message, while in closed mode, only the active council, the original proposer, or one among a set of whitelisted members can post. Mode can be changed by member or council member at any time, and default mode is open. Both council members and proposer can curate whitelist by adding and removing members. A poster can edit a post an unlimited number of times, but only if they have access. A thread can no longer be edited when a certain number of blocks \(see [Proposals](proposals.md#constants-1)\) have passed since being rejected or executed. Lastly, there is total cap on the number of posts that can be posted in a single thread \(see [Proposals](proposals.md#constants-1)\).

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
| Constitutionality |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

There is no direct effect of this proposal, its utility is purely for social coordination of matters outside of the direct state of the blockchain state.

### Runtime Upgrade

NB!!! fix here to use new scheme from 1057.

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
| Approval Threshold |  |
| Slashing Quorum |  |
| Slashing Threshold |  |
| Proposal Stake |  |
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

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
| Constitutionality |  |

#### Creation Conditions

_xxx_

#### Execution Conditions

_xxxx_

#### Effect

To avoid the Lead paying themselves too much, or frivolous spending in general, the Lead can only spend as much as the Mint Capacity. Effectively, a budget for their spending. Once the Mint runs out, recurring rewards for the Content Curators \(including themselves\) will be frozen.

If the Lead, or anyone else, wants to replenish or drain the existing Mint, a proposal can be made. If voted in, the new Capacity proposed will be set immediately.

## Constants

* Rejection Fee: Up to number of tokens slashed if prosal rejected, but not with slashing.
* Number of blocks after reject/execute a proposal discussion is closed.
* Max posts per thread
* Max active proposals allowed at any given time

Here are the values of these parameters for each proposal

| Proposal | VP | GP | AQ | AT | SQ | ST | PS | C |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Runtime Upgrade | 1230 | 12301 | 45 | 21 | 10 | 5 | 100,00,00 |  |
| c |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |

## Operations

xxxdd

### Submit Proposal

The number of active proposals &lt; fixed number

The conditions are

1. Signer is controller account of referenced proposer.
2. If trigger is provided, that block must be greater than the current block plus DP+GL.
3. If S &gt; 0 then there must be provided a staking account, and it must be signed with, and it must have a free balance no less than S, and the only other lock which may exist on it is an election related lock.
4. Creation conditions are satisified.

### Vote

xx

Add informatino here about how exactly the logic for doing premature state transitioning works.!!!!!

### Post to Thread

xx

### Edit to Post

xx

### Change Thread Mode

xx

### Add to Thread Whitelist

xx

### Remove from Thread Whitelist

xxx

## Events

New council elected...any non finalized has all stage & votes reset. All finalized for next period pending are reset.  
what happens to cosnitutinality counter???? =&gt; reset, cause it failed



Close Thread

## Example

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

