

- **Bytes_sent**
  发送到所有客户端的总字节数。

- **Com_xxx**
  服务器维护了一组状态变量，用作计数器，指示特定类型的语句（命令）已执行的次数。此类变量有几十个，且名称相似，因此此处不逐一列出。每个语句计数器变量名都以 `com_` 开头，并带有后缀以指示该计数器对应的语句类型。例如，`Com_select` 和 `Com_drop_table` 分别指示服务器已执行的 SELECT 和 DROP TABLE 语句的数量。

- **Compression**
  通过客户端/服务器协议发送的流量是否使用压缩。该变量在 MySQL 5.0.16 中引入。

- **Connections**
  尝试连接到服务器的次数（包括成功和未成功的尝试）。

- **Created_tmp_disk_tables**
  服务器在处理语句时创建的磁盘上临时表的数量。

- **Created_tmp_files**
  服务器创建的临时文件数量。

- **Created_tmp_tables**
  服务器在处理语句时创建的内存中临时表的数量。

- **Delayed_errors**
  在处理 INSERT DELAYED 行时发生的错误数。

- **Delayed_insert_threads**
  INSERT DELAYED 处理器的数量。

- **Delayed_writes**
  已写入的 INSERT DELAYED 行数。

- **Flush_commands**
  已执行的 FLUSH 语句的数量。

- **Handler_commit**
  提交事务的请求数。

- **Handler_delete**
  从表中删除一行的请求数。

- **Handler_discover**
  此变量用于 NDBCLUSTER 存储引擎。它指示服务器向 NDB 询问表名并成功找到（发现）该表的次数。

- **Handler_prepare**
  两阶段提交的准备操作数量。该变量在 MySQL 5.0.3 中引入。

- **Handler_read_first**
  从索引读取第一行的请求数。

- **Handler_read_key**
  基于索引值读取一行的请求数。

- **Handler_read_next**
  按索引顺序读取下一行的请求数。

- **Handler_read_prev**
  按索引降序读取上一行的请求数。

- **Handler_read_rnd**
  基于位置读取一行的请求数。

- **Handler_read_rnd_next**
  读取下一行的请求数。如果此数值较高，说明你可能正在执行许多需要全表扫描或没有正确使用索引的语句。

- **Handler_rollback**
  回滚事务的请求数。

- **Handler_savepoint**
  创建事务保存点的请求数。该变量在 MySQL 5.0.3 中引入。

- **Handler_savepoint_rollback**
  回滚到事务保存点的请求数。该变量在 MySQL 5.0.3 中引入。

- **Handler_update**
  更新表中一行的请求数。

- **Handler_write**
  向表中插入一行的请求数。

- **InnoDb_xxx**
  参见第 D.3.1 节，“InnoDB 状态变量”。

- **Key_blocks_not_flushed**
  键缓存中已被修改但尚未刷新到磁盘的块数。

- **Key_blocks_unused**
  键缓存中未使用的块数。

- **Key_blocks_used**
  键缓存中曾经同时使用的最大块数。

- **Key_read_requests**
  从键缓存读取块的请求数。

- **Key_reads**
  从磁盘读取索引块的数量。

- **Key_write_requests**
  向键缓存写入块的请求数。

- **Key_writes**
  向磁盘写入索引块的数量。

- **Last_query_cost**
  查询优化器最近一次查询成本计算结果。该值仅对不使用 UNION 或子查询的查询有用。如果尚未计算查询成本，值为 0；在 MySQL 5.0.7 之前为 -1。从 5.0.16 开始，对于使用查询缓存服务的查询，该值会被设置。该变量在 MySQL 5.0.1 中引入。

- **Max_used_connections**
  曾经同时打开的最大连接数。

- **Not_flushed_delayed_rows**
  等待写入的 INSERT DELAYED 语句的行数。

- **Open_files**
  打开的文件数量。

- **Open_streams**
  打开的流数量。流是指通过 fopen() 打开的文件；这仅适用于日志文件。

- **Open_table_definitions**
  缓存的 .frm 文件数量。该变量在 MySQL 5.1.3 中引入。

- **Open_tables**
  打开的表数量。这不包括 TEMPORARY 表。

- **Opened_files**
  服务器已打开的文件总数。（某些存储引擎可能不会增加此计数器。）该变量在 MySQL 5.1.21 中引入。

- **Opened_tables**
  服务器已打开的表总数。如果此数值较高，最好考虑增加表缓存大小。

- **Prepared_stmt_count**
  预编译语句的数量。该变量在 MySQL 5.0.21/5.1.10 中作为 prepared_stmt_count 系统变量引入，并在 5.0.32/5.1.11 中转换为 Prepared_stmt_count 状态变量。

- **Qcache_xxx**
  参见第 D.3.2 节，“查询缓存状态变量”。

- **Questions**
  服务器接收的语句数量（包括成功和未成功的语句）。Questions 与 Uptime 的比率得出每秒语句数。

- **Rpl_status**
  此变量未使用。

- **Select_full_join**
  “全”连接的数量；即未使用索引进行的连接。

- **Select_full_range_join**
  使用参考表上的范围搜索进行的连接数量。

- **Select_range**
  使用第一表上的范围进行的连接数量。

- **Select_range_check**
  必须使用范围搜索来获取二级表上的行而进行的连接数量。

- **Select_scan**
  使用第一表全扫描进行的连接数量。

- **Slave_open_temp_tables**
  从服务器 SQL 线程打开的临时表数量。

- **Slave_retried_transactions**
  从服务器 SQL 线程重试事务的次数。该变量在 MySQL 5.0.4 中引入。

- **Slave_running**
  从服务器的 I/O 线程和 SQL 线程是否都在运行。

- **Slow_launch_threads**
  创建耗时超过 `slow_launch_time` 秒的线程数量。

- **Slow_queries**
  执行耗时超过 `long_query_time` 秒的查询数量。

- **Sort_merge_passes**
  排序算法执行的合并通道次数。

- **Sort_range**
  使用范围执行的排序操作数量。

- **Sort_rows**
  已排序的行数。

- **Sort_scan**
  使用全表扫描执行的排序操作数量。

- **Ssl_xxx**
  参见第 D.3.3 节，“SSL 状态变量”。

- **Table_locks_immediate**
  可以立即满足而无需等待的表锁定请求数。

- **Table_locks_waited**
  仅能通过等待才能满足的表锁定请求数。如果此值较高，说明你对表锁存在大量竞争。

- **Tc_log_max_pages_used**
  用于事务协调器恢复日志文件的最大页数。该变量在 MySQL 5.0.3 中引入。

- **Tc_log_page_size**
  事务协调器恢复日志文件的页大小。该变量在 MySQL 5.0.3 中引入。

- **Tc_log_page_waits**
  两阶段提交必须等待事务协调器恢复日志文件中空闲页的次数。该变量在 MySQL 5.0.3 中引入。

- **Threads_cached**
  线程缓存中的线程数量。

- **Threads_connected**
  打开的连接数。

