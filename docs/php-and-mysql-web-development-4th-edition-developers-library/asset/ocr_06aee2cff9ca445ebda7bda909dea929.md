# 2.2 MySQL Identifier Syntax and Naming Rules

USE db_name;
SHOW TABLES FROM db_name;

To refer to a table, you have two choices:

+   * A fully qualified table name consists of a database identifier and a table identifier:
+     SHOW COLUMNS FROM db_name.tbl_name;
+     SELECT * FROM db_name.tbl_name;

+   * A table identifier by itself refers to a table in the default (current) database. If samppdb
+     is the default database, the following statements are equivalent:
+     SELECT * FROM member;
+     SELECT * FROM samppdb.member;

If no database has been selected, you cannot refer to a table without specifying a database qualifier because it is unclear which database the table belongs to.

The same considerations about qualifying table names apply to names of views (which are “virtual” tables) and stored programs.

To refer to a table column, there are three choices:

+   * A name written as db_name.tbl_name.col_name is fully qualified.
+   * A partially qualified name written as tbl_name.col_name refers to a column in the named table in the default database.
+   * An unqualified name written simply as col_name refers to whatever table is indicated by the surrounding context. The following two queries use the same column names, but the context supplied by the FROM clause of each statement indicates the table from which to select the columns:
+     SELECT last_name, first_name FROM president;
+     SELECT last_name, first_name FROM member;

It’s usually unnecessary to supply fully qualified names, although it’s always legal to do so if you like. If you select a database with a USE statement, that database becomes the default database and is implicit in every unqualified table reference. If you’re using a SELECT statement that refers to only one table, that table is implicit for every column reference in the statement. It’s necessary to qualify identifiers only when a table or database cannot be determined from context. For example, if a statement refers to tables from multiple databases, any table not in the default database must be referenced using the db_name.tbl_name form to let MySQL know which database contains the table. Similarly, if a query uses multiple tables and refers to a column name that is used in more than one table, it’s necessary to qualify the column identifier with a table identifier to make it clear which column you mean.

If you use quotes when referring to a qualified name, quote individual identifiers within the name separately. For example:

SELECT * FROM 'sampdb'.'member' WHERE 'sampdb'.'member'.'member_id' > 100;