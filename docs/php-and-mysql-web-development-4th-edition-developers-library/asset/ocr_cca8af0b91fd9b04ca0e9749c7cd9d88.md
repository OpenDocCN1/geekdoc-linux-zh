5. Attempt a table repair again using the procedure at the beginning of this section.

# 14.6.3.3 Getting mysamchk to Run Faster

`mysamchk` can take a long time to run, especially if you're working with a large table or using one of the more-extensive checking or repair methods. You can speed up this process by telling `mysamchk` to use more memory when it runs. `mysamchk` has several variables that can be set, the most important of which control the sizes of the buffers that it uses (see following table).

| Variable | Meaning |
| :--- | :--- |
| `key_buffer_size` | Size of buffer used to hold index blocks |
| `read_buffer_size` | Size of buffer used for read operations |
| `sort_buffer_size` | Size of buffer used for sorting |
| `write_buffer_size` | Size of buffer used for write operations |


To find out what values `mysamchk` uses for these variables by default, run it with the `--help` option. To specify a different value, use `--var_name=value` on the command line. For example, if you have sufficient memory to spare, you can tell `mysamchk` to use a 16MB sort buffer and 1MB read and write buffers by invoking it like this:

```
% mysamchk --sort_buffer_size=16M --read_buffer_size=1M \
         --write_buffer_size=1M other-options tbl_name
```

For repair operations, `--sort_buffer_size` applies when the `--recover` option is given, but not with `--safe-recover`. A `--key_buffer_size` setting applies when `--safe-recover` is given or when you check the table with `--extend-check`.

# 14.7 Using Backups for Data Recovery

Recovery procedures involve two sources of information: your backup files and your binary log. Backup files can be either dump files generated with `mysqldump` or files copied using one of the binary backup methods.

The backup files restore tables to the state they were in at the time the backup was performed. The binary log files that were written after the backup contain the statements that have modified the tables since then. `mysqldbinlog` converts these log files back into text SQL statements so that you can execute them with `mysql`. This enables you to reapply the changes made between the time of the backup and the time at which problems occurred.

The recovery procedure varies depending on how much information you must restore. In fact, it may be easier to restore an entire database than a single table, because it's easier to apply the binary log files for a database than for a table.