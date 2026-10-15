
Is that it? Well, almost. That tells you how to retrieve user data, but you should be sure to sanitize it so users do not try to sneak HTML or JavaScript into your database as something you think is innocuous. PHP gives you the strip_tags() function for this purpose. It takes a string and returns the same string with all HTML tags removed.

## Databases

The ease with which PHP can be used to create dynamic, database-driven websites is for many the key reason to use it. The stock build of PHP comes with support for MySQL, PostgreSQL, SQLite, Oracle, Microsoft SQL Server, ODBC, plus several other popular databases, so you are sure to find something to work with your data.

If you want to, you can learn all the individual functions for connecting to and manipulating each database PHP supports, but a much smarter idea is to use PEAR::DB. PEAR::DB is an abstraction layer over the databases that PHP supports, which means you write your code once, and—with the smallest of changes—it will work on every database server.

PEAR is the script repository for PHP and contains numerous tools and prewritten solutions for common problems. PEAR::DB is perhaps the most popular part of the PEAR project, but it is worth checking out the PEAR site to see whether anything else catches your eye.

### Introduction to PEAR::DB

To get basic use out of PEAR::DB, you need to learn how to connect to a database, run a SQL query, and work with the results. This is not a SQL tutorial, so we have assumed you are already familiar with the language. For the sake of this tutorial, we have also assumed you are working with a database called dentists and a table called patients that contains the following fields:

- ID—The primary key, auto-incrementing integer for storing a number unique to each patient
- Name—A varchar(255) field for storing a patient name
- Age—Integer
- Sex—1 for male, 2 for female
- Occupation—A varchar(255) field for storing a patient occupation

Also for the sake of this tutorial, we will use a database server on IP address 10.0.0.1, running MySQL, with username ubuntu and password alm65z. You will need to replace these details with your own—use localhost for connecting to the local server.

The first step to using PEAR::DB is to include the standard PEAR::DB file, DB.php. Your PHP will be configured to look inside the PEAR directory for include() files, so you do not need to provide any directory information.

PEAR::DB is object oriented, and you specify your connection details at the same time as you create the initial DB object. This is done using a URL-like system that specifies the database server type, username, password, server, and database name all in one. After you have specified the database server here, everything else is abstracted, meaning you only need to change the connection line to port your code to another database server.

This first script connects to our server and prints a status message (see Listing 29.6).

### LISTING 29.6 Connecting to a Database Through PEAR::DB

```
<?php

include("DB.php");
$dsn = "mysql://ubuntu:alm65z@10.0.0.1/dentists";
$conn = DB::connect($dsn);

if (DB::isError($conn)) {
    echo $conn->getMessage() . "\n";
} else {
    echo "Connected successfully!\n";
}
?>
```

You should be able to see how the connection string breaks down. It is server type first, then a username and password separated by a colon, then an @ symbol followed by the IP address to which to connect, and then a slash and the database name. Notice how the call to connect is DB::connect(), which calls PEAR::DB directly and returns a database connection object for storage in $conn. The variable name $dsn was used for the connection details because it is a common acronym standing for data source name.

If DB::connect() successfully connects to a server, it returns a database object we can use to run SQL queries. If not, we get an error returned that we can query using functions such as getMessage(). In the previous script, we print the error message if we fail to connect, but we also just print a message if we succeed. Next, we will change that so we run an SQL query if we have a connection.

Running SQL queries is done through the query() function of our database connection, passing in the SQL we want to execute. This then returns a query result that can be used to get the data. This query result can be thought of as a multidimensional array because it has many rows of data, each with many columns of attributes. This is extracted using the fetchInto() function, which loops through the query result converting one row of data into an array that it sends back as its return value. You need to pass in two parameters to fetchInto() specifying where the data should be stored and how you want it stored. Unless you have unusual needs, specifying DB_FETCHMODE_ASSOC for the second parameter is a smart move.
