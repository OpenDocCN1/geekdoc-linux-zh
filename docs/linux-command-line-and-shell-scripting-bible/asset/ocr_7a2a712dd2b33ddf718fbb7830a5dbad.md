# Part V    Advanced Topics

One uncommon SQL command that the mysql program implements is the SHOW command. Using this command you can extract information about the MySQL server, such as the databases and tables created:

```
mysql> SHOW DATABASES;
+----------------------+
| Database             |
+----------------------+
| Information_schema   |
| mysql                 |
+----------------------+
2 rows in set (0.04 sec)

mysql> USE mysql;
Database changed
mysql> SHOW TABLES;
+----------------------+
| Tables_in_mysql     |
+----------------------+
| columns_priv         |
| db                   |
| help_category        |
| help_keyword         |
| help_relation        |
| help_topic          |
| host                 |
| proc                 |
| procs_priv           |
| tables_priv          |
| time_zone            |
| time_zone_leap_second|
| time_zone_name       |
| time_zone_transition |
| time_zone_transition_type|
| user                 |
+----------------------+
17 rows in set (0.00 sec)
```

In this example, I used the SHOW SQL command to display the databases currently configured on the MySQL server, then the USE SQL command to connect to a single database. Your mysql session can only be connected to one database at a time.

You'll notice that after each command I added a semicolon. The semicolon indicates the end of a command to the mysql program. If you don't use a semicolon, it prompts for more data:

```
mysql> SHOW
  -> DATABASES;
```

648