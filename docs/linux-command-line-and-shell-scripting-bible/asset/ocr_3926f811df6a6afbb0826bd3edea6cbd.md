# Part V Advanced Topics

or, in PostgreSQL:

```
[rich@textbox ~] psql test
Welcome to psql 8.2.6, the PostgreSQL interactive terminal.

t=> INSERT INTO employees VALUES (1, 'Blum', 'Rich', 25000.00);
INSERT 0 1
test=>
```

Since the new user account in both MySQL and PostgreSQL has privileges to insert data, you can log in using that account. The INSERT command pushes the data values you specify into the data fields in the table. If you attempt to add another record that duplicates the empid data field value, you'll get an error message:

```
mysql> INSERT INTO employees VALUES (1, 'Blum', 'Barbara', 45000.00);
ERROR 1062 (23000): Duplicate entry '1' for key key
```

However, if you change the empid value to a unique value, everything should be OK:

```
mysql> INSERT INTO employees VALUES (2, 'Blum', 'Barbara', 45000.00);
Query OK, 1 row affected (0.00 sec)
```

You should have two data records in your table.

If you need to remove data from your table, you use the DELETE SQL command. However, you need to be very careful with it.

The basic DELETE command format is:

```
DELETE FROM table;
```

where table specifies the table to delete records from. There's just one small problem with this command: it removes all of the records in the table.

To specify a single record or a group of records to delete, you must use the WHERE clause. The WHERE clause allows you to create a filter that identifies which records to remove. You use the WHERE clause like this:

```
DELETE FROM employees WHERE empid = 2;
```

This restricts the deletion process to all of the records that have an empid value of 2. When you execute this command, the mysql program returns a message indicating how many records matched the filter:

```
mysql> DELETE FROM employees WHERE empid = 2;
Query OK, 1 row affected (0.29 sec)
```

As expected, only one record matched the filter and was removed.

662