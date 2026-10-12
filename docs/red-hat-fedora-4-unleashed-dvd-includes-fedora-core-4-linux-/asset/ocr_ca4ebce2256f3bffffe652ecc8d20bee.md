# Creating Tables

As mentioned previously, an RDBMS stores data in tables that look similar to spreadsheets. Of course, before you can store any data in a database, you need to create the necessary tables and columns to store the data. You do this by using the CREATE statement.

For example, the cd_collection table from Figure 20.2 has five columns, or fields: id, title, artist, year, and rating.

SQL provides several column types for data that define what kind of data will be stored in the column. Some of the available types are INT, FLOAT, CHAR, and VARCHAR. Both CHAR and VARCHAR hold text strings, with the difference being that CHAR holds a fixed-length string, whereas VARCHAR holds a variable-length string.

There are also special column types, such as DATE, that only take data in a date format, and ENUMs (enumerations), which can be used to specify that only certain values are allowed. If, for example, you wanted to record the genre of your CDs, you could use an ENUM column that accepts only the values POP, ROCK, EASY_LISTENING, and so on. You will learn more about ENUM later in this chapter.

Looking at the cd_collection table, you can see that three of the columns hold numerical data and the other two hold string data. In addition, the character strings are of variable length. Based on this information, you can discern that the best type to use for the text columns is type VARCHAR, and the best type to use for the others is INT. You should notice something else about the cd_collection table: One of the CDs is missing a rating, perhaps because we have not listened to it yet. This value, therefore, is optional; it starts empty and can be filled in later.

You are now ready to create a table. As mentioned before, you do this by using the CREATE statement, which uses the following syntax:

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

You should know the following about the CREATE statement:

+   * **SQL commands are not case sensitive**—For example, CREATE TABLE, create table, and create Table are all valid. You should get in the habit of using all uppercase for commands because later, when you start writing front ends to your databases in C, Perl, and so on, using all uppercase will make it easier to pick out the SQL code. (Keywords in C, Perl, and so on are almost always lowercase.)
+   * **Whitespace is generally ignored**—This means you should use it to make your SQL commands clearer.

The following example shows how to create the table for the cd_collection database:

```
CREATE TABLE cd_collection
(
  id INT NOT NULL,
```