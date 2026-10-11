+   - secure_auth (startup: set directly; runtime: global)
+     When set to ON, the server allows connections only for accounts that have the newer password format introduced in MySQL 4.1. When set to OFF, the server also allows connections to accounts that have passwords in the older format. The default is OFF.

+   - secure_file_priv (startup: set directly)
+     When set to a directory pathname, the server permits LOAD DATA and SELECT ... INTO OUTFILE statements and the LOAD_FILE() function only for operations in that directory. The value is empty by default (no such restriction). This variable was introduced in MySQL 5.0.38/5.1.17.

+   - server_id (startup: set directly; runtime: global)
+     The server's replication ID number. If 0, the server is not participating in replication. Otherwise, the value should be an integer from 1 to 2<sup>32</sup>-1. The value must be different from that of any other replication server that you are using.

+   - shared_memory (startup: set directly)
+     If set to ON, the server allows shared-memory connections by clients. The default is OFF. Shared-memory connections are supported only on Windows.

+   - shared_memory_base_name (startup: set directly)
+     The shared-memory name to use for shared-memory connections. The default name is MYSQL (case sensitive)

+   - skip_external_locking (startup: set directly)
+     Whether use of external locking (filesystem locking) is suppressed.

+   - skip_networking (startup: use --skip-networking)
+     OFF to enable TCP/IP connections. ON to disable them. In the latter case, clients can connect from the local host only, using Unix socket connections under Unix or named pipes or shared memory under Windows.

+   - skip_show_database (startup: set directly)
+     When set to OFF (the default), the SHOW DATABASES statement can be used by any user. It displays all databases if the user has the SHOW DATABASES privilege, or those databases for which the user has some privilege otherwise. When set to ON, the SHOW DATABASES statement can be used only by users who have the SHOW DATABASES privilege, and it displays all databases.

+   - slave_allow_batching (startup: set directly; runtime: global)
+     Enable a slave server to batch requests; applies only to MySQL Cluster. This variable was introduced in MySQL 5.2.5.