
- **log_bin_trust_function_creators** (startup: set directly; runtime: global)  
Creation or alteration of stored functions requires that you have the CREATE ROUTINE or ALTER ROUTINE privilege. However, if binary logging is enabled and log_bin_trust_function_creators is 0 (the default), you must also have the SUPER privilege and declare that the function is deterministic or does not modify data. To turn off these extra requirements, set log_bin_trust_function_creators to 1. This variable was introduced in MySQL 5.0.16. (From MySQL 5.0.6 through 5.0.15, the variable name is log_bin_trust_routine_creators and it also applies to stored procedures.)

- **log_error** (startup: set directly)  
The name of the error log file. If the value is empty, the server writes error output to the terminal.

- **log_output** (startup: use --log-output; runtime: global)  
The current set of output destinations for the general query log and slow-query log, if those logs are enabled. The value is a list of comma-separated destination names. Allowable destinations are TABLE, FILE and NONE. If present, NONE disables logging and takes precedence over any other values. This variable was introduced in MySQL 5.1.6.  
The general_log or slow_query_log system variable can be set at runtime to enable or disable the respective log. The general_log_file or slow_query_log_file system variable can be set at runtime to change the name of the respective log file.

- **log_queries_not_using_indexes** (startup: use --log-queries-not-using-indexes; runtime: global)  
Whether queries that do not use indexes should be logged to the slow-query log. This variable was introduced in MySQL 5.0.23/5.1.11.

- **log_slave_updates** (startup: set directly)  
For updates that a replication slave server receives from its master’s binary log, this variable controls whether the slave logs the updates to its own binary log. By default, slave update logging is disabled but can be enabled to allow a slave to act as a master to another slave in a chained replication configuration.

- **log_slow_queries**  
Whether the slow-query log is enabled. This variable can be set at runtime to enable or disable logging as of MySQL 5.1.23.

- **log_warnings** (startup: set directly; runtime: global, session)  
The logging level for logging non-critical warnings to the error log. A value of 0 disables these warnings and 1 (the default) enables warnings. Values greater than 1 increase the logging level to include information about aborted connections and (as of MySQL 5.2.6) access-denied errors.

- **long_query_time** (startup: set directly; runtime: global, session)  
Any query taking longer than this value in seconds is considered “slow” and causes the slow_queries counter to be incremented. In addition, if the slow-query log is enabled, the query is written to that log. (As of MySQL 5.1.21, slow-query logging also takes min_examined_row_limit into account.)

- The default value is 10. As of MySQL 5.1.21/6.0.4, the value can include a fractional part in microseconds and the minimum value is 0. (Any fractional part is logged only if the log destination is a file and not the mysql.slow_log table.) For older versions, the value must be an integer and the minimum is 1.

- **low_priority_updates** (startup: set directly; runtime: global, session)  
When this variable is set true, updates have lower priority than retrievals, for storage engines that use table-level locking. Statements that modify table contents (DELETE, INSERT, REPLACE, UPDATE) wait until no SELECT is active or pending for the table. SELECT statements that arrive while another is active begin executing immediately rather than waiting for low-priority modification statements. It has the same effect as specifying the LOW_PRIORITY option for statements that support it, such as INSERT and UPDATE. For individual INSERT statements, the HIGH_PRIORITY modifier can be given to cancel the effect of this variable and elevate the insert to normal priority.

sql_low_priority_updates is a deprecated synonym for low_priority_updates.

- **lower_case_file_system**  
This variable indicates the case sensitivity of filenames for the filesystem that contains the data directory. ON means that names are not case sensitive. (Think of ON as meaning that lowercase and uppercase versions of a filename are considered the same.) OFF means that names are case sensitive.

- **lower_case_table_names** (startup: set directly)  
This variable controls how the directory names and filenames corresponding to database and table names are treated when CREATE DATABASE and CREATE TABLE statements are issued. It also controls how name comparisons are performed when executing statements.

- A value of 0 causes names to be created on disk as given in CREATE DATABASE and CREATE TABLE statements. Name comparisons are case sensitive. This is the default on systems that have case-sensitive filenames.

- A value of 1 causes names to be forced to lowercase when databases and tables are created. Name comparisons are not case sensitive.

- A value of 2 causes name lettercase to be preserved, but name comparisons to not be case sensitive. That is, names are created as given in CREATE statements, but not compared in case-sensitive fashion. You should use this value only for file systems that do not have case-sensitive filenames.

If lower_case_table_names has not been set explicitly, the server sets lower_case_table_names to 2 automatically if filenames are not case sensitive on the filesystem that contains the data directory. Setting lower_case_table_names to a non-zero value also causes table aliases not to be case sensitive.

- **max_allowed_packet** (startup; set directly; runtime; global, session)  
The maximum size of the buffer used for communication between the server and the client. The buffer is initially allocated to be net_buffer_length bytes long but may grow up to max_allowed_packet bytes as necessary. The value also constrains the maximum size of strings handled within the server. The default and maximum values for max_allowed_packet are 1MB and 1GB, respectively.

- **max_binlog_cache_size** (startup; set directly; runtime; global)  
The maximum binary log cache size. Statements that make up a transaction are stored in the binary log cache and then written to the binary log at commit time. If the transaction exceeds this size, it must be flushed to a temporary disk file.

- **max_binlog_size** (startup; set directly; runtime; global)  
The maximum size of a binary log file. If the current binary log file reaches this size, the server closes it and begins the next one. The allowable range of values is 4KB to 1GB. The default is 1GB.

max_binlog_size also controls the size of slave server relay log files if max_relay_log_size is set to 0.

- **max_connect_errors** (startup; set directly; runtime; global)  
The number of failed connections from a host that are allowed before the host is blocked from further connection attempts. This is done on the basis that someone may be attempting to break in from that host. The FLUSH HOSTS statement or mysqladmin flush-hosts command may be used to clear the host cache to re-enable blocked hosts.

- **max_connections** (startup; set directly; runtime; global)  
The maximum number of simultaneous client connections allowed. The default is 151 as of MySQL 5.1.15 and 100 for older versions.

- **max_delayed_threads** (startup; set directly; runtime; global, session)  
The maximum number of threads that will be created to handle INSERT DELAYED statements. Any such statements that are received while the maximum number of handlers is already in use will be treated as non-DELAYED statements. A client can set the session value to 0 to disable DELAYED inserts for its own connection.

- **max_error_count** (startup; set directly; runtime; global, session)  
The maximum number of error, warning, and note messages to be stored. (Such events are always counted; this variable controls only how many of the associated messages are stored and available to SHOW ERRORS and SHOW WARNINGS.)
