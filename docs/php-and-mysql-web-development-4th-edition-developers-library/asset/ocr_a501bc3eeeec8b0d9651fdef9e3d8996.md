CREATE TABLE, DROP TABLE, GRANT, and so forth. Binary log contents are written as data modification “events” encoded in binary format. The binary log files are accompanied by an index file that lists which binary log files exist on the server. The binary log has two purposes:

+   It can be used in conjunction with your backups to restore tables after a crash. You can restore databases from your backup files, and then use mysqldbinlog to convert the binary log contents to text statements. Any statements that modified the databases subsequent to the backup can be used as input to mysql to bring databases to the state they were in at the time of the crash.

+   The data modification events stored in the binary log are transmitted to replication slave servers.

+   **The relay log and the relay log index file.** If the server acts as a replication slave, it maintains a relay log that contains a record of data-modification events received from the master that need to be executed. Relay log files have the same format as binary log files, and there is an index file that lists which relay log files exist on the slave.

Of all the logs, the general query log is most useful for monitoring the server, so when you first start using MySQL, I recommend that you enable the general log in addition to whatever other logs you want. After you have gained some experience with MySQL, you may want to turn off the general log to reduce your disk space requirements.

By default, each enabled log is written as a file (or sequence of files) in the data directory. In MySQL 5.1, you have a choice of writing some logs to alternative destinations: The error log can be sent to syslog, and the general and slow-query logs can be written to tables in the mysql database.

The server doesn't create any log unless you ask for it, with these exceptions:

+   On Unix, if you start the server with the mysqld_safe script, that script sets up the error log and tells the server to use it.

+   On Windows, the server creates the error log unless you specify the --console option to send diagnostic information to the console window rather than to a file.

Logs are controlled by specifying startup options for mysqld. Other than the binary and relay logs, these logs are written in text format and can be viewed directly. To display the contents of a binary or relay log file, use the mysqldbinlog utility.

To enable server logging, use the options shown in the following table. If the log filename is optional (as indicated by square brackets) and you don't provide a name, the server uses a default name and writes the log file in the data directory. The server derives the default name for each of the log files from the name of your server host, represented by *HOSTNAME* in the following discussion. If you specify a log name as a relative pathname, the server interprets it relative to the data directory. A full pathname can be specified to place the log in some other directory. The server will create any log file that does not