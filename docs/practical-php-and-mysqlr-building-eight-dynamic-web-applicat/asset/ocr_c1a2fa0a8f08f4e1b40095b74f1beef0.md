```
```sql
$database = "productsdb";
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
?>
```
```

The first four lines in the code create some variables that contain the relevant pieces of information that are required to connect to a database. It is important to remember that these four lines literally are just set a bunch of variables; no connection is made at this point. You can call these variables what you like, but you will need to provide legitimate information for the host, username, password, and database that you are using on the MySQL server.

After you set the variables, you can make the connection. This happens with the `$db = mysql_connect($dbhost, $dbuser, $dbpassword)` line. This line uses the mysql_connect( ) function to pass the host, username, and password variables to the MySQL server and put the result of the connection in the $db variable. You then use the $db variables as a pointer to the main connection. To keep the code simple, this example does not involve any error checking; often you would check to see if the connection is suitable and possibly display a suitable error message. Some programmers feel this is unnecessary as you will get a PHP error message anyway if the connection is rejected, but if you implement your own errors, you can format and reference your errors in a nicer way.

When the connection has been made, you need to select the database that you want to use (remember, MySQL can have a number of different databases). This is performed with the mysql_select_db( ) on the next line. Here you specify the variable with the chosen database and also specify the connection ($db) that the database should be selected from.

At this point, you are now connected. Any other MySQL-related connections on this page will be applied to the connection that has just been created.

![](bbox=[0.06, 0.83, 0.16, 0.97])

# **Database Connections Are Per Page**

The database connection you made does not span across other pages. You need to include the connection details on each page that needs to access MySQL. Of course, ways of making this more efficient will be covered later in the book.

At this point, you are ready to start playing with the database on this page.