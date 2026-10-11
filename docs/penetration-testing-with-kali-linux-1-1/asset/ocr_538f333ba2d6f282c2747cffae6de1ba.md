![](bbox=[0.12, 0.035, 0.27, 0.09])

Now we know that the database used by this WordPress instance is 10.3.20-MariaDB.

> *MariaDB is a fork of MySQL. It was designed to work as a plug-and-play alternative to MySQL and SQL injection exploits used for MySQL typically work for MariaDB as well.*

Now that we know the SQL injection works, we need to determine our next step. While uploading a PHP shell through MariaDB might enable us to get remote code execution on the WordPress instance, it could be very temperamental and difficult if we don't have more information about the system.

Let's start with something easier and extract the admin's username and password hash. To do this, we will need to get a list of tables, find the user's table, get a list of columns, and then finally extract the relevant information.

To get a list of table names, we need to query the *information_schema.tables* table for the *table_name* column. This can be done by altering the cookie payload as shown in Listing 867.

```
"1650149780'\') OR 1=2 UNION SELECT 1,2,3,4,5,6,7,8,9,**table_name**,11 FROM **information_schema.tables**#"
```

*Listing 867 - Listing all tables*

Note that we have also removed the "ALL" from the original payload. This is to decrease the results as we don't care about duplicate values.