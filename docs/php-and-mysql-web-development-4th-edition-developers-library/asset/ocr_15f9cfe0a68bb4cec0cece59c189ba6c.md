The standard `--help` option prints the help message with options grouped by function. `mysamchk` also supports `--HELP` and `-H` options that display all options in a single alphabetical list.

# **F.3.2 Options Specific to `mysamchk`**

Some of these options refer to index numbers. Indexes are numbered beginning with 1. You can issue a `SHOW INDEX` statement or use a `mysqlsh --keys` command to determine the index numbering for a particular table. The `Key_name` column in the output lists indexes in the same order that `mysamchk` sees them.

+   
+   *   `--analyze`, `-a`
+       Performs key distribution analysis. This can help the server perform index-based lookups and joins more quickly. To obtain information about key distribution after the analysis, run `mysamchk` again with the `--description` and `--verbose` options.
+   *   `--backup`, `-B`
+       For options that modify the data (.MYD) file, makes a backup using a filename of the form `tbl_name-time.BAK`. `time` is a number representing a timestamp. `mysamchk` creates the backup file in the directory where the table files are located.
+   *   `--block-search=n`, `-b n`
+       Prints out the start of the table row that contains a block starting at block n. This is for debugging only.
+   *   `--check`, `-c`
+       Checks tables for errors. This is the default action if no options are specified.
+   *   `--check-only-changed`, `-C`
+       Checks tables only if they have not been changed since the last check.
+   *   `--correct-checksum`
+       For tables created with the `CHECKSUM = 1` option, ensures that the checksum information in the table is correct.
+   *   `--data-file-length=n`, `-D n`
+       The maximum length in bytes to which the data file should be allowed to grow when rebuilding a data file that has become full. (This occurs when a file reaches the size limit imposed by MySQL or by the file-size constraints of your operating system. It also occurs when the number of rows reaches the limit imposed by internal table data structures.) This option is effective only when used with `--recover` or `--safe-recover`.
+   *   `--description`, `-d`
+       Prints descriptive information about the table.
+