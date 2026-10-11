
On Windows, the user can connect by specifying a host value of `localhost` or `127.0.0.1`. Both of these connections are made using TCP/IP, except that if the server supports shared-memory connections, a connection to `localhost` is made using shared memory by default. If the server supports named-pipe connections, the user can connect through the pipe by specifying a hostname of `\.` (period).

If the username or hostname part of an *account* value can be used as an unquoted identifier, you need not quote it. If it contains any special characters such as `"` or `'` or `%`, you must quote it. For example, in `boris@localhost`, both parts are legal without quotes. However, it is always safe to use quotes, and the examples in this book do so as a rule. Usernames and hostnames can be quoted either with string quoting characters or identifier quoting characters. Quote the username and hostname separately: Use `'boris'@'localhost'`, not `'boris@localhost'`.

If you give no hostname part at all in an account specifier, it's the same as using a host part of `%`. Thus, `max` and `max'@'%'` are equivalent *account* values. This means that if you intend to specify an account of `boris'@'localhost'` but mistakenly write `'boris@localhost'` instead, MySQL will accept it as legal. What happens is that MySQL interprets `'boris@localhost'` as containing only a user part and adds the default host part of `%` to it, resulting in an effective account name of `boris@localhost'@'%'`. To avoid this, remember to quote the user and host parts of account names separately.

### 12.4.1.2 Specifying the Local Hostname in Account Names

It's common to have problems connecting from the server host if you use the server's hostname rather than `localhost`. This can occur due to a mismatch between the way the name is specified in the grant tables and the way DNS name resolver reports the name to programs. Suppose that the server host's fully qualified name is `cobra.snake.net`. If the resolver reports an unqualified name, such as `cobra`, but the grant tables contain rows with the fully qualified name (or vice versa), this mismatch will occur.

To determine if this is happening on your system, try connecting to the local server using a `-h` option that specifies the name of your host:

```
mysql -h cobra.snake.net
```

Then look in the server's general log file. How does the server write the hostname there when it reports the connection attempt? Is the name in unqualified or fully qualified form? That tells you how you'll need to specify the hostname part when you use it in account names.

### 12.4.2 Granting Privileges

To give access privileges to an account, use the `GRANT` statement, which looks like this:

```sql
GRANT privileges (columns)
ON what
TO account [IDENTIFIED BY 'password']
[REQUIRE encryption requirements] [WITH grant_or_resource_management_options];
```

If the named account exists, GRANT modifies its privileges. If the account does not exist, GRANT creates it with the given privileges. To avoid the possibility of GRANT creating a new account that has no password (and thus is insecure), enable the `NO_AUTO_CREATE_USER` SQL mode. This mode is available as of MySQL 5.0.2 and prevents GRANT from creating the account unless an `IDENTIFIED BY` clause is present.

Several of these clauses are optional and need not be specified at all. In general, you'll most commonly use the following parts:

- *privileges* indicates the privileges to assign to the account. For example, the `SELECT` privilege enables a user to issue SELECT statements and the `SHUTDOWN` privilege enables the user to shut down the server. Multiple privileges can be named, separated by commas.
- *columns* indicates the columns to which a privilege applies, separated by commas and listed within parentheses. This is optional, and you use it only to set up column-specific privileges. The column list must follow the name of each privilege to which it applies.
- *what* indicates the level at which the privileges apply. The most powerful level is the global level, for which any given privilege applies to all databases and all tables. Global privileges can be thought of as superuser privileges. Privileges also can be made database-specific, table-specific, column-specific (if you specify a columns clause), or routine-specific.
- *account* indicates which account is being granted the privileges. The account format is `user_name'@'host_name`, as described in Section 12.4.1.1, “Specifying Account Names.”
- *password* indicates the password to assign to the account. This is optional and is unnecessary if the account already exists and has a password. If you include the `IDENTIFIED BY` clause for an existing account, the new password replaces the current one. As with CREATE USER, when you do use `IDENTIFIED BY`, the password value should be the literal text of the password. GRANT will encode the password for you; don't use the `PASSWORD()` function.

The REQUIRE and WITH clauses are optional. REQUIRE is used for setting up accounts that must connect over secure connections using SSL. WITH is used to grant the `GRANT OPTION` privilege that enables the account to give its own privileges to other users. WITH also is used to specify resource management options that enable you to place limits on how many connections or statements an account can use per hour. These options help you prevent the account from hogging the server.

To specify what an account can do, it’s generally possible to figure out the kind of `GRANT` statement to issue by asking these questions:

- What type of access should the account be given? That is, what level of privileges should the user have, and what should they apply to?
- Are secure connections required?
- Should the user be allowed to administer privileges?
- Should the user’s resource consumption be limited?

The following sections show how to answer these questions and provide examples that illustrate how to use the various clauses of the `GRANT` statement.

#### 12.4.2.1 Defining the Privileges an Account Has

You can grant several types of privileges. These are summarized in Table 12.3, Table 12.4, and Table 12.5, and are described in more detail in Chapter 13, “Access Control and Security.” That chapter discusses the privileges in terms of both their purpose and their relationship to the underlying grant tables.

**Table 12.3 Administrative Privileges**

| Privilege Name | Operation Enabled by Privilege |
|---|---|
| CREATE USER | Use high-level account-management statements |
| FILE | Read and write files on the server host |
| GRANT OPTION | Grant the account’s privileges to other accounts |
| PROCESS | View information about the threads executing within the server |
| RELOAD | Reload the grant tables or flush the logs or caches |
| REPLICATION CLIENT | Ask about master and slave server locations |
| REPLICATION SLAVE | Act as a replication slave server |
| SHOW DATABASES | See all database names with SHOW DATABASES |
| SHUTDOWN | Shut down the server |
| SUPER | Kill threads and perform other supervisory operations |

**Table 12.4 Object Privileges**

| Privilege Name | Operation Enabled by Privilege |
|---|---|
| ALTER | Alter tables and indexes |
| ALTER ROUTINE | Alter or drop stored functions and procedures |
| CREATE | Create databases and tables |
| CREATE ROUTINE | Create stored functions and procedures |
| CREATE TEMPORARY TABLES | Create temporary tables using the `TEMPORARY` keyword |
| CREATE VIEW | Create views |
| DELETE | Delete rows from tables |
| DROP | Remove databases, tables, and other objects |
| EVENT | Create, drop, or alter events for the event scheduler |
| EXECUTE | Execute stored functions and procedures |
| INDEX | Create or drop indexes |
| INSERT | Insert new rows into tables |
| LOCK TABLES | Explicitly lock tables with `LOCK TABLES` statements |
| REFERENCES | Unused (reserved for future use) |
| SELECT | Retrieve rows from tables |
| SHOW VIEW | See view definitions with `SHOW CREATE VIEW` |
| TRIGGER | Create or drop triggers |
| UPDATE | Modify table rows |

**Table 12.5 Miscellaneous Privileges**

| Privilege Name | Operation Enabled by Privilege |
|---|---|
| `ALL` (`[PRIVILEGES]`) | All operations (except `GRANT`) |
| `USAGE` | A special “no privileges” privilege |

The privileges shown in Table 12.3 are administrative privileges. Normally, you grant them relatively sparingly because they enable users to affect the operation of the server. (The `SHUTDOWN` privilege is not one you should hand out on an everyday basis, for example.) The privileges in Table 12.4 apply to databases, tables, columns, and stored routines. They control access to data managed by the server. The privilege specifiers in Table 12.5 are special. `ALL` means “all privileges” (except that it does not include the `GRANT OPTION` privilege). `USAGE` means “no privileges.” That is, “create the account, but don’t grant it any privileges.” `USAGE` also can be used to modify non-privilege-related aspects of an existing account without changing its current privileges. (See Section 12.4.2.2, “Using the ‘No Privileges’ `USAGE` Privilege.”)

`CREATE VIEW` and `SHOW VIEW` were introduced in MySQL 5.0.1. `ALTER ROUTINE`, `CREATE ROUTINE`, and `CREATE USER` were introduced in MySQL 5.0.3, which is also the version in which the `EXECUTE` privilege became operational. `EVENT` and `TRIGGER` were introduced in MySQL 5.1.6. (Before 5.1.6, `SUPER` rather than `TRIGGER` is required to manipulate triggers.)
