You can see that the only table defined so far for the allusers database is the one called name.

+   3. **For displaying the format of the name table, type the following command at the `mysql>` prompt:**
+   ```sql
+   mysql> DESCRIBE name;
+   ```
+   The format of the name table appears, as follows:

```text
+------------+------------+------+-----+-------+
| Field      | Type       | Null | Key | Default | Extra |
+------------+------------+------+-----+-------+
| firstname  | varchar(20)| NO   |     |       |
| lastname   | varchar(20)| NO   |     |       |
| streetaddr | varchar(30)| NO   |     |       |
| city       | varchar(20)| NO   |     |       |
| state      | varchar(20)| NO   |     |       |
| zipcode    | varchar(20)| NO   |     |       |
+------------+------------+------+-----+-------+
```

+   4. **For adding data to the new table, you can use the `INSERT INTO` command from the `mysql>` prompt. Here is an example of how to add a person’s name and address to the new table:**
+   ```sql
+   mysql> INSERT INTO name
+       -> VALUES ('Jay','Bharati','J P Road Andheri',
+       -> 'Mumbai','MH','400058');
+   ```
+   In this example, the `INSERT INTO` command identifies the name table. Then it indicates that values for a record in that table include the name Jay Bharati at the address J.P. Road Andheri, Mumbai, MH 400058

+   5. **For checking whether the data has been properly entered into the new table, type the following command from the `mysql>` prompt:**
+   ```sql
+   mysql> SELECT * FROM name;
+   ```
+   The output of the preceding command appears, as follows:

```text
+-----------+----------+---------------+-------+-------+---------+
| firstname | lastname | streetaddr    | city  | state | zipcode |
+-----------+----------+---------------+-------+-------+---------+
| Jay       | Bharati  | J P Road Andheri | Mumbai | MH | 400058  |
+-----------+----------+---------------+-------+-------+---------+
```

The resulting output shows the data you just entered, displayed in the columns you defined for the name table. If you like, you can continue adding data in this way.
Typing each data item individually can be tedious. As an alternative, you can add your data to a plain-text file and load it into your MySQL database, as described in the following section.