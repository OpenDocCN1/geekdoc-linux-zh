```
demodb# DROP USER msmith ;
DROP USER
demodb# \q
$ 
```

# Granting and Revoking Privileges in PostgreSQL

As in MySQL, granting and revoking privileges in PostgreSQL is done with the GRANT and REVOKE statements. The syntax is the same as in MySQL except PostgreSQL doesn't use the IDENTIFIED portion of the statement because with PostgreSQL, passwords are assigned when you create the user with the CREATE USER statement, as discussed previously. Here is the syntax of the GRANT statement:

```
GRANT what_to_grant ON where_to_grant user_name;
```

The following command, for example, grants all privileges to the user foobar on the database-sampledata:

```
GRANT ALL ON sampledata TO foobar;
```

To revoke privileges, you use the REVOKE statement. Here's an example:

```
REVOKE ALL ON sampledata FROM foobar;
```

This command removes all privileges from the user foobar on the database. Advanced administration and user configuration are complex topics. This section cannot begin to cover all the aspects of PostgreSQL administration or of privileges and users. For more information on administering PostgreSQL, see the PostgreSQL documentation or consult a book on PostgreSQL (Sams Publishing).

# Database Clients

Both MySQL and PostgreSQL use a client/server system for accessing databases. In the simplest terms, the database server handles the requests that come into the database, and the database client handles getting the requests to the server as well as getting the output from the server to the user.

Users never interact directly with the database server, even if it happens to be located on the same machine that they are using. All requests to the database server are handled by a database client, which might or not be running on the same machine as the data-server.

Both MySQL and PostgreSQL use command-line clients. A command-line client is a primitive way of interfacing with a database and generally isn't used by end users. As DBA, however, you use the command-line client to test new queries interactively without writing to front-end programs for that purpose. In later sections of this chapter,