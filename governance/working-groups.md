---
description: >-
  Working groups organize subcommittees of incentivized and staked contributors
  around making a subsystem of the platform to work.
---

# Working Groups

## Introduction

A working group is an organizational body, subject to the oversight of the council, which is responsible for the day to day functioning of some subsystem of the platform. There is exactly one working group per subsystem. The rationale for having a working group for this purpose, rather than having the council directly involved, has three parts. First, since all council members are supposed to be fully informed on all matters the cumulative workload of overseeing all subsystems would not be feasible for a single council. Second, even if it was feasible, voting is not a sound means of making such decisions, because there is a lack of guaranteed coherence in the decisions over time. Third, each subsystem will over time likely require a differentiated skill set, knowledge base and social capital. The appropriate analogy for understanding the role of the working groups in the overall operation of the system would be a commission or agency body in a political institution.

## Roles

The relevant roles in a working group are

* **Applicant:** A member who has submitted an application to join an opening for a worker role in the working group. A given member may apply more than once to a given opening, and also if they already occupy the role as worker the same group. Openings are created by the lead \(see below\), or by the council when wanting to fill the lead role.
* **Worker:** A member who has, through an application, entered the working group.The worker may or may not be staked, and is receiving payouts to a designated account at regular intervals. The worker role gives some ability to act in a domain specific way within the given subsystem. So for example in the context of the forum, a worker in the forum working group can be assigned to be a moderator in certain forum categories, and have associated moderation privileges. Lastly, a member may act as multiple works simultaneously, or over time, in the same working group.
* **Lead:** A designated worker who is responsible for hiring and managing the other workers, as well as allocating funds from a budget towards purposes that support the success of the subsystem.

## Concepts

### Worker

A has the following information associated

* **Membership**: The membership to which this role corresponds. Comes from the initial application to the opening by which worker is hired.
* **Role account**: The account currently used to authenticate as this role in the relevant subsystem. Authentication in the working group is done using the controller account of the member, so as to allow for division of labor behind a single membership across multiple roles, while not requiring full trust. Is updatable by member.
* **Staking profile:** Is only set if the role initially required stake in the opening from which it was hired, and includes
  * **Staking account:** Holds the stake currently associated with the role. .
  * **Unstaking period:** The number of blocks required from a worker initiating leaving the group until their staked funds are unlocked.
* **Reward account**: The destination account to which periodic rewards are paid out.

  All roles have the following information associated.

* **Reward rate per block:** The number of tokens the worker earns per block, although payouts do not occur per block, but every `REWARD_PAYOUT_PERIOD` blocks. This is earned for every block from being hired to being terminated, or initiating leaving the group. It is not earned during unstaking.
* **Owed reward:** The total reward this worker was not paid over a number of payout periods where there was not sufficient funds in the working group budget

### Rewards

All workers are paid every `REWARD_PAYOUT_PERIOD` blocks, and each worker is to be credited according to their own reward rate, and any possibly outstanding owed reward. During this payout, where workers are processed in some consistent order \(for a given set of workers\), the crediting only occurs while the budget constraint `current_budget` is respected. Also, workers unstaking are ignored. For each payout, the constraint is tightened. If a worker cannot be paid out in full, then the difference is added to their owed reward. The budget will then have to be reset by the council. When a worker is terminated, or leaves, any owed reward and outstanding reward from the last payout, are attempted paid out, however if the budget does not allow it, then the worker suffers the loss.

### Spending

In addition to rewards, the lead can spend from this budget for arbitrary purposes, to fund expenses and initiatives that are in line with the purpose of the group.

### Staking

Some worker roles may require staking in order to apply and remain in the role. Staking for worker roles is done using a designated working group lock on a single account per worker role. The amount required is set by the discretion of the lead, and the requirement may be adjusted up or down at a later time on a worker by worker basis, as long as some non-zero amount was required to begin with. Changing the staking requirement is unilaterally done by the lead, or the council  by adjusting the size of the lock, however, one can only increase the lock if there is sufficient free balance in the account. In order for the worker to have to opt-in for a stake increase, no free balance should be kept in a staking account.  
  
Lastly, consult the [Staking](../key-concepts/staking.md#reuse) article to see a list of other staking purposes, and corresponding locks, which can be combined with staking for a given working group.

### Slashing

Slashing is initiated by the council, or the lead, by pure discretion. The full staked amount is at risk of getting slashed, but need not be, and there is no limit to the number of times one may get slashed. Importantly, slashing can also occur while a worker is unbonding. This is of particular importance to avoid a lead attempting to leave the role the moment a slashing proposal is observed. Such last minute exits cannot avoid slashing so long as the unbonding period chosen by the council for the lead, is sufficiently long compared to the inherent delays in the proposal system. There is a similar, but much less severe, concern about workers trying to race with slashing transactions submitted by the lead by attempting to preempt slashing by observing the pool of unconfirmed transactions. The unbonding period required to make this infeasible can be mucher shorter, essentially just however long is required to have a sufficiently high certainty that the slashing transaction is included in a block.

### Hiring

Hiring is the process by which a worker enters the group. Both normal workers and the lead worker, are hired, in the latter case the council initiates the hiring. Hirings are organized into _openings_, where zero or more _applicants_ may be selected as winners, and becoming workers. An opening for the lead position will always result in hiring at most one worker, and this worker becomes the lead.

#### Application

An application has the following 

#### Opening

xxx



_openings_, of which there can be multiple active simultaneously within a single group. The life cycle of an opening has the following stages

* **Waiting:** An opening can be scheduled to begin in a future block, at which point it will be in the _waiting period_ until that time, and during that period the only thing that can happen is that it can be cancelled.
* **Application:** The _application period_ is the stage where members can submit a bid to occupy the role in question, by submitting an application.
* **Review:** The _review period_ is a stage which serves as a grace period before the hiring process must be concluded by either actively selecting some applicants as hired, and others as not, or by allowing anyone to withdraw their application,

  and thus stake associated with applying to the opening.

The opening can be cancelled at any time in the latter two stages.

## Constants

Hard-coded values are defined _for each working group_, and they can only be altered with a runtime upgrade.

| Name | Description |
| :--- | :--- |
| `MAX_NUMBER_OF_WORKERS` | The maximum number of workers that can be part of the working group simultaneously. |
| `REWARD_PAYOUT_PERIOD` | The number of blocks between each time workers are paid their total reward for the period. |

## Parameters

Parameters are on-chain values that can be updated through the proposal system in order to alter the constraints and functionality of the working group.

| Name | Description |
| :--- | :--- |
| `current_budget` | The total number of tokens available to be spent for discretionary spending by lead and rewards to all group members. |

## Operations

### Creating an Opening

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

If the lead is being hired, the opening would be created by the council, if a worker is to be hired, the lead would be the creator. In what follows, let's refer to the opening creator and manager as the _authority_. Such a process will, in a successful scenario, result in one or more roles being filled. When the opening is created, it has the following associated information

* **Activation:** Whether its going to start accepting applications immediately, or some time in the future.
* **Text:** A human readable description of what is involved in the role being hired for.
* **Policy:** An up front commitment to a number of immutable policy variables governing both the opening and the role itself. These are
  * Whether there is an upper limit to the number of applications that can proceed to the review period.
  * Whether stake is required for the application itself, and if so how much \(can be lower bound or exact\), unstaking periods for review period expiry and if kicked out in application period due to limited space.
  * Whether stake is required for the role itself, with similar parameters as for the application.
  * Whether the stake of anyone hired can be slashed, or not, and if it can, how many times, and how many % of stake can be slashed at most.
  * Maximum length of the review period.
  * Unstaking periods for application stake in the following scenarios:
    * applicant hired
    * opening cancelled
    * application terminated by authority
    * application terminated by applicant
  * Unstaking periods for role stake in the following scenarios:
    * applicant failed to be hired
    * opening cancelled
    * application terminated by authority
    * application terminated by applicant

### Accept applications

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in the waiting stage, the authority can transition it to the application stage.

### Terminate application

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in either the application or review stage, the authority can terminate any application, and while there is no slashing, the unbonding periods from the initial policy apply.

### Begin review

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in the application stage, the authority can transition it to the review stage.

### Fill opening

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in the review stage, the authority can select a \(possibly empty\) subset of the currently active applications as being hired, resulting in everyone else as failing to be hired. The distinction lies in what happens to the different associated stakes, and also that the successful applications result in the creation of a corresponding new actor in the working group. The authority can also provide a policy for the rewards to be set for all the new actors, which covers

* how much they should be paid individually
* at what interval they should be paid
* when the first payment should occur

### Apply to opening

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in the application stage, a member can submit an application, which includes the following

* the account to be set as the role account in the event of a hiring
* the amount of funds to allocate for the role stake
* the amount of funds to allocate for the application stake
* a human readable text

The account used as the source of funds for the staking is the account sending the transaction, which is the membership role account. If only a limited number of applications can proceed to the review period, and that limit is exceeded with this new application, then this new application is only included if it the total amount of stake it provides is larger than at least one other active application. If that is the case, then that application is displaced, and cannot proceed to the review period.

### Withdraw application

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

When an opening is in the application stage, a member with an active application can withdraw the application.

### Update role account

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Any role can unilaterally update the current role account by authenticating with their underlying membership.

### Update reward account

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Any role can unilaterally update the reward account.

### Leave role

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Any role can unilaterally leave, triggering any associated role unstaking period, during which they can still get slashed.

### Terminate role

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Any role can instantly be removed. The lead can be removed by the council, and a worker can be removed by the lead. The relevant unstaking period from the policy parameter of the opening from which the role was set applies.

### Slash

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Slashing happens instantly, and can happen to both the lead and a worker, and can be up to the entire balance in the role stake. When the lead is slashed, its due to the council, and when a worker is slashed, its due to the lead.

### Decrease stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Decreasing role stake happen instantly, and it can be triggered by the lead when applying to a worker, or triggered by the council when it applying to the lead. Stake can be reduced any amount, and the funds are returned to the role account.

### Increase stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

`........`

Increasing role stake happens instantly, and it can be triggered by the worker or the lead, on behalf of themselves only. Stake can be increased any amount, and it originates from the role account.

