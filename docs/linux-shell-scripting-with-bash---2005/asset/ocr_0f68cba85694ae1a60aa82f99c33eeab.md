The tree contains...

```
3 = Clarke Plumbing
1 = Crotwer Insurance Brokers Limited
0 = Hazel's Ladies Wear
5 = Scott Furniture Ltd
2 = Shakur LLP
6 = Zap Electric
```

Looking up some items...

```
Zap Electric is in the tree at 6
Clarke Plumbing is in the tree at 3
Bogus test data is not in the tree
```

Because of their sorted nature, binary trees can also be used as a simple sort. However, the `Linux` *sort* command is almost always faster.

# ## Working with PostgreSQL Databases (`psql`)

Text files and Bash arrays are fast and convenient for small quantities of data. If you are going to work with hundreds of thousands of pieces of information, you need to use a database to manage your information.

Most databases (including Oracle, MySQL, and PostgreSQL) come with console client applications. These applications are sometimes referred to as “monitors” or “console monitors.” Console clients look and operate much as a shell but they have a different command prompt and expect `SQL` commands instead of `Linux` or `Bash` commands. With the proper options, console clients can run database commands on behalf of a Bash script.

The PostgreSQL database is available with most `Linux` distributions but it might not be installed by default depending on your installation settings. For example, a “desktop” or “workstation” installation might not include PostgreSQL. The PostgreSQL database has a console client called `psql`. If `psql` is not installed, see if it is available on your distribution disks. The remainder of this section assumes that you have PostgreSQL installed and the database server is up and running.

To log into PostgreSQL, use `psql` with the `-user username` (or `-U username`) switch. The `-list` (or `-l`) switch lists all available databases.

```
$ psql -user gordon --list
```

List of databases
Name   |   Owner   | Encoding
--------+-----------+----------
custinfo | postgres | SQL_ASCII
template0| postgres | SQL_ASCII
template1| postgres | SQL_ASCII
(3 rows)