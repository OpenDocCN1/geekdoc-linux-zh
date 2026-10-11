+   - **Master_Host**
+     The master hostname or IP number.

+   - **Master_User**
+     The username of the account used for connecting to the master.

+   - **Master_Port**
+     The port number for connecting to the master.

+   - **Connect_Retry**
+     The number of seconds to wait between attempts to connect to the master.

+   - **Master_Log_File**
+     The name of the current master binary log file.

+   - **Read_Master_Log_Pos**
+     The current position within the master binary log file where the slave I/O thread is reading.

+   - **Relay_Log_File**
+     The name of the current relay log file.

+   - **Relay_Log_Pos**
+     The current position of the slave SQL thread within the relay log file.

+   - **Relay_Master_Log_File**
+     The name of the master binary log file that contains the event most recently executed by the SQL thread.

+   - **Slave_IO_Running**
+     Whether the slave I/O thread is running.

+   - **Slave_SQL_Running**
+     Whether the slave SQL thread is running.

+   - **Replicate_Do_DB**
+     A comma-separated list of databases that are explicitly replicated with `--replicate-do-db` options, blank if no such options were given.

+   - **Replicate_Ignore_DB**
+     A comma-separated list of databases that are explicitly excluded from replication with `--replicate-ignore-db` options, blank if no such options were given.

+   - **Replicate_Do_Table**
+     A comma-separated list of tables that are explicitly replicated with `--replicate-do-table` options, blank if no such options were given.

+   - **Replicate_Ignore_Table**
+     A comma-separated list of tables that are explicitly excluded from replication with `--replicate-ignore-table` options, blank if no such options were given.