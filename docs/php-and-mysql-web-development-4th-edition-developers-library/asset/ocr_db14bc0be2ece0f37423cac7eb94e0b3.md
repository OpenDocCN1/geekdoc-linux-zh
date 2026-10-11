```
DROP TABLE IF EXISTS `absence` ;
CREATE TABLE `absence` {
 `student_id` int(10) unsigned NOT NULL,
 `date` date NOT NULL,
 PRIMARY KEY (`student_id`,`date`),
 CONSTRAINT `absence_ibfk_1` FOREIGN KEY (`student_id`)
 REFERENCES `student` (`student_id`)
} ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

```
--
-- Dumping data for table `absence`
--
LOCK TABLES `absence` WRITE;
/*!40000 ALTER TABLE `absence` DISABLE KEYS */;
INSERT INTO `absence` VALUES (3,'2008-09-03'),(5,'2008-09-03'),
(10,'2008-09-06'),(10,'2008-09-09'),(17,'2008-09-07'),(20,'2008-09-07');
/*!40000 ALTER TABLE `absence` ENABLE KEYS */;
UNLOCK TABLES;
```

The rest of the file consists of more SQL statements such as CREATE TABLE and INSERT.

Dump files often are large, so you'll likely want to do what you can to make them smaller. `mysqldump` has an `--opt` option, which enables several other options that have the effect of optimizing the dump process to generate smaller output. These options also optimize the restore process because the output can be processed more quickly when you reload the dump file later. For example, one effect of `--opt` is to cause `mysqldump` to write multiple-row INSERT statements. These take less space and can be loaded more quickly than the equivalent set of single-row INSERT statements.

The `--opt` option is enabled by default (this has been true since MySQL 4.1), so it need not be specified explicitly. If you want to disable it, use `--skip-opt`.

Another way to reduce the size of a dump file is to compress it. On Windows, you can use WinZip or similar program to compress the dump and produce a file in Zip format. On Unix, you might use `gzip` or `bzip2` instead. You can even compress the backup as you generate it by using a command pipeline:

```
$ mysqldump sampdb | gzip > /archive/mysql/sampdb.2008-01-02.gz
$ mysqldump sampdb | bzip2 > /archive/mysql/sampdb.2008-01-02.bz2
```

If large dump files are difficult to manage, it's possible to dump the contents of individual tables by naming them following the database name on the `mysqldump` command line. `mysqldump` will dump just the named tables rather than all the tables in the database, resulting in smaller, more manageable files. The following example shows how to dump subsets of the `sampdb` tables into separate files:

```
$ mysqldump sampdb member president > hist-league.sql
$ mysqldump sampdb student score grade_event absence > gradebook.sql
```