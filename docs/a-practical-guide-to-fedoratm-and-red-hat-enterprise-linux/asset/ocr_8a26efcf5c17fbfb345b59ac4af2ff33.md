```
SELECT * FROM stores
name number city
headquarters 4 new york
midwest 5 chicago
west coast 6 san francisco
3 rows in set
```

The *stores* table has 3 columns named **name**, **number**, and **city**. The data type for the **name** and **city** columns is VARCHAR. A VARCHAR column stores a variable-length string without the padding required by a CHAR column. In this example, the **name** and **city** columns can store up to 20 characters each.

The size of a VARCHAR is the sum of the length prefix plus the number of characters in the string being stored. The length prefix for a column declared to hold fewer than 255 characters is 1 byte; larger columns have a 2-byte length prefix. In contrast, a CHAR column always occupies the number of characters it was declared to be.

The number in parentheses in a VARCHAR declaration specifies the maximum number of characters any row in the column can hold. In the example, the **city** column is declared to be VARCHAR(20) so a row in that column cannot hold more than 20 characters. The row with **new york** in the **city** column takes up 9 bytes of storage (8 + 1). If the column had been declared to be CHAR(20), each row would occupy 20 bytes, regardless of the length of the string it held.

# Joins

A join operation combines rows from/across two or more related tables in a database according to some relationship between these tables. Take the **maxdb** database, for example: The **people** table has columns that hold information about employee name, hire date, the store where the employee works, and whether the employee is hourly (as opposed to salaried); the **stores** table has columns that hold information about the store name, number, and city it is located in. With this setup, you cannot determine which city an employee works in by querying either the **people** or **stores** table alone; you must join the tables to get this information.

You join tables using a SELECT statement that specifies a column in each of the tables and the relationship between those columns. The query that would satisfy the example specifies the **store** column in the **people** table and the **number** column in the **stores** table; the relationship between those columns is equality because both of those columns hold the store number. When you equate like values in these columns, you can display **stores** information for each **name** in the **people** table (or **people** information for each [store] **number** in the **stores** table).

The following query selects rows from the **people** and **stores** tables and joins the rows where the value of **store** in the **people** table equals the value of **number** in the **stores** table (**store = number**). This query uses an implicit join; it does not use the **JOIN** keyword. The examples following this one use JOIN. Using this keyword makes no