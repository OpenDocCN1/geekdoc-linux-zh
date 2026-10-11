
# 13.2 External Security: Preventing Unauthorized Network Access

The intent here is to grant the user fred all privileges for the samdb database and to enable him to connect from any host he likes. Unfortunately, the probable result is that fred will be able to connect from any host, except the server host itself! Suppose that the server host is named cobra.snake.net. If fred tries to connect remotely from the host boa.snake.net, the attempt succeeds:

```
$ mysql -p -u fred -h cobra.snake.net samdb
Enter password: cocoa
mysql>
```

But if fred tries to connect locally from the server host cobra.snake.net, the attempt fails, even though fred supplies his password correctly:

```
$ mysql -p -u fred -h localhost samdb
Enter password: cocoa
ERROR 1045 (28000): Access denied for user 'fred@localhost'
(using password: YES)
```

This problem occurs if your user table contains any default anonymous-user rows that have blank usernames. Such rows are created by the `mysql_install_db` initialization script under Unix and are present in the pre-initialized user table included with Windows distributions. (Section 12.1, “Securing a New MySQL Installation,” has a detailed description of the initial user table rows.) The reason the second connection attempt fails is that when the server attempts to validate fred, one of the anonymous-user rows takes precedence over fred’s row in the matching order. The anonymous-user row requires the user to connect with no password (rather than with the password cocoa), so a password mismatch results.

Why does this happen? To understand what’s going on, it’s necessary to consider both how MySQL’s grant tables are set up initially and how the server uses user table rows when it validates client connections. For example, under Unix, when you run the `mysql_install_db` script on cobra.snake.net to initialize the grant tables, the resulting user table contains rows with Host and User values that look like this:

| Host | User |
| :--- | :--- |
| localhost | root |
| cobra.snake.net | root |
| 127.0.0.1 | root |
| localhost | |
| cobra.snake.net | |

The first three rows enable users to connect as root from the local server. The last two rows enable users to connect anonymously from the local server. After the administrator sets up the account for fred with the GRANT statement shown earlier, the user table contains these rows:

| Host | User |
| :--- | :--- |
| localhost | root |
| cobra.snake.net | root |
| 127.0.0.1 | root |
| localhost | |
| cobra.snake.net | |
| % | fred |

But the order of the rows as shown is not the order that the server uses when validating connection requests. Instead, it sorts rows by host first and then by user within host, putting more-specific values first and less-specific values last:

| Host | User |
| :--- | :--- |
| localhost | root |
| localhost | |
| 127.0.0.1 | root |
| cobra.snake.net | root |
| cobra.snake.net | |
| % | fred |

The two rows with localhost in the host column sort together, with the row for root first because that’s a more specific username than the blank value. The rows with cobra.snake.net sort together in a similar way. Furthermore, all of these rows have a literal Host value without any wildcard characters, so they all sort ahead of the row for fred, which does use a wildcard character in its Host value. In particular, both of the anonymous-user rows take precedence over fred’s row in the sort order.

The result is that when fred attempts to connect from the local host, one of the rows with a blank username matches before the row containing % in the Host column. The blank password in the anonymous-user row doesn’t match fred’s password of cocoa, so the connection fails. One implication of this phenomenon is that it is possible for fred to connect from the local host, but only if he specifies no password. Unfortunately, then he will be validated as an anonymous user and won’t have the privileges associated with the fred@% account.

What all this means is that although it’s very convenient to use wildcards when you set up an account for a user who will connect from multiple hosts, the user may have problems connecting from the local host due to the anonymous rows in the user table.

What is the solution to this problem? Actually, you can solve it two ways. First, you can set up a second account for `fred` that explicitly lists `localhost` as the host value:

`GRANT ALL ON sampledb.* TO 'fred'@'localhost' IDENTIFIED BY 'coccol';`

If you do that, the server will sort the rows from the `user` table as follows:

| Host | User |
| :--- | :--- |
| localhost | fred |
| localhost | root |
| localhost | |
| 127.0.0.1 | root |
| cobra.snake.net | root |
| cobra.snake.net | |
| % | fred |

Now when `fred` connects from the local host, the row with `localhost` and `fred` will match ahead of the anonymous-user rows. When he connects from any other host, the row with `%` and `fred` will match. The downside of having two accounts for `fred` is that whenever you want to change his privileges or password, you'll have to make the change twice.

The second solution is much easier: Remove the anonymous accounts from the `user` table with these `DROP USER` statements:

`DROP USER ''@'localhost';`
`DROP USER ''@'cobra.snake.net';`

The remaining `user` table rows sort into this order:

| Host | User |
| :--- | :--- |
| localhost | root |
| 127.0.0.1 | root |
| cobra.snake.net | root |
| % | fred |

Now when `fred` attempts to connect from the local host, he'll succeed, because there won't be any rows in the `user` table that will match ahead of his.

In general, I recommend that if you want to make your life easier as an administrator, you should delete any anonymous-user accounts that are present in the initial grant tables. In my view, these accounts are not very useful, and they tend to cause more problems than they're worth.

The puzzle presented in this section addresses a specific situation, but contains a more general lesson. If privileges for a given account don't work the way you expect, look in the grant tables to see whether there's some row containing `Host` values that are more specific than the row for the user in question and that will match connection attempts by that user. If so, that may explain the problem. You might need to make the user's row more specific, or add another row to cover the more specific case.

### 13.2.4 Grant Table Risks to Avoid

This section describes precautions to observe when you grant privileges, and the attendant risks of unwise choices.

- Avoid creating anonymous-user accounts. Even if they don't have sufficient privileges to cause damage directly, allowing a user to connect still may provide access to that user to look around and gather information such as what databases and tables you have, or to monitor the server with SHOW STATUS and SHOW VARIABLES.

- Find accounts that have no passwords and either remove them or assign passwords. To find such accounts, use this query:

```sql
mysql> SELECT Host, User FROM mysql.user WHERE Password = '';
```

Find accounts that have password hash values in the older pre-MySQL 4.1 format and change them to the more secure password hash format that is used as of MySQL 4.1. Values in the older format have a length of 16 and do not begin with the `*` character, so you can identify them using either of these statements:

```sql
mysql> SELECT Host, User FROM mysql.user WHERE LENGTH(Password) = 16;
mysql> SELECT Host, User FROM mysql.user WHERE Password NOT LIKE '*%';
```

However, that you cannot institute this security measure unless all client programs that connect to your server are from MySQL 4.1 or later and can authenticate using the newer password mechanism. Assuming that you can use newer passwords for all clients, you need only make sure that the server was not started with the `--old-passwords` option, and then use SET PASSWORD to set the password for each account that has an old-format password. The new password format will be used for each account. For additional security, start the server with the `--secure-auth` option. Otherwise, a client can reset its password to the old format with OLD_PASSWORD() and then connect using that password. `--secure-auth` prevents clients from connecting unless they have a new-format password.

- Unless you really need to use patterns in hostname specifiers, avoid doing so when setting up accounts. Broadening the range of hosts from which a given user can connect also broadens the range from which an imposter claiming to be that user can try to break in.

- Grant superuser privileges sparingly. That is, don't enable privileges in user table rows. Those privileges are global and enable the user to affect the operation of your server or to access any database. Grant privileges at a more specific level instead, to restrict user access to particular databases or database objects such as tables or stored routines.

- Don't grant privileges for the `mysql` database that contains the grant tables. A user with privileges for that database may be able to modify its tables to acquire privileges on any other database as well. In effect, granting privileges that enable a user to modify the `mysql` database tables gives that user *all* global privileges: If the user can modify the tables
