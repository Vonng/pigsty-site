---
title: "Available Metrics List"
linkTitle: "Available Metrics List"
date: 2020-11-05
weight: 3
description: >
  Available metrics list 
---

```
pg_activity_count,gauge,"connection count of given (datname,state)"
pg_activity_max_conn_duration,gauge,"max backend session duration since state change among (datname, state)"
pg_activity_max_duration,gauge,"max duration since state change among (datname, state)"
pg_activity_max_tx_duration,gauge,"max transaction duration since state change among (datname, state)"
pg_backend_count,gauge,backend process count
pg_backup_time,gauge,seconds since current backup start. null if don't have one
pg_bgwriter_buffers_alloc,counter,buffers allocated
pg_bgwriter_buffers_backend,counter,buffers written directly by a backend
pg_bgwriter_buffers_backend_fsync,counter,times a backend had to execute its own fsync
pg_bgwriter_buffers_checkpoint,counter,buffers written during checkpoints
pg_bgwriter_buffers_clean,counter,buffers written by the background writer
pg_bgwriter_checkpoint_sync_time,counter,"time spending on syncing files to disk, in µs"
pg_bgwriter_checkpoint_write_time,counter,"time spending on writing files to disk, in µs"
pg_bgwriter_checkpoints_req,counter,requested checkpoints that have been performed
pg_bgwriter_checkpoints_timed,counter,scheduled checkpoints that have been performed
pg_bgwriter_maxwritten_clean,counter,times that bgwriter stopped a cleaning scan
pg_bgwriter_stats_reset,counter,time when statistics were last reset
pg_boot_time,gauge,unix timestamp when postmaster boot
pg_checkpoint_checkpoint_lsn,counter,lsn of checkpoint
pg_checkpoint_elapse,gauge,time elapsed since this checkpoint in seconds
pg_checkpoint_full_page_writes,gauge,is full page write enabled ?
pg_checkpoint_newest_commit_ts_xid,gauge,xid with newest commit ts by the checkpoint
pg_checkpoint_next_multi_offset,gauge,next multixact id offset of this checkpoint
pg_checkpoint_next_multixact_id,gauge,next multixact id of this checkpoint
pg_checkpoint_next_oid,gauge,next object id since this checkpoint
pg_checkpoint_next_xid,gauge,next xid since this checkpoint
pg_checkpoint_next_xid_epoch,gauge,next xid epoch since this checkpoint
pg_checkpoint_oldest_active_xid,gauge,oldest active xid of the checkpoint
pg_checkpoint_oldest_commit_ts_xid,gauge,xid with oldest commit ts by the checkpoint
pg_checkpoint_oldest_multi_dbid,gauge,which db contins the oldest multi xid
pg_checkpoint_oldest_multi_xid,gauge,oldest active multi xid of the checkpoint
pg_checkpoint_oldest_xid,gauge,oldest existing xid of the checkpoint
pg_checkpoint_oldest_xid_dbid,gauge,which db contains the oldest xid
pg_checkpoint_prev_tli,gauge,previous WAL timeline
pg_checkpoint_redo_lsn,counter,redo start LSN
pg_checkpoint_time,gauge,timestamp of this checkpoint
pg_checkpoint_tli,gauge,current WAL timeline
pg_class_relage,gauge,age of non-index relation
pg_class_relpages,gauge,exact page count of this relation
pg_class_relsize,gauge,size of this relation
pg_class_reltuples,gauge,estimate relation tuples
pg_conf_reload_time,gauge,seconds since last configuration reload
pg_database_age,gauge,database age calculated by age(datfrozenxid)
pg_database_allow_conn,gauge,"1 allow connection, 0 does not allow"
pg_database_conn_limit,gauge,"connection limit, -1 for no limit"
pg_database_frozen_xid,gauge,tuple with xmin below this will always be visable (until wrap around)
pg_database_is_template,gauge,"1 for template db , 0 for normal db"
pg_db_blk_read_time,counter,"Time spent reading data file blocks by backends in this database, in milliseconds"
pg_db_blk_write_time,counter,"Time spent writing data file blocks by backends in this database, in milliseconds"
pg_db_blks_access,counter,blocks read plus blocks hit
pg_db_blks_hit,counter,blocks found in pg buffer
pg_db_blks_read,counter,blocks read from disk in this database
pg_db_checksum_failures,counter,"Number of data page checksum failures detected in this database, 12+ only"
pg_db_checksum_last_failure,gauge,"Time at which the last data page checksum failure was detected, 12+ only"
pg_db_confl_bufferpin,counter,Number of queries in this database that have been canceled due to pinned buffers
pg_db_confl_deadlock,counter,Number of queries in this database that have been canceled due to deadlocks
pg_db_confl_lock,counter,Number of queries in this database that have been canceled due to lock timeouts
pg_db_confl_snapshot,counter,Number of queries in this database that have been canceled due to old snapshots
pg_db_confl_tablespace,counter,Number of queries in this database that have been canceled due to dropped tablespaces
pg_db_conflicts,counter,Number of queries canceled due to conflicts with recovery in this database. (slave only)
pg_db_deadlocks,counter,Number of deadlocks detected in this database
pg_db_numbackends,gauge,backends currently connected to this database
pg_db_stats_reset,counter,Time at which these statistics were last reset
pg_db_temp_bytes,counter,Temporary file byte count
pg_db_temp_files,counter,Number of temporary files created by queries in this database
pg_db_tup_deleted,counter,rows deleted by queries in this database
pg_db_tup_fetched,counter,rows fetched by queries in this database
pg_db_tup_inserted,counter,rows inserted by queries in this database
pg_db_tup_modified,counter,rows modified by queries in this database
pg_db_tup_returned,counter,rows returned by queries in this database
pg_db_tup_updated,counter,rows updated by queries in this database
pg_db_xact_commit,counter,transactions in this database that have been committed
pg_db_xact_rollback,counter,transactions in this database that have been rolled back
pg_db_xact_total,counter,transactions in this database that have been issued
pg_downstream_count,gauge,count of corresponding replication state
pg_exporter_last_scrape_time,gauge,seconds exporter spending on scrapping
pg_exporter_query_cache_ttl,gauge,times to live of query cache
pg_exporter_query_scrape_duration,gauge,seconds query spending on scrapping
pg_exporter_query_scrape_error_count,gauge,times the query failed
pg_exporter_query_scrape_hit_count,gauge,numbers  been scrapped from this query
pg_exporter_query_scrape_metric_count,gauge,numbers of metrics been scrapped from this query
pg_exporter_query_scrape_total_count,gauge,times exporter server was scraped for metrics
pg_exporter_scrape_duration,gauge,seconds exporter spending on scrapping
pg_exporter_scrape_error_count,counter,times exporter was scraped for metrics and failed
pg_exporter_scrape_total_count,counter,times exporter was scraped for metrics
pg_exporter_server_scrape_duration,gauge,seconds exporter server spending on scrapping
pg_exporter_server_scrape_total_count,gauge,times exporter server was scraped for metrics
pg_exporter_server_scrape_total_seconds,gauge,seconds exporter server spending on scrapping
pg_exporter_up,gauge,always be 1 if your could retrieve metrics
pg_exporter_uptime,gauge,seconds since exporter primary server inited
pg_flush_lsn,counter,"primary only, location of current wal syncing"
pg_func_calls,counter,how many times this function has been called
pg_func_self_time,counter,"how much time spent in this function itself (other func not included), in ms"
pg_func_total_time,counter,"how much time spent in this function and it's child function, in ms"
pg_in_recovery,gauge,server is in recovery mode? 1 for yes 0 for no
pg_index_idx_blks_hit,counter,blocks hit from cache of this index
pg_index_idx_blks_read,counter,blocks been read from disk of this index
pg_index_idx_scan,counter,index scans initiated on this index
pg_index_idx_tup_fetch,counter,live table rows fetched by simple index scans using this index
pg_index_idx_tup_read,counter,index entries returned by scans on this index
pg_insert_lsn,counter,"primary only, location of current wal inserting"
pg_is_in_backup,gauge,1 if backup is in progress
pg_is_in_recovery,gauge,1 if in recovery mode
pg_is_wal_replay_paused,gauge,1 if wal play paused
pg_lag,gauge,replication lag in seconds from view of standby server
pg_last_replay_time,gauge,time when last transaction been replayed
pg_lock_count,counter,Number of locks of corresponding mode
pg_lsn,counter,"log sequence number, current write location"
pg_meta_info,gauge,constant 1
pg_query_blk_io_time,counter,time spent reading/writing blocks in µs (if track_io_timing is enabled)
pg_query_calls,counter,times been executed
pg_query_max_time,gauge,"Maximum time spent in the statement, in µs"
pg_query_mean_time,gauge,"Mean time spent in the statement, in µs"
pg_query_min_time,gauge,"Minimum time spent in the statement, in µs"
pg_query_rows,counter,rows retrieved or affected by the statement
pg_query_stddev_time,gauge,"Population standard deviation of time spent in the statement, in µs"
pg_query_total_time,counter,"Total time spent in the statement, in µs"
pg_receive_lsn,counter,"standby only, location of wal synced to disk"
pg_recovery_backup_end_lsn,counter,pg control recovery backup end lsn
pg_recovery_backup_start_lsn,counter,pg control recovery backup start lsn
pg_recovery_min_lsn,counter,pg control recovery min lsn
pg_recovery_min_timeline,counter,pg control recovery min timeline
pg_recovery_require_record,gauge,do recovery need a end of backup record
pg_replay_lsn,counter,"standby only, location of wal applied"
pg_replication_backend_uptime,gauge,how long since standby connect to this server
pg_replication_backend_xmin,gauge,this standby's xmin horizon reported by hot_standby_feedback.
pg_replication_flush_diff,gauge,last log position flushed to disk by this standby server diff with current lsn
pg_replication_flush_lag,gauge,latest ACK lsn diff with flush (sync-remote-flush lag)
pg_replication_flush_lsn,counter,last log position flushed to disk by this standby server
pg_replication_lsn,counter,current log position on this server
pg_replication_replay_diff,gauge,last log position replayed into the database on this standby server diff with current lsn
pg_replication_replay_lag,gauge,latest ACK lsn diff with replay (sync-remote-apply lag)
pg_replication_replay_lsn,counter,last log position replayed into the database on this standby server
pg_replication_sent_diff,gauge,last log position sent to this standby server diff with current lsn
pg_replication_sent_lsn,counter,last log position sent to this standby server
pg_replication_sync_priority,gauge,priority of being chosen as synchronous standby
pg_replication_write_diff,gauge,last log position written to disk by this standby server diff with current lsn
pg_replication_write_lag,gauge,latest ACK lsn diff with write (sync-remote-write lag)
pg_replication_write_lsn,counter,last log position written to disk by this standby server
pg_setting_block_size,gauge,"pg page block size, 8192 by default"
pg_setting_data_checksums,gauge,"whether data checksum is enabled, 1 enabled 0 disabled"
pg_setting_max_connections,gauge,number of concurrent connections to the database server
pg_setting_max_locks_per_transaction,gauge,no more than this many distinct objects can be locked at any one time
pg_setting_max_prepared_transactions,gauge,maximum number of transactions that can be in the prepared state simultaneously
pg_setting_max_replication_slots,gauge,maximum number of replication slots
pg_setting_max_wal_senders,gauge,maximum number of concurrent connections from standby servers
pg_setting_max_worker_processes,gauge,maximum number of background processes that the system can support
pg_setting_wal_keep_segments,gauge,minimum number of past log file segments kept in the pg_wal directory
pg_setting_wal_log_hints,gauge,"whether wal_log_hints is enabled, 1 enabled 0 disabled"
pg_size_bytes,gauge,file size in bytes
pg_slot_active,gauge,whether the slot is currently being used
pg_slot_catalog_xmin,gauge,oldest txid that this slot needs the database to retain for catalog
pg_slot_confirm_lsn,counter,"lsn that confirmed by logical standby, null for physical slot"
pg_slot_restart_lsn,counter,"lsn that needs retain, wal after that will be kept"
pg_slot_retained_bytes,gauge,bytes retained for this slot
pg_slot_temporary,gauge,whether the slot is a temporary replication slot
pg_slot_xmin,gauge,oldest txid that this slot needs the database to retain
pg_sync_standby_disabled,gauge,"1 if disabled, 0 if enabled"
pg_sync_standby_enabled,gauge,"1 if enabled, 0 if disabled"
pg_table_analyze_count,counter,manual analyze count
pg_table_autoanalyze_count,counter,automatic analyze count
pg_table_autovacuum_count,counter,automatic vacuum count
pg_table_bloat_ratio,gauge,"estimated bloat ratio of this table, 0~1"
pg_table_bloat_size,gauge,total size in bytes of this table
pg_table_heap_blks_hit,counter,relation heap hit
pg_table_heap_blks_read,counter,relation heap read
pg_table_idx_blks_hit,counter,index hit
pg_table_idx_blks_read,counter,index read
pg_table_idx_scan,counter,index scans initiated on this table
pg_table_idx_tup_fetch,counter,rows fetched by index scans
pg_table_last_analyze,gauge,when table was manually analyzed last time
pg_table_last_autoanalyze,gauge,when table was automatically analyzed last time
pg_table_last_autovacuum,gauge,when table was automatically vacuumed last time
pg_table_last_vacuum,gauge,when table was manually vacuumed last time (FULL not count)
pg_table_n_dead_tup,gauge,estimated dead rows
pg_table_n_live_tup,gauge,estimated live rows
pg_table_n_mod_since_analyze,gauge,rows changed since last analyze
pg_table_n_tup_del,counter,rows deleted
pg_table_n_tup_hot_upd,counter,rows updated in HOT mode
pg_table_n_tup_ins,counter,rows inserted
pg_table_n_tup_mod,counter,rows modified (insert + update + delete)
pg_table_n_tup_upd,counter,rows updated
pg_table_seq_scan,counter,sequential scans initiated on this table
pg_table_seq_tup_read,counter,live rows fetched by sequential scans
pg_table_size_bytes,gauge,"total size of this table (including toast, index, toast index)"
pg_table_size_indexsize,gauge,size of all related indexes
pg_table_size_relsize,gauge,"size of this table itself (main, vm, fsm)"
pg_table_size_toastsize,gauge,size of corresponding toast tables
pg_table_tbl_scan,counter,total table scan = index scan + seq scan
pg_table_tidx_blks_hit,counter,toast index hit
pg_table_tidx_blks_read,counter,toast index read
pg_table_toast_blks_hit,counter,toast heap hit
pg_table_toast_blks_read,counter,toast heap read
pg_table_tup_read,counter,total tuples read = index fetch + seq read
pg_table_vacuum_count,counter,manual vacuum count (FULL not count)
pg_timestamp,gauge,database current timestamp
pg_up,gauge,"last scrape was able to connect to the server: 1 for yes, 0 for no"
pg_uptime,gauge,seconds since postmaster start
pg_version,gauge,server version number
pg_walreceiver_current_ts,gauge,current_timestamp
pg_walreceiver_init_lsn,counter,first time received lsn when WAL receiver is started
pg_walreceiver_init_tli,gauge,first time received timeline number when WAL receiver is started
pg_walreceiver_last_lsn,counter,latest lsn that already flushed to standby disk
pg_walreceiver_last_tli,gauge,latest timeline that already flushed to standby disk
pg_walreceiver_receive_ts,gauge,receipt time of last message received from origin WAL sender
pg_walreceiver_report_lsn,counter,with time zone	Time of last write-ahead log location reported to origin WAL sender
pg_walreceiver_report_ts,gauge,timestamp of last time reporting to sender
pg_walreceiver_send_ts,gauge,send time of last message received from origin WAL sender
pg_write_lsn,counter,"primary only, location of current wal writing"
pg_xact_xmax,gauge,first as-yet-unassigned txid. txid >= this are invisible.
pg_xact_xmin,gauge,earliest txid that is still active
pg_xact_xnum,gauge,current active transaction count
pgbouncer_database_current_connections,gauge,current number of connections for this database
pgbouncer_database_disabled,gauge,"1 if this database is currently disabled, else 0"
pgbouncer_database_max_connections,gauge,maximum number of allowed connections for this database
pgbouncer_database_paused,gauge,"1 if this database is currently paused, else 0"
pgbouncer_database_pool_size,counter,maximum number of server connections
pgbouncer_database_reserve_pool,gauge,maximum number of additional connections for this database
pgbouncer_exporter_last_scrape_time,gauge,seconds exporter spending on scrapping
pgbouncer_exporter_query_cache_ttl,gauge,times to live of query cache
pgbouncer_exporter_query_scrape_duration,gauge,seconds query spending on scrapping
pgbouncer_exporter_query_scrape_error_count,gauge,times the query failed
pgbouncer_exporter_query_scrape_hit_count,gauge,numbers  been scrapped from this query
pgbouncer_exporter_query_scrape_metric_count,gauge,numbers of metrics been scrapped from this query
pgbouncer_exporter_query_scrape_total_count,gauge,times exporter server was scraped for metrics
pgbouncer_exporter_scrape_duration,gauge,seconds exporter spending on scrapping
pgbouncer_exporter_scrape_error_count,counter,times exporter was scraped for metrics and failed
pgbouncer_exporter_scrape_total_count,counter,times exporter was scraped for metrics
pgbouncer_exporter_server_scrape_duration,gauge,seconds exporter server spending on scrapping
pgbouncer_exporter_server_scrape_total_count,gauge,times exporter server was scraped for metrics
pgbouncer_exporter_server_scrape_total_seconds,gauge,seconds exporter server spending on scrapping
pgbouncer_exporter_up,gauge,always be 1 if your could retrieve metrics
pgbouncer_exporter_uptime,gauge,seconds since exporter primary server inited
pgbouncer_in_recovery,gauge,server is in recovery mode? 1 for yes 0 for no
pgbouncer_list_items,gauge,count of curresponding pgbouncer object
pgbouncer_pool_active_clients,gauge,client connections that are linked to server connection and can process queries
pgbouncer_pool_active_servers,gauge,server connections that are linked to a client
pgbouncer_pool_idle_servers,gauge,server connections that are unused and immediately usable for client queries
pgbouncer_pool_login_servers,gauge,server connections currently in the process of logging in
pgbouncer_pool_maxwait,gauge,"how long the first(oldest) client in the queue has waited, in seconds, key metric"
pgbouncer_pool_maxwait_us,gauge,microsecond part of the maximum waiting time.
pgbouncer_pool_tested_servers,gauge,server connections that are currently running reset or check query
pgbouncer_pool_used_servers,gauge,server connections that have been idle for more than server_check_delay (means have to run check query)
pgbouncer_pool_waiting_clients,gauge,client connections that have sent queries but have not yet got a server connection
pgbouncer_stat_avg_query_count,gauge,how many times this function has been called
pgbouncer_stat_avg_query_time,gauge,"how much time spent in this function and it's child function, in ms"
pgbouncer_stat_avg_recv,gauge,"how much time spent in this function and it's child function, in ms"
pgbouncer_stat_avg_sent,gauge,"how much time spent in this function itself (other func not included), in ms"
pgbouncer_stat_avg_wait_time,gauge,"how much time spent in this function itself (other func not included), in ms"
pgbouncer_stat_avg_xact_count,gauge,"how much time spent in this function itself (other func not included), in ms"
pgbouncer_stat_avg_xact_time,gauge,how many times this function has been called
pgbouncer_stat_total_query_count,gauge,relation name of this relation
node_arp_entries,gauge,ARP entries by device
node_boot_time_seconds,gauge,"Node boot time, in unixtime."
node_context_switches_total,counter,Total number of context switches.
node_cooling_device_cur_state,gauge,Current throttle state of the cooling device
node_cooling_device_max_state,gauge,Maximum throttle state of the cooling device
node_cpu_guest_seconds_total,counter,Seconds the cpus spent in guests (VMs) for each mode.
node_cpu_seconds_total,counter,Seconds the cpus spent in each mode.
node_disk_discard_time_seconds_total,counter,This is the total number of seconds spent by all discards.
node_disk_discarded_sectors_total,counter,The total number of sectors discarded successfully.
node_disk_discards_completed_total,counter,The total number of discards completed successfully.
node_disk_discards_merged_total,counter,The total number of discards merged.
node_disk_io_now,gauge,The number of I/Os currently in progress.
node_disk_io_time_seconds_total,counter,Total seconds spent doing I/Os.
node_disk_io_time_weighted_seconds_total,counter,The weighted # of seconds spent doing I/Os.
node_disk_read_bytes_total,counter,The total number of bytes read successfully.
node_disk_read_time_seconds_total,counter,The total number of seconds spent by all reads.
node_disk_reads_completed_total,counter,The total number of reads completed successfully.
node_disk_reads_merged_total,counter,The total number of reads merged.
node_disk_write_time_seconds_total,counter,This is the total number of seconds spent by all writes.
node_disk_writes_completed_total,counter,The total number of writes completed successfully.
node_disk_writes_merged_total,counter,The number of writes merged.
node_disk_written_bytes_total,counter,The total number of bytes written successfully.
node_entropy_available_bits,gauge,Bits of available entropy.
node_exporter_build_info,gauge,"A metric with a constant '1' value labeled by version, revision, branch, and goversion from which node_exporter was built."
node_filefd_allocated,gauge,File descriptor statistics: allocated.
node_filefd_maximum,gauge,File descriptor statistics: maximum.
node_filesystem_avail_bytes,gauge,Filesystem space available to non-root users in bytes.
node_filesystem_device_error,gauge,Whether an error occurred while getting statistics for the given device.
node_filesystem_files,gauge,Filesystem total file nodes.
node_filesystem_files_free,gauge,Filesystem total free file nodes.
node_filesystem_free_bytes,gauge,Filesystem free space in bytes.
node_filesystem_readonly,gauge,Filesystem read-only status.
node_filesystem_size_bytes,gauge,Filesystem size in bytes.
node_forks_total,counter,Total number of forks.
node_intr_total,counter,Total number of interrupts serviced.
node_ipvs_connections_total,counter,The total number of connections made.
node_ipvs_incoming_bytes_total,counter,The total amount of incoming data.
node_ipvs_incoming_packets_total,counter,The total number of incoming packets.
node_ipvs_outgoing_bytes_total,counter,The total amount of outgoing data.
node_ipvs_outgoing_packets_total,counter,The total number of outgoing packets.
node_load1,gauge,1m load average.
node_load15,gauge,15m load average.
node_load5,gauge,5m load average.
node_memory_Active_anon_bytes,gauge,Memory information field Active_anon_bytes.
node_memory_Active_bytes,gauge,Memory information field Active_bytes.
node_memory_Active_file_bytes,gauge,Memory information field Active_file_bytes.
node_memory_AnonHugePages_bytes,gauge,Memory information field AnonHugePages_bytes.
node_memory_AnonPages_bytes,gauge,Memory information field AnonPages_bytes.
node_memory_Bounce_bytes,gauge,Memory information field Bounce_bytes.
node_memory_Buffers_bytes,gauge,Memory information field Buffers_bytes.
node_memory_Cached_bytes,gauge,Memory information field Cached_bytes.
node_memory_CmaFree_bytes,gauge,Memory information field CmaFree_bytes.
node_memory_CmaTotal_bytes,gauge,Memory information field CmaTotal_bytes.
node_memory_CommitLimit_bytes,gauge,Memory information field CommitLimit_bytes.
node_memory_Committed_AS_bytes,gauge,Memory information field Committed_AS_bytes.
node_memory_DirectMap1G_bytes,gauge,Memory information field DirectMap1G_bytes.
node_memory_DirectMap2M_bytes,gauge,Memory information field DirectMap2M_bytes.
node_memory_DirectMap4k_bytes,gauge,Memory information field DirectMap4k_bytes.
node_memory_Dirty_bytes,gauge,Memory information field Dirty_bytes.
node_memory_HardwareCorrupted_bytes,gauge,Memory information field HardwareCorrupted_bytes.
node_memory_HugePages_Free,gauge,Memory information field HugePages_Free.
node_memory_HugePages_Rsvd,gauge,Memory information field HugePages_Rsvd.
node_memory_HugePages_Surp,gauge,Memory information field HugePages_Surp.
node_memory_HugePages_Total,gauge,Memory information field HugePages_Total.
node_memory_Hugepagesize_bytes,gauge,Memory information field Hugepagesize_bytes.
node_memory_Hugetlb_bytes,gauge,Memory information field Hugetlb_bytes.
node_memory_Inactive_anon_bytes,gauge,Memory information field Inactive_anon_bytes.
node_memory_Inactive_bytes,gauge,Memory information field Inactive_bytes.
node_memory_Inactive_file_bytes,gauge,Memory information field Inactive_file_bytes.
node_memory_KernelStack_bytes,gauge,Memory information field KernelStack_bytes.
node_memory_Mapped_bytes,gauge,Memory information field Mapped_bytes.
node_memory_MemAvailable_bytes,gauge,Memory information field MemAvailable_bytes.
node_memory_MemFree_bytes,gauge,Memory information field MemFree_bytes.
node_memory_MemTotal_bytes,gauge,Memory information field MemTotal_bytes.
node_memory_Mlocked_bytes,gauge,Memory information field Mlocked_bytes.
node_memory_NFS_Unstable_bytes,gauge,Memory information field NFS_Unstable_bytes.
node_memory_PageTables_bytes,gauge,Memory information field PageTables_bytes.
node_memory_Percpu_bytes,gauge,Memory information field Percpu_bytes.
node_memory_SReclaimable_bytes,gauge,Memory information field SReclaimable_bytes.
node_memory_SUnreclaim_bytes,gauge,Memory information field SUnreclaim_bytes.
node_memory_ShmemHugePages_bytes,gauge,Memory information field ShmemHugePages_bytes.
node_memory_ShmemPmdMapped_bytes,gauge,Memory information field ShmemPmdMapped_bytes.
node_memory_Shmem_bytes,gauge,Memory information field Shmem_bytes.
node_memory_Slab_bytes,gauge,Memory information field Slab_bytes.
node_memory_SwapCached_bytes,gauge,Memory information field SwapCached_bytes.
node_memory_SwapFree_bytes,gauge,Memory information field SwapFree_bytes.
node_memory_SwapTotal_bytes,gauge,Memory information field SwapTotal_bytes.
node_memory_Unevictable_bytes,gauge,Memory information field Unevictable_bytes.
node_memory_VmallocChunk_bytes,gauge,Memory information field VmallocChunk_bytes.
node_memory_VmallocTotal_bytes,gauge,Memory information field VmallocTotal_bytes.
node_memory_VmallocUsed_bytes,gauge,Memory information field VmallocUsed_bytes.
node_memory_WritebackTmp_bytes,gauge,Memory information field WritebackTmp_bytes.
node_memory_Writeback_bytes,gauge,Memory information field Writeback_bytes.
node_netstat_Icmp6_InErrors,unknown,Statistic Icmp6InErrors.
node_netstat_Icmp6_InMsgs,unknown,Statistic Icmp6InMsgs.
node_netstat_Icmp6_OutMsgs,unknown,Statistic Icmp6OutMsgs.
node_netstat_Icmp_InErrors,unknown,Statistic IcmpInErrors.
node_netstat_Icmp_InMsgs,unknown,Statistic IcmpInMsgs.
node_netstat_Icmp_OutMsgs,unknown,Statistic IcmpOutMsgs.
node_netstat_Ip6_InOctets,unknown,Statistic Ip6InOctets.
node_netstat_Ip6_OutOctets,unknown,Statistic Ip6OutOctets.
node_netstat_IpExt_InOctets,unknown,Statistic IpExtInOctets.
node_netstat_IpExt_OutOctets,unknown,Statistic IpExtOutOctets.
node_netstat_Ip_Forwarding,unknown,Statistic IpForwarding.
node_netstat_TcpExt_ListenDrops,unknown,Statistic TcpExtListenDrops.
node_netstat_TcpExt_ListenOverflows,unknown,Statistic TcpExtListenOverflows.
node_netstat_TcpExt_SyncookiesFailed,unknown,Statistic TcpExtSyncookiesFailed.
node_netstat_TcpExt_SyncookiesRecv,unknown,Statistic TcpExtSyncookiesRecv.
node_netstat_TcpExt_SyncookiesSent,unknown,Statistic TcpExtSyncookiesSent.
node_netstat_TcpExt_TCPSynRetrans,unknown,Statistic TcpExtTCPSynRetrans.
node_netstat_Tcp_ActiveOpens,unknown,Statistic TcpActiveOpens.
node_netstat_Tcp_CurrEstab,unknown,Statistic TcpCurrEstab.
node_netstat_Tcp_InErrs,unknown,Statistic TcpInErrs.
node_netstat_Tcp_InSegs,unknown,Statistic TcpInSegs.
node_netstat_Tcp_OutSegs,unknown,Statistic TcpOutSegs.
node_netstat_Tcp_PassiveOpens,unknown,Statistic TcpPassiveOpens.
node_netstat_Tcp_RetransSegs,unknown,Statistic TcpRetransSegs.
node_netstat_Udp6_InDatagrams,unknown,Statistic Udp6InDatagrams.
node_netstat_Udp6_InErrors,unknown,Statistic Udp6InErrors.
node_netstat_Udp6_NoPorts,unknown,Statistic Udp6NoPorts.
node_netstat_Udp6_OutDatagrams,unknown,Statistic Udp6OutDatagrams.
node_netstat_Udp6_RcvbufErrors,unknown,Statistic Udp6RcvbufErrors.
node_netstat_Udp6_SndbufErrors,unknown,Statistic Udp6SndbufErrors.
node_netstat_UdpLite6_InErrors,unknown,Statistic UdpLite6InErrors.
node_netstat_UdpLite_InErrors,unknown,Statistic UdpLiteInErrors.
node_netstat_Udp_InDatagrams,unknown,Statistic UdpInDatagrams.
node_netstat_Udp_InErrors,unknown,Statistic UdpInErrors.
node_netstat_Udp_NoPorts,unknown,Statistic UdpNoPorts.
node_netstat_Udp_OutDatagrams,unknown,Statistic UdpOutDatagrams.
node_netstat_Udp_RcvbufErrors,unknown,Statistic UdpRcvbufErrors.
node_netstat_Udp_SndbufErrors,unknown,Statistic UdpSndbufErrors.
node_network_address_assign_type,gauge,address_assign_type value of /sys/class/net/<iface>.
node_network_carrier,gauge,carrier value of /sys/class/net/<iface>.
node_network_carrier_changes_total,counter,carrier_changes_total value of /sys/class/net/<iface>.
node_network_carrier_down_changes_total,counter,carrier_down_changes_total value of /sys/class/net/<iface>.
node_network_carrier_up_changes_total,counter,carrier_up_changes_total value of /sys/class/net/<iface>.
node_network_device_id,gauge,device_id value of /sys/class/net/<iface>.
node_network_dormant,gauge,dormant value of /sys/class/net/<iface>.
node_network_flags,gauge,flags value of /sys/class/net/<iface>.
node_network_iface_id,gauge,iface_id value of /sys/class/net/<iface>.
node_network_iface_link,gauge,iface_link value of /sys/class/net/<iface>.
node_network_iface_link_mode,gauge,iface_link_mode value of /sys/class/net/<iface>.
node_network_info,gauge,"Non-numeric data from /sys/class/net/<iface>, value is always 1."
node_network_mtu_bytes,gauge,mtu_bytes value of /sys/class/net/<iface>.
node_network_net_dev_group,gauge,net_dev_group value of /sys/class/net/<iface>.
node_network_protocol_type,gauge,protocol_type value of /sys/class/net/<iface>.
node_network_receive_bytes_total,counter,Network device statistic receive_bytes.
node_network_receive_compressed_total,counter,Network device statistic receive_compressed.
node_network_receive_drop_total,counter,Network device statistic receive_drop.
node_network_receive_errs_total,counter,Network device statistic receive_errs.
node_network_receive_fifo_total,counter,Network device statistic receive_fifo.
node_network_receive_frame_total,counter,Network device statistic receive_frame.
node_network_receive_multicast_total,counter,Network device statistic receive_multicast.
node_network_receive_packets_total,counter,Network device statistic receive_packets.
node_network_speed_bytes,gauge,speed_bytes value of /sys/class/net/<iface>.
node_network_transmit_bytes_total,counter,Network device statistic transmit_bytes.
node_network_transmit_carrier_total,counter,Network device statistic transmit_carrier.
node_network_transmit_colls_total,counter,Network device statistic transmit_colls.
node_network_transmit_compressed_total,counter,Network device statistic transmit_compressed.
node_network_transmit_drop_total,counter,Network device statistic transmit_drop.
node_network_transmit_errs_total,counter,Network device statistic transmit_errs.
node_network_transmit_fifo_total,counter,Network device statistic transmit_fifo.
node_network_transmit_packets_total,counter,Network device statistic transmit_packets.
node_network_transmit_queue_length,gauge,transmit_queue_length value of /sys/class/net/<iface>.
node_network_up,gauge,"Value is 1 if operstate is 'up', 0 otherwise."
node_nf_conntrack_entries,gauge,Number of currently allocated flow entries for connection tracking.
node_nf_conntrack_entries_limit,gauge,Maximum size of connection tracking table.
node_ntp_leap,gauge,"NTPD leap second indicator, 2 bits."
node_ntp_offset_seconds,gauge,ClockOffset between NTP and local clock.
node_ntp_reference_timestamp_seconds,gauge,"NTPD ReferenceTime, UNIX timestamp."
node_ntp_root_delay_seconds,gauge,NTPD RootDelay.
node_ntp_root_dispersion_seconds,gauge,NTPD RootDispersion.
node_ntp_rtt_seconds,gauge,RTT to NTPD.
node_ntp_sanity,gauge,NTPD sanity according to RFC5905 heuristics and configured limits.
node_ntp_stratum,gauge,NTPD stratum.
node_processes_max_processes,gauge,Number of max PIDs limit
node_processes_max_threads,gauge,Limit of threads in the system
node_processes_pids,gauge,Number of PIDs
node_processes_state,gauge,Number of processes in each state.
node_processes_threads,gauge,Allocated threads in system
node_procs_blocked,gauge,Number of processes blocked waiting for I/O to complete.
node_procs_running,gauge,Number of processes in runnable state.
node_schedstat_running_seconds_total,counter,Number of seconds CPU spent running a process.
node_schedstat_timeslices_total,counter,Number of timeslices executed by CPU.
node_schedstat_waiting_seconds_total,counter,Number of seconds spent by processing waiting for this CPU.
node_scrape_collector_duration_seconds,gauge,node_exporter: Duration of a collector scrape.
node_scrape_collector_success,gauge,node_exporter: Whether a collector succeeded.
node_sockstat_FRAG6_inuse,gauge,Number of FRAG6 sockets in state inuse.
node_sockstat_FRAG6_memory,gauge,Number of FRAG6 sockets in state memory.
node_sockstat_FRAG_inuse,gauge,Number of FRAG sockets in state inuse.
node_sockstat_FRAG_memory,gauge,Number of FRAG sockets in state memory.
node_sockstat_RAW6_inuse,gauge,Number of RAW6 sockets in state inuse.
node_sockstat_RAW_inuse,gauge,Number of RAW sockets in state inuse.
node_sockstat_TCP6_inuse,gauge,Number of TCP6 sockets in state inuse.
node_sockstat_TCP_alloc,gauge,Number of TCP sockets in state alloc.
node_sockstat_TCP_inuse,gauge,Number of TCP sockets in state inuse.
node_sockstat_TCP_mem,gauge,Number of TCP sockets in state mem.
node_sockstat_TCP_mem_bytes,gauge,Number of TCP sockets in state mem_bytes.
node_sockstat_TCP_orphan,gauge,Number of TCP sockets in state orphan.
node_sockstat_TCP_tw,gauge,Number of TCP sockets in state tw.
node_sockstat_UDP6_inuse,gauge,Number of UDP6 sockets in state inuse.
node_sockstat_UDPLITE6_inuse,gauge,Number of UDPLITE6 sockets in state inuse.
node_sockstat_UDPLITE_inuse,gauge,Number of UDPLITE sockets in state inuse.
node_sockstat_UDP_inuse,gauge,Number of UDP sockets in state inuse.
node_sockstat_UDP_mem,gauge,Number of UDP sockets in state mem.
node_sockstat_UDP_mem_bytes,gauge,Number of UDP sockets in state mem_bytes.
node_sockstat_sockets_used,gauge,Number of IPv4 sockets in use.
node_systemd_socket_accepted_connections_total,counter,Total number of accepted socket connections
node_systemd_socket_current_connections,gauge,Current number of socket connections
node_systemd_system_running,gauge,Whether the system is operational (see 'systemctl is-system-running')
node_systemd_timer_last_trigger_seconds,gauge,Seconds since epoch of last trigger.
node_systemd_unit_state,gauge,Systemd unit
node_systemd_units,gauge,Summary of systemd unit states
node_systemd_version,gauge,Detected systemd version
node_tcp_connection_states,gauge,Number of connection states.
node_textfile_scrape_error,gauge,"1 if there was an error opening or reading a file, 0 otherwise"
node_time_seconds,gauge,System time in seconds since epoch (1970).
node_timex_estimated_error_seconds,gauge,Estimated error in seconds.
node_timex_frequency_adjustment_ratio,gauge,Local clock frequency adjustment.
node_timex_loop_time_constant,gauge,Phase-locked loop time constant.
node_timex_maxerror_seconds,gauge,Maximum error in seconds.
node_timex_offset_seconds,gauge,Time offset in between local system and reference clock.
node_timex_pps_calibration_total,counter,Pulse per second count of calibration intervals.
node_timex_pps_error_total,counter,Pulse per second count of calibration errors.
node_timex_pps_frequency_hertz,gauge,Pulse per second frequency.
node_timex_pps_jitter_seconds,gauge,Pulse per second jitter.
node_timex_pps_jitter_total,counter,Pulse per second count of jitter limit exceeded events.
node_timex_pps_shift_seconds,gauge,Pulse per second interval duration.
node_timex_pps_stability_exceeded_total,counter,Pulse per second count of stability limit exceeded events.
node_timex_pps_stability_hertz,gauge,"Pulse per second stability, average of recent frequency changes."
node_timex_status,gauge,Value of the status array bits.
node_timex_sync_status,gauge,"Is clock synchronized to a reliable server (1 = yes, 0 = no)."
node_timex_tai_offset_seconds,gauge,International Atomic Time (TAI) offset.
node_timex_tick_seconds,gauge,Seconds between clock ticks.
node_udp_queues,gauge,Number of allocated memory in the kernel for UDP datagrams in bytes.
node_uname_info,gauge,Labeled system information as provided by the uname system call.
node_vmstat_oom_kill,unknown,/proc/vmstat information field oom_kill.
node_vmstat_pgfault,unknown,/proc/vmstat information field pgfault.
node_vmstat_pgmajfault,unknown,/proc/vmstat information field pgmajfault.
node_vmstat_pgpgin,unknown,/proc/vmstat information field pgpgin.
node_vmstat_pgpgout,unknown,/proc/vmstat information field pgpgout.
node_vmstat_pswpin,unknown,/proc/vmstat information field pswpin.
node_vmstat_pswpout,unknown,/proc/vmstat information field pswpout.
node_xfs_allocation_btree_compares_total,counter,Number of allocation B-tree compares for a filesystem.
node_xfs_allocation_btree_lookups_total,counter,Number of allocation B-tree lookups for a filesystem.
node_xfs_allocation_btree_records_deleted_total,counter,Number of allocation B-tree records deleted for a filesystem.
node_xfs_allocation_btree_records_inserted_total,counter,Number of allocation B-tree records inserted for a filesystem.
node_xfs_block_map_btree_compares_total,counter,Number of block map B-tree compares for a filesystem.
node_xfs_block_map_btree_lookups_total,counter,Number of block map B-tree lookups for a filesystem.
node_xfs_block_map_btree_records_deleted_total,counter,Number of block map B-tree records deleted for a filesystem.
node_xfs_block_map_btree_records_inserted_total,counter,Number of block map B-tree records inserted for a filesystem.
node_xfs_block_mapping_extent_list_compares_total,counter,Number of extent list compares for a filesystem.
node_xfs_block_mapping_extent_list_deletions_total,counter,Number of extent list deletions for a filesystem.
node_xfs_block_mapping_extent_list_insertions_total,counter,Number of extent list insertions for a filesystem.
node_xfs_block_mapping_extent_list_lookups_total,counter,Number of extent list lookups for a filesystem.
node_xfs_block_mapping_reads_total,counter,Number of block map for read operations for a filesystem.
node_xfs_block_mapping_unmaps_total,counter,Number of block unmaps (deletes) for a filesystem.
node_xfs_block_mapping_writes_total,counter,Number of block map for write operations for a filesystem.
node_xfs_directory_operation_create_total,counter,Number of times a new directory entry was created for a filesystem.
node_xfs_directory_operation_getdents_total,counter,Number of times the directory getdents operation was performed for a filesystem.
node_xfs_directory_operation_lookup_total,counter,Number of file name directory lookups which miss the operating systems directory name lookup cache.
node_xfs_directory_operation_remove_total,counter,Number of times an existing directory entry was created for a filesystem.
node_xfs_extent_allocation_blocks_allocated_total,counter,Number of blocks allocated for a filesystem.
node_xfs_extent_allocation_blocks_freed_total,counter,Number of blocks freed for a filesystem.
node_xfs_extent_allocation_extents_allocated_total,counter,Number of extents allocated for a filesystem.
node_xfs_extent_allocation_extents_freed_total,counter,Number of extents freed for a filesystem.
node_xfs_read_calls_total,counter,Number of read(2) system calls made to files in a filesystem.
node_xfs_vnode_active_total,counter,Number of vnodes not on free lists for a filesystem.
node_xfs_vnode_allocate_total,counter,Number of times vn_alloc called for a filesystem.
node_xfs_vnode_get_total,counter,Number of times vn_get called for a filesystem.
node_xfs_vnode_hold_total,counter,Number of times vn_hold called for a filesystem.
node_xfs_vnode_reclaim_total,counter,Number of times vn_reclaim called for a filesystem.
node_xfs_vnode_release_total,counter,Number of times vn_rele called for a filesystem.
node_xfs_vnode_remove_total,counter,Number of times vn_remove called for a filesystem.
node_xfs_write_calls_total,counter,Number of write(2) system calls made to files in a filesystem.
```