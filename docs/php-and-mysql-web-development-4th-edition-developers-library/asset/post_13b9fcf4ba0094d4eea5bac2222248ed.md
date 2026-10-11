
In general, statement-based logging produces smaller log files with contents that are easier to understand. Row-based logging provides finer specification of updates to be made, which is advantageous for replication when the original statements might be non- deterministic and produce different effects on master and slave.

As of MySQL 5.1, the logging format is selected by using the --binlog-format option at startup or (as of 5.1.8) by setting the global binlog_format system variable at runtime. The default format as of 5.1.12 is MIXED. Other values are STATEMENT or ROW to force a given format.

### 14.8.4 Using a Replication Slave for Making Backups

If you have a replication slave server set up, it can help you resolve a conflict of interest that arises from your duties as a MySQL administrator:

- On the one hand, it's important to maximize the availability of your server to the members of your user community, which includes allowing them to make database updates.
- On the other hand, it's important to make backups, which is best done while you prevent anyone from making database changes. Also, for recovery purposes, backups are most useful if you make sure your backup file and log file checkpoints are synchronized, either by stopping the server or by locking all the tables at once.

The goal of maintaining accessibility conflicts with enforcing complete or partial loss of database access to clients while making backups. A replication slave provides a way out of this dilemma. Rather than making backups of the master server, use the slave server instead. Stop the slave or suspend replication on it before you make the backup. Then restart the slave or resume replication afterward, and the slave will catch up on any updates made by the master server during the backup period. This way you need not stop the master or otherwise make it unavailable to clients during the backup.

The following list describes some possible strategies for backing up the slave:

- For a binary backup of all slave data, stop the slave server, follow the instructions in Section 14.4.2.1, "Making a Complete Binary Backup", and restart the server.
- For a backup using a method such as mysqldump that does not require the slave to be stopped, you can back up the slave while the SQL thread is stopped, and then restart the thread after making the backup: Suspend replication on the slave with STOP SLAVE SQL_THREAD and flush its logs. Then make the backup and resume replication with START SLAVE. This way the slave won't make changes to databases while you're backing them up. The I/O thread can be left running; it will continue to write events to the relay log that it receives from the master. When you restart the SQL thread after making the backup, it catches up with any accumulated updates.

This approach assumes that clients do not make updates on the slave server. You should also not use this method if you intend to use a binary backup method that copies database files directly. Even though the SQL thread is stopped, there might be information cached in memory that has not been flushed to disk.

- Some backup methods do not require even that you suspend replication. For example, if you're backing up a single database containing only MyISAM tables, you can use mysqlhotcopy or mysqldump with the appropriate options to lock all the tables at once. In these cases, the slave server can continue to run, but it won't attempt any updates to the locked tables during the backup. When the backup program finishes and releases the locks, the slave resumes update processing automatically.

## A

### Obtaining and Installing Software

This appendix describes how to obtain the sampdb distribution that is used for setting up the sample database that serves for examples throughout this book. To use the distribution, you’ll also need to have MySQL running. To that end, the appendix also discusses how to obtain and install MySQL and related software such as the Perl DBI and CGI.pm modules, PHP, and Apache. It provides information for both Unix and Windows.

The purpose of this appendix is to bring together in one place summary installation instructions for each of the packages that are discussed here, not to replace the instructions that come with the packages. In fact, I encourage you to read the package instructions. This appendix provides general information that should suffice for many situations, but each package also contains instructions to help you troubleshoot problems when a standard installation procedure fails. For example, the MySQL manual contains a chapter that deals extensively with installation procedures and includes solutions for many operating system-specific problems.

### A.1 Obtaining the sampdb Sample Database Distribution

The sampdb distribution is available at `http://www.kitebird.com/mysql-book/` and contains the files that are used to set up and access the sampdb sample database. The distribution is available in compressed `tar` file and `Zip` archive formats. To unpack a distribution in `tar` format, use one of these commands (use the second command if your version of `tar` doesn’t understand the `z` option):

```
% tar zxf sampdb.tar.gz
% gunzip < sampdb.tar.gz | tar xf -
```

To unpack a `Zip`-format distribution, use a utility such as `WinZip`, `pkunzip`, or `unzip`.

When you unpack the distribution, it will create a directory named sampdb containing several files and subdirectories:

- A `README.txt` file containing additional general instructions for using the distribution. This is the first file you should look at. Individual subdirectories of the distribution may also contain a `README.txt` file with more information.
- Files for creating and loading the `sampdb` database. These are used in Chapter 1, “Getting Started with MySQL.”
- A `capi` directory containing the C programs used in Chapter 7, “Writing MySQL Programs Using C”
- A `perlapi` directory containing the Perl DBI scripts used in Chapter 8, “Writing MySQL Programs Using Perl DBI”
- A `phpapi` directory containing the PHP scripts used in Chapter 9, “Writing MySQL Programs Using PHP”
- An `ssl` directory containing certificate and key files for setting up SSL connections between MySQL client programs and the server.

The `sampdb` directory also includes a few other directories containing files that are referenced at various other points in this book. Check the `README.txt` file for further information.

### A.2 Obtaining MySQL and Related Software

To use this book, you must install MySQL if you haven't already done so. For third-party tools, you need install only those that you plan to use:

- To write Perl scripts that access MySQL databases, you must install the DBI and DBD::mysql modules. If you plan to write Web-based DBI scripts, you'll probably want to install the CGI.pm module as well, and you'll need a Web server. The Apache server is used in this book, but others may work, too.
- If you want to write PHP scripts as described in this book, you must install PHP and also the PHP Data Objects (PDO) database-access extension. Normally, PHP is used for Web scripting, which means you also need a Web server. The Apache server is used in this book for PHP scripts.

Precompiled binaries are available for many of the installation packages. For example, RPM packages are available for Linux. If you prefer to compile software from source, or if a binary distribution isn't available for your platform, you'll need a C compiler (C++ for MySQL).

If you have an account with an Internet service provider that offers MySQL services, it's very likely that all these packages have been installed already. In that case, you can go ahead and use them and skip the rest of this appendix. Otherwise, the primary distribution points for each of the packages you'll need are shown in the following table. Several
