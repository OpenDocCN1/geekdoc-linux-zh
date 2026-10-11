+   * `--parallel-recover`, `-p`
+   
+       Performs recovery the same way as for `--recover`, but rebuild the indexes in parallel using multiple threads. This can be faster than a non-parallel rebuild, but this option should be considered experimental.

+   * `--quick`, `-q` *(`boolean`)*
+   
+       This option is used in conjunction with `--recover` for faster repair than when `--recover` is used alone. The data file is not touched when both options are given. To force the program to modify the data file if duplicate key values are found, specify the `--quick` option twice.

+   * `--read-only`, `-T`
+   
+       Causes the table not to be marked as having been checked.

+   * `--recover`, `-r`
+   
+       Performs a normal recovery operation. This can fix most problems except the occurrence of duplicate values in an index that should contain only unique values.

+   * `--safe-recover`, `-O`
+   
+       Performs recovery using a method that is slower than one used for `--recover`, but that can fix a few problems that `--recover` cannot. `--safe-recover` also uses less disk space than `--recover`.

+   * `--set-auto-increment[={n}|-A{n}]`
+   
+       Sets the AUTO_INCREMENT counter so that subsequent sequence values start at *n* (or at a higher value if the table already contains rows with AUTO_INCREMENT values as large as *n*). If no value *n* is specified, this option sets the next AUTO_INCREMENT value to one greater than the current maximum value stored in the table.
+   
+       If *n* is specified after *-A*, there must be no intervening space or the value will not be interpreted correctly.
+   
+       You can set the AUTO_INCREMENT value for a MyISAM table without using myisamchk by issuing a statement of the following form:
+       ```sql
+       ALTER TABLE tbl_name AUTO_INCREMENT = n;
+       ```

+   * `--set-character-set=charset`
+   
+       The character set to use for rebuilding and sorting table index entries. This option was removed in MySQL 5.0.3 and replaced with `--set-collation`.

+   * `--set-collation=collation`
+   
+       The collation to use for rebuilding and sorting table index entries. (The collation name implies the character set name.) This option was introduced in MySQL 5.0.3 and replaces `--set-character-set`.

+   * `--sort-index`, `-S`
+   
+       Sorts the index blocks to speed up sequential block reads for subsequent retrievals.