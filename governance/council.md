---
description: >-
  The politically selected governance body responsible for managing the proposal
  system for the benefit of voters.
---

# Council

## NOTES

* recall that failure is both in too fe candidates and in not enough votes reveald...
* voters only locked in until election starts
* candidacy is locked in until loss or next council elected.

## Introduction

The council is a political organ 

* political
* fast- day to day: stand in representation of the full set of stakeholders on a day to day basis.

## Roles

The relevant roles in the council system are

* **Voters:** Anyone who stakes for the purposes of influencing the outcome of an election. Is not tied to membership, so a member can vote multiple times for different candidates from different accounts.
* **Candidate:** A member who has staked and stands as an alternative for council membership in an ongoing election cycle.
* **Council Member:** A member who has stood as a candidate in an election and won a place in a council. Has the primary responsibility to participate in voting on and deliberating around proposals in the proposal system.

## Concepts

### Staking

xxvoting locks, even odd council locks.  
....

### Budget

The budget of the council is the root resource pool for all token minting on the platform, _with the exception of validator rewards_. The lifetime of the budget is divided into periods, called _budget periods_, which occurs every `BUDGET_PERIOD_LENGTH` blocks. Whenever one of the following actions occur, the budget is impacted as described.

| Event | Budget Impact |
| :--- | :--- |
| Working group budget increased by `X > 0` |  `-X` |
| Working group budget decreased by `X > 0` | `+X` |
| Spending proposal with amount `X > 0` | `-X` |
| Council reward payout `X > 0` | `-X` |
| Budget period ends | `+budget_increments` |

Events that negatively impact the budget balance can only occur if the impact does not occur if they exceed the balance of the budget.

_Notice that working group spending, such as lead spending, or subsystem specific spending, such as minting initial credit for invited new members, does not directly count against the council budget, but against the relevant working group budget._

### **Council**

The council has a fixed number of seats `NUMBER_OF_COUNCIL_SEATS` occupied by members. The seats are always occupied, allowing the platform to dispose of all proposals they may come in at any time. The council body has two high level states described as follows.

* **Normal:** During this stage the council operates normally. After `NORMAL_PERIOD_LENGTH` blocks have passed since this period started, a transition is made to the election stage.
* **Election:** During this stage, not only does the council operate, but there is an election ongoing. Read more about elections the [Council](council.md#election) section below.

During both these stages, the following can or does occur.

#### Unstaking Failed Candidacy

If someone announced their candidacy in an election, but did not end up winning, then they can at any time after the conclusion of that election cycle free their stake

#### Unstaking Vote

If someone voted for a candidate in an election, they will and can free their stake at a later time. Importantly, a vote which was devoted to a losing candidate can be freed the moment the election cycle is over, while a vote which was devoted to a winner can only be freed after the announcing period of the next election begins. The idea behind this asymmetry is to lock ....

#### Rewards

Every `REWARD_PERIOD_LENGTH` blocks all council members are paid out the same flat reward rate `council_member_reward` and any possibly outstanding owed reward. During this payout, where council members are processed in some consistent order, the crediting only occurs while the budget constraint is respected. For each payout, the constraint is tightened. If a council member cannot be paid out in full, then the difference is added to their owed reward. When a council period ends, any owed reward and outstanding reward from the last payout, are attempted paid out, however if the budget does not allow it, then the council member suffers the loss. 

### Candidate

A candidate is defined by the following information

* **Id:** A unique immutable non-negative integer identifying a candidate, automatically assigned when candidacy is announced successfully.
* **Member:** The member behind the candidacy.
* **Program:** A human readable description of the candidacy. Some socially enforced schema for the encoding of the program.
* **Staking account:** The account holding the

### Council Member

A council membership is defined by the following information

* **Id**: A unique immutable non-negative integer identifying a council member, automatically assigned when a council member is elected.
* **Member:** The membership to which this role corresponds.
* **Role account**: The account currently used to authenticate as this role in the relevant subsystem. Authentication in the working group is done using the controller account of the member, so as to allow for division of labor behind a single membership across multiple roles, while not requiring full trust. Is updatable by member.
* **Reward account**: The destination account to which periodic rewards are paid out.
* **Staking account:** Holds the stake currently associated with the role. .
* **Owed reward:** The total reward this council member was not paid over a number of payout periods where there was not sufficient funds in the council budget.
* **Ending statement:** An optional mutable human readable statement a council member can provide which relfects their view on the council period.

### Vote

A vote is a defined by the following

* **Id:** ....
* **Candidate:** ...
* Staking account: ...
* **Staking balance:** ...
* **Cycle Id:** ...
* **Commitment:** ...

### Election

An election is the periodic process by which a new council is selected by voters among candidates running for a seat on the next council. Elections occur periodically, and each one has a sequence of stages referred to as the election cycle. An election will begin while the current council is active, and the sitting council is only relieved once a new one has been successfully elected. As will become clear, this process can go on for a unknown amount of time.

State  
candidates: member -&gt; candidate  
Announcing Block: when we started:  
whether cylce is odd or even!!



* **Announcing Period:** This is the first stage in the election cycle. During this time members can announce that they will stand as candidates for the next council. The same member can only  When time wxpired.... enough people or not? reset everyone and start over.
* **Voting Period:** This is the stage where voters can submit votes in favour of candidates.
* **Revealing Period:** ...

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:center">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>NUMBER_OF_COUNCIL_SEATS</code>
      </td>
      <td style="text-align:left">The number of council seats.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>NORMAL_PERIOD_LENGTH</code>
      </td>
      <td style="text-align:left">The number of blocks in the normal period.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>VOTING_PERIOD_LENGHT</code>
      </td>
      <td style="text-align:left">The number of blocks in the voting period.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>REVEALING_PERIOD_LENGTH</code>
      </td>
      <td style="text-align:left">The number of blocks in the revealing period.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>REWARD_PERIOD_LENGTH</code>
      </td>
      <td style="text-align:left">The number or blocks between each reward
        <br />payout to council members.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BUDGET_PERIOD_LENGTH</code>
      </td>
      <td style="text-align:left">
        <p>The number of blocks between each time the the</p>
        <p>council budget is topped up.</p>
      </td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
  </tbody>
</table>

## Parameters

Parameters are on-chain values that can be updated through the proposal system in order to alter the constraints and functionality of the council system.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>budget_increments</code>
      </td>
      <td style="text-align:left">The amount of tokens added to budget at end of each budget period.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>council_member_reward</code>
      </td>
      <td style="text-align:left">
        <p>The number of tokens to be paid to each council member</p>
        <p>in each reward payout.</p>
      </td>
    </tr>
  </tbody>
</table>

## Operations

### Announce Candidacy

**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

### Submit Sealed Vote

**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

### Reveal Vote

**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

### Recover Voting Stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

### Recover Candidacy Stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

### Submit Reign Note



**Parameters**

| Name | Description |
| :--- | :--- |
| `x` | ... |

#### Conditions

* ...
* ....

#### Effect

* ....

## Examples

xxx





