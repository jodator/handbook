---
description: >-
  Funding public goods where the community can help with financing, experts can
  help adjudicate quality of deliverables and service providers have an
  incentive to find popular initiatives.
---

# Bounties

## Introduction

The only other way to fund the production of goods that create benefits to a broad set of platform participants is through a financing proposal or discretionary spending by a working group lead out of the group budget. These processes incur the transaction costs of beneficiaries having to convince a number of external decision-makers, such as a council financing quorum, that this is a good idea. For smaller initiatives that ideally should start and finish sooner, or where they depend on knowledge or insight that is not as broadly shared, these processes become too costly.

## Assurance Contracts and Dominant Assurance Contracts

An assurance contract is a funding scheme which is intended to override the inherent free-riding problem in financing public goods by allowing contributors to enter into binding conditional commitments to provide resources to fund the good if a sufficient level of funding is committed. By setting the level sufficiently high, every public good beneficiary becomes close to pivotal to getting the good produced, which generates a rationale incentive to unilaterally commit. Dominant assurance contracts are such schemes where the funding has to be deployed towards a specific service provider or entrepreneur who will produce the good using the funding, and in exchange for this privileged to possibly generate a profit from this activity, the entrepreneur has to put up an initial bounty, called a _cherry_ , which is split among all contributors pro-rata. This cherry generates an incentive for contributors, as even when the funding fails, they get a benefit.

## Roles

* **Creator:** The agent responsible for creating the bounty, is either a specific member, or the council.
* **Oracle:** The agent responsible for deciding the outcome of a bounty where entrants have submitted work. Is either a specific member, or the council as whole.
* **Contributor:** An agent responsible for contributing funds that finance the bounty. Is either a specific member or the council as a whole.
* **Worker:** A member who has announced their participation in producing deliverable in a given bounty.

Notice that when the council is an actor, it means that if the lifetime of a bounty spans the boundry of two councils, then a different set of council members are likely in place to exercise control over the same bounty.

## Concepts

### Funding Period Type

The funding period type refers to how funds are collected for the benefit of a bounty, and there are fundamentally two types:

* **Perpetual:** The funding has not preset termination date, and new contributors can join on an ongoing basis. There is however a _target_ which sets the upper bound for how much can be contributed.
* **Limited:** The funding lasts for no longer than a given number of blocks, called the _funding period_ . There is a lower bound and upper bounfor how much must be contributed

### Bounty Type

There are two types of bounties in terms of who can participate as worker. There are _open_ bounties, where any member can participate, and there are _closed_ bounties, where the creator can pre-determine a set of member who can participate. The primary purpose of closed bounties is to enable dominant assurance contracts, where the creator combines setting themselves as the only feasible worker with also..

### Entry

xxxx &lt; WIP &gt; define later.

* Member
* Staking Account:
* Submitted At
* Work: List of ....
* ...
* Status: ...judgement result: ...
  * None
  * winner
  * rejected

### Bounty

A bounty is defined is defined by the following information

* **Oracle:** Bounty oracle, is either a member or the council.
* **Type:** Bounty type, is open or closed.
* **Creator:** Bounty creator, is either a member or the council.
* **Cherry:** Amount of funds contributed by creator as cherry.
* **Work Period Length:** The number of blocks which must pass, from the end of the funding stage, before the oracle for the bounty can adjudicate the outcome of the bounty.
* **Judging Period Length:** The maximum number of blocks which can pass, from the end of the working period, while the oracle does not adjudicate a the outcome and funds cannot be withdrawn.
* **Contributions:** The net amount contributed for each contributor to the bounty.
* **Metadata:** Structured data encoding the purpose and terms of the bounty.
* **Stage:** The stage of the bounty see next subsection

#### Stage

Below is a list of the stages a bounty can be in, and what each of them mean:

* **Funding Period:** This is the initial stage of a bounty once it is created, and it is during this stage that the bounty can accept funding contributions. It is also during this stage the bounty can be vetoed by the council. The creator can also cancel the bounty in this stage if there are no contributions. If a contribution is made that brings the cumulative funding equal to or above the upper bound, then the difference is returned, and the bounty proceeds to the `Working Period` stage. Lastly if the funding period is limited and the time passes this time, then the bounty proceeds to the `Experied Funding Period`stage if there was at least one contribution made, otherwise it proceeds to the `Bounty Failed` stage.
* **Expired Funding Period:** During this stage the bounty is only waiting to get cancelled by the creator, terminating the bounty.
* **Working Period:** This is the stage where workers announce their entries and submit their work, and optionally also withdraw. After the working period length has expired since the initiation of the working period, the stage transitions to the `Judgement Period`.
* **Judgement Period:** This is the stage during which the oracle can evaluate the submitted work entries during the working periods. The judgement identifies a set of winning contributors, possibly empty, each with a non-zero number of tokens as a reward. The total reward must perfectly consume the contributed funding to the bounty, but reward distribution need not be uniform. If the oracle selects an empty set of winners, or does not provide a judgement within the end of the judgement period, a transition is made to the `Bounty Failed` stage, otherwise a transition to `Bounty Successful` stage is made if the set is non-empty.
* **Withdrawal Period:**  This represents the stage where funds can be withdrawn from the bounty, eventually leading to the bounty getting terminated.
  * **Bounty Successful:** This represents the case where the some subset of workers have been selected as winners, and each must cash out to claim their reward. Workers who did not win also have to cash out their possible prior stake.....  When the last cashout is made, the bounty is terminated.
  * **Bounty Failed:** xx

The stages and transitions are summarized in the image below.

![Bounty life-cycle stages.](../.gitbook/assets/bounties_statechart.png)

## Constants

xxx

## Extrinsics

### Create Bounty

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Cancel Bounty

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |
| `metadata` | .... |

#### Conditions

* xxx

#### Effect

* A xx



### Veto Bounty

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx



### Fund Bounty

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx



### Withdraw Funding

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Announce Work Entry

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Withdraw Work Entry

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Submit Work

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Submit Oracle Judgement

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx

### Withdraw Work Entrant Funds

**Parameters**

| Name | Description |
| :--- | :--- |
| `xxx` | To be root account of membership. |

#### Conditions

* xxx

#### Effect

* A xx



