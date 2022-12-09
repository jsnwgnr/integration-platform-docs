---
layout: default
title: Serialized Job Queues
nav_order: 1
parent: Advanced Topics
---
# Serialized Job Queues

## Overview

By default, all Integration Manager jobs run in parallel, up to the available concurrency, i.e. number of engines or nodes that you have licensed. Most of the time different kinds of jobs can run concurrently without issue.

Sometimes, however, the SAME job running concurrently can have undesirable outcome, i.e. the integration may not be idempotent.

Some examples:
* Actions on a database are not atomic, i.e. global transaction logic
* Common local files are used for lookup (and potentially updated with new information on a regular basis)
* A Job Config that is scheduled to run every 15 minutes but occasionally takes longer and overlaps

In these scenarios, you can protect your data without complex integration logic by using a Serialized Job Queue.

## Configuring a Serialized Job Queue

Strictly speaking, a mutex is a locking mechanism used to synchronize access to a resource. Only one task (can be a thread or process based on OS abstraction) can acquire the mutex. It means there is ownership associated with a mutex, and only the owner can release the lock (mutex). 

A serialized job queue can be configured for any Job Template or Job Config. In essence, this prevents running multiple jobs for the same Job Config at the same time.

In order to enable a serialized job queue for a Job Config, you simply set the "blocking" property to true (blocking is false by default).

This can be accomplished via a simple API PATCH method:

```
REQUEST:
PATCH https://api.im.actiandatacloud.com/v2/api/jobconfigs/[jobconfig id]
Authorization: Bearer [access token value]
Content-Type: application/json

{"blocking": true}
```

## Prerequisites

DataCloud subscribers have access to Serialized Job Queues out-of-box without additional configuration.

On-premise and VPC deployments of Integration Manager must have the ZooKeeper configuration enabled and connected, see Server Admin > Apache ZooKeeper Setup.