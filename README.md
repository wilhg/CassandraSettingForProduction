Cassandra Configrure
===
---
> refer the comment in the configure

### Minimal properties 
- `cluster_name` should be set
- `listen_address` should be local ip, but not `localhost`
- `commitlog_directory` (default: /var/lib/cassandra/commitlog) commit log
- `data_file_directories` (default: /var/lib/cassandra/data) SSTable
- `saved_caches_directory` (default: /var/lib/cassandra/saved_caches) where table key and row caches are stored

### Commonly used properties
- `endpoint_snitch`: shall be *GossipingPropertyFileSnitch*
- `seed_provider` - `seeds` 不同的rack需要有一个seed. [check here](http://www.datastax.com/documentation/cassandra/2.0/cassandra/initialize/initializeMultipleDS.html)
- `concurrent_reads`: 16 * number_of_drives
- `concurrent_writes`: 8 * number_of_cpu_cores

### Performance tuning properties
- `commitlog_sync`: periodic(default) or batch
- `concurrent_compactors`: per CPU core
- `commitlog_total_space_in_mb`: tune carefully and in small increments
- `in_memory_compaction_limit_in_mb`: 5% to 10% of the available Java heap size.
- `trickle_fsync`: true(if SSD)

---
[Tuning Java resources](http://www.datastax.com/documentation/cassandra/2.0/cassandra/operations/ops_tune_jvm_c.html)

[Monitoring a Cassandra cluster](http://www.datastax.com/documentation/cassandra/2.0/cassandra/operations/ops_monitoring_c.html)

[Compression♂SSTable](http://www.datastax.com/documentation/cassandra/2.0/cassandra/operations/ops_config_compress_t.html)

[Data caching](http://www.datastax.com/documentation/cassandra/2.0/cassandra/operations/opsDataCachingTOC.html)

#####Tips for efficient cache use
- Store lower-demand data or data with extremely long rows in a table with minimal or no caching.
- Deploy a large number of Cassandra nodes under a relatively light load per node.
- Logically separate heavily-read data into discrete tables.
