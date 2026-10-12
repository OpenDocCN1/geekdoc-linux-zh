
In this example, the new user named `phudson` is created and allowed to create new databases and database users (you should carefully consider who is allowed to create new databases or additional users).

You can also use the PostgreSQL command-line client to create a new user by typing `psql` along with name of the database and then use the **CREATE USER** command to create a new user. Here is an example:

CREATE USER foobar ;

> **CAUTION**
> PostgreSQL allows you to omit the **WITH PASSWORD** portion of the statement. However, doing so causes the user to be created with no password. This is a security hole, so you should always use the **WITH PASSWORD** option when creating users.

> **NOTE**
> When you are finished working in the `psql` command-line client, you can type `\q` to get out of it and return to the shell prompt.

## Deleting Database Users in PostgreSQL

To delete a database user, you use the `dropuser` command, along with the user’s name, and the user’s access is removed from the default database, like this:

$ dropuser msmith
DROP USER

You can also log in to your database by using `psql` and then use the **DROP USER** commands. Here’s an example:

```text
$ psql demodb
Welcome to psql, the PostgreSQL interactive terminal.

Type: \copyright for distribution terms
     \h for help with SQL commands
     \? for help on internal slash commands
     \g or terminate with semicolon to execute query
     \q to quit

demodb=# DROP USER msmith ;
DROP USER
demodb=# \q
$ 
```

## Granting and Revoking Privileges in PostgreSQL

As in MySQL, granting and revoking privileges in PostgreSQL is done with the **GRANT** and **REVOKE** statements. The syntax is the same as in MySQL except that PostgreSQL doesn't use the **IDENTIFIED BY** portion of the statement because with PostgreSQL, passwords are assigned when you create the user with the **CREATE USER** statement, as discussed previously. Here is the syntax of the **GRANT** statement:

```text
GRANT what_to_grant ON where_to_grant TO user_name;
```

The following command, for example, grants all privileges to the user *foobar* on the database *sampledata*:

```text
GRANT ALL ON sampledata TO foobar;
```

To revoke privileges, you use the **REVOKE** statement. Here is an example:

```text
REVOKE ALL ON sampledata FROM foobar;
```

This command removes all privileges from the user *foobar* on the database *sampledata*.

Advanced administration and user configuration are complex topics. This section cannot begin to cover all the aspects of PostgreSQL administration or of privileges and users. For more information on administering PostgreSQL, see the PostgreSQL documentation or consult a book on PostgreSQL, such as *PostgreSQL* (Sams Publishing).

## Database Clients

Both MySQL and PostgreSQL use a client/server system for accessing databases. In the simplest terms, the database server handles the requests that come into the database and the database client handles getting the requests to the server as well as getting the output from the server to the user.

Users never interact directly with the database server even if it happens to be located on the same machine they are using. All requests to the database server are handled by a database client, which might or might not be running on the same machine as the database server.

Both MySQL and PostgreSQL have command-line clients. A command-line client is a very primitive way of interfacing with a database and generally isn't used by end users. As a DBA, however, you use the command-line client to test new queries interactively without having to write front-end programs for that purpose. In later sections of this chapter, you will learn a bit about the MySQL graphical client and the web-based database administration interfaces available for both MySQL and PostgreSQL.

The following sections examine two common methods of accessing a remote database, a method of local access to a database server, and the concept of web access to a database.

> **NOTE**
> You should consider access and permission issues when setting up a database. Should users be able to create and destroy databases? Or should they only be able to use existing databases? Will users be able to add records to the database and modify existing records? Or should users be limited to read-only access to the database? And what about the rest of the world? Will the general public need to have any kind of access to your database through the Internet? As DBA, you must determine the answers to these questions.

## SSH Access to a Database

Two types of remote database access scenarios are briefly discussed in this section. In the first scenario, the user directly logs in to the database server through SSH (to take advantage of the security benefits of encrypted sessions) and then starts a program on the server to access the database. In this case, shown in Figure 20.4, the database client is running on the database server itself.

![](img/774d40fd20903495c5cd00e2efad3f33_611_0.png)

**FIGURE 20.4** The user logs in to the database server located on host simba from the workstation (host cheetah). The database client is running on simba.

In the other scenario, shown in Figure 20.5, the user logs in to a remote host through SSH and starts a program on it to access the database, but the database is actually running on a different system. Three systems are now involved—the user's workstation, the remote host running the database client, and the remote host running the database server.

The important thing to note in Figure 20.5 is the middleman system leopard. Although the client is no longer running on the database server itself, it isn't running on the user's local workstation, either.

![](img/774d40fd20903495c5cd00e2efad3f33_612_0.png)

**FIGURE 20.5** The user logs in to the remote host `leopard` from the workstation (host `cheetah`) and starts a database client on `leopard`. The client on `leopard` then connects to the database server running on host `simba`. The database client is running on `leopard`.

## Local GUI Client Access to a Database

A user can log in to the database server by using a graphical client (which could be running on Windows, Macintosh, or a Unix workstation). The graphical client then connects to the database server. In this case, the client is running on the user’s workstation. Figure 20.6 shows an example.

![](img/774d40fd20903495c5cd00e2efad3f33_612_1.png)

**FIGURE 20.6** The user starts a GUI database program on his workstation (hostname `cheetah`). This program, which is the database client, then connects to the database server running on the host `lion`.

## Web Access to a Database

In this section, we look at two basic examples of web access to the database server. In the first example, a user accesses the database through a form located on the World Wide Web. At first glance, it might appear that the client is running on the user’s workstation. Of course, in reality it is not; the client is actually running on the web server. The web browser on the user's workstation simply provides a way for the user to enter the data that he wants to send to the database and a way for the results sent from the database to be displayed to the user. The software that actually handles sending the request to the database is running on the web server in the form of a CGI script; a Java servlet; or embedded scripting such as the PHP or Sun Microsystems, Inc.'s JavaServer Pages (JSP).

Often, the terms client and front end are used interchangeably when speaking of database structures. However, Figure 20.7 shows an example of a form of access in which the client and the front end aren't the same thing at all. In this example, the front end is the form displayed in the user's web browser. In such cases, the client is referred to as *middleware*.

![](img/774d40fd20903495c5cd00e2efad3f33_613_0.png)

**FIGURE 20.7** The user accesses the database through the World Wide Web. The front end is the user's web browser, the client is running on Leopard, and the server is running on Simba.

In another possible web access scenario, it could be said that the client is a two-piece application in which part of it is running on the user's workstation and the other part is running on the web server. For example, the database programmer can use JavaScript in the web form to ensure that the user has entered a valid query. In this case, the user's query is partially processed on her own workstation and partially on the web server. Error checking is done on the user's own workstation, which helps reduce the load on the server and also helps reduce network traffic because the query is checked for errors before being sent across the network to the server.

## The MySQL Command-Line Client

The MySQL command-line client is `mysql`, and it has the following syntax:

```text
mysql [options] [database]
```

Some of the available options for `mysql` are discussed in Table 20.1. `database` is optional, and if given, it should be the name of the database to which you want to connect.
