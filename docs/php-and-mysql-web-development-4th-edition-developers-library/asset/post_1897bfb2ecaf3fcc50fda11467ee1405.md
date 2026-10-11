
For the general query log and the slow-query log, you can select whether the server writes to a log file, to a log table in the mysql database, or both. Section 12.5.6, “Using Log Tables,” describes logging to tables in more detail.

### 11.2.9.1 The Process ID File

The MySQL server writes its process ID (PID) into the PID file when it starts, and removes the file when it shuts down. Other processes can use this file to determine whether the server is running and what its process ID is if so. For example, if the operating system runs the mysql.server script at system shutdown time to stop the MySQL server, that script examines the PID file to determine which process it needs to send a termination signal to.

If the server cannot create the PID file (for example, if you run it to read-only media such as a CD-ROM), it writes a message to the error log and continues.

The PID file is not used by the embedded server, which needs no PID file because it is started and stopped by the application within which it is embedded.

### 11.2.9.2 The MySQL Logs

MySQL can maintain several types of log files. Most logging is optional; you use server startup options to enable just the logs you need and also to specify their names if you don’t like the default names. Be aware that logs can grow quite large, so it’s important to make sure they don’t fill up your filesystem. You can expire the logs periodically to keep the amount of space that they use within bounds.

This section briefly describes a few of the log files. For more information about the logs, the options that control the server’s logging behavior, and log expiration, see Section 12.5, “Maintaining Logs.”

The error log contains a record of diagnostic information produced by the server when exceptional conditions occur. If the server fails to start up or exits unexpectedly, this log is useful because it will often contain the reason why.

The general query log provides general information about server operation: who is connecting from where and what statements they are issuing. The binary log contains statement information, too, but only for statements that modify database contents. It also contains information such as timestamps needed to keep slave servers synchronized when the server is a master server in a replication setup. The contents of the binary log are written in binary format as “events” that can be executed by providing them as input to the mysql client. The accompanying binary log index file lists which binary log files the server currently is maintaining.

The binary log is useful if you have a crash and must revert to backup files, because you can repeat the updates performed after the backup was made by feeding the log files to the server. This enables you to bring your database up to the state they were in when the crash occurred. The binary log is also used if you set up replication servers, because it serves as a record of the updates that must be transmitted from a master server to slave servers. Backup procedures and replication are discussed in more detail in Chapter 14, “Database Maintenance, Backups, and Replication.”

Here is a sample of the kind of information that appears in the general query log as the result of a short client session that creates a table in the test database, inserts a row into the table, and then drops the table:

```
080412 11:38:34    31 Connect    samapd@1m0calhost on sampdb
080412 11:38:42    31 Query    CREATE TABLE mytbl (val INT)
080412 11:38:47    31 Query    INSERT INTO mytbl VALUES(1)
080412 11:38:52    31 Query    DROP TABLE mytbl
080412 11:38:56    31 Quit
```

The general log contains columns for date and time, server thread ID (connection ID), event category, and event-specific information. For any line that is missing the date and time fields, the values are the same as for the previous line that does have them. (In other words, the server logs the date and time only when they change from the previously logged date and time.)

The same session appears in the binary log as follows when viewed by displaying its contents with the mysqlbinlog program. (The output is slightly reformatted to accommodate long lines.) The statements include terminating semicolons, allowing them to be given as input to the mysql program should the updates need to be repeated for a data-base recovery operation. Comment lines begin with ‘#’ characters.

```
# at 1222
#080412 11:38:42 server id 1  log_pos 1222   Query    thread_id=31
exec_time=0     error_code=0
use sampdb;
SET TIMESTAMP=1092328722;
CREATE TABLE mytbl (val INT);
# at 1287
#080412 11:38:47 server id 1  log_pos 1287   Query    thread_id=31
exec_time=0     error_code=0
SET TIMESTAMP=1092328727;
INSERT INTO mytbl VALUES(1);
# at 1351
#080412 11:38:52 server id 1  log_pos 1351   Query    thread_id=31
exec_time=0     error_code=0
SET TIMESTAMP=1092328732;
DROP TABLE mytbl;
```

It’s a good idea to make sure that your log files are secure and not readable by arbitrary users, because they may contain the text of statements that include sensitive information such as passwords. For example, the following log entry displays the password for the root user; it’s certainly not the kind of information you want just anyone to have access to:

```
080412 16:47:24    44 Query    SET PASSWORD FOR
                        ‘root’@‘calhost’=PASSWORD(‘secret’)
```

The server writes log files to the data directory by default, so a good precaution for securing your logs is to secure the data directory against being accessed on the server host by login accounts other than the one used by the MySQL administrator. For details of this procedure, see Section 13.1.2, "Securing Your MySQL Installation."

## 11.2 Structure of the Data Directory

## 11.3 Relocating Data Directory Contents

Earlier parts of this chapter discuss the data directory structure in its default configuration, which is that all databases, status files, and log files are located within it. However, you have some latitude in determining the placement of the data directory's contents. MySQL enables you to relocate the data directory itself or certain elements within it. There are several reasons why you might want to do this:

- The filesystem that contains the data directory has become full and you need to move it to a filesystem with more capacity.
- If your data directory is on a busy disk drive, you can put it on a less active drive to balance disk activity across physical devices. You can put databases and log files on different drives or distribute databases across drives for the same reasons. Similarly, the InnoDB shared tablespace is conceptually a single large block of storage, but you can put its individual component files on different drives to improve performance. If you use partitioned tables, you can do the same with individual table partitions.
- Putting databases on one disk and logs on another disk helps minimize the damage that can be caused by a failure of a single disk.
- You might want to run multiple servers, each with its own data directory. This is one way to work around problems with per-process file descriptor limits, especially if you cannot reconfigure the kernel for your system to enable higher limits.

The rest of this section discusses which parts of the data directory can be moved and how you go about making such changes.

### 11.3.1 Relocation Methods

There are two ways to relocate the data directory or elements within it.

First, on any platform, you can specify an option at server startup, either on the command line or in an option file. For example, to specify the data directory location, start the server with a `--datadir=dir_name` option on the command line or put the following lines in an option file:

```
[mysqld]
datadir=dir_name
```

Typically, the option file group name for server options is `[mysqld]`, as shown in the example. However, depending on your circumstances, other option group names may be more appropriate. For example, the `[embedded]` group applies to the embedded server. If you're running multiple servers using `mysqld_multi`, the group names will be of the
