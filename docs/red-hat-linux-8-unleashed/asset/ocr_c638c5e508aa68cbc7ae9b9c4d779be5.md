If you have decided to use a directory other than /usr/local/postgresql/data as the data directory, you should replace the directory in the postmaster command line with whatever directory you are using.

> By default, Red Hat Linux makes the PostgreSQL data directory /var/lib/postgresql/data. This isn't a very good place to store the data, however, because most people do not have the necessary space in the /var partition for any kind of serious data storage. Note that if you change the directory to something else (such as /usr/local/postgresql/data, as in the examples in this section), you need to edit the PostgreSQL startup file located in /etc/rc.d/init.d to reflect the change.

# Creating a Database in PostgreSQL

Creating a database in PostgreSQL is very straightforward, but it must be performed by a user who has permissions to create databases in PostgreSQL—for example, initially the user named postgres. You can simply issue the following command from the shell prompt (not the PSQL client prompt, but a normal Red Hat Linux shell prompt):

```
# su postgres
bash-2.05b$ createdb database
```

where database is the name of the database that you want to create.

The createdb program is actually a wrapper that makes it easier to create databases without having to log in and use psql. However, you can also create databases within psql with the CREATE DATABASE statement. Here's an example:

```
CREATE DATABASE database;
```

You need to create at least one database before you start the psql client program. You should create this database while you are logged in as the user postgres. To log in as this user, you need to become root, and then use so to become the user postgres. To connect to the new database, you start the psql client program with the name of the new database as a command-line argument, like so:

```
$ psql sampledat
```

# Creating Database Users in PostgreSQL

To create a database user, you use so to become the user postgres from the Red Hat root account. You can then use the PostgreSQL createuser command to quickly create a user who is allowed to access databases or create new users, like this: