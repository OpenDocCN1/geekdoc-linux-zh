By default, Fedora makes the PostgreSQL data directory `/var/lib/pgsql/data`. This isn't a very good place to store the data, however, because most people do not have the necessary space in the `/var` partition for any kind of serious data storage. Note that if you do change the data directory to something else (such as `/usr/local/pgsql/data, as in the examples in this section), you need to edit the PostgreSQL startup file (named postgres) located in `/etc/rc.d/init.d` to reflect the change."

# ## Creating a Database in PostgreSQL

Creating a database in PostgreSQL is straightforward, but it must be performed by a user who has permissions to create databases in PostgreSQL—for example, initially the user named postgres. You can then simply issue the following command from the shell prompt (not the PSQL client prompt, but a normal shell prompt):

```
# su - postgres
-bash-2.05$ createdb database
```

where database is the name of the database you want to create.

The createdb program is actually a wrapper that makes it easier to create databases without having to log in and use psql. However, you can also create databases from within psql with the CREATE DATABASE statement. Here's an example:

CREATE DATABASE database;

You need to create at least one database before you can start the psql client program. You should create this database while you're logged in as the user postgres. To log in as this user, you need to use su to become root and then use su to become the user postgres. To connect to the new database, you start the psql client program with the name of the new database as a command-line argument, like so:

$ psql sampledata

If you don't specify the name of a database when you invoke psql, the command attempts to connect to a database that has the same name as the user as which you invoke psql (that is, the default database).

# ## Creating Database Users in PostgreSQL

To create a database user, you use su to become the user postgres from the Linux root account. You can then use the PostgreSQL createuser command to quickly create a user who is allowed to access databases or create new database users, like this:

```
$ createuser phudson
Shall the new user be allowed to create databases? (y/n) y
Shall the new user be allowed to create more new users? (y/n) y
CREATE USER
```