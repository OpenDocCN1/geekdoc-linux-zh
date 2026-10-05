SQL syntax, commands, and functions vary based on relational database they were made for. MySQL, Microsoft SQL Server, PostgreSQL, and Oracle are the most popular database implementations, and we are going to inspect each variant's characteristics.

An example, let's build a simple MySQL query to parse the users table and retrieve a specific user entry.

We can use the SELECT statement to inspect the database that we want to retrieve (*) the records from a specific location defined by the FROM keyword and followed by the target, in the case the use users table. Finally, we'll direct the database to filter out for records belonging to the user leon.

```
SELECT * FROM users WHERE user_name='leon'
```

Listing 177 - SQL query that parses the users table

To automate functionality, web applications often embed SQL queries within their source code.

We can better understand this concept by examining the backend PHP code portion for verifying user-submitted credentials login:

```
<?php
$uname = $_POST['username'];
$password = $_POST['password'];

$sql_query = "SELECT * FROM users WHERE user_name='$uname' AND password='$password";
$result = mysqli_query($con, $sql_query);
?>
```

Listing 178 - SQL Query Embedded in PHP Login Source Code

Highlighted above is a pre-compiled SQL query that searches the users table for the username and its respective password, which are saved into the uname + *password variables. The query string is then stored in sqlQuery and used to perform the query against the local database through the mysqli_query function, which saves the result of the query in $result.

> Note that the i in the mysqli_query function for improved and should not be confused with the vulnerability (as the i in SQL stands for injection).

So far, we've described a very basic interaction between backend PHP code and the database. Reviewing the above code snippet, we'll notice that both the user_name and password variables are retrieved from the user request and inserted directly into the sqlQuery string, without any prior check. This means that an attacker could modify the SQL statement before it is executed by the SQL database.

An attacker could insert a SQL statement inside the user or password field to circumvent the intended application logic.