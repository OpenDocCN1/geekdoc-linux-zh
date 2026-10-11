# **EXPLANATION**

+   2. The `show database` command lists all the databases on this server. Typically, when you install MySQL, you will be given the `mysql` database and the `test` database. The `test` database is just for testing purposes and is empty. The `mysql` database contains all the MySQL server privilege information.

# Creating and Dropping a Database. Creating a database is simple. Designing it is another story and depends on your requirements and the model you will use to organize your data. Even with the smallest database, you will have to create a table. The next section will discuss how to create and drop both databases and tables. Assuming you have been granted permission to create a database, you can do it at the `mysql` command line or with the `mysqlqadmin` tool as shown in the following example.

# **EXAMPLE 15.4**

+   1. `mysql> CREATE database my_sample_db;`
+       `Query OK, 1 row affected (0.00 sec)`
+   
+   2. `mysql> USE my_sample_db;`
+       `Database changed`
+   
+   3. `mysql> SHOW tables;`
+       `Empty set (0.00 sec)`
+   
+   4. `mysql> CREATE table test (`
+       `--> field1 INTEGER,`
+       `--> field2 VARCHAR(50)`
+       `-->);`
+       `Query OK, 0 rows affected (0.36 sec)`
+   
+   5. `mysql> SHOW tables;`
+       `+--------------------+`
+       `| Tables_in_my_sample_db |`
+       `+--------------------+`
+       `| test               |`
+       `+--------------------+`
+       `1 row in set (0.00 sec)`
+   
+   6. `mysql> DROP table test;`
+       `Query OK, 0 rows affected (0.11 sec)`
+   
+   7. `mysql> DROP database my_sample_db;`
+       `Query OK, 0 rows affected (0.01 sec)`