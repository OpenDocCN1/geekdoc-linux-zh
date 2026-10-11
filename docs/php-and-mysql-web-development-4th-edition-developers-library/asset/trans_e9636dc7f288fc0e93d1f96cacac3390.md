
Threads_created
为处理客户端连接而创建的线程总数。

Threads_running
处于活动状态（非睡眠状态）的线程数。

Uptime
自服务器启动运行以来经过的秒数。

Uptime_since_flush_status
自最近一次执行 FLUSH STATUS 以来经过的秒数。此变量在 MySQL 5.0.35 中引入。此功能仅适用于 MySQL 社区服务器。

## D.3.1 InnoDB 状态变量

以下变量显示有关 InnoDB 存储引擎运行的信息。其中许多变量可以通过 SHOW ENGINE INNODB STATUS 的输出获取，但在 SHOW STATUS 的输出中解析起来更便捷。这些变量中的大多数是在 MySQL 5.0.2 中引入的；例外情况会特别注明。

- Innodb_buffer_pool_pages_data
  InnoDB 缓冲池中包含数据的页数。这既统计未修改的干净页面，也统计包含已修改数据的脏页面。

- Innodb_buffer_pool_pages_dirty
  InnoDB 缓冲池中包含已修改数据的页数。

- Innodb_buffer_pool_pages_flushed
  已发出刷新请求的 InnoDB 缓冲池页数。

- Innodb_buffer_pool_pages_free
  InnoDB 缓冲池中的空闲页数。

- Innodb_buffer_pool_pages_latched
  InnoDB 缓冲池中正在被读取或写入，或因其他原因无法被刷新和释放以重新使用的页数。

- Innodb_buffer_pool_pages_misc
  InnoDB 缓冲池中为内部操作分配的页数。

- Innodb_buffer_pool_pages_total
  InnoDB 缓冲池中的总页数。

- InnoDB_buffer_pool_read_ahead_rnd
  InnoDB 发起的随机预读次数。当 InnoDB 必须按非顺序读取大表的一部分时，会发生这种情况。

- InnoDB_buffer_pool_read_ahead_seq
  InnoDB 发起的顺序预读次数。当 InnoDB 执行顺序全表扫描时，会发生这种情况。

- InnoDB_buffer_pool_read_requests
  InnoDB 发出的逻辑读请求数。

- InnoDB_buffer_pool_reads
  由于无法从 InnoDB 缓冲池执行逻辑读而执行的单页物理读次数。

- InnoDB_buffer_pool_wait_free
  InnoDB 需要等待向缓冲池写入操作被刷新的次数。写入通常在后台执行，但当需要读取页面或创建新页面而没有可用页面时，InnoDB 必须执行等待。

- InnoDB_buffer_pool_write_requests
  向 InnoDB 缓冲池执行写入的次数。

- InnoDB_data_fsyncs
  InnoDB 执行的数据同步到磁盘操作数。

- InnoDB_data_pending_fsyncs
  待处理的 InnoDB 数据同步到磁盘操作数。

- InnoDB_data_pending_reads
  待处理的 InnoDB 数据读取操作数。

- InnoDB_data_pending_writes
  待处理的 InnoDB 数据写入操作数。

- InnoDB_data_read
  InnoDB 读取的字节数。

- InnoDB_data_reads
  InnoDB 数据读取操作数。

- InnoDB_data_writes
  InnoDB 数据写入操作数。

- InnoDB_data_written
  InnoDB 写入的字节数。

- InnoDB_dblwr_pages_written
  写入 InnoDB 双写缓冲区的页数。

- InnoDB_dblwr_writes
  写入 InnoDB 双写缓冲区的次数。

- InnoDB_log_waits
  InnoDB 需要等待日志缓冲区写入操作被刷新的次数。

- InnoDB_log_write_requests
  写入 InnoDB 日志文件的请求数。

- InnoDB_log_writes
  写入 InnoDB 日志文件的次数。

- InnoDB_os_log_fsyncs
  InnoDB 日志文件的同步到磁盘操作数。

- InnoDB_os_log_pending_fsyncs
  InnoDB 日志文件的待处理同步到磁盘操作数。

- InnoDB_os_log_pending_writes
  InnoDB 日志文件的待处理写入操作数。

- InnoDB_os_log_written
  写入 InnoDB 日志文件的字节数。

- InnoDB_page_size
  InnoDB 使用的编译时确定的页面大小。这可用于将以页面单位计量的测量值转换为字节单位。默认值为 16KB。

- InnoDB_pages_created
  InnoDB 创建的页数。

- InnoDB_pages_read
  InnoDB 读取的页数。

- InnoDB_pages_written
  InnoDB 写入的页数。

- InnoDB_row_lock_current_waits
  InnoDB 正在等待获取的行锁数量。此变量在 MySQL 5.0.3 中引入。

- InnoDB_row_lock_time
  获取 InnoDB 行锁所花费的总时间（以毫秒为单位）。此变量在 MySQL 5.0.3 中引入。

- InnoDB_row_lock_time_avg
  获取一个 InnoDB 行锁所需的平均时间（以毫秒为单位）。此变量在 MySQL 5.0.3 中引入。

- InnoDB_row_lock_time_max
  获取一个 InnoDB 行锁所需的最大时间（以毫秒为单位）。此变量在 MySQL 5.0.3 中引入。

- InnoDB_row_lock_waits
  InnoDB 需要等待获取行锁的次数。此变量在 MySQL 5.0.3 中引入。

- InnoDB_rows_deleted
  从 InnoDB 表中删除的行数。

- InnoDB_rows_inserted
  插入到 InnoDB 表中的行数。

- InnoDB_rows_read
  从 InnoDB 表中读取的行数。

- InnoDB_rows_updated
  在 InnoDB 表中更新的行数。

## D.3.2 查询缓存状态变量

以下变量显示有关查询缓存运行的信息。

- Qcache_free_blocks
  查询缓存中空闲内存块的数量。

- Qcache_free_memory
  查询缓存中的空闲内存量。

- Qcache_hits
  由缓存中持有的查询满足的查询请求数。

- Qcache_inserts
  曾经注册到查询缓存中的查询总数。

- Qcache_lowmem_prunes
  为了给新结果腾出空间而从查询缓存中移除的缓存查询结果数量。

- Qcache_not_cached
  不可缓存或通过使用 SQL_NO_CACHE 关键字抑制缓存的查询数量。

- Qcache_queries_in_cache
  注册在缓存中的查询数量。

- Qcache_total_blocks
  查询缓存中内存块的总数。

## D.3.3 SSL 状态变量

以下变量提供有关 SSL 管理代码的信息。其中许多变量反映当前连接的状态，除非连接实际上是安全的，否则它们将为空。除非实际上已将 SSL 支持编译到服务器中，否则这些变量不可用。

- Ssl_accept_renegotiates
  在服务器模式下启动重新协商的次数。

- Ssl_accepts
  在服务器模式下启动的 SSL/TLS 握手次数。

- Ssl_callback_cache_hits
  在服务器模式下从外部会话缓存成功检索会话的次数。

- Ssl_cipher
  连接的 SSL 密码套件（协议）（如果没有生效的密码套件，则为空）。您可以使用此变量来确定连接是否加密。

- Ssl_cipher_list
  可用的 SSL 密码套件列表。

- Ssl_client_connects
  在客户端模式下启动的 SSL/TLS 握手次数。

- Ssl_connect_renegotiates
  在客户端模式下启动重新协商的次数。

- Ssl_ctx_verify_depth
  SSL 上下文验证深度。

- Ssl_ctx_verify_mode
  SSL 上下文验证模式。

- Ssl_default_timeout
  默认的 SSL 会话超时时间。

- Ssl_finished_accepts
  在服务器模式下成功建立的 SSL/TLS 会话数量。

- Ssl_finished_connects
  在客户端模式下成功建立的 SSL/TLS 会话数量。

- Ssl_session_cache_hits
  在会话缓存中找到的 SSL 会话数量。

- Ssl_session_cache_misses
  未在会话缓存中找到的 SSL 会话数量。

