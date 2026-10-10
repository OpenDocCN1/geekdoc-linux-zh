604  Chapter 13  Configuring Network Services

# # Configuring PostgreSQL

PostgreSQL is a powerful SQL server that provides a large number of features. Although many Linux server distributions allow you to install PostgreSQL SQL during the Linux installation process, you can easily install it from a software repository afterwards. During installation, the PostgreSQL installation creates a postgres user within the /etc/passwd and /etc/shadow files that has a home directory of /var/lib/postgresql and a shell of /bin/bash.

Next, you can prepare PostgreSQL for use by following these steps:

+   1. Assign the postgres user a password using the passwd postgres command.
+   2. Optionally modify the PostgreSQL configuration file, postgresql.conf. The location of this file differs depending on your Linux distribution, but it is often stored under the /var/lib/postgresql directory or the /etc/postgresql directory.
+   3. Start the PostgreSQL daemon and configure it to start at boot time.

# ## Configuring PostgreSQL Databases

To configure PostgreSQL databases, you must first log in as the postgres user. Next, you can execute one of several PostgreSQL command-line utilities to create and manage databases. These commands are summarized in Table 13-6.

For example, to create a database called sampled after logging in as the postgres user, you could use the following command:

```
[root@server1 -]$ createdb sampled db
[root@server1 -]$_
```

| Command | Description |
| --- | --- |
| clusterdb | Associates a PostgreSQL database to another database on a different server |
| createdb | Creates a PostgreSQL database |
| createlang | Allows a new programming language to be used with PostgreSQL |
| createuser | Creates a PostgreSQL user |
| dropdb | Deletes a PostgreSQL database |
| droplang | Removes support for a programming language within PostgreSQL |
| dropuser | Deletes a PostgreSQL user |
| pg_dump | Backs up PostgreSQL database settings |
| pg_dumpall | Backs up a PostgreSQL database cluster settings |
| pg_restore | Restores PostgreSQL database settings |
| psql | The PostgreSQL utility |
| reindexdb | Reindexes a PostgreSQL database |
| vacuumdb | Analyzes and regenerates internal PostgreSQL database statistics |

**Table 13-6**  *PostgreSQL command-line utilities*

Copyright 2016 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. Due to electronic rights, some third party content may be suppressed from the eBook and/or EChapter(s). Editorial review has deemed that any suppressed content does not materially affect the overall learning experience. Cengage Learning reserves the right to remove additional content at any time if subsequent rights restrictions require it.