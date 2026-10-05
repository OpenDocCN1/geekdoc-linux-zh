Let's consider an example. When the user types leon, the SQL server searches for the username 'leon' and returns the result. In order to search the database, the SQL server runs the query SELECT * FROM users user_name=leon. If instead, the user enters 'leon!@#$', the SQL server will run the query SELECT * FROM users WHERE user_name=leon!@#$. Nothing in our code block checks for these special characters, and it's this lack of filtering that causes the vulnerability.

We'll discover how these types of scenarios can be abused in the forthcoming sections.

# 10.1.2 DB Types and Characteristics

When testing a web application, sometimes lack prior knowledge of the underlying database system, so we should be prepared to interact with different SQL database variants.

There are many DB variants that differ in syntax, function, and features. In this section we are going to focus on two of the most common database variants, MySQL and Microsoft SQL Server (MSSQL).

> The two SQL variants we're exploring in this Module are not limited to on-premise installations, as they can be found in cloud deployments.

MySQL⁴⁵¹ is one of the most commonly deployed database variants, along with MariaDB⁴⁵² an open-source fork of MySQL.

To explore MySQL basics, we can connect to the remote MySQL instance from our local Kali machine.

Using the mysql command, we'll connect to the remote SQL instance by specifying username and password, along with the default MySQL server port 3306.

```
kal@kali:~$ mysql -u root -p -h 192.168.0.16 -P 3306
```

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
Type 'help'; or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]

Listing 179 - Connecting to the remote MySQL instance

From the MySQL console shell, we can run the version() function to retrieve the version running instance.

```
MySQL [(none)]> select version();
+----------------++
| version() |
+----------------++
| 8.0.21  |
```

⁴⁵¹ (Oracle, 2022), https://www.mysql.com/
⁴⁵² (MariaDB Foundation, 2021), https://mariadb.org

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.