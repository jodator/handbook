---
description: >-
  An immutable, auditable, public forum is the main communication and
  coordination forum among platform members.
---

# Forum

## Introduction

The forum is the primary place for community wide asynchronous written communication about all topics relevant to platform among members. It is hierarchically organised into a tree of categories, each with designated moderators responsible for policing and encouraging effective and benefictial interactions among members. The moderators are part of a designated forum working group, and the lead of that working group can decide what moderators are responsible for what categories. Categories contain subcategories, and threaded topic based discussions, called _threads_, where any member can open a thread, and others can come and make replies in the form of _posts_. Some threads can also include a poll, allowing any member to weight in on some question.

## Roles

* **Member:** Members particpate as normal forum users, creating and responding to threads, participating in polls, and so on.
* **Moderator:** Moderators are assigned to subsets of categories... \(stickied???\) hierarchical or just plain????
* **Lead:** The forum lead is a member occupying the lead role in the forum working group. Beyond the normal working group lead obligations, this 

## Concepts

### Category

A category is defined by the following

* **Parent:** An optional referene to a parent category. When not set, it indicates this is a root level category.
* **Title:** A human readable category name.
* **Description:** A human readable description.
* **Stickied Threads**: A list of threads in this categories that have been designated as having long run importance to the category.
* Archival Status: &lt;...... explain archival status ....&gt;

### Poll

A poll is created and exists in the context of a thread, and it is defined by the following

* **Description:** A human readable description of what question is being polled.
* **Deadline:** Some block before which is the only time anyone can participate in the poll.
* **Alternatives:** A list of alternatives, each with its own explainer text, vote count and members who have voted in favor of it.

### Thread

A thread is defined by the following

* **Title:** The human readable title
* **Category:** The category within which the thread lives.
* **Author:** Member who created the thread.
* **Number of Posts:** 
* **Poll:** An optional poll for the thread.
* Archived: &lt;.....???. ....&gt;

### Post

A post in a thread is defined by the following

* Thread: ..
* Text:
* Author: ..



## Constants

| Name | Description | Value |
| :--- | :--- | :---: |
|  |  |  |
| `MAX_NUMBER_OF_POLL_ALTERNATIVES` | Upper bound on number of alternatives in new poll. | `fill-in` |

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





