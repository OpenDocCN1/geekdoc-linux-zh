

- `REAL_AS_FLOAT`
  `REAL` 数据类型将成为 `FLOAT` 的同义词，而不是 `DOUBLE` 的同义词。

- `STRICT_ALL_TABLES`
  启用对所有存储引擎输入数据值的严格检查，以便让 MySQL 拒绝大多数无效值。此模式是在 MySQL 5.0.2 中引入的。使用 `TRADITIONAL` 可以更加严格。

- `STRICT_TRANS_TABLES`
  启用对事务性存储引擎输入数据值的严格检查，以便让 MySQL 拒绝大多数无效值。此外，在可能的情况下（例如对于单行 `INSERT` 语句），也启用对非事务性存储引擎的严格检查。此模式是在 MySQL 5.0.2 中引入的。使用 `TRADITIONAL` 可以更加严格。

下表列出了组合 SQL 模式，并显示了每种模式作为简写所代表的一组模式。

| 组合模式 | 组成模式 |
| :--- | :--- |
| ANSI | `ANSI_QUOTES`, `IGNORE_SPACE`, `PIPES_AS_CONCAT`, `REAL_AS_FLOAT` |
| DB2 | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MAXDB | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_AUTO_CREATE_USER`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MSSQL | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MYSQL323 | `HIGH_NOT_PRECEDENCE`, `NO_FIELD_OPTIONS` |
| MYSQL40 | `HIGH_NOT_PRECEDENCE`, `NO_FIELD_OPTIONS` |
| ORACLE | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_AUTO_CREATE_USER`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| POSTGRESQL | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| TRADITIONAL | `ERROR_FOR_DIVISION_BY_ZERO`, `NO_AUTO_CREATE_USER`, `NO_ZERO_DATE`, `NO_ZERO_IN_DATE`, `STRICT_ALL_TABLES`, `STRICT_TRANS_TABLES` |

在 MySQL 5.0.3 之前，*ANSI* 还包含 *ONLY_FULL_GROUP_BY*。*TRADITIONAL* 模式的命名源于它启用了那些使输入值处理方式类似于拒绝无效数据的传统数据库的模式。它类似于严格模式，但包含几个额外的约束，以实现更严格的检查。*TRADITIONAL* 模式是在 MySQL 5.0.2 中引入的。

- *sql_select_limit* (运行时: 全局, 会话)
  指定从 *SELECT* 语句返回的最大行数。如果语句中存在显式的 *LIMIT* 子句，则优先于此变量。默认值是每张表允许的最大行数。如果修改过该值，将值设为 *DEFAULT* 可恢复此默认值。

  此变量在存储例程中没有效果，或者对于不向客户端返回行的 *SELECT* 操作（如子查询、*INSERT ... SELECT* 和 *CREATE TABLE ... SELECT*）也没有效果。

- *sql_slave_skip_counter* (运行时: 全局)
  如果你拥有 *SUPER* 权限，你可以将此作为 *GLOBAL* 变量设置为 *n* 的值，以指示从属复制服务器跳过其主服务器发送的下一个 *n* 个事件。

- *ssl_xxx* (启动时: 使用 `--ssl-xxx`)
  *ssl_xxx* 变量指示启动时提供给服务器的相应 `--ssl-xxx` 选项的值。（例如，*ssl_ca* 指示 `--ssl-ca` 选项的值。）如果未提供相应选项，则每个变量的值为空字符串。如果不可用 SSL 支持，则这些变量的值为 *NULL*。这些变量是在 MySQL 5.0.23/5.1.11 中引入的。

- *storage_engine* (启动时: 使用 `--default-storage-engine`; 运行时: 全局, 会话)
  对于未指定 *ENGINE = engine_name* 选项或指定了不支持的 *engine_name* 值而创建的表，默认使用的存储引擎。

- *sync_binlog* (启动时: 直接设置; 运行时: 全局)
  当设置为 0（默认值）时，服务器不会将二进制日志刷新到磁盘。当设置为正值 *n* 时，服务器在每次向二进制日志写入 *n* 次后刷新日志。在这种情况下，较低的数值在发生崩溃时提供更高的安全性，但也会更严重地影响性能。

- *sync_frm* (启动时: 直接设置; 运行时: 全局)
  当设置为 0 时，创建非临时表时，服务器不会将 *.frm* 文件刷新到磁盘。默认值是 1，即会刷新该文件。

- *system_time_zone*
  服务器的系统时区。服务器启动时会尝试通过咨询系统来确定该变量的值。你可以设置 *tz* 环境变量或指定 *mysqld_safe* 的 `--timezone` 选项来显式设置该值。

- *table_cache, table_open_cache* (启动时; 直接设置; 运行时: 全局)
  可以同时打开的最大表数。此缓存在线程之间共享。table_cache 是原始变量名，在 MySQL 5.1.3 中更改为 table_open_cache。

- *table_definition_cache* (启动时; 直接设置; 运行时: 全局)
  服务器可以存储在其定义缓存中的表定义（来自 .frm 文件）的数量。此变量是在 MySQL 5.1.3 中引入的。

- *table_lock_wait_timeout* (启动时; 直接设置; 运行时: 全局)
  对于具有打开游标的连接，等待表级锁超时前的秒数。默认值为 50。此变量是在 MySQL 5.0.10 中引入的。

- *table_type* (启动时; 使用 --default-storage-engine; 运行时: 全局, 会话)
  此变量是 storage_engine 的弃用同义词；它在 MySQL 5.2.5 中已被移除。

- *thread_cache_size* (启动时; 直接设置; 运行时: 全局)
  在线程缓存中保持的最大线程数。如果线程缓存未已满，断开连接的客户端的线程会被放入缓存。这使得新的连接可以通过重用缓存中的线程来提供服务，而不是创建新线程，只要线程仍保留在缓存中。当服务器为每个当前连接的客户端使用一个线程时，会使用线程缓存。

- *thread_concurrency* (启动时; 直接设置)
  此变量仅适用于 Solaris。该值传递给 thr_concurrency()，为线程管理器提供关于同时运行多少个线程的提示。

- *thread_handling* (启动时; 直接设置)
  服务器用于处理客户端连接的线程模型。值可以是 one-thread（单个连接线程）、one-pool-per-connection（每个当前连接的客户端一个线程）或（从 MySQL 6.0.4 开始）pool-of-threads（固定大小的线程池，为所有连接的客户端提供服务）。此变量是在 MySQL 5.1.17 中引入的。

- *thread_pool_size* (启动时; 直接设置)
  如果 thread_handling 的值为 pool-of-threads，则用于语句处理线程池的大小。默认值为 20。此变量是在 MySQL 6.0.4 中引入的。

- *thread_stack* (启动时; 直接设置)
  每个线程的栈大小。

- *time_format*
  此变量未被使用。

- *time_zone* (启动时: 使用 `--default-time-zone`; 运行时: 全局, 会话)
  服务器的当前时区。值为 SYSTEM 表示服务器使用 system_time_zone 变量的值。客户端可以修改此变量的会话值以设置其自身连接的时区。

- *timed_mutexes* (启动时: 使用 `--timed-mutexes`; 运行时: 全局)
  是否收集 InnoDB 互斥锁计时信息。此变量是在 MySQL 5.0.3 中引入的。

- *tmp_table_size* (启动时: 直接设置; 运行时: 全局, 会话)
  内部临时表允许的最大字节数。（服务器在处理语句时自动创建的表。）如果临时表超过 max_heap_table_size 和 tmp_table_size 中较小的那个值，服务器会将其从内存中的内部表转换为磁盘上的 MyISAM 表。如果你有充足的内存，此变量的较高值允许服务器在内存中维护较大的临时表，而无需将其转换为磁盘格式。

- *tmpdir* (启动时: 直接设置)
  服务器创建临时文件的目录路径名。选项值可以指定为目录列表，按轮询方式使用。在 Unix 下，用冒号分隔目录名称；在 Windows 或 NetWare 下，用分号分隔。

- *transaction_alloc_block_size* (启动时: 直接设置; 运行时: 全局, 会话)
  为处理作为事务的一部分存储的语句所需的临时内存分配块大小，这些语句在提交时之前写入二进制日志。

- *transaction_prealloc_size* (启动时: 直接设置; 运行时: 全局, 会话)
  为处理作为事务一部分的语句所分配的缓冲区大小。与在 transaction_alloc_block_size 变量控制下分配的块不同，此缓冲区在语句之间不会释放。

- *tx_isolation* (启动时: 使用 `--transaction-isolation`; 运行时: 全局, 会话)
  默认的事务隔离级别。

- *updatable_views_with_limit* (启动时: 直接设置; 运行时: 全局, 会话)
  当设置为 0 或 NO 时，服务器禁止更新（UPDATE 或 DELETE 语句）那些在底层表中不使用主键的视图，即使更新包含一个 LIMIT 1 子句将更新限制为单行。当设置为 1 或 YES（默认值）时，允许更新，并且服务器仅产生一个警告。此变量是在 MySQL 5.0.2 中引入的。

- *version*
  服务器版本。该值由版本号组成，可能后面跟有一个或多个后缀。后缀值列在附录 C“操作符和函数参考”中 VERSION() 函数的描述中。

