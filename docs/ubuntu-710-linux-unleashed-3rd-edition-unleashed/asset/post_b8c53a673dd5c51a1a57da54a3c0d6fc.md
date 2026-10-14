
## TIP

By default, Ubuntu makes the PostgreSQL data directory `/var/lib/pgsql/data`. This isn’t a very good place to store the data, however, because most people do not have the necessary space in the `/var` partition for any kind of serious data storage. Note that if you do change the data directory to something else (such as `/usr/local/pgsql/data`, as in the examples in this section), you need to edit the PostgreSQL startup file (named `postgres`) located in `/etc/init.d` to reflect the change.

## Creating a Database in PostgreSQL

Creating a database in PostgreSQL is straightforward, but it must be performed by a user who has permissions to create databases in PostgreSQL—for example, initially the user named postgres. You can then simply issue the following command from the shell prompt (not the PSQL client prompt, but a normal shell prompt):

```
# su - postgres
-bash-2.05$ createdb database
```

where *database* is the name of the database you want to create.

The createdb program is actually a wrapper that makes it easier to create databases without having to log in and use psql. However, you can also create databases from within psql with the CREATE DATABASE statement. Here’s an example:

```
CREATE DATABASE database;
```

You need to create at least one database before you can start the psql client program. You should create this database while you’re logged in as the user postgres. To log in as this user, you need to use su to become root and then use su to become the user postgres. To connect to the new database, you start the psql client program with the name of the new database as a command-line argument, like so:

```
$ psql sampledata
```

If you don’t specify the name of a database when you invoke psql, the command attempts to connect to a database that has the same name as the user as which you invoke psql (that is, the default database).

## Creating Database Users in PostgreSQL

To create a database user, you use su to become the user postgres from the Linux root account. You can then use the PostgreSQL createuser command to quickly create a user who is allowed to access databases or create new database users, like this:

```
$ createuser phudson
Shall the new user be allowed to create databases? (y/n) y
```

```
Shall the new user be allowed to create more new users? (y/n) y
CREATE USER
```

In this example, the new user named phudson is created and allowed to create new databases and database users (you should carefully consider who is allowed to create new databases or additional users).

You can also use the PostgreSQL command-line client to create a new user by typing psql along with name of the database and then use the CREATE USER command to create a new user. Here is an example:

```
CREATE USER foobar ;
```

> **CAUTION**
> PostgreSQL allows you to omit the WITH PASSWORD portion of the statement. However, doing so causes the user to be created with no password. This is a security hole, so you should always use the WITH PASSWORD option when creating users.

> **NOTE**
> When you are finished working in the psql command-line client, you can type \q to get out of it and return to the shell prompt.

## Deleting Database Users in PostgreSQL

To delete a database user, you use the dropuser command, along with the user's name, and the user's access is removed from the default database, like this:

```
$ dropuser msmith
DROP USER
```

You can also log in to your database by using psql and then use the DROP USER commands. Here's an example:

```
$ psql demodb
Welcome to psql, the PostgreSQL interactive terminal.

Type: \copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate with semicolon to execute query
\q to quit
```

```
demodb=# DROP USER msmith ;
DROP USER
demodb=# \q
$
```

## Granting and Revoking Privileges in PostgreSQL

As in MySQL, granting and revoking privileges in PostgreSQL is done with the GRANT and REVOKE statements. The syntax is the same as in MySQL except that PostgreSQL doesn't use the IDENTIFIED BY portion of the statement because with PostgreSQL, passwords are assigned when you create the user with the CREATE USER statement, as discussed previously. Here is the syntax of the GRANT statement:

```
GRANT what_to_grant ON where_to_grant TO user_name;
```

The following command, for example, grants all privileges to the user foobar on the database sampledata:

```
GRANT ALL ON sampleddata TO foobar;
```

To revoke privileges, you use the REVOKE statement. Here is an example:

```
REVOKE ALL ON sampleddata FROM foobar;
```

This command removes all privileges from the user foobar on the database sampleddata.

Advanced administration and user configuration are complex topics. This section cannot begin to cover all the aspects of PostgreSQL administration or of privileges and users. For more information on administering PostgreSQL, see the PostgreSQL documentation or consult a book on PostgreSQL, such as PostgreSQL (Sams Publishing).

## Database Clients

Both MySQL and PostgreSQL use a client/server system for accessing databases. In the simplest terms, the database server handles the requests that come into the database and the database client handles getting the requests to the server as well as getting the output from the server to the user.

Users never interact directly with the database server even if it happens to be located on the same machine they are using. All requests to the database server are handled by a database client, which might or might not be running on the same machine as the database server.

Both MySQL and PostgreSQL have command-line clients. A command-line client is a very primitive way of interfacing with a database and generally isn't used by end users. As a DBA, however, you use the command-line client to test new queries interactively without having to write front-end programs for that purpose. In later sections of this chapter, you
