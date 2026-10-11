
- **binlog_cache_size** (startup: set directly; runtime: global)
  The size of the cache that is used to store SQL statements that are part of a transaction before they are flushed to the binary log. (This occurs only if the transaction is committed or includes statements that update non-transactional tables. If the transaction updates only transactional tables and is rolled back, the statements are discarded.)

- **binlog_format** (startup: set directly; runtime: global)
  The binary logging format. Values can be STATEMENT, ROW, or (as of 5.1.8) MIXED, for statement-based, row-based, or mixed logging format. With mixed format, the server switches between statement- and row-based logging automatically. The default value as of 5.1.12 is MIXED. This variable was introduced in MySQL 5.1.5 and can be set at runtime as of 5.1.8.

- **bulk_insert_buffer_size** (startup: set directly; runtime: global, session)
  The size of the cache used to help optimize bulk inserts into MyISAM tables. This includes LOAD DATA statements, multiple-row INSERT statements, and INSERT INTO ... SELECT statements. Setting the value to zero disables the optimization.

- **character_set_client** (runtime: global, session)
  The character set of statements sent by the client to the server.

- **character_set_connection** (runtime: global, session)
  The character set of the client-server connection. This is used to interpret string literals (except those that begin with an introducer) and for the character set of strings that result from number-to-string conversions.

- **character_set_database**
  The character set of the default database, if there is one. If there is no default database (for example, if the client connects without selecting a database), this variable is set to the value of character_set_server. The value of character_set_database is set by the server each time you select a different database.

- **character_set_filesystem** (startup: set directly; runtime: global, session)
  The filesystem character set, used to evaluate string literals that indicate filenames, such as the data file in LOAD DATA statements. The server converts the filename from the character set named by character_set_client to that named by character_set_filesystem before accessing the file. The default value is binary (no conversion). This variable was introduced in MySQL 5.0.19/5.1.6.

- **character_set_results** (runtime: global, session)
  The character set of query results sent by the server to the client.

- **character_set_server** (startup: set directly; runtime: global, session)
  The server’s default character set.

- **character_set_system**
  The system character set. Its value is always utf8. This is the character set used for metadata such as database, table, and column names. It is also used for functions such as DATABASE(), CURRENT_USER(), USER(), and VERSION().

- **character_sets_dir** (startup: set directly)
  The directory where character set files are located.

- **collation_connection** (runtime: global, session)
  The connection character set collation.

- **collation_database**
  The database character set collation, if there is one. If there is no default database (for example, if the client connects without selecting one), this variable is set to the value of collation_server. The value of collation_database is set by the server each time you select a different database.

- **collation_server** (startup: set directly; runtime: global, session)
  The server character set collation.

- **completion_type** (startup: set directly; runtime: global, session)
  The completion type for transactions. A value of 0 (the default) leaves COMMIT and ROLLBACK unaffected. A value of 1 causes them to be equivalent to COMMIT AND CHAIN and ROLLBACK AND CHAIN. A value of 1 causes them to be equivalent to COMMIT RELEASE and ROLLBACK RELEASE. With AND CHAIN, when a transaction completes, the server starts a new one with the same isolation level. With AND RELEASE, when a transaction completes, the server terminates the connection. This variable was introduced in MySQL 5.0.3.

- **concurrent_insert** (startup: set directly; runtime: global)
  Whether the server allows INSERT statements on a MyISAM table that has no holes in the middle of the data file concurrently with active SELECT statements for the table. Values of 0 or 1 disable or enable this feature. A value of 2 (allowable as of MySQL 5.0.6) enables concurrent inserts for MyISAM tables regardless of whether they have with holes in the data file; if so, new rows are added to the end of the table if it is in use. This variable has a value of 1 by default, but can be disabled at startup by setting it directly or by using the --skip-concurrent-insert option.

- **connect_timeout** (startup: set directly; runtime: global)
  The number of seconds that mysqld waits for packets during the initial connection handshake. The default is 10 as of MySQL 5.0.52/5.1.23 and 5 for older versions.

- **datadir** (startup: set directly)
  The pathname to the MySQL data directory.

- **date_format**
  This variable is unused.

- **datetime_format**
  This variable is unused.

- **default_week_format** (startup; set directly; runtime: global, session)
  This variable indicates the default mode value to use when the WEEK() or YEARWEEK() function is invoked without the optional mode argument.

- **delay_key_write** (startup; set directly; runtime: global)
  Whether the server respects delayed key writes for MyISAM tables that are created with the DELAY_KEY_WRITE option. This variable can have three values:

- ON (the default value) tells the server to honor the DELAY_KEY_WRITE option for tables defined with that option: Key writes are delayed for tables defined with DELAY_KEY_WRITE=1, but not for tables defined with DELAY_KEY_WRITE=0.
- OFF means that key writes are never delayed for any table, no matter how it was defined.
- ALL forces key writes always to be delayed for every table, no matter how it was defined.

- **delayed_insert_limit** (startup; set directly; runtime: global)
  The number of rows from INSERT DELAYED statements that the delayed-row handler for a table will insert before checking whether any new SELECT statements for the table have arrived. If any have arrived, the handler suspends the insert operation to enable retrievals to execute.

- **delayed_insert_timeout** (startup; set directly; runtime: global)
  When a handler for INSERT DELAYED operations finishes inserting queued rows, it waits this many seconds to see whether any new INSERT DELAYED rows arrive. If so, it handles them; otherwise, it terminates.

- **delayed_queue_size** (startup; set directly; runtime: global)
  The number of rows that may be queued per table for INSERT DELAYED statements. If the queue is full, further INSERT DELAYED statements for the table block until there is room in the queue.

- **div_precision_increment** (startup; set directly; runtime: global, session)
  For division of two exact-value numbers performed with the / operator, this variable indicates how many digits of scale to add. For example, 1.7 is 1.4285 or .1428571 when div_precision_increment has a value of 4 or 6, respectively. The value can range from 0 to 30 and has a default of 4. This variable was introduced in MySQL 5.0.6.

- **event_scheduler** (startup; set directly)
  The status of the event scheduler. Values can be OFF, ON, or DISABLED. If the event scheduler is set to DISABLED at startup, its status cannot be changed at runtime. If the scheduler is set to either `OFF` or `ON` at startup, its status can be changed between those two values at runtime. This variable was introduced in MySQL 5.1.6.

- **expire_logs_days** (startup: set directly; runtime: global)
  If set to a value other than the default of 0, the server automatically removes binary log files older than this many days and updates the binary log index file. Expiration is checked when the server starts up and when it opens a new binary log file.

- **flush** (startup: use `--flush`; runtime: global)
  A value of `ON` or `OFF` indicates whether the server flushes tables after each update. The default is `OFF`; use the `--flush` option on the command line to enable flushing after updates.

- **flush_time** (startup: set directly; runtime: global)
  If this variable has a non-zero value, tables are closed to flush pending changes to disk every `flush_time` seconds. If your system is unreliable and tends to lock up or restart often, forcing out table changes this way degrades performance but can reduce the chance of table corruption or data loss. The default value is 0 for Unix and 1800 (30 minutes) for Windows.

- **ft_boolean_syntax** (startup: set directly; runtime: global)
  The list of operators that are supported for `FULLTEXT` searches that use `IN BOOLEAN MODE`.

- **ft_max_word_len** (startup: set directly)
  The maximum length of words that can be included in `FULLTEXT` indexes. Longer words are ignored. If you change the value of this variable, you should rebuild the `FULLTEXT` indexes for any tables that have them. The default value is 84.

- **ft_min_word_len** (startup: set directly)
  The minimum length of words that can be included in `FULLTEXT` indexes. Shorter words are ignored. If you change the value of this variable, you should rebuild the `FULLTEXT` indexes for any tables that have them. The default value is 4.

- **ft_query_expansion_limit** (startup: set directly)
  This variable is used for full-text searches that are done using the `WITH QUERY EXPANSION` clause. It determines the number of “top matches” to use for the second phase of each search.

- **ft_stopword_file** (startup: set directly)
  The stopword file for `FULLTEXT` indexes. The default is to use the built-in list of stopwords. To disable stopwords, set the value to the empty string. If you change the value of this variable or the contents of the stopword list, you should rebuild the `FULLTEXT` indexes for any tables that have them.
