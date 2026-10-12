```
| Tables in allusers |
+---------------------+
| names               |
+---------------------+
1 row in set (0.00 sec)
```

You can see that the only table defined so far for the allusers database is the one called names.

+   3. To display the format of the names table, type the following command at the mysql> prompt:

```
mysql> DESCRIBE names;
```

| Field      | Type         | Null | Key | Default | Extra |
|------------|--------------|------|-----|---------|-------|
| firstname  | varchar(20)  |      |     |         |       |
| lastname   | varchar(20)  |      |     |         |       |
| streetaddr | varchar(30)  |      |     |         |       |
| city       | varchar(20)  |      |     |         |       |
| state      | varchar(20)  |      |     |         |       |
| zipcode    | varchar(10)  |      |     |         |       |

+   4. To add data to the new table, you can use the `INSERT INTO` command from the mysql> prompt. Here is an example of how to add a person's name and address to the new table:

```
mysql> INSERT INTO names
    -> VALUES ('Jerry','Wingnut','167 E Street',
    -> 'Roy','UT','84103');
```

In this example, the `INSERT INTO` command identifies the names table. Then it indicates that values for a record in that table include the name Jerry Wingnut at the address 167 E Street, Roy, UT 84103.

+   5. To check that the data has been properly entered into the new table, type the following command from the mysql> prompt:

```
mysql> SELECT * FROM names;
```

| firstname | lastname | streetaddr   | city  | state | zipcode |
|-----------|----------|--------------|-------|-------|---------|
| Jerry     | Wingnut  | 167 E Street | Roy   | UT    | 84103   |

The resulting output shows the data you just entered, displayed in the columns you defined for the names table. If you like, you can continue adding data in this way.