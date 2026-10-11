# # F.18 mysqlshow

*mysqlshow* lists databases, tables within a database, or information about columns or indexes within a table. It acts as a command-line interface to the `SHOW` SQL statement:

```
`mysqlshow [options] [db_name [tbl_name [col_name]]]`
```

If no database name is specified, *mysqlshow* lists all databases on the server host. If a database name but no table name is specified, all tables in the database are listed. If database and table names are specified, but no column name is specified, it lists the columns in the table. If all the names are specified, *mysqlshow* shows information about the given column.

The final argument may contain the `'*` and `_*` SQL wildcard characters, which are treated the same way as for the `LIKE` operator. Output is limited to values that match the wildcards. If the final argument contains the `'*` or `_*` shell wildcard characters, they are treated as `'*` and `_*`, respectively .

# ## F.18.1 Standard Options Supported by mysqlshow

```

```text
--character-sets-dir			--shared-memory-base-name
--compress				--compress
--debug				--passoword		--user
--debug-check			--pipe			--verbose
--debug-info			--port			--version
--default-character-set		--protocol
```

```

--debug-info and --debug-check are available as of MySQL 5.1.14 and 5.1.21, respectively.

The `--verbose` option causes additional columns to be included in the output (tables per database, rows per table, and so forth). The option may be given multiple times. *mysqlshow* also supports the standard SSL options.

# ## F.18.2 Options Specific to mysqlshow

+   * `--count` *(boolean)*
+     
+     Includes the number or rows per table in the output. Counting the rows may be slow for some storage engines. This option was introduced in MySQL 5.0.6.

+   * `--keys`, `~-k` *(boolean)*
+     
+     Shows information about table indexes in addition to information about table columns. This option is meaningful only if you specify a table name.

+   * `--status`, `~-s` *(boolean)*
+     
+     Displays the same kind of table information displayed by the `SHOW TABLE STATUS` statement.