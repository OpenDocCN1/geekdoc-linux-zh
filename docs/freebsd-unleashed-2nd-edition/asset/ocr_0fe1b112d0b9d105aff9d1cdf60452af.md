If you wish, you can create a file called **admins** in `/usr/local/pgsql/data`, with one database username per line; only those users will be allowed to work with the databases. You can do the same with each new database you create—simply add a different file for each database, with the name of the user who owns it, and the name of the file in place of **admins** in this example.

Alternatively, you can enforce a policy whereby local users can connect, without passwords, only to their own databases (those that have names that match the usernames). For instance, the user **frank** would have a database called “frank.” This can be done with the following configuration line:

```
local           all                                 ident  sameuser
```

# # Writing Administration Scripts

You've reached the next level in our breakneck tour through the world of databases; now that the tables in the sample databases are set up, we can now move on past the use of the interactive command line and learn how to automate some of the longer, more painful queries. The MySQL or PostgreSQL command line will always be useful for design and tinkering purposes. However, some tasks that must be done on a regular basis and require long, involved queries demand that you find a less frustrating way to accomplish them.

Perl and Python both provide toolkits with which you can write scripts to interface with the database. These toolkits enable you to issue queries, extract data, process it, and feed data back into the system, all within loops and conditionals and all the other programmatic benefits that those languages offer.

# ## Database Connectivity with Perl

As a courtesy, the necessary Perl modules for connectivity to MySQL are installed along with the MySQL port. These also are located in `/usr/ports/databases/p5-mysql`; the documentation can be read with `perldoc Mysql`.

The crucial part of these modules is the setup part of any script that intends to connect to a MySQL database. This setup block includes the following lines, which should go right at the top of the script:

```
use Mysql;  
$dbh = Mysql->connect(undef, "PictureArchive", "frank", "<frank's password>");
```

After you add these lines to the script, you have a database handle to work with: `$dbh`. A whole suite of operations can be performed on this handle; this chapter doesn't discuss all of them—just the most important operations. You will find the rest in the `perldoc Mysql` documentation.