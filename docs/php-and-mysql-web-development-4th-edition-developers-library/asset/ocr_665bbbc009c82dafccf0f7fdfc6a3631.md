To match a literal instance of a wildcard character in a **LIKE** pattern, precede it with a backslash. Generally, this is done to match a literal `"_"`, which occurs frequently in database, table, and column names.

Any **SHOW** statement that supports a **LIKE** clause can also be written to use a **WHERE** clause. The **SHOW** statement still displays a fixed set of columns, but **WHERE** provides more flexibility about specifying which rows to return. The **WHERE** clause should refer to the columns displayed by the **SHOW** statement. If the column name is a reserved word such as **KEY**, specify it as a quoted identifier. This statement determines which column in the *student* table is the primary key:

```
mysql> SHOW COLUMNS FROM student WHERE `Key` = 'PRI';
```

| Field | Type | Null | Key | Default | Extra |
|:---|:---|:---|:---|:---|:---|
| student_id | int(10) unsigned | NO | PRI | NULL | auto_increment |

It's sometimes useful to be able to tell from within an application whether a given table exists. You can use **SHOW TABLES** to find out (but remember that **SHOW TABLES** does not list **TEMPORARY** tables):

```
SHOW TABLES LIKE 'tbl_name*';
SHOW TABLES FROM db_name LIKE 'tbl_name*';
```

If the **SHOW TABLES** statement lists information for the table, it exists. It's also possible to determine table existence, even for **TEMPORARY** tables, with either of the following statements:

```
SELECT COUNT(*) FROM tbl_name;
SELECT * FROM tbl_name WHERE FALSE;
```

Each statement succeeds if the table exists, and fails if it doesn't. The first statement is most appropriate for MyISAM tables, for which `COUNT(*)` with no **WHERE** clause is highly optimized. It's not so good for InnoDB tables, which require a full scan to count the rows. The second statement is more general because it runs quickly for any storage engine. These statements are most suitable for use within application programming languages such as Perl or PHP because you can test the success or failure of the query and take action accordingly. They're not especially useful in a batch script that you run from `mysql` because you can't do anything if an error occurs except terminate (or ignore the error, but then there's obviously no point in running the query at all).

To determine the storage engine for individual tables, you can use **SHOW TABLE STATUS** or **SHOW CREATE TABLE**. The output from either statement includes a storage engine indicator.