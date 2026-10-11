# Querying the Database

When you want to get, set, or update information in the database, you use SQL queries. You experimented with SQL a little earlier when you created your tables in phpMyAdmin. Take a deep breath, as now you will be writing specific SQL queries by hand. Don’t worry; that doesn’t sound nearly as scary as you may think.

Beneath the mysql_select_db line, add the following code (shown in bold):

```
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
```

```
$sql = "SELECT * FROM products";
$result = mysql_query($sql);
```

The first line (the $sql line) simply sets another variable, but this one contains the SQL for the query that you want to send to MySQL. SQL is a very simple and effective language, and you will be using it throughout the book—with each piece of SQL being fully explained as you go along. In this particular line, you are selecting all the rows from the products table. You can read the SQL line from left to right to understand how it works:

First select (SELECT) everything (*) from (FROM) the products table (products) and then end the query (;).

Every SQL statement should end with a semi-colon. Although you do not need to explicitly add a semicolon in your PHP scripts, it is good form to do so. It just keeps you in the habit of adding a semi-colon, particularly if you use the command-line MySQL client.

# NOTE

# Other Clients

There are a number of ways to talk to MySQL. Some of these are Web-based (such as phpMyAdmin), some are graphical desktop applications (such as the MySQL Control Center), and some are command-line based (such as the mysql command).

At this point, the SQL has not actually been sent to the server; you have merely created a variable that contains the query. The next line actually sends the query to the database. The mysql_query() function is used to send the SQL (in the $sql variable) to the database, and the results of the query is placed into the $result variable.