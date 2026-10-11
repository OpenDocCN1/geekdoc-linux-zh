+   - The InnoDB log files.

+   - The option file in which the shared tablespace configuration is specified.
+      (Make a copy of the option file because you'll want it for reinitializing the shared tablespace should you suffer loss of the current option file.)

To make a binary Falcon backup, the procedure is similar except that you copy the Falcon tablespace and log files (the files with .fts, .fil1, and .fil2 extensions).

# 14.5 Copying Databases to Another Server

Database backups can be used to copy a database from one MySQL server to another. This section describes some methods for performing database transfers. For purpose of this discussion, I assume that the objective is to transfer a database from the server on the local host to a server on the remote host boa.snake.net. However, the two servers could just as well running on the same host. Also, although the following discussion describes how to copy entire databases, you can adapt the techniques for copying individual tables.

The following discussion shows how to use two methods for copying a database to another server. The first makes a backup of the database that results in a file or set of files. You can copy the file to the second server host and load them into the second MySQL server. The second method dumps the database over the network from one server and loads it directly into the other server. This avoids the need for any intermediate files.

# 14.5.1 Copying Databases Using a Backup File

To copy a database using a text backup file, create the file using mysqldump, copy it to the second server host, and load it into the MySQL server there. The following example illustrates how to copy the sampdb database with this procedure:

+   1. Create a dump file:

```
$ mysqldump --databases sampdb > sampdb.sql
```

The --databases option causes mysqldump to add CREATE DATABASE IF EXISTS and USE statements for the sampdb database. That way, when you load the dump file on the remote host, it automatically creates and selects the database so the dumped tables are loaded into that database.

+   2. Copy the dump file to the remote host. The following command uses scp to copy the file to the /tmp directory on boa.snake.net:

```
$ scp sampdb.sql boa.snake.net:/tmp
```

+   3. Log in on the remote host and load the dump file into the MySQL server there:

```
$ mysql < /tmp/sampdb.sql
```