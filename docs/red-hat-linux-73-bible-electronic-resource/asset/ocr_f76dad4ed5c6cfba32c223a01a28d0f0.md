| Variable | current value: |
| :--- | :--- |
| bdb_lock_max | 10000 |
| binlog_cache_size | 32768 |
| connect_timeout | 5 |
| delayed_insert_timeout | 300 |
| delayed_insert_limit | 100 |
| delayed_queue_size | 1000 |
| flush_time | 0 |
| interactive_timeout | 28800 |
| join_buffer_size | 131072 |
| key_buffer_size | 8388600 |
| long_query_time | 10 |
| lower_case_table_names | 0 |
| max_allowed_packet | 1048576 |
| max_binlog_cache_size | 4294967295 |
| max_binlog_size | 1073741824 |
| max_connections | 100 |
| max_connect_errors | 10 |
| max_delayed_threads | 20 |
| max_heap_table_size | 16777216 |
| max_join_size | 4294967295 |
| max_sort_length | 1024 |
| max_tmp_tables | 32 |
| max_user_connections | 0 |
| max_write_lock_count | 4294967295 |
| myisam_sort_buffer_size | 8388608 |
| net_buffer_length | 16384 |
| net_retry_count | 10 |
| net_read_timeout | 30 |
| net_write_timeout | 60 |
| open_files_limit | 0 |
| query_buffer_size | 0 |
| record_buffer | 131072 |
| slow_launch_time | 2 |
| sort_buffer | 2097144 |
| table_cache | 64 |
| thread_concurrency | 10 |
| thread_cache_size | 0 |
| tmp_table_size | 1048576 |
| thread_stack | 65536 |
| wait_timeout | 28800 |

After the server is started, you can see the values that are actually in use by running the mysqladmin command with the variables option. (Pipe the output to the less command so you can page through the information.) Here is an example:

```
# mysqladmin variables | less
+-------------------------------------------+
| Variable_name                 | Value   |
```