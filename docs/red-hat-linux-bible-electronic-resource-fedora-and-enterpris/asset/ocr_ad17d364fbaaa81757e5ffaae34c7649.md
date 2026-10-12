+   1. If you are not already connected to a mysql session, type the following command (assuming the mysql user name of root):

```
# mysql -u root -p
Enter password: ********
mysql>
```

+   2. To create the user named bobby and a password i8yer2shuz, use the GRANT command as follows:

```
mysql> GRANT USAGE ON *.*
   -> TO bobby@localhost IDENTIFIED BY "i8yer2shuz";
```

At this point, someone could log in from the localhost using the name bobby and i8yer2shuz password (mysql -u bobby -p). But the user would have no privilege to work with any of the databases. Next you need to grant privileges.

+   3. To grant bobby privileges to work with the database called allusers, you could type the following:

```
mysql> GRANT DELETE,INSERT,SELECT,UPDATE ON allusers.*
   -> TO bobby@localhost;
```

In this example, the user named bobby is allowed to log in to the MySQL server on the localhost and access all tables from the allusers database (USE allusers). For that database, bobby can use the DELETE, INSERT, SELECT, and UPDATE commands.

+   4. To see the privileges that you just granted, you can select mysql as your current database, then select the db table as follows:

```
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db="allusers";
+---------------------+----------------+--------------+--------------+--------------+
| Host                | Db             | User         | Select_priv  | Insert_priv  | Update_priv | Delete_priv  | ...
|---------------------+----------------|--------------|--------------|--------------|
+---------------------+----------------+--------------+--------------+--------------+
| localhost           | allusers       | bobby        | Y            | Y            | Y           | Y           | ...
+---------------------+----------------+--------------+--------------+--------------+
```

The output here shows all users who are specifically granted privileges to the allusers database. Only part of the output is shown here because it is very long. You should either make a very wide Terminal window to view the output or learn how to read wrapped text. Other privileges on the line will be set to N (no access).