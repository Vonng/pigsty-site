---
title: "Metrics"
linkTitle: "Metrics"
weight: 3
description: >
  Introduction of metrics
---


## Metrics

There are tons of metrics available in Pigsty.

### Source

Metrics are collected from exporters.

* Node Metrics (around 2000+ per instance)
* Postgres database metrics and pgbouncer connection pooler metrics (1000+ per instance)
* HAProxy load balancer metrics (400+ per instance)

### Category

Metrics can be categorized as four major groups: Error, Saturation, Traffic and Latency.

* **Errors**
  * Config Errors: NUMA, Checksum, THP, Sync Commit, etc...
  * Hardware errors: EDAC Mem Error
  * Software errors: TCP Listen Overflow, NTP time shift.
  * Service Aliveness: node, postgres,pgbouncer,haproxy,exporters, etc...
  * Client Queuing, Idle In Transaction, Sage, Deadlock, Replication break, Rollbacks, etc....
* **Saturation**
  * **PG Load**, Node Load
  * CPU Usage, Mem Usage, Disk Space Usage, Disk I/O Usage, Connection Usage, XID Usage
  * Cache Hit Rate / Buffer Hit Rate
* **Traffic**
  * QPS, TPS, Xacts, Rollbacks, Seasonality
  * In/Out Bytes of NIC/Pgbouncer, WAL Rate, Tuple CRUD Rate, Block/Buffer Access
  * Disk I/O, Network I/O, Mem Swap I/O
* **Latency** 
  * Transaction Response Time (Xact RT)
  * Query Response Time (Query RT)
  * Statement Response Time (Statement RT)
  * Disk Read/Write Latency
  * Replication Lag (in bytes or seconds)

> There are just a small portion of metrics. 

### Derived Metrics

In addition to metrics above, there are a large number of derived metrics. For example, QPS from pgbouncer will have following derived metrics

```yaml
################################################################
#                     QPS (Pgbouncer)                          #
################################################################
# TPS realtime (irate1m)
- record: pg:db:qps_realtime
expr: irate(pgbouncer_stat_total_query_count{}[1m])
- record: pg:ins:qps_realtime
expr: sum without(datname) (pg:db:qps_realtime{})
- record: pg:svc:qps_realtime
expr: sum by(cls, role) (pg:ins:qps_realtime{})
- record: pg:cls:qps_realtime
expr: sum by(cls) (pg:ins:qps_realtime{})
- record: pg:all:qps_realtime
expr: sum(pg:cls:qps_realtime{})

# qps (rate1m)
- record: pg:db:qps
expr: pgbouncer_stat_avg_query_count{datname!="pgbouncer"}
- record: pg:ins:qps
expr: sum without(datname) (pg:db:qps)
- record: pg:svc:qps
expr: sum by (cls, role) (pg:ins:qps)
- record: pg:cls:qps
expr: sum by(cls) (pg:ins:qps)
- record: pg:all:qps
expr: sum(pg:cls:qps)
# qps avg30m
- record: pg:db:qps_avg30m
expr: avg_over_time(pg:db:qps[30m])
- record: pg:ins:qps_avg30m
expr: avg_over_time(pg:ins:qps[30m])
- record: pg:svc:qps_avg30m
expr: avg_over_time(pg:svc:qps[30m])
- record: pg:cls:qps_avg30m
expr: avg_over_time(pg:cls:qps[30m])
- record: pg:all:qps_avg30m
expr: avg_over_time(pg:all:qps[30m])
# qps µ
- record: pg:db:qps_mu
expr: avg_over_time(pg:db:qps_avg30m[30m])
- record: pg:ins:qps_mu
expr: avg_over_time(pg:ins:qps_avg30m[30m])
- record: pg:svc:qps_mu
expr: avg_over_time(pg:svc:qps_avg30m[30m])
- record: pg:cls:qps_mu
expr: avg_over_time(pg:cls:qps_avg30m[30m])
- record: pg:all:qps_mu
expr: avg_over_time(pg:all:qps_avg30m[30m])
# qps σ: stddev30m qps
- record: pg:db:qps_sigma
expr: stddev_over_time(pg:db:qps[30m])
- record: pg:ins:qps_sigma
expr: stddev_over_time(pg:ins:qps[30m])
- record: pg:svc:qps_sigma
expr: stddev_over_time(pg:svc:qps[30m])
- record: pg:cls:qps_sigma
expr: stddev_over_time(pg:cls:qps[30m])
- record: pg:all:qps_sigma
expr: stddev_over_time(pg:all:qps[30m])
```

There are hundreds of rules defining extra metrics based on primitive metrics.

