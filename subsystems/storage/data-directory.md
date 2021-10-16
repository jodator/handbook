---
description: xxxxx
---

# Data Directory

## Introduction

xxx

## Concepts

xxx

entity relationships??

\<image>

### Data Object



The fundamental concept in the system is a _data object_, which represents single static binary object in the system. The main goal of the system is to retain an index of all such objects, including who owns them, and information about what actors are currently tasked with storing and distributing them to end users. The system is unaware of the underlying content represented by such an object, as it is used by different parts of the Joystream system. It can represent assets as diverse as

* Video media, with a particular resolution and encoding, living in the content directory.
* Image media used for the avatar of a member, an election candidate or for the cover of a channel in the content directory.
* A data attachment to a blog post, proposal or role application.

xxx



* accepted: bool, /// Defines whether the data object was accepted by a liason.
* deletion_prize: Balance, /// A reward for the data object deletion.
* size: u64, /// Object size in bytes.
* pub ipfs_content_id: Vec, /// Content identifier presented as IPFS hash.

### Bag

A _data object bag_, or _bag_ for short, is a dynamic collection of data objects which can be treated as one subject in the system. Each bag has an owner, which is established when the bag is created. A data object lives in exactly one bag, but may be moved across bags by the owner of the bag. Only the owner can create new data objects in a bag, or opt into absorbing objects from another bag.

The purpose of the concept of bags is to limit the on-chain footprint of administrating multiple objects which should be treated the same way. This is achieved by establishing a small immutable identifier for these objects. The canonical example would be assets that will be consumed together, such as the cover photo and different video media encodings of a single piece of video content. Storage and distribution nodes have commitments to bags, not individual data objects.

There are two different kinds of bags, _static bags_ and _dynamic bags_. The former are all created when the system goes live and cannot be deleted, and of the latter there are few different types, and new instances of each type can be created over time. Specifically there is one static bag for the council and each working group, and there is a member, channel and DAO dynamic bag _type_. When a new member, channel or DAO is created, then a new instance of each such type is created.

A _dynamic bag creation policy_ holds parameter values impacting how exactly the creation of a new dynamic bag occurs, and there is one such policy for each type of dynamic bag. It describes how many storage buckets should store the bag, and from what subset of distribution bucket families (described below) to select a given number of distribution buckets (described below).



dynamic bagtype

Member, /// Member dynamic bag type. Channel, /// Channel dynamic bag type.



BagID

Static(StaticBagId), Dynamic(DynamicBagIdType\<MemberId, ChannelId>), /// Dynamic bag type.



pub enum StaticBagId { /// Dedicated bag for a council. Council,

```
/// Dedicated bag for some working group.
WorkingGroup(WorkingGroup),
```

}



* stored_by: BTreeSet, /// Associated storage buckets.
* distributed_by: BTreeSet, /// Associated distribution buckets.
* deletion_prize: Option, /// Bag deletion prize (valid for dynamic bags).
* objects_total_size: u64, /// Total object size for bag.
* objects_number: u64, /// Total object number for bag.

### Storage Bucket

A _storage bucket_ is a commitment to hold some set of bags for long term storage. A bucket may have a _bucket operator_, which is a single worker in the storage working group. There is distinct _bucket operator metadata_ associated with each, which describes things such as how to resolve the host. The operator of a bucket may change over time. As previously described, when new dynamic bags are created, they are allocated to one or more such buckets, unless the bucket has been temporarily disabled from accepting new bags. A bucket also has a _voucher_, which describes the limits on how much data and the number of objects can be assigned to the bucket, across all bags, as well as current usage. This limitation is enforced when data objects are uploaded or moved. The voucher limits can be updated by the



* operator_status: StorageBucketOperatorStatus, /// Current storage operator status.
* accepting_new_bags: bool, /// Defines whether the bucket accepts new bags.
* voucher: Voucher, /// Defines limits for a bucket.

### Distributor Bucket

A _distribution bucket_ is a commitment to distribute a set of bags to end users. A bucket may have multiple _bucket operators_, each being a worker in the distribution working group. The same metadata concept applies here as well, and additionally covers whether the operator is live or not. Bags are assigned to buckets when being uploaded, or later by the lead by manual intervention. Buckets are partitioned into so called _distribution bucket families_. These families group buckets with interchangeable semantics from distributional point of view, and the purpose of the grouping is to allow sharding over the bag space for a given service level when creating new bags. Here is an example that can make this more clear. A subset of families could for example represent each country in East Asia, where each family corresponds to a specific country. The buckets in a family, say the family for Mongolia, will be operated by infrastructure which can provide sufficiently low latency guarantees w.r.t. the corresponding country. The bag for a channel known to be particularly popular in this area could be setup so as to use these buckets disproportionately.



* accepting_new_bags: bool, /// Distribution bucket accepts new bags.
* distributing: bool, /// Distribution bucket serves objects.
* pending_invitations: BTreeSet, /// Pending invitations for workers to distribute the bucket.
* operators: BTreeSet, /// Active operators to distribute the bucket.
* assigned_bags: u64, /// Number of assigned bags.

### Dynamic Bag Creation Policy

xx

### Distributor Bucket Family

xx

### Blacklist

xxx

### Voucher

xxx

* size_limit: u64, /// Total size limit.
* objects_limit: u64, /// Object number limit.
* size_used: u64, /// Current size.
* objects_used: u64, /// Current object number.

blacklists: important to explain signififacna nd enforcebilit

## On-chain Hooks

xxx

## Constants

xx

type DataObjectDeletionPrize: Get\<BalanceOf>; /// Defines a prize for a data object deletion. type BlacklistSizeLimit: Get; /// Defines maximum size of the "hash blacklist" collection. type ModuleId: Get; type StorageBucketsPerBagValueConstraint: Get; /// "Storage buckets per bag" value constraint. type DistributionBucketsPerBagValueConstraint: Get; /// "Distribution buckets per bag" value constraint. type DefaultMemberDynamicBagNumberOfStorageBuckets: Get; /// Defines the default dynamic bag creation policy for members (storage bucket number). type DefaultChannelDynamicBagNumberOfStorageBuckets: Get; /// Defines the default dynamic bag creation policy for channels (storage bucket number). type MaxRandomIterationNumber: Get; /// Defines max random iteration number (eg.: when picking the storage buckets). type MaxDistributionBucketFamilyNumber: Get; /// Defines max allowed distribution bucket family number. type MaxDistributionBucketNumberPerFamily: Get; /// Defines max allowed distribution bucket number per family. type MaxNumberOfPendingInvitationsPerDistributionBucket: Get; /// Max number of pending invitations per distribution bucket. type MaxDataObjectSize: Get; /// Max data object size in bytes.

## Extrinsics

xxx

### create_storage_bucket

xx

### update_storage_buckets_for_bag

xx

### delete_storage_bucket

xx

### invite_storage_bucket_operator

xx

### cancel_storage_bucket_operator_invite

xx

### remove_storage_bucket_operator

xx

### update_uploading_blocked_status

xx

### update_storage_buckets_per_bag_limit

xx

### update_storage_buckets_voucher_max_limits

xx

### update_number_of_storage_buckets_in_dynamic_bag_creation_policy

xx

### update_blacklist

xx

### set_storage_bucket_voucher_limits

xx

### accept_storage_bucket_invitation

xx

### set_storage_operator_metadata

xx

### accept_pending_data_objects

xx

### create_distribution_bucket_family

xx

### delete_distribution_bucket_family

xx

### create_distribution_bucket

xx

### delete_distribution_bucket

xx

### update_distribution_bucket_status

xx

### update_distribution_buckets_for_bag

xx

### distribution_buckets_per_bag_limit

xx

### update_families_in_dynamic_bag_creation_policy

xx

### cancel_distribution_bucket_operator_invite

xx

### remove_distribution_bucket_operator

xx

### set_distribution_bucket_family_metadata

xx

### accept_distribution_bucket_invitation

xx

### set_distribution_operator_metadata

xx
