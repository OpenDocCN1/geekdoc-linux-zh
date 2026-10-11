
## 14.6.2 Using mysqlcheck to Check and Repair Tables

The mysqlcheck program provides a command-line interface to the CHECK TABLE and REPAIR TABLE statements. It connects to the server and issues the appropriate statements for you based on the options you specify. Therefore, mysqlcheck can check or repair tables for the same storage engines as CHECK TABLE and REPAIR TABLE.

Typically, you invoke mysqlcheck with a database name, optionally followed by one or more table names. With just a database name, mysqlcheck checks all the tables in the database:

```
% mysqlcheck sampdb
```

With table names following the database name, mysqlcheck checks only those tables:

```
% mysqlcheck sampdb president member
```

If you specify the --databases option, all following arguments are interpreted as database names and mysqlcheck checks all the tables in each database:

```
% mysqlcheck --databases sampdb test
```

If you specify --all-databases, mysqlcheck checks all tables in all databases. No database or table name arguments are needed:

```
% mysqlcheck --all-databases
```

mysqlcheck is more convenient than issuing the CHECK TABLE and REPAIR TABLE statements directly, because those statements require that you explicitly name each table to be checked or repaired. With mysqlcheck, it’s much easier to check all tables in a database: It looks up the names of the tables in the database for you and constructs statements that name the appropriate tables.

By default, mysqlcheck checks tables using a medium check, but supports options that enable explicit selection of the type of operation to perform. The following table shows some mysqlcheck options and the CHECK TABLE options to which they correspond. (As with CHECK TABLE, these options apply to MyISAM tables but may not be used by other storage engines.)

| mysqlcheck Option | CHECK TABLE Option |
|:------------------|:-------------------|
| --check-only-changed | CHANGED |
| --extend | EXTENDED |
| --fast | FAST |
| --medium-check | MEDIUM |
| --quick | QUICK |

mysqlcheck can also perform table repair operations, but only for MyISAM tables. The following table shows some mysqlcheck options and the REPAIR TABLE options to which they correspond. (As with REPAIR TABLE, these options apply to MyISAM tables but may not be used by other storage engines.)

| mysqlcheck Option | REPAIR TABLE Option |
|:------------------|:-------------------|
| --repair | no options (performs a standard repair operation) |
| --repair --extended | EXTENDED |
| --repair --quick | QUICK |
| --repair --use-frm | USE_FRM |

## 14.6.3 Using myisamchk to Check and Repair Tables

The myisamchk utility can check and repair MyISAM tables. myisamchk does its work by accessing table files directly, so before invoking it, it is advisable to stop the server to prevent the server from accessing the table files at the same time as myisamchk. If you leave the server running, make sure you read Section 14.2.1, “Locking Individual Tables for Read-Only or Read/Write Access.” That section discusses the proper locking protocols for preventing the server from using a table at the same time that you’re performing checking or repair procedures on it with myisamchk. The following discussion assumes that you have either stopped the server or are using the appropriate locking protocol.

myisamchk makes no assumptions about where tables are located. To run it, specify the pathnames to the table files you want to use. It’s most convenient to do this if you’re in the directory that contains the tables. Typically, you change location into the relevant database directory first before invoking myisamchk, and then tell it which tables you want to check or repair, along with the options that indicate what type of operation to perform:

```bash
% myisamchk options tbl_name ...
```

A tbl_name argument can be either a table name or the name of the table’s index file. These commands are equivalent:

```bash
% myisamchk member
% myisamchk member.MYI
```

To name all the relevant index files in the database directory, you can use a filename pattern (assuming that your command interpreter understands and expands wildcards):

```bash
% myisamchk options *.MYI
```

If you don’t want to perform a myisamchk maintenance operation on the original table files, copy them to another directory and then work with the copies in that directory.

### 14.6.3.1 Checking Tables with myisamchk

*myisamchk* provides table-checking methods that vary in how thoroughly they examine a table. To perform a normal table check, use either of the following commands:

```bash
% myisamchk tbl_name
% myisamchk --check tbl_name
```

*myisamchk*'s default action with no options is --check, so those commands are equivalent.

The normal check method usually is sufficient to identify problems. If it reports no errors but you still suspect damage (perhaps because queries are no seem to return the correct results), perform an intermediate-level check by specifying the --medium-check option. This is somewhat slower but more thorough. Finally, you can perform the most extensive check by specifying the --extend-check option. This can be very slow, but it is extremely thorough. For each row in the table's data file, the associated key for every index in the index file is checked to make sure it really points to the correct row.

If no errors are reported for a check with --extend-check, you can be sure your table is okay. If you still have problems with the table, the cause must lie elsewhere. Re-examine any statements that seem to yield problematic results to verify that they are written correctly. If you believe the problem might be with the MySQL server, consider filing a bug report or upgrading to a newer version.

If *myisamchk* reports that a table has errors, you should try to repair it.

### 14.6.3.2 Repairing Tables with myisamchk

To perform a repair operation on a table with *myisamchk*, use the following procedure. It first tries the repair types that are faster but less thorough, and then escalates to slower but more thorough methods if faster methods fail to correct the problems. Before using the repair procedure, make copies of the table files in case something goes wrong. That is unlikely, but if it happens, you can make a new copy of the table from the copied files and try a different recovery method.

> Note
> If the table contains any FULLTEXT indexes, it might be necessary to use additional myisamchk options during repairs. For details, see the FULLTEXT-related notes in the myisamchk description in Appendix F.

- 1. Try to fix the table using the --recover option. Use the --quick option as well to attempt recovery based only on the contents of the index file without touching the data file:
  % myisamchk --recover --quick tbl_name
- 2. If problems remain, rerun the command without the --quick option to enable myisamchk to modify the data file, too:
  % myisamchk --recover tbl_name
- 3. If that doesn't work, try the `--safe-recover` repair mode. This is slower than regular recovery mode, but is capable of fixing a few problems that `--recover` mode will not:
  `% myisamchk --safe-recover tbl_name`
  It's possible when you run these commands that `myisamchk` will stop with an error message of the form `can't create new temp file: filename`. Typically, this indicates the presence of a temporary file that was left around from a previous failed repair attempt. To force removal of the temporary file, repeat the command but add the `--force` option.

If the preceding repair procedure fails to repair the table, your index file may be missing or damaged beyond repair. It's also possible, although unlikely, that the table's `.frm` format file is missing. In either of these cases, you'll need to replace the affected files, and then try the repair procedure again.

To regenerate the index file for a table `t`, use this procedure if you have the table's format file, `t.frm`:

- 1. Change location into the database directory that contains the crashed table.
- 2. Move the table's data file, `t.MYD`, to a safe place.
- 3. Invoke `mysql` and re-create a new empty table by executing the following statement:
  `mysql>` TRUNCATE TABLE t;
  TRUNCATE TABLE uses the table format file, `t.frm`, to regenerate new data and index files from scratch.
- 4. Exit `mysql` and move the original data file back into the database directory, replacing the new empty data file you just created. That creates a mismatch between the data file and the index file, but the index file has a legal internal structure that the server can interpret and rebuild based on the contents of the data file and table format file.
- 5. Attempt a table repair again using the procedure at the beginning of this section.

If you don't have the table's `.frm` format file, you'll need to recover it from your backup files first. Then use the procedure at the beginning of this section. If you are missing the `.frm` file and also have no backup, but you know the CREATE TABLE statement that must be issued to create the table, you still might be able to repair it as follows:

- 1. Change location into the database directory that contains the crashed table.
- 2. Move the table's data file, `t.MYD`, to a safe place. If you want to try to use the index file, `t.MYI`, move that, too.
- 3. Invoke `mysql` and issue the CREATE TABLE statement that creates the table. This creates new `.frm`, `.MYD`, and `.MYI` files.
- 4. Exit `mysql` and move the original data file back into the database directory, replacing the new data file you just created. If you moved the index file in step 2, move it back into the database directory, too.
