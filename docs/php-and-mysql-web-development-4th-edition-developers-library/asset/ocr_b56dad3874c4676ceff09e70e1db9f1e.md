# F.9.3 Variables for mysqladmin

The following mysqladmin variables can be set using the instructions given in Section F.2.1.2, "Setting Program Variables." 

+   - connect_timeout
+   The number of seconds to wait before timing out when attempting to connect to the server.The default value is 43,200.

+   - shutdown_timeout
+   For shutdown commands, the number of seconds to wait for a successful shutdown. The default value is 3,600.

# F.9.4 mysqladmin Commands

Following any options on the command line, you can specify one or more of the following commands. Each command name can be shortened to a prefix, as long as the prefix is unambiguous. For example, processlist can be shortened to process or proc, but not to p.

Several of these commands have an equivalent SQL statement, as noted in the descriptions. See Appendix E, "SQL Syntax Reference," for more information about the meaning of these statements.

+   - create db_name
+   Creates a new database with the given name.This command is like the CREATE DATABASE db_name statement.

+   - debug
+   Instructs the server to dump debugging information to the error log.

+   - drop db_name
+   Removes the database with the given name, and any tables that may be in the database. mysqladmin asks for confirmation of this command unless the --force option was given.This command is like the DROP DATABASE db_name statement.

+   - extended-status
+   Displays the names and values of the server's status variables. This command is like the SHOW STATUS statement.

+   - flush-hosts
+   Flushes the host cache.This command is like the FLUSH HOSTS statement.

+   - flush-logs
+   Flushes (closes and reopens) the log files.This command is like the FLUSH LOGS statement.

+   - flush-privileges
+   Reloads the grant tables.This command is like the FLUSH PRIVILEGES statement.