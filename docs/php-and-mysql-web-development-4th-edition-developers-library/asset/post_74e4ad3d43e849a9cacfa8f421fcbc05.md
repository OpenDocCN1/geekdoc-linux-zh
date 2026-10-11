
## DEFAULT *default_value*

Specifies the default value for the column. This cannot be used for BLOB or TEXT types, spatial types, or columns with the AUTO_INCREMENT attribute. Except for TIMESTAMP, a default value must be a constant, specified as a number, a string, or NULL. For the rules that MySQL uses for assigning a default value if you include no DEFAULT clause, see Section 3.2.3, “Specifying Column Default Values.”

## AUTO_INCREMENT

This keyword applies only to integer and floating-point data types. An AUTO_INCREMENT column is special in that when you insert NULL into it, the value actually inserted is the next value in the column sequence. Typically, this is one greater than the current maximum value in the column. AUTO_INCREMENT values start at 1 by default. (Some storage engines allow the initial value to be specified with an AUTO_INCREMENT table option. See the discussion of table options that follows.) The column must also be indexed and should be NOT NULL. There can be at most one AUTO_INCREMENT column per table.

## [PRIMARY] KEY

Specifies that the column is a PRIMARY KEY. A PRIMARY KEY must be NOT NULL. MySQL adds NOT NULL to the column definition if you omit it.

## UNIQUE [KEY]

Specifies that the column is a UNIQUE index.

## COMMENT 'str'

A descriptive comment for the column. This attribute is displayed by SHOW CREATE TABLE and SHOW FULL COLUMNS. The comment can contain up to 1024 characters (255 characters before MySQL 5.2.4).

The PRIMARY KEY, UNIQUE, INDEX, FULLTEXT, and SPATIAL clauses specify indexes. PRIMARY KEY and UNIQUE specify indexes that must contain unique values. INDEX and KEY are synonymous; they specify indexes that may contain duplicate values. The index is based on the columns named in index_columns, which is a list of one or more columns in the table separated by commas. If the index name index_name is not specified, MySQL chooses a name automatically based on the name of the first indexed column.

FULLTEXT and SPATIAL indexes are allowed only for MyISAM tables. FULLTEXT indexes are allowed only for non-binary string columns (CHAR, VARCHAR, TEXT), and SPATIAL indexes only for NOT NULL spatial columns.

PRIMARY KEY columns must always be not NULL; MySQL adds NOT NULL to the definition of such columns if you omit it.

For index definitions that include index_type or index_option clauses, some storage engines allow you to specify the indexing algorithm or other index definition modifiers. See the entry for CREATE INDEX for details about which indexing values are allowed in different versions of MySQL. For additional information about index creation, see Section 2.6.4, “Indexing Tables.”

## Table options

Each *table_option* value specifies an additional characteristic of the table, chosen from the following list. Each option setting applies to all storage engines unless otherwise noted. The = in each setting is optional and settings can be separated by whitespace or commas.

- **AUTO_INCREMENT = n**
  The first `AUTO_INCREMENT` value to be generated for the table. This option is effective for MyISAM and MEMORY tables, and for InnoDB tables as of MySQL 5.0.3. For InnoDB tables, the effect is canceled if you restart the server before generating any `AUTO_INCREMENT` values.

- **AVG_ROW_LENGTH = n**
  The approximate average row length of your table. For MyISAM tables, MySQL uses the product of the `AVG_ROW_LENGTH` and `MAX_ROWS` values to determine the maximum data file size. The MyISAM storage engine can use internal row pointers from 2 to 7 bytes wide. The default pointer width is wide enough to allow tables up to 256TB. If you require a larger table (and your operating system supports larger files), the `MAX_ROWS` and `AVG_ROW_LENGTH` table options provide information that allows the MyISAM storage engine to adjust the internal pointer width. A large product of these values causes the engine to use wider pointers, enabling file sizes up to 65,536TB. Conversely, a small product allows the engine to use smaller pointers. This won’t save you much space for a single small table, but the cumulative savings may be significant if you have many of them.
  To size the data pointers directly, set the `myisam_data_pointer_size` system variable before creating the table.

- **[DEFAULT] CHARACTER SET = charset**
  The table’s default character set. *charset* may be a character set name, or `DEFAULT` to use the database character set. This option determines which character set to use for character columns that are defined without an explicit character set. In the following example, `c1` will be assigned the `sjis` character set and `c2` the `ujis` character set:

  ```sql
  CREATE TABLE t
  (
      c1 CHAR(50) CHARACTER SET sjis,
      c2 CHAR(50)
  ) CHARACTER SET ujis;
  ```
  This table option also applies to subsequent table modifications made with `ALTER TABLE` for character column definition changes that do not name a character set explicitly.

- **CHECKSUM = { 0 | 1 }**
  If this option is set to 1, MySQL maintains a live checksum for the table that is updated whenever the table is modified. There is a slight penalty for updates to the table, but the presence of checksums improves the table checking process. (MyISAM tables only)

- **[DEFAULT] COLLATE = collation**
  The table's default character set collation. collation may be a collation name, or DEFAULT to use the default collation of the table character set.

- **COMMENT = 'str'**
  A descriptive comment for the table. This comment is displayed by SHOW CREATE TABLE and SHOW TABLE STATUS. The comment can contain up to 2048 characters (60 characters before MySQL 5.2.4).

- **CONNECTION = 'connect_str'**
  The string that specifies how to connect to the remote server for a FEDERATED table. This option was introduced in MySQL 5.0.13. Older versions should use COMMENT to specify connect_str.

- **DATA DIRECTORY = 'dir_name'**
  This option is used only for MyISAM tables and only on Unix. It indicates the directory where the data (.MYD) file should be written. 'dir_name' must be a full pathname. This option works only if the server is started without the --skip-symbolic-links option. On some Unix variants, symlinks are not thread-safe and are disabled by default.

- **DELAY_KEY_WRITE = { 0 | 1 }**
  If this is set to 1, the key cache is flushed only occasionally for the table, rather than after each insert operation (MyISAM tables only). This improves performance but may require that the table be repaired if a crash occurs.

- **ENGINE = engine_name**
  The storage engine to use for the table. The various storage engines are described in the Section 2.6.1, “Storage Engine Characteristics.” The default engine is MyISAM unless the server has been configured otherwise. You can start the server with a different default engine by using the --default-storage-engine option. The known engine names can be displayed with the SHOW ENGINES statement. If you attempt to create a table using a storage engine that is not available, the effect of the statement is subject to the setting of the NO_ENGINE_SUBSTITUTION SQL mode.

- **INDEX DIRECTORY = 'dir_name'**
  This option is like DATA DIRECTORY but indicates the directory where the index (.MYI) file should be written. It is subject to the same constraints as DATA DIRECTORY.

- **INSERT_METHOD = ( NO | FIRST | LAST )**
  This is used for MERGE tables to specify how to insert rows. A value of **NO** disallows inserts entirely. Values of **FIRST** or **LAST** indicate that rows should be inserted into the first or last of the MyISAM tables that make up the MERGE table.

- **KEY_BLOCK_SIZE = n**
  A suggested size in bytes that the storage engine should use for key blocks in indexes. A value of 0 means to use the default size. This table default can be overridden by index definitions include their own **KEY_BLOCK_SIZE** option. This option was introduced in MySQL 5.1.10.

- **MAX_ROWS = n**
  A hint to the storage engine about the maximum number of rows you plan to store in the table. The table will be created to allow at least this many rows. The description of the **AVG_ROW_LENGTH** option indicates how this value is used.

- **MIN_ROWS = n**
  A hint to the storage engine about the minimum number of rows you plan to store in the table. This option can be used for MEMORY tables to give the MEMORY storage engine a hint about how to optimize memory usage.

- **PACK_KEYS = ( 0 | 1 | DEFAULT )**
  This option controls index compression for MyISAM tables, which enables runs of similar index values to be compressed. The usual effect is an improvement in retrieval performance but an update penalty. A value of 0 specifies no index compression. A value of 1 specifies compression for string (CHAR, VARCHAR, BINARY, VARBINARY) and numeric index values. A value of **DEFAULT** can be used, which specifies compression only for long string columns.

- **PASSWORD = 'str'**
  A password for encrypting the table's format file. This option normally has no effect; it is enabled only for certain support contract customers.

- **ROW_FORMAT = ( DEFAULT | DYNAMIC | FIXED | COMPRESSED | REDUNDANT | COMPACT )**
  The row storage type. For MyISAM tables, a value of **DYNAMIC** or **FIXED** specifies variable-length or fixed-length row format. A value of **COMPRESSED** can be set only by the myisampack program and indicates that the table is compressed and read-only.
  The **REDUNDANT** and **COMPACT** formats apply to InnoDB tables. **COMPACT** format is used by default as of MySQL 5.0.3. The original format can be specified with *row_format* = **REDUNDANT**. A storage engine may ignore this option if the specified row format cannot be used. For example, **FIXED** cannot be used if the table contains **BLOB** or **TEXT** columns. Use *show table status* and check the *Row_format* value to see what format the storage engine actually chose.
