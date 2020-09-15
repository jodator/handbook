---
description: >-
  An immutable, auditable, public forum is the main communication and
  coordination forum among platform members.
---

# Forum

## Introduction

The forum is the primary place for community-wide asynchronous written communication about all topics relevant to the platform among members. It is hierarchically organized into a tree of categories, each with designated moderators responsible for policing and encouraging effective and beneficial interactions among members. The moderators are part of a designated forum working group, and the lead of that working group can decide what moderators are responsible for what categories. Categories contain subcategories, and threaded topic-based discussions, called _threads_, where any member can open a thread, and others can come and make replies in the form of _posts_. Some threads can also include a poll, allowing any member to weight in on a question.

## Roles

* **Member:** Members participate as normal forum users, creating and responding to threads, participating in polls, and so on.
* **Moderator:** Moderators are assigned to subsets of categories... \(stickied???\) hierarchical or just plain????
* **Lead:** The forum lead is a member occupying the lead role in the forum working group. Beyond the normal working group lead obligations, this 

## Concepts

### Archiving

Both categories and threads can be _archived,_ and updating this is the responsibility of the moderators. Archiving should be understood as a read-only mode for normal usage of the given part of the forum.

### Category

A category is defined by the following

* **Id:** A global unique post identifier, effectively the number of posts created in the forum prior to this one. From this one can infer of posts in a thread.
* **Parent:** An optional reference to a parent category. When not set, it indicates this is a root level category.
* **Title:** A human-readable category name.
* **Description:** A human-readable description.
* **Stickied Threads**: A list of threads in this category that have been designated as having long-run importance to the category.
* **The number of subcategories:** The current number of categories with this category as its parent.
* **The number of threads:** The number of threads directly contained in this category, so not including subcategories in the count.
* **The number of moderators:** The number of moderates directly assigned to this category.
* **Archived:** Whether the category is archived or not. This impacts whether one can use the category, such as creating threads or posts directly, or recursively, within the category.

### Thread

A thread is defined by the following

* **Id:** A global unique post identifier, effectively the number of posts created in the forum prior to this one. From this one can infer of posts in a thread.
* **Title:** The human-readable title
* **Category:** The category within which the thread lives.
* **Author:** Member who created the thread.
* **Number of Posts:** The current number of posts in this thread.
* **Poll:** An optional poll for the thread, defined by the following
  * **Description:** A human-readable description of what question is being polled.
  * **Deadline:** Some block before which is the only time anyone can participate in the poll.
  * **Alternatives:** A list of alternatives, each with its own explainer text, vote count, and members who have voted in favor of it.
* Archival Status: xxx

### Post

A post in a thread is defined by the following

* **Id:** A global unique post identifier, effectively the number of posts created in the forum prior to this one. From this one can infer of posts in a thread.
* **Thread:** The thread 
* **Text:** xxxx
* **Author:** ....

## Constants

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

## Operations

### Create Category

Parameters

Conditions

Effect

### Category Updated

Parameters

Conditions

Effect

### Set Category Stickied Threads

Parameters

Conditions

Effect

### Add Moderator to Category

Parameters

Conditions

Effect

### Remove Moderator from Category

Parameters

Conditions

Effect

### Delete Category

Parameters

Conditions

Effect

### Lock/Archive Category

Parameters

Conditions

Effect

### Create Thread

Parameters

Conditions

Effect

### Update Thread Archival Status

Parameters

Conditions

Effect

### Edit Thread Title

Parameters

Conditions

Effect

### Move Thread

Parameters

Conditions

Effect

### Moderate Thread

Parameters

Conditions

Effect

### Delete Thread

Parameters

Conditions

Effect

### Create Post

Parameters

Conditions

Effect

### Edit Post

Parameters

Conditions

Effect

### React to Post

Parameters

Conditions

Effect

### Moderate Post

Parameters

Conditions

Effect

### Delete Post

Parameters

Conditions

Effect

### Vote On Poll

Parameters

Conditions

Effect

## Examples

xxx





