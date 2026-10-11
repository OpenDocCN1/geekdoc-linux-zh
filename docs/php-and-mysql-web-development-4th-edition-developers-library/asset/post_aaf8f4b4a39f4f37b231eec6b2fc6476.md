
## F.9 mysqladmin 命令参考 (续)

- `flush-status`  
Clears the status variables. (This resets several counters to zero.) This command is like the `FLUSH STATUS` statement.

- `flush-tables`  
Flushes the table cache. This command is like the `FLUSH TABLES` statement.

- `flush-threads`  
Flushes the thread cache.

- `kill id,id,...`  
Kills the server threads specified by the given identifier numbers. If you specify multiple numbers, the ID list should contain no spaces so that it will not be confused for another command following the `kill` command. To find out what threads are currently running, use `mysqladmin processlist`. This command is like issuing a `KILL` statement for each thread ID.

- `old-password new_password`  
This command is like the `password` command except that it causes the password to be stored in the password-hashing format used prior to MySQL 4.1.

- `password new_password`  
Changes the password for the account that the server authenticates you as when you connect. (Being able to connect to the server using this account serves as verification that you know the current password.) The password will be set to `new_password`. This command is like the `SET PASSWORD` statement.  
On Unix, you can use either single quotes or double quotes in the `mysqladmin` command to quote the password if it contains characters that your command interpreter considers special. On Windows, you should use only double quotes. Windows command interpreters do not recognize single quotes as argument-quoting characters. If you use any single quotes, they become part of your password!

- `ping`  
Checks whether the MySQL server is running.

- `processlist`  
Displays a list of the currently executing server activity. This command is like the `SHOW PROCESSLIST` statement. With the `-verbose` option, this command is like `SHOW FULL PROCESSLIST`.

- `refresh`  
This command flushes the table cache and the grant tables, and closes and reopens the log files. If the server is a replication master server, the command tells it to delete the binary log files listed in the binary log index file and to truncate the index. If the server is a slave server, the command tells it to forget its position in the master binary log.

- `reload`  
Reloads the grant tables. This command is like the `FLUSH PRIVILEGES` statement.

- `shutdown`  
Shuts down the server.

- `start-slave`  
Starts a replication slave server. This command is like the `START SLAVE` statement.

- `status`  
Displays a short status message from the server.

- `stop-slave`  
Stops a replication slave server. This command is like the `STOP SLAVE` statement.

- `variables`  
Displays the names and values of the server's variables. This command is like the `SHOW GLOBAL VARIABLES`. (There is no support for `SHOW SESSION VARIABLES` because that wouldn't make any sense.)

- `version`  
Retrieves and displays the server version information string. This is the same information that is returned by the `VERSION()` SQL function. (See Appendix C, “Operator and Function Reference.”)

## F.10 mysqlbinlog

The `mysqlbinlog` program displays the contents of a binary log file in readable format:

`mysqlbinlog [options] file_name ...`

By default, `mysqlbinlog` reads local log files directly without connecting to a server. It is also possible to connect to a server and ask it to send log files over the connection. See the description for the `--read-from-remote-server` option.

The format of the binary log has changed from time to time. To avoid compatibility problems, you may find it necessary to use a version of `mysqlbinlog` that is at least as recent as your server version.

`mysqlbinlog` also can read relay log files created by replication slave servers because the binary and relay logs have the same format.

### F.10.1 Standard Options Supported by `mysqlbinlog`

- `--character-sets-dir`
- `--debug`
- `--debug-check`
- `--debug-info`
- `--help`
- `--host`
- `--password`
- `--port`
- `--protocol`
- `--socket`
- `--user`
- `--version`

`--character-sets-dir` is available as of MySQL 5.0.3. `--debug-check` and `--debug-info` are available as of MySQL 5.1.21.

### F.10.2 Options Specific to `mysqlbinlog`

- `-base64-output[=value]`  
  Indicates when output should consist of BINLOG statements in base-64-encoded form. This option was introduced in MySQL 5.1.5 as a boolean option. As of 5.1.24, it takes argument values of `auto` (use base-64 only when necessary), `always`, or `never`. The default is `auto` if the option is not given; if given with no argument, the default is `always`.

- `-database=db_name` , `-d db_name`  
  Extracts statements from the log file only for the named database. This option works only when reading local logs.

- `-disable-log-bin` , `-D` (boolean)  
  Includes statements in the output that disable binary logging of the update statements in the log. This prevents the statements from being logged again when they are re-executed.

- `-force-if-open` , `-F` (boolean)  
  Reads binary log files even if they were not closed properly (or are currently in use). This option was introduced in MySQL 5.1.15.

- `-force-read` , `-f` (boolean)  
  This option controls what `mysqlbinlog` does when it reads an event from the binary log that it is unable to recognize. By default, it stops. If this option is enabled, `mysqlbinlog` continues after logging a warning and discarding the event.

- `-hexdump` , `-H` (boolean)  
  Includes a hexadecimal/ASCII event dump in the output. This option was introduced in MySQL 5.0.16.

- `-local-load=dir_name` , `-l dir_name`  
  The directory in which to create temporary data files for processing `LOAD DATA LOCAL` statements.

- `-offset=n` , `-o n`  
  Skips the first n events in the log file.

- `-position=n` , `-j n`  
  This option is deprecated in favor of `-start-position`.

- `--read-from-remote-server` , `-R` (boolean)  
  Reads binary log files by making a network connection to a server and asking it to send the logs over the connection. To do this, use the `--read-from-remote-server` option and give the `--host`, `--password`, `--port`, `--protocol`, `--socket`, and `--user` options as necessary to specify connection parameters. Without `--read-from-remote-server`, those options are ignored.

- `--result-file=file_name` , `-r file_name`  
  Writes output to the named file.

- `--server-id=n`  
  Dumps only events created by the server with this ID. This option was introduced in MySQL 5.1.4.

- `--set-charset=charset`  
  Includes a `SET NAMES` statement in the output. This option was introduced in MySQL 5.0.23/5.1.12.

- `--short-form` , `-s`  
  Shows only the statements that are present in the log; omits any extra information in the log that is associated with the statements and does not show row-based events.

- `--start-datetime=date_time`  
  Starts reading binary log events beginning with the first event that has a time at or later than the given `date_time` value. `date_time` should be specified in a legal DATETIME format in the time zone local to the host on which you run `mysqlbinlog`. Quote the value if necessary for your command interpreter.

- `--start-position=n`  
  Starts reading binary log events at the given position in the first log file named on the command line.

- `--stop-datetime=date_time`  
  Stops reading binary log events beginning with the first event that has a time at or later than the given `date_time` value. `date_time` should be specified in a legal DATETIME format in the time zone local to the host on which you run `mysqlbinlog`. Quote the value if necessary for your command interpreter.

- `--stop-position=n`  
  Stops reading binary log events at the given position in the last log file named on the command line.

- `--to-last-log` , `-R` (boolean)  
  When reading log files from a server (which requires the `--read-from-remote-server` option), this option causes binary log files to be read through the last log file of the server, rather than at the end of the last requested log file. `--to-last-log`
