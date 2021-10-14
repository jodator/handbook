---
description: >-
  Storing and distributing static assets, such as videos, avatars, covers and
  attachments, to end users is a key service of the network, and a dedicated
  subset of actors in the DAO operate dedicated nod
---

# Storage & Bandwidth

## Introduction

The system has a variety of static data assets 

* **Content Directory:** xx
* **Membership:** xx (not in Giza)
* **Proposals:** xx (not in Giza)
* **Council:** xxx (not in Giza)

## Note

This subsystem is under active development, and this document attempts to both explain how the current production system (as of Giza) works, as well as give indications about what is expected to be added later before mainnet.

## Goals

Here are some highlighted goals 

* Distinct roles for storage and distributing data.
* Storage system with redundancy and only partial replication in nodes.
* Distribution system with flexible policy space, allowing for Content Delivery Network (CDN) like organisation.
* Storage providers incentivized by a mix of
  * payment for uploads (not in Giza)
  * probabilistic on-chain proof-of-storage challenges (not in Giza)
  * payment from peer providers & bandwidth providers during synching (not in Giza)
  * slashing by discretion from group lead, with subsequent loss of reputational capital of membership in this role.
  * working group payments
* Bandwidth providers incentives by a mix of
  * slashing by discretion from group lead, with subsequent loss of reputational capital of membership in this role.
  * payment from gateway providers (not in Giza)
  * working group payments
* On-chain host resolution metadata.
* Rich ownership model where members, channels, working groups and even the council as a whole can custody storage assets.

## Concepts

### Working Groups

ddd

### Data Directory

xxx

### Integrations

xxx

### Storage Node

xxx Explain what it is, link to sub page about this.

### Bandwidth Node

xxx explain what it is, link to sub page about this.

## Architecture

.... give some big overview ...overview diagram

## Scenarios

### Upload

xxx

### New storage provider

xxx

### New bandwidth provider

xxx

### Download

xxx

### Deletion

xxx
