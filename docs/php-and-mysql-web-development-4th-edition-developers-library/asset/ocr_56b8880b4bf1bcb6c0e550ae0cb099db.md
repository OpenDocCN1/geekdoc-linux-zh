mysqlampack while it was running, in which case the file safely can be removed. If you know that to be the case, use --force to tell mysampack to pack the table even if the temporary file exists. (Alternatively, remove the temporary file manually.)

+   - `--join=join_tbl, -j join_tbl`

Joins (merges) all the tables named on the command line into a single packed table named `join_tbl`. All the tables to be merged must have the same structure. (Column names, types, and indexes must be identical.) This option is unrelated to `MERGE` tables. The operation does not create the `.frm` file for the output table. You can create it by copying the `.frm` file from one of the source tables after `mysampack` completes.

+   - `--test, -t`

Causes `mysampack` to run in test mode. A packing test is run, and information is printed about the results you would obtain if you actually packed the table.

+   - `--tmpdir=dir_name, -T dir_name`

The pathname of the directory to use for temporary files.

+   - `--wait, -w (boolean)`

Waits and retries if a table is in use. (You should not pack a table if it might be updated while you’re packing it.)

# # F.5 `mysql`

The `mysql` client program enables you to connect to the server, issue SQL statements, and view the results.

```
mysql [options] [db_name]
```

If you specify a `db_name` argument, that database becomes the default database for your session. If you specify no `db_name` argument, `mysql` starts with no default database and you’ll need to either qualify all table references with a database name or issue a `USE db_name` statement to specify a default database.

`mysql` can be run interactively. You can also use it in batch mode to execute statements that are stored in a file if you redirect the input of the command to read from that file. For example:

```
$ mysql -u sampdb -p -h cobra.snake.net sampdb < my_sql_file
```

In interactive mode, when `mysql` starts, it displays a `mysql>` prompt to indicate that it’s waiting for input. To issue a statement, type it in (using multiple lines if necessary) and then indicate the end of the statement by typing `;` (semicolon) or `\g`. `mysql` sends the statement to the server, displays the results, and then prints another prompt to indicate that it’s ready for another statement. `\G` also terminates a statement, but causes statement results to be displayed vertically (that is, with one column value per output line).