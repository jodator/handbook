# Working Groups

## TODO

* why key segregation: fund & risk managemnt policy flexibility.
* Unstaking period must be longer than grace period, or whatever period is needed, for slashing proposal of leads, and slashing must work while unstaking! \(unstaking period is parameter for making openng!\)
* Missing Constants table that provides constant values for each group, such as unstaking period, even if identical.

## Introduction

A working group is an executive body, subject to the oversight of the council, which is responsible for the day to day functioning of some subsystem of the platform. There is exactly one working group per subsystem. The rationale for having a working group for this purpose, rather than having the council directly involved, has three parts. First, since all council members are supposed to be fully informed on all matters the cumulative workload of overseeing all subsystems would not be feasible for a single council. Second, even if it was feasible, voting is not a sound means of making such decisions, because there is a lack of guaranteed coherence in the decisions over time. Third, each subsystem will over time likely require a differentiated skillset, knowledge base and social capital. The appropriate analogy for understanding the role of the working groups in the overall operation of the system would be a commission or agency body in a political institution.

## Roles

There are two roles in a working group, a _lead_ and a _worker_. There is at most one lead, but but at times there is no lead. There are multiple workers in each group, and each working group will have an upper bound on how many workers can be part of the group at any time. A single member can occupy the role of lead in multiple groups simultaneously, and even multiple worker roles in the same group simultaneously. Each separate role does however have its own independent stake and policy variables associated with it. All roles have the following information associated

* **Membership**: The membership to which this role corresponds.
* **Role account**: The account currently used to authenticate as this role, as well as the source account for any staked quantity, and thus also where unstaked funds return.
* **Reward account**: The destination account to which periodic rewards are paid out.

## Financing

Each group has a separate budget which funds all expenses in that group, namely

* periodic reward to lead
* periodic reward to each worker
* discretionary spending by lead

The financing dynamics of a group work as follows. Time is split into periods of a fixed length, and at the beginning of each period, the budget for the group is reset. Over the period, all spending out of the budget happens by minting fresh tokens for a given purpose. Periodic rewards to the lead and the worker all payout at a given fixed interval, where fresh tokens our minted out of the budget, and sent to an account provided by the given recipient. The payouts may happen at different blocks for different actors, as they are aligned w.r.t. when the actor was introduced into the group. These autonomous reward payouts are optimistic, in that, if they fail because the budget has been expended, then no payout is made.

## Hiring

All roles in a group are occupied by an on boarding process analogous to how someone is hired for a role in real world organisations. This hiring activity is organised into _openings_, of which there can be multiple active simultaneously within a single group. The life cycle of an opening has the following stages

* **Waiting:** An opening can be scheduled to begin in a future block, at which point it will be in the _waiting period_ until that time, and during that period the only thing that can happen is that it can be cancelled.
* **Application:** The _application period_ is the stage where members can submit a bid to occupy the role in question, by submitting an application.
* **Review:** The _review period_ is a stage which serves as a grace period before the hiring process must be concluded by either actively selecting some applicants as hired, and others as not, or by allowing anyone to withdraw their application,

  and thus stake associated with applying to the opening.

The opening can be cancelled at any time in the latter two stages.

## Constants

TBD.  
  
Hard-coded values are defined _for each working group_, and they can only be altered with a runtime upgrade.

* C1
* C2
* C3

| Name | Description |
| :--- | :--- |
| `MAX_NUMBER_OF_WORKERS` | The maximum number of workers that can be part of the working group simultaneously. |

## Stake

There are two separate forms of stake which may be required of applicants to an opening. Application stake is stake that is required simply in order to apply, and it will always be released before the opening ends. It cannot be slashed. Role stake is the stake that is required as part of entering the role itself, and if hired, the stake is not released at that time, and it is subject to slashing risk.

### Creating an opening

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

When an opening is in the waiting stage, the authority can transition it to the application stage.

### Terminate application

When an opening is in either the application or review stage, the authority can terminate any application, and while there is no slashing, the unbonding periods from the initial policy apply.

### Begin review

When an opening is in the application stage, the authority can transition it to the review stage.

### Fill opening

When an opening is in the review stage, the authority can select a \(possibly empty\) subset of the currently active applications as being hired, resulting in everyone else as failing to be hired. The distinction lies in what happens to the different associated stakes, and also that the successful applications result in the creation of a corresponding new actor in the working group. The authority can also provide a policy for the rewards to be set for all the new actors, which covers

* how much they should be paid individually
* at what interval they should be paid
* when the first payment should occur

### Apply to opening

When an opening is in the application stage, a member can submit an application, which includes the following

* the account to be set as the role account in the event of a hiring
* the amount of funds to allocate for the role stake
* the amount of funds to allocate for the application stake
* a human readable text

The account used as the source of funds for the staking is the account sending the transaction, which is the membership role account. If only a limited number of applications can proceed to the review period, and that limit is exceeded with this new application, then this new application is only included if it the total amount of stake it provides is larger than at least one other active application. If that is the case, then that application is displaced, and cannot proceed to the review period.

### Withdraw application

When an opening is in the application stage, a member with an active application can withdraw the application.

## Role life cycle

### Update role account

Any role can unilaterally update the current role account by authenticating with their underlying membership.

### Update reward account

Any role can unilaterally update the reward account.

### Leave role

Any role can unilaterally leave, triggering any associated role unstaking period, during which they can still get slashed.

### Terminate role

Any role can instantly be removed. The lead can be removed by the council, and a worker can be removed by the lead. The relevant unstaking period from the policy parameter of the opening from which the role was set applies.

### Slash

Slashing happens instantly, and can happen to both the lead and a worker, and can be up to the entire balance in the role stake. When the lead is slashed, its due to the council, and when a worker is slashed, its due to the lead.

### Decrease stake

Decreasing role stake happen instantly, and it can be triggered by the lead when applying to a worker, or triggered by the council when it applying to the lead. Stake can be reduced any amount, and the funds are returned to the role account.

### Increase stake

Increasing role stake happens instantly, and it can be triggered by the worker or the lead, on behalf of themselves only. Stake can be increased any amount, and it originates from the role account.

## Oversight

### Change budget

The council can set the size of the budget, but there is a hard upper bound to what they can set.

