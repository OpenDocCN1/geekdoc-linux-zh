+   character_set_system
+   The system character set. Its value is always utf8. This is the character set used for metadata such as database, table, and column names. It is also used for functions such as DATABASE(), CURRENT_USER(), USER(), and VERSION().

+   character_sets_dir (startup: set directly)
+   The directory where character set files are located.

+   collation_connection (runtime: global, session)
+   The connection character set collation.

+   collation_database
+   The database character set collation, if there is one. If there is no default database (for example, if the client connects without selecting one), this variable is set to the value of collation_server. The value of collation_database is set by the server each time you select a different database.

+   collation_server (startup: set directly; runtime: global, session)
+   The server character set collation.

+   completion_type (startup: set directly; runtime: global, session)
+   The completion type for transactions. A value of 0 (the default) leaves COMMIT and ROLLBACK unaffected. A value of 1 causes them to be equivalent to COMMIT AND CHAIN and ROLLBACK AND CHAIN. A value of 1 causes them to be equivalent to COMMIT RELEASE and ROLLBACK RELEASE. With AND CHAIN, when a transaction completes, the server starts a new one with the same isolation level. With AND RELEASE, when a transaction completes, the server terminates the connection. This variable was introduced in MySQL 5.0.3.

+   concurrent_insert (startup: set directly; runtime: global)
+   Whether the server allows INSERT statements on a MyISAM table that has no holes in the middle of the data file concurrently with active SELECT statements for the table. Values of 0 or 1 disable or enable this feature. A value of 2 (allowable as of MySQL 5.0.6) enables concurrent inserts for MyISAM tables regardless of whether they have with holes in the data file; if so, new rows are added to the end of the table if it is in use. This variable has a value of 1 by default, but can be disabled at startup by setting it directly or by using the --skip-concurrent-insert option.

+   connect_timeout (startup: set directly; runtime: global)
+   The number of seconds that mysqld waits for packets during the initial connection handshake. The default is 10 as of MySQL 5.0.52/5.1.23 and 5 for older versions.

+   datadir (startup: set directly)
+   The pathname to the MySQL data directory.

+   date_format
+   This variable is unused.