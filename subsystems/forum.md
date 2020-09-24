---
description: >-
  An immutable, auditable, public forum is the main communication and
  coordination forum among platform members.
---

# Forum

## Introduction

The forum is the primary place for community-wide asynchronous written communication about all topics relevant to the platform among members. It is hierarchically organized into a tree of categories, each with designated moderators responsible for policing and encouraging effective and beneficial interactions among members. The moderators are part of a designated forum working group, and the lead of that working group can decide what moderators are responsible for what categories. Categories contain subcategories, and threaded topic-based discussions, called _threads_, where any member can open a thread, and others can come and make replies in the form of _posts_. Some threads can also include a poll, allowing any member to weight in on a question.

## Roles

The relevant actors in the forum are

* **Member:** A members participate as normal forum users, creating and responding to threads, participating in polls, and so on.
* **Moderator:** A moderator is assigned to one or more categories. Importantly, when assigned to a category, the moderator can act as a moderator in any descendant category. The root category is an exception where moderator can act, only the lead can moderate. Lastly, a moderator cannot participate in normal forum activities _as a moderator,_ only in distinct moderator activities.
* **Lead:** The forum lead is a member occupying the lead role in the forum working group. Beyond the normal working group lead obligations, the lead can act as a moderator as well, including in the root category.

## Concepts

### Archiving

Both categories and threads can be _archived._ When a category is directly archived, or is an ancestor of a directly archived category, it is considered archived. If not, its considered _active_. Likewise, when a thread can be directly archived, or is in a category which is archived, it is considered archived. If not, its considered active. In either case, being archived prevents normal users from updating any associated forum state, for example through user level interactions like creating threads, creating posts, reacting to posts, etc. However, actions associated with moderators and the lead are still unconstrained.

### Category

Any non-root category is defined by the following

* **Id:** A global unique category identifier, effectively the number of categories created in the forum prior to this one.
* **Parent:** An optional reference to a parent category. When not set, it indicates this is a root level category.
* **Title:** A human-readable category name.
* **Description:** A human-readable description.
* **Stickied Threads**: A list of threads in this category that have been designated as having long-run importance to the category.
* **Subcategories:** The categories with this category as its parent.
* **Threads:** The threads directly contained in this category.
* **Moderators:** The moderator directly assigned to this category.
* **Archival Status:** Whether the category is archived or not. This impacts whether one can use the category, such as creating threads or posts directly, or recursively, within the category.

### Thread

A thread is defined by the following

* **Id:** A global unique thread identifier, effectively the number of threads created in forum prior to this one. From this one can infer a chronological ordering of threads within the category. Importantly, because of the way information is organized in the blockchain state, the identifier for the category is also also required when identifying a thread.
* **Title:** The human readable title.
* **Author:** Member who created the thread.
* **Posts:** The posts in this thread.
* **Poll:** An optional poll for the thread, defined by the following
  * **Description:** A human readable description of what question is being polled.
  * **Deadline:** Some block before which is the only time anyone can participate in the poll.
  * **Alternatives:** A list of alternatives, each with its own explainer text, vote count and members who have voted in favor of it.
* **Archival Status:** Whether thread is archived or not.

### Post

A post in a thread is defined by the following

* **Id:** A global unique post identifier, effectively the number of posts created in the forum prior to this one. From this one can infer a chronological ordering of posts within the thread. Importantly, because of the way information is organized in the blockchain state, the identifiers for the category and thread are also also required when identifying a post.
* **Text:** The post thread
* **Author:** Member who created the pot.

### Reaction

A _reaction_ is a signal a member can send to associate a sentiment, in the form of a non-negative integer called a _reaction value_, with a forum post. Importantly, it is only possible to react, not unreact, that is to withdraw a reaction. The semantics of different values, or of submitting the same value more than once, will require social consensus.

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

### General

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
      <td style="text-align:left"><code>MAX_SUBCATEGORIES</code>
      </td>
      <td style="text-align:left">Maximum allowed subcategories in any
        <br />category to be created.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_THREADS_IN_CATEGORY</code>
      </td>
      <td style="text-align:left">Maximum number of threads in any category for
        <br />any new thread.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_POSTS_IN_THREAD</code>
      </td>
      <td style="text-align:left">
        <p>Maximum number of posts allowed in any thread for</p>
        <p>any new post.</p>
      </td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_MODERATORS_IN_CATEGORY</code>
      </td>
      <td style="text-align:left">
        <p>Maximum number of moderators allowed in a category</p>
        <p>for any new assignment of the moderator to category.</p>
      </td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_NUM_CATEGORIES</code>
      </td>
      <td style="text-align:left">
        <p>Maximum number of categories allowed in total for</p>
        <p>any new category to be created.</p>
      </td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_POLL_ALTERNATIVES</code>
      </td>
      <td style="text-align:left">Upper bound on the number of alternatives in a new poll.</td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_CATEGORY_TREE_DEPTH</code>
      </td>
      <td style="text-align:left">
        <p>Maximum category tree depth allowed for any</p>
        <p>new category to be created.</p>
      </td>
      <td style="text-align:center"><code>fill-in</code>
      </td>
    </tr>
  </tbody>
</table>

Notice that a lot of the limits are forward-looking. In the even to of a runtime upgrade, it may be that the limits are changed in a more restrictive direction, in which case it should not be expected that there is a migration that throws out the storage state, instead, the limit should only be understood to have bearing on future actions.

### Working Group

| Name | Value |
| :--- | :--- |
| `MAX_NUMBER_OF_WORKERS` | `fill-in` |
|  | . |



## Operations

### Create Category

**Parameters**

| Name | Description |
| :--- | :--- |
| `parent` | Optional parent category identifier. |
| `title` | Title of category. |
| `description` | Category description. |

#### Conditions

* Signer is working group lead.
* If provided, `parent` corresponds to valid category. \[Remove: , and it is not directly or indirectly archived.\]
* Limit `MAX_NUM_CATEGORIES` is respected.
* Limit `MAX_CATEGORY_TREE_DEPTH` is respected.

#### Effect

A new category is created.

### Update Category Archival Status

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `new_archival_status` | Whether new status is archived or active. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* If signer is moderator, then this moderator must be assigned have control of the category.
* The category has archival status different from `new_archival_status`.

#### Effect

Archival status of category corresponding to `category_id` is updated to `new_archival_status`.

### Update Category Title

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `new_title` | New title for category. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* If signer is moderator, then this moderator must be assigned have control of the category.

#### Effect

The title of the category corresponding to `category_id` is set to `new_title`.

### Update Category Description

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `new_description` | New description for category. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* If signer is moderator, then this moderator must be assigned have control of the category.

#### Effect

The description of the category corresponding to `category_id` is set to `new_description`.

### Set Category Stickied Threads

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `threads` | List of thread identifiers. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* If signer is moderator, then this moderator must be assigned have control of the category.
* All identifiers `threads`corresponding to existing threads.

#### Effect

The stickied threads of the category corresponding to `category_id` is set to `threads`.

### Update Category Membership of Moderator

**Parameters**

| Name | Description |
| :--- | :--- |
| `category_id` | Category identifier. |
| `moderator` | Working group identifier of moderator. |
| `is_member` | Whether moderator should be member. |

#### Conditions

* Signer is working group lead.
* `category_id` corresponds to an existing category.

_Note: There is no check that the provided moderator identifier corresponds to a genuine working group moderator._

#### Effect

If `is_member` is true, then the `moderator` identifier is added to the category moderators for category corresponding to `category_id` so long as the `MAX_MODERATORS_IN_CATEGORY` limit is respected. If `is_member`is not true, then the `moderator` is removed if present.

### Delete Category

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* There are no threads in the category.
* There are no subcategories in the category.
* If the parent of the category is the root, then `actor` must be the lead, otherwise for other categories `actor` must be lead, or moderator must be assigned have control of the category.

#### Effect

The category is dropped.

### Create Thread

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Identifier of member. |
| `category_id` | Category identifier. |
| `title` | Thread title. |
| `text` | Body text of thread. |
| `poll` | Optional poll information for thread. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* Limit `MAX_THREADS_IN_CATEGORY` is respected.
* The category is not archived.
* If poll information is provided, make sure 
  * limit `MAX_POLL_ALTERNATIVES` is respected, and that there are at least two alternatives.
  * the end time is in the future.

#### Effect

A thread is created.

### Update Thread Archival Status

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `new_archival_status` | Whether new status is archived or active. |

#### Conditions

* Signer uses role account of `actor`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* If signer is moderator, then this moderator must be assigned have control of the category.
* The thread has archival status different from `new_archival_status`.

#### Effect

Archival status of thread corresponding to `thread_id` is updated to `new_archival_status`.

### Edit Thread Title

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `new_title` | Thread title. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* `member_id` corresponds to the author of the thread.
* The category is not archived. \[WIP\]
* The thread is not archived. \[WIP\]

#### Effect

The title of the thread is set to `new_title`.

### Move Thread

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `new_category_id` | Category identifier. |

#### Conditions

* Signer uses role account of `actor`. 
* `category_id` corresponds to an existing category.
* `new_category_id` corresponds to an existing category.
* `category_id` and `new_category_id` are distinct.
* `thread_id` corresponds to an existing thread.
* If signer is moderator, then this moderator must be assigned have control of the category corresponding to `category_id`.
* If signer is moderator, then this moderator must be assigned have control of the category corresponding to `new_category_id`.
* Limit `MAX_THREADS_IN_CATEGORY` is respected for category corresponding to `new_category_id`. \[WIP\]

#### Effect

The thread has relocated to category corresponding to `new_category_id`.

### Delete Thread

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either member identifier, lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `rationale` | Human-readable text. |

#### Conditions

* Signer uses role account of `actor`. 
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* If signer is 
  * moderator, then this moderator must be assigned have control of the category corresponding to `category_id`.
  * member, then member is thread author and 
    * thread can at most have the one post.
    * category is not archived.
    * thread is not archived.

#### Effect

The thread and all corresponding posts are removed.

### Create Post

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `text` | Human-readable text. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* category is not archived.
* thread is not archived.
* Limit `MAX_POSTS_IN_THREAD` is respected.

#### Effect

A new post is created in thread with text `text`and author is `member_id`.

### Edit Post

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `post_id` | Post identifier. |
| `new_text` | Human-readable text. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* `post_id` corresponds to an existing post.
* member is author of post.
* category is not archived.
* thread is not archived.

#### Effect

Post text is set to `new_text`.

### React to Post

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `post_id` | Post identifier. |
| `reaction_value` | Reaction value. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* `post_id` corresponds to an existing post.
* member is author of post.
* category is not archived.
* thread is not archived.

#### Effect

Reaction with value `reaction_value`is accepted.

### Delete Post

**Parameters**

| Name | Description |
| :--- | :--- |
| `actor` | Either member identifier, lead or working group identifier of moderator. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `post_id` | Post identifier. |
| `reaction_value` | Reaction value. |

#### Conditions

* Signer uses role account of `actor`. 
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* `post_id` corresponds to an existing post.
* post is not first post in thread.
* If signer is 
  * moderator, then this moderator must be assigned have control of the category corresponding to `category_id`.
  * member, then member is post author and
    * category is not archived.
    * thread is not archived.

#### Effect

Post is deleted.

### Vote On Poll

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `category_id` | Category identifier. |
| `thread_id` | Thread identifier. |
| `alternative_index` | Index of a poll alternative. |

#### Conditions

* Signer uses role account of member corresponding to `member_id`.
* `category_id` corresponds to an existing category.
* `thread_id` corresponds to an existing thread.
* thread has poll which has not expired.
* member has not already voted in poll.
* `alternative-index` identifies an alternative in the poll.

#### Effect

The member is registered as having voted for alternative `aleternative_index`

## Examples

**WIP**





