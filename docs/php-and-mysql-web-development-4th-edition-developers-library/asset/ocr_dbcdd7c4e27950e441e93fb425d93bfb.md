To create an empty copy of a table and then populate it from the original table, use CREATE TABLE ... LIKE followed by INSERT INTO ... SELECT:

```
```
CREATE TABLE new_tbl_name LIKE tbl_name;
INSERT INTO new_tbl_name SELECT * FROM tbl_name;
```
```

To create a table as a temporary copy of itself, include the TEMPORARY keyword:

```
```
CREATE TEMPORARY TABLE new_tbl_name LIKE tbl_name;
INSERT INTO new_tbl_name SELECT * FROM tbl_name;
```
```

Using a TEMPORARY table with the same name as the original can be useful when you want to try some statements that modify the contents of the table, but you don’t want to change the original table. To use prewritten scripts that use the original table name, you don’t need to edit them to refer to a different table; just add the CREATE TEMPORARY TABLE and INSERT statements to the beginning of the script. The script will create a temporary copy and operate on the copy, which the server deletes when the script finishes. (However, bear in mind the auto-reconnect caveat noted in Section 2.6.2.3, “Temporary Tables.”)

To insert into the new table only some of the rows from the original table, add a WHERE clause that identifies which rows to select. The following statements create a new table named student_f that contains only the rows for female students in the student table:

```
```
CREATE TABLE student_f LIKE student;
INSERT INTO student_f SELECT * FROM student WHERE sex = 'f';
```
```

If you don’t care about returning the exact column definitions from the original table, CREATE TABLE ... SELECT sometimes is easier to use than CREATE TABLE ... LIKE because it can create and populate the new table in a single statement:

```
```
CREATE TABLE student_f SELECT * FROM student WHERE sex = 'f';
```
```

CREATE TABLE ... SELECT also can create new tables that don’t contain exactly the same set of columns in an existing table. You can use it to cause a new table to spring into existence on the fly to hold the result of an arbitrary SELECT query. This makes it exceptionally easy to create a table fully populated with the data in which you’re interested, ready to be used in further statements. However, the new table can contain strange column names if you’re not careful. When you create a table by selecting data into it, the column names are taken from the columns that you are selecting. If a column is calculated as the result of an expression, the name of the column is the text of the expression, which creates a table with an unusual column name:

```
```
mysql> CREATE TABLE mytbl SELECT PI() * 2;
mysql> SELECT * FROM mytbl;
+----------------+
| PI() * 2       |
+----------------+
| 6.283185       |
+----------------+
```
```