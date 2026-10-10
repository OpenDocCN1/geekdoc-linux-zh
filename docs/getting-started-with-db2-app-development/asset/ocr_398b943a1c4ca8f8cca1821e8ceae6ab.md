# 10.3.3 Inserting, updating and deleting data

Similar to the **SELECT** statement, an **INSERT**, **UPDATE** or **DELETE** SQL statement that is already known at the time the application is written can be executed directly by calling the function `ibm_db.exec_immediate`. For a SQL statement that contains variable inputs or parameter markers, refer to section **10.3.4**.

After successful execution of the SQL statements, you can use the `ibm_db.num_rows` function to return the number of rows that the SQL statement affected.

Let's take a look at the example in **Listing 10.7**.

```
(1) stmt = ibm_db.exec_immediate (conn, "CREATE TABLE PRODUCT(product_id char(6), name char(30))")
(2) stmt = ibm_db.exec_immediate (conn, "Insert into PRODUCT values ('000001','Computer'), ('000002','TV')")
(3) print "Returns for insert: ", ibm_db.num_rows(stmt)
(4) stmt = ibm_db.exec_immediate (conn, "update PRODUCT set name = 'notebook' where product_id='000001'")
(5) print "Returns for update: ", ibm_db.num_rows(stmt)
(6) stmt = ibm_db.exec_immediate (conn, "delete from PRODUCT where product_id='000003'")
(7) print "Returns for delete: ", ibm_db.num_rows(stmt)
(8) stmt = ibm_db.exec_immediate (conn, "drop table PRODUCT")
```

# Listing 10.7 - the script ins_upd_del.py

Items in **Listing 10.7** are explained as follows:

+   1. Calls the function `ibm_db.exec_immediate` to create the table **PRODUCT**
+   2. Calls the function `ibm_db.exec_immediate` to insert rows into the **PRODUCT** table
+   3. Prints the number of rows that were inserted
+   4. Updates some rows in the table
+   5. Prints the number of rows that were updated
+   6. Delet es some rows in the table
+   7. Prints the number of rows deleted
+   8. Drops the table.

The above code snippets are part of the script `ins_upd_del.py` included in the exercise files accompanying the book. You can test the code by modifying the user ID and password in the script appropriately and run it as:

```
python ins_upd_del.py
```

The result of executing the script is illustrated in **Figure 10.6**.