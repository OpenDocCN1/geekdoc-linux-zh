The `--help` option by itself displays only a brief usage message. To see the full help message, use this command:

```
% `mysql` --verbose --help
```

`mysqld` also supports the standard SSL options.

Note that although `--socket` is supported, the corresponding short form (`-s`) is not. On Windows, `--socket` sets the pipe name if the server supports named-pipe connections.

On Unix, if the `-user` option is given, it specifies the username or numeric user ID of the account to use for running the server. In this case, when the server starts, it looks up the user and group ID values of the account from the password file and then changes its user and group IDs to match. In this way, the server runs with the privileges associated with that user, not `root` privileges. (The server must be started as `root` for the `-user` option to be effective; it will not be able to change its user ID otherwise and a warning is issued.)

# F.12.2 Options Specific to `mysqld`

The first list of options here describes general options. It is followed by lists of options specific to Windows, to InnoDB, and to replication.

+   `--allow-suspicious-udfs` *(boolean)*

Enables the server to load older user-defined functions (UDFs) that might define only the symbol corresponding to the function name and not any of the related standard support-routine symbols. This capability is disabled by default as a precaution against loading functions that might not be true UDFs. This option was introduced in MySQL 5.0.3.

+   `--ansi`, `-a`

Tells the server to use standard SQL behavior for certain types of syntax, rather than MySQL-specific syntax. This option can be used to make the server more standards-compliant.

This option is equivalent to using the `--sql-mode` option with the `REAL_AS_FLOAT`, `PIPES_AS_CONCAT`, `ANSI_QUOTES`, `IGNORE_SPACE`, and `ONLY_FULL_GROUP_BY` mode values.

+   `--basedir=`*dir_name*, `-b` *dir_name*

The pathname to the MySQL installation directory. Many other pathnames are resolved in relation to this directory if they are given as relative pathnames.

+   `--big-tables`

Enables large result sets to be processed by saving all temporary results to disk rather than by holding them in memory. This avoids most “table full” messages that occur as a result of having insufficient memory to hold large result sets. This option is unnecessary now because the server automatically saves results to disk as required.