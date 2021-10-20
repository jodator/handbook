---
description: >-
  An on-chain index of all data stored and distributed in the system, with
  associated information about ownership, what providers are tasked with storing
  and providing bandwidth, as well as utilization
---

# Data Directory

## Introduction

This subsystem serves to retain an index of all static assets, including who owns them, and information about what actors are currently tasked with storing and distributing them to end users. It has no awareness of the underlying content or purpose represented by such an object, as it is used by different parts of the system. It can represent assets as diverse as

* Video media, with a particular resolution and encoding, living in the content directory.
* Image media used for the avatar of a member, an election candidate or for the cover of a channel in the content directory.
* A data attachment to a blog post, proposal or role application.

In the future it will be extended with autonomous interactive auditing features for storage providers and payments between service providers to incentive replication.

## Concepts

\<entity relationships image>

### Data Directory Account

The

### Data Object

A _data object_ represents a single static data asset, like an image or video media, and it is defined by the following information

* **Id:** A unique immutable non-negative integer identifying an individual data object, is automatically assigned by the blockchain upon creation.
* **Accepted:** Whether the object has been verified as correctly uploaded to an initial storage providers. The storage provider making such a confirmation for a given object is referred to as the _liasion_ for the object.
* **Deletion Prize:** An amount of funds locked up as a state bloat bond for the object.
* **Size:** The claimed size of the object, as stupulated during creation by the owner, and implicitly understood to be verified by the liasion.
* **Hash:** The IPFS CID of the object, specifically SS58 format of Multihash with blake3 hashing algorithm.

### Bag Id

A _Bag Id_ is a value which can identify a specific bag, see section on [#bag](data-directory.md#bag "mention") for further elaboration, and it takes one of the following varieties

* **Static:** A _static bag id_ identifies one of the built in bags in the system, and it comes in one of the following subvarieties
  * **Council:** identifies the bag reserved for the council to manage through its proposal system.
  * **Membership Working Group:** identifies the bag for the membership working group.
  * **Storage Working Group:** identifies the bag for the storage working group.
  * **Bandwidth Working Group:** identifies the bag for the bandwidth working group.
  * **Content Directory Working Group:** identifies the bag for the content directory working group.
  * **Forum Working Group:** identifies the bag for the forum working group
  * **Operations Working Group Alfa, Beta, Gamma:** each identifies the bag for the corresponding operations working group.
* **Dynamic:** A _dynamic bag id_ identifies one of the dynamic, so not built in, bags in the system, and it comes in one of the following subvarieties:
  * **Member:** has associated membership id and identifies bag for this member.
  * **Channel:** has associated channel id, and identifies the bag for this channel.

### Bag

A _data object bag_, or _bag_ for short, is a dynamic collection of data objects which can be treated as one subject in the system. Each bag has an owner, which is established when the bag is created. A data object lives in exactly one bag, but may be moved across bags by the owner of the bag. Only the owner can create new data objects in a bag, or opt into absorbing objects from another bag. The purpose of the concept of bags is to limit the on-chain transactional footprint of administrating multiple objects which should be treated the same way. This is achieved by establishing a small immutable identifier for these objects. The canonical example would be assets that will be consumed together, such as the cover photo and different video media encodings of a single piece of video content. Storage and distribution nodes have commitments to bags, not individual data objects.&#x20;

A bag is defined by the following information

* **Id:** an id of type [#bag-id](data-directory.md#bag-id "mention") for this bag.
* **StoredBy:** set of ids for [#storage-bucket](data-directory.md#storage-bucket "mention") tasked with storing the objects in the bag.
* **DistribtedBy:** set of ids for [#distributor-bucket](data-directory.md#distributor-bucket "mention")  tasked with distributing the objects in the bag.
* **DeletionPrize:** amount of money placed in [#undefined](data-directory.md#undefined "mention") as staking bond for cleaning up unused bag.
* **ObjectSize:** cumulative size of all data objects in the bag.
* **ObjectCount:** cumulative number of objects in the bag.

### Storage Bucket

A _storage bucket_ represents a commitment to hold some set of bags for long term storage. A bucket may have a _bucket operator_, which is a single worker in the storage working group. There is distinct _bucket operator metadata_ associated with each, which describes things such as how to resolve the host. The operator of a bucket may change over time. As previously described, when new dynamic bags are created, they are allocated to one or more such buckets, unless the bucket has been temporarily disabled from accepting new bags.&#x20;

* **Id:** A unique immutable non-negative integer identifying an individual storage bucket, is automatically assigned by the blockchain upon creation.
* OperaturStatus: ...
* AceeptingNewBags:  ... accepting\_new\_bags: bool, /// Defines whether the bucket accepts new bags.
* TotalSizeLimit: ...
* ObjectCountLimtobjects\_limit: u64, /// Object number limit.
* TotalSize: ...
* ObjectCount: ...

### Distributor Bucket

A _distribution bucket_ represents a commitment to distribute a set of bags to end users. A bucket may have multiple _bucket operators_, each being a worker in the distribution working group. The same metadata concept applies here as well, and additionally covers whether the operator is live or not. Bags are assigned to buckets when being uploaded, or later by the lead by manual intervention.&#x20;

* **Id:** A unique immutable non-negative integer identifying an individual distributor bucket, is automatically assigned by the blockchain upon creation.
* **AcceptingNewBags:** bool, /// Distribution bucket accepts new bags.
* distributing: bool, /// Distribution bucket serves objects.
* pending\_invitations: BTreeSet, /// Pending invitations for workers to distribute the bucket.
* operators: BTreeSet, /// Active operators to distribute the bucket.
* assigned\_bags: u64, /// Number of assigned bags.

### Dynamic Bag Creation Policy

A _dynamic bag creation policy_ holds parameter values impacting how exactly the creation of a new dynamic bag occurs, and there is one such policy for each type of dynamic bag. It describes how many storage buckets should store the bag, and from what subset of distribution bucket families (described below) to select a given number of distribution buckets (described below).

### Distributor Bucket Family

Buckets are partitioned into so called _distribution bucket families_. These families group buckets with interchangeable semantics from distributional point of view, and the purpose of the grouping is to allow sharding over the bag space for a given service level when creating new bags. Here is an example that can make this more clear. A subset of families could for example represent each country in East Asia, where each family corresponds to a specific country. The buckets in a family, say the family for Mongolia, will be operated by infrastructure which can provide sufficiently low latency guarantees w.r.t. the corresponding country. The bag for a channel known to be particularly popular in this area could be setup so as to use these buckets disproportionately.

### Blacklist

blacklists: important to explain signififacna nd enforcebilit

## On-chain Hooks

xxx

## Constants

xx

type DataObjectDeletionPrize: Get\<BalanceOf>; /// Defines a prize for a data object deletion. type BlacklistSizeLimit: Get; /// Defines maximum size of the "hash blacklist" collection. type ModuleId: Get; type StorageBucketsPerBagValueConstraint: Get; /// "Storage buckets per bag" value constraint. type DistributionBucketsPerBagValueConstraint: Get; /// "Distribution buckets per bag" value constraint. type DefaultMemberDynamicBagNumberOfStorageBuckets: Get; /// Defines the default dynamic bag creation policy for members (storage bucket number). type DefaultChannelDynamicBagNumberOfStorageBuckets: Get; /// Defines the default dynamic bag creation policy for channels (storage bucket number). type MaxRandomIterationNumber: Get; /// Defines max random iteration number (eg.: when picking the storage buckets). type MaxDistributionBucketFamilyNumber: Get; /// Defines max allowed distribution bucket family number. type MaxDistributionBucketNumberPerFamily: Get; /// Defines max allowed distribution bucket number per family. type MaxNumberOfPendingInvitationsPerDistributionBucket: Get; /// Max number of pending invitations per distribution bucket. type MaxDataObjectSize: Get; /// Max data object size in bytes.

## Extrinsics

xxx

### create\_storage\_bucket

xx

### update\_storage\_buckets\_for\_bag

xx

### delete\_storage\_bucket

xx

### invite\_storage\_bucket\_operator

xx

### cancel\_storage\_bucket\_operator\_invite

xx

### remove\_storage\_bucket\_operator

xx

### update\_uploading\_blocked\_status

xx

### update\_storage\_buckets\_per\_bag\_limit

xx

### update\_storage\_buckets\_voucher\_max\_limits

xx

### update\_number\_of\_storage\_buckets\_in\_dynamic\_bag\_creation\_policy

xx

### update\_blacklist

xx

### set\_storage\_bucket\_voucher\_limits

xx

### accept\_storage\_bucket\_invitation

xx

### set\_storage\_operator\_metadata

xx

### accept\_pending\_data\_objects

xx

### create\_distribution\_bucket\_family

xx

### delete\_distribution\_bucket\_family

xx

### create\_distribution\_bucket

xx

### delete\_distribution\_bucket

xx

### update\_distribution\_bucket\_status

xx

### update\_distribution\_buckets\_for\_bag

xx

### distribution\_buckets\_per\_bag\_limit

xx

### update\_families\_in\_dynamic\_bag\_creation\_policy

xx

### cancel\_distribution\_bucket\_operator\_invite

xx

### remove\_distribution\_bucket\_operator

xx

### set\_distribution\_bucket\_family\_metadata

xx

### accept\_distribution\_bucket\_invitation

xx

### set\_distribution\_operator\_metadata

xx
