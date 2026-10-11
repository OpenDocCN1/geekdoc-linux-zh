
# 12.4.2.3 REQUIRE

REQUIRE X509 imposes no constraints on the certificate’s contents other than that it be valid. To be even more strict, REQUIRE enables you to indicate that the client’s X509 certificate must have certain characteristics. These characteristics are given with ISSUER or SUBJECT options in the REQUIRE clause. ISSUER and SUBJECT refer to the certificate issuer and recipient. For example, the ssl directory of the sampledb distribution includes a client certificate file, client-cert.pem, that you can use for testing SSL connections. The issuer and subject values in the certificate can be displayed using the openssl command:

```
% openssl x509 -issuer -subject -noout -in client-cert.pem
issuer=  /C=US/ST=WI/L=Madison/O=sampledb/OU=CA/CN=sampledb
subject=  /C=US/ST=WI/L=Madison/O=sampledb/OU=client/CN=sampledb
```

The following GRANT statement indicates an account for which the client must present a certificate that matches both of those values:

```
GRANT ALL ON sampledb.* TO 'eladio'@'%.snake.net'
  REQUIRE ISSUER '/C=US/ST=WI/L=Madison/O=sampledb/OU=CA/CN=sampledb'
        AND SUBJECT '/C=US/ST=WI/L=Madison/O=sampledb/OU=client/CN=sampledb';
```

You can also use REQUIRE to indicate that the connection must be encrypted using a particular cipher type:

```
GRANT ALL ON sampledb.* TO 'eladio'@'%.snake.net'
  REQUIRE CIPHER 'DHE-RSA-AES256-SHA';
```

To indicate explicitly that secure connections are not required, use REQUIRE NONE. This is the default when you create a new account, but it can be useful for removing a requirement for SSL from an account that currently has it.

Some additional points to be aware of when using a REQUIRE clause:

-   Issuing a GRANT statement that requires an account to use secure connections only sets up a constraint on the account. It doesn’t actually provide the means for a client program to connect securely with that account. For that to happen, MySQL must be configured to include SSL support, and you must start the server and clients in a particular way. Section 13.3, “Setting Up Secure Connections,” describes how to do this.

-   If you specify that connections for an account must use SSL, but SSL is not supported by either the server or client programs, the account is effectively unusable.

-   REQUIRE is used only to indicate whether an account *must* connect using secure connections. If the server and client programs are configured with SSL support, any user is still *able* to use secure connections, even if not required to do so.

-   There is little point in using a REQUIRE clause for accounts that don’t connect to the server over an external network. Such connections can’t be snopped, so making them encrypted gains you nothing and incurs increased computational load without benefit. Accounts like this include those that connect to the server only through a Unix socket file, a named pipe, shared memory, or to the IP number 127.0.0.1 (the host’s loopback interface). These connections use interfaces that are handled internally to the host and for which no traffic crosses an external network.

# 12.4.2.4 Enabling an Account to Administer Privileges

You can enable an account to grant its own privileges to other accounts by specifying the WITH GRANT OPTION clause. To use this clause, you must have the GRANT OPTION privilege yourself.

One reason to give an account the GRANT OPTION privilege is to enable the owner of a database to control access to the database: Grant the owner all privileges on the database, including the GRANT OPTION privilege. For example, if you want alicia to be able to connect from any host in the big-corp.com domain and administer privileges for all tables in the sales database, set up the account this way:

```
CREATE USER 'alice'@'%.big-corp.com' IDENTIFIED BY 'shale';
GRANT ALL ON sales.* TO 'alice'@'%.big-corp.com' WITH GRANT OPTION;
```

In effect, the WITH GRANT OPTION clause enables you to delegate access-granting rights to another user. But be aware that two users with the GRANT OPTION privilege can grant each other their own privileges. If you’ve given one user only the SELECT privilege but another user has GRANT OPTION plus other privileges in addition to SELECT, the second user can make the first one “stronger.”

Another way to grant the GRANT OPTION privilege is simply to list it in the beginning part of the GRANT statement:

```
GRANT GRANT OPTION ON sales.* TO 'alice'@'%.big-corp.com';
```

However, a statement such as this one will not work:

```
GRANT ALL, GRANT OPTION ON sales.* TO 'alice'@'%.big-corp.com';
```

In a GRANT statement, ALL can be used only by itself, not in a list that names other privilege specifiers.

GRANT OPTION applies to all privileges at or below the level at which it is granted, not to individual privileges. If you give an account the GRANT OPTION privilege at a given level, the account can grant any privilege that it holds at that level. You cannot specify that the account can grant some of the privileges that it holds at that level but not others.

# 12.4.2.5 Limiting an Account’s Resource Consumption

The MySQL grant system enables you to place limits on the number of times per hour that an account can connect to the server, and the number of statements or updates per hour the account can issue. To specify these limits, use a WITH clause. The following statement sets up an account 'spike'@'localhost' that has full access to the sampledb database, but can connect only ten times per hour and issue 200 statements per hour (of which at most 50 can be updates):

```
CREATE USER 'spike'@'localhost' IDENTIFIED BY 'pyrite';
GRANT ALL ON sampledb.* TO 'spike'@'localhost'
  WITH MAX_CONNECTIONS_PER_HOUR 10
       MAX_QUERIES_PER_HOUR 200
       MAX_UPDATES_PER_HOUR 50;
```

The default value for each option is zero, which means "no limit." This means that if you have placed a resource limit on an account, you can remove the limit by changing the limit value to zero. For example, to remove the limit on the number of times per hour that spike can connect, use this statement:

```
GRANT USAGE ON *.* TO 'spike'@'localhost'
  WITH MAX_CONNECTIONS_PER_HOUR 0;
```

A user cannot subvert these limits by using multiple connections to the server, because all connections for a given account are counted together.

As of MySQL 5.0.3, a fourth resource limit, MAX_USER_CONNECTIONS, is available to control the maximum number of simultaneous connections that the account can have. If the limit is zero (the default), the limit is controlled by the value of the max_user_connections system variable. A non-zero value limits the account to that many simultaneous connections.

The order of the resource management options within the WITH clause does not matter.

Any administrative user who has the RELOAD privilege can reset the current counter values by issuing a FLUSH USER_RESOURCES statement. FLUSH PRIVILEGES does this as well. After the counters have been reset, accounts that have reached their hourly limits once again can connect and issue statements. A reset also occurs for an individual account if you issue a GRANT statement that sets that account's limits.

# 12.4.3 Displaying Account Privileges

To see what privileges an account has, use the SHOW GRANTS statement:

```
SHOW GRANTS FOR 'sampadm'@'localhost';
```

To see your own privileges, use either of these statements:

```
SHOW GRANTS;
SHOW GRANTS FOR CURRENT_USER();
```

# 12.4.4 Revoking Privileges and Removing Users

To take away some or all of an account's privileges, use the REVOKE statement. The syntax for REVOKE is somewhat similar to that for the GRANT statement, except that TO is replaced by FROM, and there are no IDENTIFIED BY, REQUIRE, or WITH clauses:

The GRANT OPTION privilege is not included in ALL. If you have granted it, revoke it by naming it explicitly in the *privileges* part of a REVOKE statement:

```
REVOKE GRANT OPTION ON sales.* FROM 'alice'@'%.big-corp.com';
```

To revoke a privilege, you must have that privilege yourself, and you must have the GRANT OPTION privilege.

To revoke all privileges held by an account at all levels, use this statement:

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM account;
```

Notice that there is no ON clause in this syntax. It requires the global CREATE USER privilege or the UPDATE privilege for the mysql database.

If you revoke all of an account’s privileges at the database, table, column, or routine level, MySQL removes the corresponding account row from the db, tables_priv, columns_priv, or proc_priv table. Revoking all of an account’s global privileges sets the privilege columns to 'N' in its user table row, but does not delete the row. That is, REVOKE does not delete the account entirely, which means that the user can still connect to the server. To remove an account completely, use DROP USER instead of REVOKE (see Section 12.4.1, “High-Level MySQL Account Management”).

Somewhat paradoxically, there are a few revocation operations that are done with GRANT. For example, if you specify that an account must connect using SSL, there is no REVOKE syntax for rescinding that requirement. Instead, issue a GRANT statement that grants the USAGE privilege at the global level (to leave existing privileges unchanged) and include a REQUIRE NONE clause to indicate that SSL is not required:

```
GRANT USAGE ON *.* TO account REQUIRE NONE;
```

Similarly, if you set up resource limits on a user, you don’t remove those limits with REVOKE. Instead, use GRANT with USAGE to set the limit values to zero (“no limit”):

```
GRANT USAGE ON *.* TO account
  WITH MAX_CONNECTIONS_PER_HOUR 0 MAX_QUERIES_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0;
```

# 12.4.5 Changing Passwords or Resetting Lost Passwords

One way to change or reset an account’s password is to use an UPDATE statement that identifies the User and Host values for the account’s user table row, and then flush the privileges:

```
mysql> USE mysql;
mysql> UPDATE user SET Password=PASSWORD('silicon')
    -> WHERE User='boris' AND Host='localhost';
mysql> FLUSH PRIVILEGES;
```

However, it’s easier to use SET PASSWORD because you name the account using the same format as for other account-management statements, and it’s unnecessary to flush the privileges explicitly:
