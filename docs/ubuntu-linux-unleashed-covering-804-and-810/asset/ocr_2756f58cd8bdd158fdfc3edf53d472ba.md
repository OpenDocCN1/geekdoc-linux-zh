perhaps because we have not listened to it yet. This value, therefore, is optional; it starts empty and can be filled in later.

You are now ready to create a table. As mentioned before, you do this by using the CREATE statement, which uses the following syntax:

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

You should know the following about the CREATE statement:

+   - **SQL commands are not case sensitive**—For example, CREATE TABLE, create table, and Create Table are all valid.
+   - **Whitespace is generally ignored**—This means you should use it to make your SQL commands clearer.

The following example shows how to create the table for the cd_collection database:

```
CREATE TABLE cd_collection
(
  id INT NOT NULL,
  title VARCHAR(50) NOT NULL,
  artist VARCHAR(50) NOT NULL,
  year VARCHAR(50) NOT NULL,
  rating VARCHAR(50) NULL
);
```

Notice that the statement terminates with a semicolon. This is how SQL knows you are finished with all the entries in the statement. In some cases, the semicolon can be omitted, and we will point out these cases when they arise.

# TIP

SQL has a number of reserved keywords that cannot be used in table names or field names. For example, if you keep track of CDs you do want to take with you on vacation, you would not be able to use the field name select because that is a reserved key word. Instead, you should either choose a different name (selected?) or just prefix the field name with an f, such as fselect.

# Inserting Data into Tables

After you create the tables, you can put data into them. You can insert data manually with the INSERT statement, which uses the following syntax:

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

This statement inserts value1, value2, and so on into the table table_name. The values that are inserted constitute one row, or record, in the database. Unless specified otherwise, values are inserted in the order in which the columns are listed in the database table. If, for some reason, you want to insert in a different order (or if you want to insert