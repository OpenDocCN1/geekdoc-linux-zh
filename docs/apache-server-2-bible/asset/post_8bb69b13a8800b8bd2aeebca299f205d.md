
## Note

By default, session data are stored in files (because `session.save_handler = files` in `php.ini`) and also by default the data is stored in session files (`prefix sess_identifier`) in the `/tmp` directory. If you wish to change the session file directory, set the `session.save_path` directive in `php.ini` to point to a different directory. Make sure session files are not readable by anyone other than the Web server user.

# Using MySQL with PHP

PHP works very well with MySQL, Postgres, Oracle, and other popular databases. MySQL is the most widely used database platform for PHP. If you have not yet installed MySQL on your system, you can learn how to install it at www.mysql.com.

## Creating a simple PHP page to access a MySQL database

To access a MySQL database you need a username and password that MySQL accepts for access to the desired database. For example, Listing 15-11 shows a PHP script called `simple_query.php`, which accesses a MySQL database called `www` as user `httpd` with password `nosecret` from the local host.

**Listing 15-11: simple_query.php**

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';

    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<?php
    $result = mysql_query("SELECT * from $table", $dbh);
    while ($myRow = mysql_fetch_row($result)) {
        printf("<tr><td>%s</td><td>%s</td></tr>", $myRow[0],
               $myRow[1]);
    }
?>
</table>
</body>
</html>
```

Here’s what’s going on in the above listing:

1. This script defines the `$host`, `$user`, `$passwd`, `$database`, and `$table` variables that can be set to the appropriate MySQL server host name, username, password, database name, and table name.
2. The script then uses the `mysql_connect()` function to create a connection to the database server every time the page is requested. The connection handle is stored in another variable called `$dbh`.
3. The `mysql_select_db()` function selects the `$database`-specified database to use. At this point, the `$dbh` handle is connected to the database server and it operates on the named database.
4. The script prints out a regular HTML document, which has another tiny PHP script embedded in it, which performs a SQL query to the connected database by using the `mysql_query()` function. The query is supplied as the argument for this function along with the database handle (`$dbh`).
5. After the query is done, the script uses `mysql_fetch_row()` method to extract rows of data from the resulting data set. This function returns an array of columns for each row of data returned.
6. A `printf()` function is used to print two elements of the `$myRow` array. Notice that the very first element of the `$myRow` array is indexed with 0.
7. The while loop continues until there are no more rows left for `mysql_fetch_row` to fetch, at which time the script completes and rest of the HTML document is printed. The resulting page looks as follows on some sample data:

```html
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<tr><td>kabir</td><td>mysecret1</td></tr>
<tr><td>esmith</td><td>sale007</td></tr>
</table>
</body>
</html>
```

8. As you can see, the embedded PHP script is parsed out and the end user on the browser side does not even know which database or which user/password was used to produce this page.

If you have a lot of pages where you use the same MySQL database to display data elements using various queries, you should use the `include()` function to simplify your code management tasks. For example, Listing 15-12 shows a modified version of `simple_query.php` script that includes the `include()` function.

**Listing 15-12: simple_query2.php**

```php
<?php include('/usr/local/apache/secrets/mysql/header.inc'); ?>
<html>
<head><title>Simple Query Script</title></head>
<body>
<table border=1>
<tr><th>Name</th> <th>Password</th></tr>
<?php
    $sth = mysql_query("SELECT * from $table", $dbh);
    while ($myRow = mysql_fetch_row($sth)) {
        printf("<tr><td>%s</td><td>%s</td></tr>", $myRow[0],
               $myRow[1]);
    }
?>
</table>
</body>
</html>
```

When the above script is accessed via the Web the resulting page is same as the one produced by `simple_query.php`. However, here the script uses a header file that contains the database connection script as shown below:

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';
    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
```

By removing this script from each page that uses it, you make it very easy to change the host name, username, password, database name, and table name. If you have 20 pages that use the same database and table, you can now update the password once in the `header.inc` file and be done!

## Securing PHP include files

If you use include files, as shown in the last section, to store username, password, and other information, such as database host name, database name, and table names, that are not to be seen by users, make sure you keep the include files in a safe directory where Web browsers cannot browse them. The best place is outside the document tree of the Web site. If the document root is `/www/mysite/htdocs`, then create a directory called `/www/mysite/secret/mysql` and keep the include files there.

If you must create the include files inside the document root, disallow Web browsing by using the following configuration in `httpd.conf`:

```apache
<Directory /path/to/include_files>
<Limit>
Order Deny,Allow
Deny from all
</Limit>
</Directory>
```

Don't forget to replace `/path/to/include_files` with the path to the real directory of the include files. If you keep your include files all over the Web site, you can still disable Web access to them by using the following configuration segment in `httpd.conf`:

```apache
<Files ~ "*.inc*">
Order allow,deny
Deny from all
</Files>
```

This will only work if you always make sure all your PHP include files are named with the extension `.inc`.

# Authenticating users with PHP and MySQL

You can use a PHP script to authenticate users via MySQL database. Listing 15-13 shows a simple script that uses a MySQL database to authenticate users.

**Listing 15-13: auth.php**

```php
<?php
ob_start();
include('/usr/local/apache/htdocs/mysql/header.inc');
function show_dialog($realm = "Restricted Section") {
    header("WWW-Authenticate: Basic realm=$realm");
    header('HTTP/1.0 401 Unauthorized');
    echo 'Authorization Required.';
    exit;
}

if ((!isset($PHP_AUTH_USER)) || (!isset($PHP_AUTH_PW))) {
    show_dialog();
} else if ((!isset($PHP_AUTH_USER)) && (!isset($PHP_AUTH_PW))) {
    $sth = mysql_query("SELECT 1 from $table WHERE
                        username = '$PHP_AUTH_USER'
        and
        passwd = '$PHP_AUTH_PW'",
        $dbh);

    $success = mysql_fetch_row($sth);
    if ($success[0] == '1') {
        show_dialog();
    } else {
        echo "<p>You're authorized!</p>";
        # Do something here
    }
}
ob_end_flush();
?>
```

When this script is requested, it uses the `isset()` function checks whether two variables called `$PHP_AUTH_USER` and `$PHP_AUTH_PW` are set. These two variables are set by PHP if a user has entered a username and password in response to a basic authentication challenge.

Because the first-time user has not yet seen the authentication challenge dialog box, these two variables are empty and the `show_dialog()` function is called. This function simply prints out the *Basic HTTP* authentication headers, which forces the Web browser to display a dialog box asking the user to enter a username and a password.

When the user enters a username and password pair, the pair is sent via the authentication response header to the Apache server, which is seen by **PHP**. **PHP** then sets the `$PHP_AUTH_USER` and `$PHP_AUTH_PW` variables accordingly. After the script is called again automatically in the authentication response request, the script uses the *MySQL* database to verify whether or not the username/password pair exists. If the user credentials (username/password pair) are valid, the script displays the message “You’re authorized” and terminates. On the other hand, if the credentials are invalid, the authentication challenge is reissued.

Notice that the `include('/usr/local/apache/htdocs/mysql/header.inc')` call hides all the database connectivity code. The `header.inc` file is shown below:

```php
<?php
    $host = 'localhost';
    $user = 'httpd';
    $passwd = 'nosecret';
    $database_name = 'www';
    $table = 'users';
    $dbh = mysql_connect($host, $user, $passwd);
    mysql_select_db($database_name, $dbh);
?>
```

Here the *MySQL* database called `www` is on `localhost` and can be accessed by a user called `httpd` using `nosecret` as the password. The `www` database has a table called `users`. You can change these parameters as desired to connect to the appropriate database on the local host or a remote *MySQL* database server. This include file opens a connection to the named database on the appropriate host and returns a connection handle called `$dbh`, which is available to `auth.php`.

In the `auth.php` script, notice this line:

```php
    $sth = mysql_query("SELECT 1 from $table
        WHERE username = '$PHP_AUTH_USER' and
               passwd  = '$PHP_AUTH_PW'",
        $dbh);
```

This line performs an SQL query that returns 1 if user-supplied credentials (stored in `$PHP_AUTH_USER` and `$PHP_AUTH_PW` automatically by **PHP**) matches a `username` and `passwd` field, respectively, in the `users` table.
