# OffSec Penetration Testing with Kali Linux

```
-----------------------------
1 row in set (0.107 sec)
```

Listing 180 - Retrieving the version of a MySQL database

We can also verify the current database user for the ongoing session via the system_user() function, which returns the current username and hostname for the MySQL connection.

```
MySQL [[none]] select system_user();
```

```
-----------------------------
| system_user() |
-----------------------------
| root@192.168.20.50 |
-----------------------------
1 row in set (0.104 sec)
```

Listing 181 - Inspecting the current session's user

The database query we ran confirmed we are logged in as the database root through a remote connection from 192.168.20.50.

> The root user in this example is the database-specific root user, not the system-wide administrative root user.

We now collect a list of all databases running in the MySQL session by issuing the command, followed by the databases keyword.

```
MySQL [[none]] show databases;
```

```
-----------------------------
| Database |
-----------------------------
| information_schema |
| mysql |
| performance_schema |
| sys |
| test |
-----------------------------
5 rows in set (0.107 sec)
```

Listing 182 - Listing all Available user in the mysql database.

As an example, let's retrieve the password of the offsec user

Within the mysql database, we will filter using a SELECT statement for the user and authentication_string value belonging to the user table. Next, we will filter all the results via a WHERE clause that matches only the offsec user.

```
MySQL> SELECT user, authentication_string FROM mysql.user WHERE user = 'offsec';
```

```
----------------------------------------------------------------------
| user | authentication_string |
----------------------------------------------------------------------
| offsec | $A005$7qvorpP81LTKHj54xux4VsXe5EAa1cFUYdQMbXQVEZG9XWd/e6 |
----------------------------------------------------------------------
1 row in set (0.106 sec)
```

Listing 183 - Inspecting user's encrypted password

PWK - © 2023 OffSec Services Limited. All rights reserved.