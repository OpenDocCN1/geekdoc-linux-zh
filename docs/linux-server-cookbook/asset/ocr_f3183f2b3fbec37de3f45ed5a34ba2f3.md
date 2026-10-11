For example, add a new column called \textit{phone} to the previous table created; the following syntax can be used:

```
ALTER TABLE students ADD COLUMN phone CHAR(20) UNIQUE;
```

# ## INSERT statement

This statement is used to insert data in a table; the syntax is as follows:

```
INSERT INTO <target_table> [ ( <target_col_name> [ , … ] ) ]
{
    VALUES ( { <value> | DEFAULT | NULL } [ , … ] ) [ , ( … ) ] |
    <query>
}
```

For example, to insert a new student to the previously created table named \textit{students}, the following syntax will perform it:

```
INSERT INTO students
VALUES(1, "Alberto", "Gonzalez", "64543210");
```

It is possible to specify only the columns where the data will be specified, as is shown in the following example:

```
INSERT INTO students(id, name, lastname)
VALUES(2, "John", "Doe");
```

In the previous example, the field \textbf{phone} will be set to \textbf{null}. If the column is configured to not be blank, an error will be thrown, and the insert will not be performed.

# ## SELECT statement

This statement is used to query data from data. It is possible to query all the data or filter for specific values. It is also possible to show all the columns or specify the columns to be listed. The simple syntax for \textbf{SELECT} is as follows:

```
SELECT [ * | column_list ]
    [FROM table_references]
    [WHERE where_condition]
```

The following example will query for the records inside the table \textit{students} where the column \textit{name} contains the value, Alberto:

```
SELECT * FROM students WHERE name = "Alberto";
```