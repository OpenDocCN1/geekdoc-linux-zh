If you are installing from the Fedora RPM files, a necessary **postgres** user account (that is, an account with the name of the user running the server on your system) is created for you automatically:

```
$ fgrep postgres /etc/passwd
postgres:x:26:26:Postgre$QL Server::/var/lib/pgsql::/bin/bash
```

Otherwise, you need to create a user called **postgres** during the installation. This user shouldn't have login privileges because only root should be able to use su to become this user and no one will ever log in directly as the user. (Refer to Chapter 10, "Managing Users," for more information on how to add users to a Fedora system.) After you have added the user, you can install each of the Postgre$QL RPMs you downloaded using the standard rpm -i command for a default installation.

# Initializing the Data Directory in Postgre$QL

After the RPMs are installed, you need to initialize the data directory. To do so, you must first create the data directory and you must be the root user. The following example assumes that the data directory is /usr/local/pgsql/data.

Create the /usr/local/pgsql/data directory (using mkdir) and change the ownerships of the directory (using chown and chgrp) so it is owned by the user **postgres**. Then use su and, as the user **postgres**, issue the following commands:

```
# mkdir /usr/local/pgsql
# chown postgres /usr/local/pgsql
# chgrp postgres /usr/local/pgsql
# su - postgres
 -bash-2.05$ initdb -D /usr/local/pgsql/data
```

The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale en_US.UTF-8.
This locale setting will prevent the use of indexes for pattern matching operations. If that is a concern, rerun initdb with the collation order set to "C". For more information see the Administrator's Guide.

```
creating directory /usr/local/pgsql/data... ok
creating directory /usr/local/pgsql/data/base/... ok
creating directory /usr/local/pgsql/data/global... ok
creating directory /usr/local/pgsql/data/pg_xlog... ok
creating template1 database in /usr/local/pgsql/data/base/1... ok
creating configuration files... ok
initializing pg_shadow... ok
enabling unlimited row size for system tables... ok
```