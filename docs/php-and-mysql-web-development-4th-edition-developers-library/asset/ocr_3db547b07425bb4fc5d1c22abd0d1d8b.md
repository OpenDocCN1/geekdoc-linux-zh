+   - `--show-slave-auth-info` (boolean)
+   
+   Causes a master server to display slave server usernames and passwords in the output of the `SHOW SLAVE HOSTS` statement.
+   
+   - `--skip-slave-start`
+   
+   Causes the server not to start the slave threads automatically. They must be started manually by issuing a `START SLAVE` statement.
+   
+   - `--slave-allow-batching` (boolean)
+   
+   Sets the `slave_allow_batching` system variable. This option was introduced in MySQL 5.2.5.
+   
+   - `--slave-load-tmpdir=dir_name`
+   
+   The pathname to the directory used by a slave server for processing `LOAD DATA` statements. If this option is not specified, it defaults to the value of `--tmpdir`.
+   
+   - `--slave-skip-errors=error_list`
+   
+   The list of errors that a slave server should ignore rather than suspending replication if they occur. (However, it's usually better to determine what is causing problems so that you can resolve them rather than using this option to ignore them.) A value of all means all error should be ignored. Otherwise, the value should be a list of one or more error numbers separated by commas.
+   
+   - `--sporadic-binlog-dump-fail` (boolean)
+   
+   This option is used by the MySQL test suite for replication testing.

# F.12.3 Variables for mysqld

To see the full help message that displays the system variable values that mysqld will use by default, use this command:

```plain
% mysqld --verbose --help
```

To see what system variable values the currently executing mysqld is using, use this command:

```plain
% mysqladmin variables
```

You can also check the current system variable values by issuing a SHOW VARIABLES statement. Individual system variables are described in Appendix D. System variable values can be set at startup time using the instructions given in Section F.2.1.2, “Setting Program Variables.” In addition, many system variables can be modified dynamically; for more information, see Section 12.5.1, “Setting and Checking System Variable Values,” and the entry for the SET statement in Appendix E.