The previous example tells `mysql` to change the table in the current database called `names` (`ALTER TABLE names`), add a column named `curdate` (`ADD curdate`), and assign the value of that column to display the current date (`TIMESTAMP data_type`). If you decide later that you want to remove that column, you can remove it by typing the following:

```
```sql
mysql> ALTER TABLE names DROP COLUMN curdate;
```
```

If you want to change the name of an existing column, you can do so using the `CHANGE` option to `ALTER`. Here is an example:

```
```sql
mysql> ALTER TABLE names CHANGE city town varchar(20);
```
```

In the previous example, the `names` table is chosen (`ALTER TABLE names`) to change the name of the `city` column to `town` (`CHANGE city town`). The data type of the column must be entered as well (`varchar(20)`), even if you are not changing it. In fact, if you just want to change the data type of a column, you would use the same syntax as the previous example but you would simply repeat the column name twice. Here is an example:

```
```sql
mysql> ALTER TABLE names CHANGE zipcode zipcode INTEGER;
```
```

The previous example changes the data type of the `zipcode` column from its previous type (`varchar`) to the `INTEGER` type.

# ## Updating and deleting MySQL records

You can select records based on any value you choose and update any values in those records. When you are in your `mysql` session, you can use `UPDATE` to change the values in a selected table. Here is an example:

```
```sql
mysql> UPDATE names SET streetaddr = "933 3rd Avenue" WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```

The previous example attempts to update the `names` table (`UPDATE names`). In this example, each record that has the `firstname` column set to `"Chris"` will have the value of the `streetaddr` column for that record changed to `"933 3rd Avenue"` instead. Note that the `Query` found 1 row that matched. That one row matched was also changed, with no error warnings necessary. You can use any combination of values to match records (using `WHERE`) and change column values (using `SET`) that you would like. After you have made a change, it is a good idea to display the results to make sure that the change was made as you expected. To remove an entire row (that is, one record), you can use the `DELETE` command. For example, if you wanted to delete any row where the value of the `firstname` column is `"Chris"`, you could type the following:

```
```sql
mysql> DELETE FROM names WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
```
```

The next time you display the table, there will no longer be any records where the first name is Chris.