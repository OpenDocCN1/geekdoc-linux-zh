On Windows, the user can connect by specifying a host value of `localhost` or `127.0.0.1`. Both of these connections are made using TCP/IP, except that if the server supports shared-memory connections, a connection to `localhost` is made using shared memory by default. If the server supports named-pipe connections, the user can connect through the pipe by specifying a hostname of `\.` (period).

If the username or hostname part of an *account* value can be used as an unquoted identifier, you need not quote it. If it contains any special characters such as `"` or `'` or `%`, you must quote it. For example, in `boris@localhost`, both parts are legal without quotes. However, it is always safe to use quotes, and the examples in this book do so as a rule. Usernames and hostnames can be quoted either with string quoting characters or identifier quoting characters. Quote the username and hostname separately: Use `'boris'@'localhost'`, not `'boris@localhost'`.

If you give no hostname part at all in an account specifier, it's the same as using a host part of `%`. Thus, `max` and `max'@'%'` are equivalent *account* values. This means that if you intend to specify an account of `boris'@'localhost'` but mistakenly write `'boris@localhost'` instead, MySQL will accept it as legal. What happens is that MySQL interprets `'boris@localhost'` as containing only a user part and adds the default host part of `%` to it, resulting in an effective account name of `boris@localhost'@'%'`. To avoid this, remember to quote the user and host parts of account names separately.

# ## 12.4.1.2 Specifying the Local Hostname in Account Names

It's common to have problems connecting from the server host if you use the server's hostname rather than `localhost`. This can occur due to a mismatch between the way the name is specified in the grant tables and the way DNS name resolver reports the name to programs. Suppose that the server host's fully qualified name is `cobra.snake.net`. If the resolver reports an unqualified name, such as `cobra`, but the grant tables contain rows with the fully qualified name (or vice versa), this mismatch will occur.

To determine if this is happening on your system, try connecting to the local server using a `-h` option that specifies the name of your host:

```
```
mysql -h cobra.snake.net
```
```

Then look in the server's general log file. How does the server write the hostname there when it reports the connection attempt? Is the name in unqualified or fully qualified form? That tells you how you'll need to specify the hostname part when you use it in account names.

# ## 12.4.2 Granting Privileges

To give access privileges to an account, use the `GRANT` statement, which looks like this:

```
```sql
GRANT privileges (columns)
ON what
TO account [IDENTIFIED BY 'password']
```
```