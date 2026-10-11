+   ▪ Include your database backup files in your regular filesystem backups. If you have a complete crash that wipes out not only your data directory but also the disk drive containing your database backups, you’ll be in real trouble. Back up your log files, too.

+   ▪ Expire your backup files periodically to keep them from filling your disk. One way to do this is to use file rotation techniques. Section 12.5.7, “Log Management,” discusses these techniques in relation to log files, but the same principles apply to backup file expiration as well.

The sections immediately following describe several specific backup methods. If you are using replication, Section 14.8.4, “Using a Replication Slave for Making Backups,” describes a method that leaves your master server completely undisturbed.

# 14.4.1 Making Text Backups with mysqldump

The mysqldump program creates text dump files. By default, it writes a dump file in SQL format consisting of CREATE TABLE statements that create the tables being dumped and INSERT statements containing the data for the rows in the tables. To re-create the dumped tables later, reload the dump file into MySQL by using it as input to mysql. For example, to dump and reload a single table (sampdb.member), use these commands:

```
```
$ mysqldump sampdb member > member.sql
$ mysql sampdb < member.sql
```
```

Don’t use mysqlimport to reload SQL-format mysqldump output. mysqlimport expects to read rows of data, not SQL statements.

To back up all tables from all databases into a single file, you can use a command like this:

```
```
$ mysqldump --all-databases > /archive/mysql/mysql-dump-2008-01-02
```
```

However, the result is a rather large dump file if you have a lot of data. You can dump each single database into its own file as follows:

```
```
$ mysqldump mysql > /archive/mysql/mysql.2008-01-02
$ mysqldump sampdb > /archive/mysql/sampdb.2008-01-02
$
... 
```
```

The beginning of a mysqldump output file looks something like this:

```
```
-- MySQL Dump 10.11
--
-- Host: localhost   Database: sampdb
-- ------------------------------------------------------
-- Server version   5.0.54-log

... several SET statements ...

--
-- Table structure for table `absence`
-- 
```
```