
word as an identifier. If the `ANSI_QUOTES` SQL mode is enabled, identifiers can be quoted within either backticks or double quotes.

- Identifiers may be up to 64 characters long.

In addition, the operating system on which a MySQL server runs may impose other constraints on identifiers. These stem from filesystem naming conventions because database and table names correspond to names of directories and files: Every database is represented in the filesystem by its database directory, and every table, no matter what storage engine is used, is represented in the filesystem by at least an `.frm` file. Therefore, these restrictions apply:

- MySQL allows database and table names to be up to 64 characters long, but the length of names is also bound by the length allowed by your operating system.
- Case sensitivity of the underlying filesystem affects how you name and refer to databases and tables. If the filesystem is case sensitive (as is typical for Unix), the two filenames `abc` and `ABC` refer to different files. If the filesystem is not case sensitive (as for Windows, or for HFS+ filesystems under Mac OS X), `abc` and `ABC` refer to the same file. You should keep this issue in mind if you develop a database on a server that uses case-sensitive filenames and there is a possibility you might move or replicate the database to a server where filenames are not case sensitive.

Before MySQL 5.1.6, additional filesystem-related naming constraints are enforced:

- Database and table names cannot contain characters that are illegal in filenames. However, the rules for legal characters vary per operating system, which means there are characters that MySQL might allow in a name but that you would be well advised to avoid. For example, by using a quoted identifier, you can include a `*` character in a table name on Unix. But Windows does not allow `*` characters in filenames, so you would not be able to replicate or move the table to Windows without renaming it first. It’s best to stick with plain characters and avoid exotic ones.
- A database or table name cannot include the pathname separator character, even if quoted. On Unix and Windows, pathname components are separated by `/` and `\`, respectively, and neither character may be used. Both are disallowed regardless of platform to make it easier to move databases and tables from one platform to another. (For example, if you were allowed to use `/` in the name of a table on Windows, you could not move or replicate the table to Unix.)

The problems just described that are caused by illegal or nonportable characters in filenames go away as of MySQL 5.1.6, because the server encodes special characters in identifiers that may be problematic in filenames. This encoding enables the restriction in names against `/`, `\`, and other characters to be lifted. In a name as used in SQL statements, any character outside the set of digits and Latin letters is mapped in the corresponding filename to `@` followed by an encoded character value. For example, `?` and `!` have encodings of `003f` and `0021`, so a table named `odd?name!` has an `.frm` file named `odd@003fname@0021.frm`. Other files associated with the table are named similarly.

If you upgrade to MySQL 5.1.6 or later from an older version, be sure to tell the server to re-encode any database and table names as necessary by using this command:

```
mysqlcheck --all-databases --check-upgrade --fix-db-names --fix-table-names
```

As mentioned earlier, filesystem case sensitivity affects database and table naming. One way to deal with this issue is to always use names that have a given lettercase. Another is to run the server with the `lower_case_table_names` system variable set to 1, which has two effects:

- The server converts a table's name to lowercase before creating the corresponding disk files.
- When the table is referenced later in a statement, the server converts its name to lowercase before attempting to find the table on disk.

The result of these actions is that names uniformly are treated as not case sensitive, regardless of the filesystem case sensitivity. This makes it easier to move databases and tables between systems. However, if you plan to use this strategy, you should configure the server to set the `lower_case_table_names` variable *before* you start creating databases or tables, not after. If you set the variable after having already created databases or tables that have names that include uppercase characters, the setup will not have the desired effect because you will already have names stored on disk that are not entirely lowercase. To avoid this problem, rename any tables that have names containing uppercase characters to names that are entirely lowercase before setting `lower_case_table_names`. (To rename a table, use `ALTER TABLE` or `RENAME TABLE`.) If you have a lot of tables that need to be re-named, or databases that have names containing uppercase characters, it is easier to dump the databases and then re-create them after setting `lower_case_table_names`:

1. Dump each database using *mysqldump*:
    ```
    mysqldump --databases db_name > db_name.sql
    ```
2. Drop each database with `DROP DATABASE`.
3. Stop the server, reconfigure it to set `lower_case_table_names`, and restart the server.
4. Reload each dump file using *mysql*:
    ```
    mysql < db_name.sql
    ```

With `lower_case_table_names` set, each database and table will be re-created with a lowercase name on disk.

`lower_case_table_names` actually has several possible values. For more information, see Appendix D, “System, Status, and User Variable Reference.”

Falcon handles database and table names in case-insensitive fashion, regardless of the actual `lower_case_table_names` setting.

## 11.2.7 Factors That Affect Maximum Table Size

Table sizes in MySQL are bounded, but sizes are limited by a combination of factors, so it is not always a simple matter to determine precisely what the bounds are.

The operating system imposes a maximum file-size limit. Limits as low as 2GB used to be common, but this is no longer true because the trend has been for operating systems to relax file size constraints over time. The operating system size limit applies to files used to represent tables, such as the `.MYD` and `.MYI` files for a MyISAM table. It also applies to the files that make up any InnoDB tablespace. However, the overall InnoDB shared tablespace size can easily exceed the maximum file size; just configure it to consist of multiple files, each of which can be the maximum file size. Another way to circumvent the file-size limit is to use raw partitions in the InnoDB tablespace. Tablespace components that are on raw partitions can be as large as the partition itself. Instructions for configuring InnoDB are given in Section 12.7.3.1, “Configuring the InnoDB Tablespace.”

In addition to operating-system limits, MySQL has its own internal limits on table sizes. These vary by storage engine:

- For MyISAM tables, the `.MYD` and `.MYI` files are limited to 256TB apiece by default. However, by using the `AVG_ROW_LENGTH` and `MAX_ROWS` options when you create the table, the files can be up to 65,536TB each. (See the description of `CREATE TABLE` in Appendix E, “SQL Syntax Reference.”) These options affect internal row pointer width, which determines the maximum number of rows the table can hold. If a MyISAM table has grown to its maximum size and you are getting error 135 or 136, you can use `ALTER TABLE` to increase the option values. To change the default MyISAM pointer width directly, set the `myisam_data_pointer_size` system variable; the new setting applies to tables created thereafter.
- The maximum size of a MERGE table is the sum of the maximum sizes of its constituent MyISAM tables.
- For InnoDB, the maximum size of the InnoDB shared tablespace is 4 billion pages, where the default page size is 16KB. (MySQL can be recompiled from source to use an InnoDB page size ranging from 8KB to 64KB.) The maximum tablespace size also is the bound on the size of any individual InnoDB table stored in the tablespace. If InnoDB is configured to use individual tablespaces, each table's contents are stored in its `.ibd` file. In this case, InnoDB table size is bound by operating system file-size limits.
- Falcon tablespace files have a maximum size of 128TB, and Falcon tables are limited to $2^{33}$ rows.

For storage engines that represent data and indexes in separate files, a table's size limit is reached when any of its individual files hits the file-size limit. For a MyISAM table, the
