If lower_case_table_names has not been set explicitly, the server sets lower_case_table_names to 2 automatically if filenames are not case sensitive on the filesystem that contains the data directory. Setting lower_case_table_names to a non-zero value also causes table aliases not to be case sensitive.

+   max_allowed_packet (startup; set directly; runtime; global, session)

The maximum size of the buffer used for communication between the server and the client. The buffer is initially allocated to be net_buffer_length bytes long but may grow up to max_allowed_packet bytes as necessary. The value also constrains the maximum size of strings handled within the server. The default and maximum values for max_allowed_packet are 1MB and 1GB, respectively.

+   max_binlog_cache_size (startup; set directly; runtime; global)

The maximum binary log cache size. Statements that make up a transaction are stored in the binary log cache and then written to the binary log at commit time. If the transaction exceeds this size, it must be flushed to a temporary disk file.

+   max_binlog_size (startup; set directly; runtime; global)

The maximum size of a binary log file. If the current binary log file reaches this size, the server closes it and begins the next one. The allowable range of values is 4KB to 1GB. The default is 1GB.

max_binlog_size also controls the size of slave server relay log files if max_relay_log_size is set to 0.

+   max_connect_errors (startup; set directly; runtime; global)

The number of failed connections from a host that are allowed before the host is blocked from further connection attempts. This is done on the basis that someone may be attempting to break in from that host. The FLUSH HOSTS statement or mysqladmin flush-hosts command may be used to clear the host cache to re-enable blocked hosts.

+   max_connections (startup; set directly; runtime; global)

The maximum number of simultaneous client connections allowed. The default is 151 as of MySQL 5.1.15 and 100 for older versions.

+   max_delayed_threads (startup; set directly; runtime; global, session)

The maximum number of threads that will be created to handle INSERT DELAYED statements. Any such statements that are received while the maximum number of handlers is already in use will be treated as non-DELAYED statements. A client can set the session value to 0 to disable DELAYED inserts for its own connection.

+   max_error_count (startup; set directly; runtime; global, session)

The maximum number of error, warning, and note messages to be stored. (Such events are always counted; this variable controls only how many of the associated messages are stored and available to SHOW ERRORS and SHOW WARNINGS.)