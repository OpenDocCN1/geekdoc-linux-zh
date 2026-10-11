latter property is desirable for member ID values, because it prevents us from using the same ID twice by mistake. Besides, MySQL requires every `AUTO_INCREMENT` column to have some kind of index, so the table definition would be illegal without one. (Any PRIMARY KEY column must also be NOT NULL, so if we omitted NOT NULL from the `member_id` definition, MySQL would add it automatically.)

If you don't understand that stuff about `AUTO_INCREMENT` and PRIMARY KEY, just think of them as giving us a magic way of generating indexed ID numbers. It doesn't particularly matter what the values are, as long as they're unique for each member. (When you're ready to learn more about how to use `AUTO_INCREMENT` columns, Chapter 3, “Data Types,” covers them in detail.)

The *expiration* column is a DATE. It allows null values, so it has a default value of `NULL` as well. `NULL` which means no date has been entered. The reason for this is that, as mentioned earlier, we're using the convention that *expiration* can be NULL to indicate which members have a lifetime membership.

Now that you've told MySQL to create a couple of tables, check to make sure that it did so as you expect. In *mysql*, issue the following statement to see the structure of the *president* table:

```
```
mysql> DESCRIBE president;
```

```

| Field       | Type         | Null | Key | Default | Extra |
|-------------|--------------|------|-----|---------|-------|
| last_name   | varchar(15)  | NO   |     |         |       |
| first_name  | varchar(15)  | NO   |     |         |       |
| suffix      | varchar(5)   | YES  |     | NULL    |       |
| city        | varchar(20)  | NO   |     |         |       |
| state       | varchar(2)   | NO   |     |         |       |
| birth       | date         | NO   |     |         |       |
| death       | date         | YES  |     | NULL    |       |


If you issue a `DESCRIBE` member statement, *mysql* will show you similar information for the member table.

`DESCRIBE` is useful when you forget the name of a column in a table, or need to know its data type or how wide it is, and so forth. It's also useful for finding out the order in which MySQL stores columns in table rows. That order is important when you issue `INSERT` or `LOAD DATA` statements that expect column values to be listed in the default column order.

The information produced by `DESCRIBE` can be obtained in different ways. It may be abbreviated as `DESC`, or written as an `EXPLAIN` or `SHOW` statement. The following statements all are synonymous:

```
```
DESCRIBE president;
DESC president;
EXPLAIN president;
SHOW COLUMNS FROM president;
SHOW FIELDS FROM president;
```

```