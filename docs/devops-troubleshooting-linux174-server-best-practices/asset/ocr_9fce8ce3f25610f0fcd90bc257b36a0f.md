+   * Slow queries
+       The number of queries that have taken more than `long_query_time` seconds
+   * Opens
+       The number of tables the server has opened
+   * Flush tables
+       The number of `flush-s`, `refresh`, and `reload` commands the server has executed
+   * Open tables
+       The number of tables that currently are open
+   * Queries per second avg
+       The average number of queries per second the database receives

For a lot of your database troubleshooting, these values may be enough for you to build a baseline and tell when some number is out of the norm, in particular the threads, slow queries, and queries-per-second metrics. Of course, if you want more in-depth information, you can get that too—via the extended-status command:

```
$ mysqladmin -u root -p extended-status
Enter password:

+------------------------------------+
| Variable_name          | Value    |
+------------------------------------+
| Aborted_clients        | 0        |
| Aborted_connects       | 5        |
| Binlog_cache_disk_use  | 0        |
| Binlog_cache_use       | 0        |
| Bytes_received         | 3264109643 |
| Bytes_sent             | 49337359253 |
| . . .                      |            |
| Threads_cached         | 7        |
| Threads_connected      | 1        |
| Threads_created        | 6575     |
| Threads_running        | 1        |
| Uptime                 | 2683061  |
| Uptime_since_flush_status | 2683061 |
+------------------------------------+
```