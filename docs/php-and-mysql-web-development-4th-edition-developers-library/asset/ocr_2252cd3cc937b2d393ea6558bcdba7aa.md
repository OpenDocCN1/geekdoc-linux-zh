the scheduler is set to either `OFF` or `ON` at startup, its status can be changed between those two values at runtime. This variable was introduced in MySQL 5.1.6.

+   expire_logs_days (startup: set directly; runtime: global)

If set to a value other than the default of 0, the server automatically removes binary log files older than this many days and updates the binary log index file. Expiration is checked when the server starts up and when it opens a new binary log file.

+   flush (startup: use `--flush`; runtime: global)

A value of `ON` or `OFF` indicates whether the server flushes tables after each update.  
The default is `OFF`; use the `--flush` option on the command line to enable flushing  
after updates.

+   flush_time (startup: set directly; runtime: global)

If this variable has a non-zero value, tables are closed to flush pending changes to disk every `flush_time` seconds. If your system is unreliable and tends to lock up or restart often, forcing out table changes this way degrades performance but can reduce the chance of table corruption or data loss. The default value is 0 for Unix and 1800 (30 minutes) for Windows.

+   ft_boolean_syntax (startup: set directly; runtime: global)

The list of operators that are supported for `FULLTEXT` searches that use `IN BOOLEAN MODE`.

+   ft_max_word_len (startup: set directly)

The maximum length of words that can be included in `FULLTEXT` indexes. Longer words are ignored. If you change the value of this variable, you should rebuild the `FULLTEXT` indexes for any tables that have them. The default value is 84.

+   ft_min_word_len (startup: set directly)

The minimum length of words that can be included in `FULLTEXT` indexes. Shorter words are ignored. If you change the value of this variable, you should rebuild the `FULLTEXT` indexes for any tables that have them. The default value is 4.

+   ft_query_expansion_limit (startup: set directly)

This variable is used for full-text searches that are done using the `WITH QUERY EXPANSION` clause. It determines the number of “top matches” to use for the second phase of each search.

+   ft_stopword_file (startup: set directly)

The stopword file for `FULLTEXT` indexes. The default is to use the built-in list of stopwords. To disable stopwords, set the value to the empty string. If you change the value of this variable or the contents of the stopword list, you should rebuild the `FULLTEXT` indexes for any tables that have them.