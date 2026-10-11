# Chapter 9 Writing MySQL Programs Using PHP

```
```text
$dbh->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
$sth = $dbh->query ('SELECT COUNT(*) FROM member');
$count = $sth->fetchColumn (0);
print ("<p>The League currently has $count members.</p>");
$dbh = NULL; # close connection
}
catch (PDOException $e) { } # empty handler (catch but ignore errors)
?
</body>
</html>
```
```

The welcome message is just static text, so it's easiest to write it as literal HTML. The membership count, on the other hand, is dynamic and changes over time, so it must be determined at execution time by querying the `member` table in the `sampdb` database. To perform that task, the code within the opening and closing script tags follows these steps:

+   1. Opens a connection to the MySQL server and makes the `sampdb` database the default database.
+   2. Enables exceptions for subsequent PDO calls so that errors can be caught easily without testing for them explicitly.
+   3. Sends a query to the server to determine how many members the Historical League has at the moment (assessed as the number of rows in the `member` table).
+   4. Uses the query result to construct a message containing the membership count.
+   5. Closes the connection to the MySQL server.

The script just shown can be found as the file named `index.php` in the `phpapi/ush1` directory of the `sampdb` distribution. Change the connection parameters as necessary, install a copy of the script as `index.php` in the `ush1` directory of your Web server's document tree, and request it from your browser using either of these URLs (changing the hostname and pathname as appropriate for your own Web server):

```
```text
http://localhost/ush1/
http://localhost/ush1/index.php
```
```

Let's break down the script into pieces to see how it works. The first step is to connect to the server:

```
```text
$dbh = new PDO('mysql:host=localhost;dbname=sampdb', 'sampadm', 'secret');
```
```

`new PDO()` invokes the constructor for the PDO class. The constructor attempts to connect to the database server and raises an exception if it fails. Otherwise, it returns a PDO object that serves as a database handle.

The first argument to `new PDO()` is a string called a "data source name."The second and third arguments are the username and password to use for connecting to the server, `sampadm` and `secret`. The DSN string tells PDO which driver to use, followed by driver-specific parameters. For MySQL, the driver name is `mysql`, and the parameters are the