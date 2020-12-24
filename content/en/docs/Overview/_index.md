---
title: "Overview"
linkTitle: "Overview"
weight: 1
description: >
  Monitoring and Provisioning PostgreSQL in a Professional Way
---

> PIGSTY: Postgres in Graphic/Guru STYle

Pigsty is a monitoring system that is specially designed for large scale PostgreSQL clusters. Along with a postgres cluster provisioning solution. It also shipped with a four-node VM sandbox environment based on vagrant for demonstration purpose.


## Quick Glance of Pigsty



![](pg-cluster.jpg)

> Dashboard that focus on an autonomous database cluster

### PG Service Dashboard

PG Service Dashboard focusing on proxy , servers, traffic routes. 

![](pg-service.jpg)

> Focusing on DNS, read-write/read-only, traffic routing, proxy & server health, etc...

### PG Instsance Dashboard

PG Instance Dashboard provides tons of metrics

![](pg-instance.jpg)

> Focusing on instance level metrics

### PG Database Dashboard

There may be multiple databases sharing same instance / cluster. So metrics here are focusing on one specific database rather than entire instance.

![](pg-database.jpg)

> Focusing on database level metrics

### PG Table Overview

PG Table Overview dashboard focus on objects within a database. For example: Table, Index, Function. 

![](pg-table-overview.jpg)

> Focusing on tables of a specific database



### PG Query

This dashboard focus on specific query in a specific database. It provides valuable informtion on database loads. 

![](pg-query.jpg)



### PG Table Catalog

PG Table Catalog will query database catalog directly using monitor user. It is not recommend but sometimes convinient.  

![](pg-table-catalog.jpg)

> View system catalog information of any specific table in database directly



### Node

![](node.jpg)

> Classical Node Exporter Dashboard





![](proxy.png)



## What is it?

It is a project makes you up & run postgres just like a professional


## Why do I want it?

You could have a production-grade database cluster in several minutes

* **What is it good for?**: Monitoring, High Availability

* **What is it not good for?**: Since it is an open source project. The author is NOT responsibile for any data loss or damange caused by this project. USE WITH CAUTION. (but we do provide business support which have availability guarenteen)

* **What is it *not yet* good for?**: It's greate! really

## Where should I go next?

Give your users next steps from the Overview. For example:

* [Getting Started](/docs/getting-started/): Get started with pigsty
* [Vagrant Sandbox](/docs/getting-started/): Explore pigsty in your own desktop
* [Monitoring System](/docs/getting-started/): Get started with $project
* [Configuration](/docs/getting-started/): Configure your own environment
* [Customize](/docs/getting-started/): Customize your own database template
* [Examples](/docs/examples/): Check out some example configuration


