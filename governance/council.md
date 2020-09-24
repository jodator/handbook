---
description: >-
  The politically selected governance body responsible for managing the proposal
  system for the benefit of voters.
---

# Council

## Introduction

The council is a political organ 

* political
* fast- day to day: stand in reprsentation of the full set of stakeholders on a day to day basis.

## Roles

The relevant roles in the council system are

* **Voters:** Anyone who stakes for the purposes of influencing the outcome of an election. Is not tied to membership, so a member can vote multiple times for different candidates from different accounts.
* **Candidate:** A member who has staked and stands as an alternative for council membership in an ongoing election cycle.
* **Council Member:** A member who has stood as a candidate in an election and won a place in a council. Has the primary responsibility to participate in voting on and deliberating around proposals in the proposal system.

## Concepts

### Staking

xxvoting locks, even odd council locks.

### Candidate

xxx  
- entry text  
- exit text

### Council Member

xxx  
- 

### Vote

xx

### Election

An election is the periodic process by which a new council is selected by voters among candidates running for a seat on the next council. Elections occur periodically, and each one has a sequence of stages referred to as the election cycle. An election will begin while the current council is active, and the sitting council is only relieved once a new one has been successfully elected. As will become clear, this process can go on for a unknown amount of time.

State

* candidates: member -&gt; candidate
* Announcing Block: when we started:
* whether cylce is odd or even!!



* **Announcing Period:** This is the first stage in the election cycle. During this time members can announce that they will stand as candidates for the next council. The same member can only  When time wxpired.... enough people or not? reset everyone and start over.
* **Voting Period:** This is the stage where voters can submit votes in favour of candidates.
* **Revealing Period:** ...

### **Council**

The council has a fixed number of seats `NUMBER_OF_COUNCIL_SEATS` occupied by members. The seats are always occupied, allowing the platform to dispose of all proposals thay may come in at any time. The council body has two high level states described as follows.

* **Normal:** During this stage the council operates normally. After `NORMAL_PERIOD_LENGTH` blocks have passed since this period started, a transition is made to the election stage.
* **Election:** During this stage, not only does the council operate, but there is an election ongoing.

During both these stages

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

| Name | Description | Value |
| :--- | :--- | :---: |
| `NUMBER_OF_COUNCIL_SEATS` | The number of council seats. | `fill-in` |
| `NORMAL_PERIOD_LENGTH` | The number of blocks in the normal period. | `fill-in` |
| `VOTING_PERIOD_LENGHT` | The number of blocks in the voting period. | `fill-in` |
| `REVEALING_PERIOD_LENGTH` | The number of blocks in the revealing period. | `fill-in` |
| `REWARD_PERIOD_LENGTH` | The number or blocks between each reward  payout to council members. | `fill-in` |



xxx

## State

budget for salaries

budget for financing proposal?

reward for council members..&lt;== should be adjustable

## Operations

### Announce Candidacy

Parameters

Conditions

Effect

### Submit Sealed Vote

Parameters

Conditions

Effect

### Reveal Vote

Parameters

Conditions

Effect

### Recover Voting Stake

Parameters

Conditions

Effect

### Recover Candidacy Stake

Parameters

Conditions

Effect

### Submit Reign Note

Parameters

Conditions

Effect



* recall that failure is both in too fe candidates and in not enough votes reveald...
* voters only locked in until election starts
* candidacy is locked in until loss or next council elected.

## Examples

xxx





