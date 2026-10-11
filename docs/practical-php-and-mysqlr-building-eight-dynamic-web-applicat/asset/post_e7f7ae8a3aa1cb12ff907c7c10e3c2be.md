
## Querying the Database

When you want to get, set, or update information in the database, you use SQL queries. You experimented with SQL a little earlier when you created your tables in phpMyAdmin. Take a deep breath, as now you will be writing specific SQL queries by hand. Don’t worry; that doesn’t sound nearly as scary as you may think.

Beneath the `mysql_select_db` line, add the following code:

```php
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
```

```php
$sql = "SELECT * FROM products";
$result = mysql_query($sql);
```

The first line (the `$sql` line) simply sets another variable, but this one contains the SQL for the query that you want to send to MySQL. SQL is a very simple and effective language, and you will be using it throughout the book—with each piece of SQL being fully explained as you go along. In this particular line, you are selecting all the rows from the products table. You can read the SQL line from left to right to understand how it works:

- First select (SELECT) everything (*) from (FROM) the products table (products) and then end the query (;).

Every SQL statement should end with a semi-colon. Although you do not need to explicitly add a semicolon in your PHP scripts, it is good form to do so. It just keeps you in the habit of adding a semi-colon, particularly if you use the command-line MySQL client.

### NOTE

#### Other Clients

There are a number of ways to talk to MySQL. Some of these are Web-based (such as phpMyAdmin), some are graphical desktop applications (such as the MySQL Control Center), and some are command-line based (such as the mysql command).

At this point, the SQL has not actually been sent to the server; you have merely created a variable that contains the query. The next line actually sends the query to the database. The `mysql_query()` function is used to send the SQL (in the `$sql` variable) to the database, and the results of the query are placed into the `$result` variable.

## Iterating Through the Results

Inside `$result` lies the holy grail, the motherland that is the result of your query. Although `$result` contains the results, you can think of it as a big conjoined mess of results. In its current form, `$result` is not all that useful, and to be really practical you need to iterate through each row from the query. If you loop through each row, you can then display the relevant information on the page. This is the grand plan.

Add the following code beneath the `mysql_query` line in your file:

```php
$sql = "SELECT * FROM products;";
$result = mysql_query($sql);

while($row = mysql_fetch_assoc($result)) {
    echo $row['product'];
}
```

In this chunk of code, you are using a `while` loop to iterate through each row in the result set. This is performed by adding a loop condition that extracts each row from `$result` by using `mysql_fetch_assoc` and then putting the row into the `$row` variable.

The purpose of the `mysql_fetch_assoc()` function is to make an associative array out of the results. This provides you with a convenient key-value (explained in the "Arrays" section earlier) means of pulling out information. As such, if you need to access the contents of the product field in the current row, you would use `$row['product']`.

## Consistency Across Pages with Sessions

One of the biggest challenges when doing any kind of Web development is maintaining state across pages in a stateless Web. This grandiose statement basically translates into "sharing information across different pages." The reason for this difficulty is that each Web page you create essentially functions as an individual program. When you build Web applications that span a number of different pages, there is no implicit means of sharing information across these pages other than using the **GET** and **POST** variables. Sessions change all of this.

**Sessions** offer a surprisingly simple and efficient means of literally sharing variables across different pages. This is achieved with a number of PHP functions that give you the ability to enable a page with sessions, create session variables, and use these session variables in your scripts. Sessions can be used to share any PHP variables you like across different pages.

### Creating the Session

To use sessions, first add the `session_start()` function at the very beginning of each page for which you want to use sessions. It is critically important that `session_start()` is right at the beginning—no fancy HTML, no picture of your Aunt Maud, and not even white space should come before it.

To demonstrate the importance of this, create a new file called `sessions.php` and add the following code:

```php
<?php
session_start();
?>
```

When you run the script, you will not see anything; the session support has been happily built into your page. Now adjust the code and put a single white space before the `<?php` tag:

```php
 ?>
<?php
session_start();
?>
```

When you make this tiny change, you are given a particularly venomous error message:

> Warning: session_start() [function.session-start]: Cannot send session cookie - headers already sent by (output started at /opt/lampp/htdocs/sites/startingchapter/sessions.php:1) in /opt/lampp/htdocs/sites/startingchapter/sessions.php on line 3

The reason it is so important to not have anything before `session_start()` is that the sessions framework makes use of the HTTP headers that form the mechanics of the Web page. These special headers are pre-pended to each Web page and as such, if you add any content before `session_start()` the script will be trying to send out content (such as the white space), then the headers, and then the main content. This is not the way the Web works and, hence, PHP will shout at you in the form of the previous warning message.

## All About Headers

Every Web page on the Internet has some information called **headers** that is invisible to most users. Headers store a number of pieces of information that browsers care about. Here are some example headers:

```
GET / HTTP/1.1
Host: www.yourfavewebsite.org
Connection: close
Accept-Encoding: gzip
Accept: text/xml, application/xml, application/xhtml+xml, text/html;q=0.9,text/plain;q=0.8,image/png, */*;q=0.5
Accept-Language: en-gb, en;q=0.5
Accept-Charset: ISO-8859-1, utf-8;q=0.7, *;q=0.7
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-GB; rv:1.8.0.3) Gecko/20060523 Ubuntu/dapper Firefox/1.5.0.3
Referer: http://www.someotherwebsite.net/
```

Beneath the headers lies the content. When you add content to the page, the headers are added automatically. As such, when data is added to the page, the headers are also sent and cannot be modified after they have been sent.

When you use sessions, the sessions system modifies some of these headers, and this is why you must add `session_start()` before any data is added to the page.

## Using Session Variables

Before you use a session variable, you need to register it. This is achieved with the rather predictably named `session_register()` function. To use it, specify the name of the variable to create inside the brackets. To demonstrate this, add the following line of code to `sessions.php` after `session_start()`:

```php
session_register("userid");
```

This line registers with the session handling system that the `userid` variable can be shared across pages. The next step is to actually set this variable to something useful. Add this line next:

```php
$_SESSION['userid'] = 10;
```

In this line, you are using the special `$_SESSION` superglobal to reference the `userid` variable. The `$_SESSION` syntax should look fairly familiar, as you used `$_GET` and `$_POST` earlier to access GET and POST variables respectively.

To test whether your session variable is accessible on the second page, create a file called `sessions2.php`, and add the following code:

```php
<?php
session_start();
echo "The userid session variable is: " . $_SESSION['userid'];
?>
```

Remember to visit `sessions.php` first (so the variable is set) and then visit `sessions2.php` to see that the variable is shared across the pages. To access the session variables, you simply include `session_start()` on the page and then refer to the variable with `$_SESSION`.

The session information is available while the browser is open. When the browser window is closed, the session information is lost. Although this is often a suitable means of destroying a session, sometimes you need to forcibly destroy the session data on command. To do this, you can use the following command:

```php
session_destroy();
```

All the session variables are then suitably deleted.

## SUMMARY

This chapter explored some of the core concepts that need to be understood before you can move on and start writing applications. Instead of spending hours covering every nuance of PHP and MySQL, you have learned the fundamentals needed to move on, and each application will present new skills, techniques, and ideas.

As with any programming language, or natural language for that matter, practice really does make perfect. Just reading how to do something in PHP and actually understanding it are two separate things. A great way to get accustomed to the language is to create lots of little scripts that test different aspects of the language. These scripts are useful not only for learning, but also they can be a great reference point further down the line when you have forgotten how to do something.
