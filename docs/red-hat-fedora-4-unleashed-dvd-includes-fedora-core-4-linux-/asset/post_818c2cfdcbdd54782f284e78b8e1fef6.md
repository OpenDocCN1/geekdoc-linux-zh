
## TABLE 20.1 Command-Line Options to Use When Invoking `mysql`

| Option | Action |
| :--- | :--- |
| `-h hostname` | Connects to the remote host *hostname* (if the database server isn't located on the local system). |
| `-u username` | Connects to the database as the user *username*. |
| `-p` | Prompts for a password. This option is required if the user you are connecting as needs a password to access the database. Note that this is a lowercase p. |
| `-P n` | Specifies *n* as the number of the port that the client should connect to. Note that this is an uppercase P. |
| `-?` | Displays a help message. |

More options are available than are listed in Table 20.1, but these are the most common options. See the man page for `mysql` for more information on the available options.

> **CAUTION**
>
> Although `mysql` allows you to specify the password on the command line after the `-p` option, and thus allows you to avoid having to type the password at the prompt, you should never invoke the client this way. Doing so causes your password to display in the process list, and the process list can be accessed by any user on the system. This is a major security hole, so you should never give your password on the `mysql` command line.

You can access the MySQL server without specifying a database to use. After you log in, you use the help command to get a list of available commands, like this:

```sql
mysql> help
```

MySQL commands:

Note that all text commands must be first on line and end with `';'`

- help (\h) Display this help.
- ? (\?) Synonym for `\`help`\`.
- clear (\c) Clear command.
- connect (\r) Reconnect to the server. Optional arguments are db and host.
- edit (\e) Edit command with $EDITOR.
- ego (\G) Send command to `mysql` server, display result vertically.
- exit (\q) Exit `mysql`. Same as `quit`.
- go (\g) Send command to `mysql` server.
- nopager (\n) Disable pager, print to stdout.
- notee (\t) Don't write into outfile.
- pager (\P) Set PAGER [to_pager]. Print the query results via PAGER.
- print (\p) Print current command.
- quit (\q) Quit `mysql`.
- rehash (\#) Rebuild completion hash.
- source (\.) Execute a SQL script file. Takes a file name as an argument.

![](img/774d40fd20903495c5cd00e2efad3f33_614_0.png)

- status (\s) Get status information from the server.
- tee (\T) Set outfile [to_outfile]. Append everything into given outfile.
- use (\u) Use another database. Takes database name as argument.

You can then access a database by using the **use** command and the name of a database that has been created (such as *animals*) and that you are authorized to connect to, like this:

```sql
mysql> use animals
Database changed
mysql>
```

## The PostgreSQL Command-Line Client

You invoke the PostgreSQL command-line client with the command **psql**. Like *mysql*, psql can be invoked with the name of the database to which you would like to connect. Also like *mysql*, psql can take several options. These options are listed in Table 20.2.

### TABLE 20.2 Command-Line Options to Use When Invoking psql

| Option | Action |
|:---|:---|
| -h *hostname* | Connects to the remote host *hostname* (if the database server isn’t located on the local system). |
| -p *n* | Specifies *n* as the number of the port that the client should connect to. Note that this is a lowercase p. |
| -U *username* | Connects to the database as the user *username*. |
| -W | Prompts for a password after connecting to the database. In PostgreSQL 7 and later, password prompting is automatic if the server requests a password after a connection has been established. |
| -? | Displays a help message. |

Several more options are available in addition to those listed in Table 20.2. See the psql’s man page for details on all the available options.

## Graphical Clients

If you’d rather interact with a database by using a graphical database client than with the command-line clients discussed in the previous section, you’re in luck: A few options are available.

MySQL has an official graphical client, called MySQLGUI. MySQLGUI is available in both source and binary formats from the MySQL website at http://www.mysql.com.

Web-based administration interfaces are also available for MySQL and PostgreSQL. phpMyAdmin and phpPgAdmin are two such products. Both of these products are based on the PHP-embedded scripting language and therefore require you to have PHP installed. Of course, you also need to have a web server installed.

## Related Fedora and Database Commands

The following commands are useful for creating and manipulating databases in Fedora:

- createdb—Creates a new PostgreSQL database
- createuser—Creates a new PostgreSQL user account
- dropdb—Deletes a PostgreSQL database
- dropuser—Deletes a PostgreSQL user account
- mysql—Interactively queries the mysqld server
- mysqladmin—Administers the mysqld server
- mysqldump—Dumps or backs up MySQL data or tables
- pgaccess—Accesses a PostgreSQL database server
- pg_ctl—Controls a PostgreSQL server or queries its status
- psql—Accesses PostgreSQL via an interactive terminal

## Reference

The following are references for the databases mentioned in this chapter:

- http://www.mysql.com—This is the official website of the MySQL database server. Here you can find the latest versions as well as up-to-date information and online documentation for MySQL. You can also purchase support contracts here. You might want to look into this if you will be using MySQL in a corporate setting. (Many corporations balk at the idea of using software for which the company has no support contract in place.)
- http://www.postgresql.org—This is the official website of the PostgreSQL database server. You are asked to select a mirror when you arrive at this site. After you select a mirror, you are taken to the main site. From there, you can find information on the latest versions of PostgreSQL and read the online documentation.
- http://www.postgresql.org/iddocs/index.php?tutorial-start.html—This interactive HTML documentation tree is a great place to get started with learning how to use PostgreSQL.
- http://www.pgsql.com—This is a commercial company that provides fee-based support contracts for the PostgreSQL database.

## CHAPTER 21
## File and Print

T here are many reasons to share files and printers across a network. Perhaps you have a set of documents that need to be accessible to more than one person at a time, or you need to be able to print to a laser printer or a color printer. Fortunately, Fedora comes with a host of tools that allow you to share files with one another and access remote printers.

For the most part, graphical tools are available to help you configure your machine, but sometimes you might need to delve into the command line and some of the configuration files to tweak it just how you want it. This chapter takes you through setting up file sharing using both NFS and Samba and explains how to add users for Samba sharing as well as working with access levels, configuring Samba using SWAT (a handy web-based configuration tool), setting up and accessing remote printers on a print queue, and configuring Network Attached Printers that use interfaces such as JetDirect.

So, whether you are sharing ogg files across the network or setting up a corporate file server to hold office documents, you will find the answers here.

## Using the Network File System

The Network File System (NFS) was developed by Sun Microsystems as a way for computers to share files as if they were local to the remote machine. NFS is commonly used to share home directories between hosts within a network. This reduces the need to have a home directory on every computer and ensures that no matter which computer you log in to, your home directory will be consistent.

## IN THIS CHAPTER

- Using the Network File System
- Putting Samba to Work
- Network and Remote Printing with Fedora
- Creating Network Printers
- Console Print Control
- Using the Common Unix Printing System GUI
- Avoiding Printer Support Problems
- Reference
