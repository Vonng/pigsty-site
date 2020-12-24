---
title: "Dashboards"
linkTitle: "Dashboards"
weight: 4
description: >
  Introduction to Dashboards
---





## Dashboards

### PG Overview

PG Overview dashboard is the entrance of entire monitoring system. 

Indexing clusters and instances, finding anomalies. Visualizing key metrics.

Other overview level dashboards:

* PG Overview: Home, index page
* PG Alerts: Simple alerting system based on grafana
* PG KPI: Key mertrics overview 

![](img/pg-overview.jpg)

> Overview of entire environment



### PG Cluster Dashboard

Index page for database cluster resource: services, instances, nodes.

Aggregated metrics on cluster level.

Cluster level dashboards:

* PG Cluster
* PG Cluster All
* PG Cluster Node
* PG Cluster Replication
* PG Cluster Activity
* PG Cluster Query
* PG Cluster Session
* PG Cluster Persist
* PG Cluster Stat

![](img/pg-cluster.jpg)

> Dashboard that focus on an autonomous database cluster

### PG Service Dashboard

PG Service Dashboard focusing on proxy , servers, traffic routes. 

![](img/pg-service.jpg)

> Focusing on DNS, read-write/read-only, traffic routing, proxy & server health, etc...

### PG Instsance Dashboard

PG Instance Dashboard provides tons of metrics

![](img/pg-instance.jpg)

> Focusing on instance level metrics

### PG Database Dashboard

There may be multiple databases sharing same instance / cluster. So metrics here are focusing on one specific database rather than entire instance.

![](img/pg-database.jpg)

> Focusing on database level metrics

### PG Table Overview

PG Table Overview dashboard focus on objects within a database. For example: Table, Index, Function. 

![](img/pg-table-overview.jpg)

> Focusing on tables of a specific database



### PG Query

This dashboard focus on specific query in a specific database. It provides valuable informtion on database loads. 

![](img/pg-query.jpg)



### PG Table Catalog

PG Table Catalog will query database catalog directly using monitor user. It is not recommend but sometimes convinient.  

![](img/pg-table-catalog.jpg)

> View system catalog information of any specific table in database directly



### Node

![](img/node.jpg)

> Classical Node Exporter Dashboard





![](img/proxy.png)

