
```php
<?php
$regex = '/([A-Za-z0-9_]+)\(\)/';
$replace = '<em>$1</em> (<a href="http://www.php.net/$1">manual</A>)';
$haystack = 'File_get_contents() is easier than using fopen(). ';
$result = preg_replace($regex, $replace, $haystack);
echo $result;
?>
```

The $1 is our backreference; it will be substituted with the results from the first subexpression. The way we have written the regular expression is very exact. The [A-Za-z0-9_]* part, which matches the function name, is marked as a subexpression. After that is \(\), which means the exact symbols (), not the regular expression meanings of them, which means that $1 in the replacement will contain fopen rather than fopen(), which is how it should be. Of course, anything that is not backreferenced in the replacement is removed, so we have to put the () after the first $1 (not in the hyperlink) to repair the function name.

After all that work, the output is perfect:

```
<em>File_get_contents()</em> (<a href="http://www.php.net/file_get_contents">manual</A>) is easier than using <em>fopen()</em> (<a href="http://www.php.net/fopen">manual</A>).
```

## Handling HTML Forms

Given that PHP's primary role is handling web pages, you might wonder why this section has been left so late in the chapter. It is because handling HTML forms is so central to PHP that it is essentially automatic.

Consider this form:

```
<form method="POST" action="thispage.php">
User ID: <input type="text" name="UserID" /> <br />
Password: <input type="password" name="Password" /> <br />
<input type="submit" />
</form>
```

When a visitor clicks Submit, thispage.php is called again and this time PHP has the variables available to it inside the $_REQUEST array. Given that script, if the user enters 12345 and frosties as her user ID and password, PHP provides you with $_REQUEST['UserID'] set to 12345 and $_REQUEST['Password'] set to frosties. Note that it is important that you use HTTP post unless you specifically want GET. POST enables you to send a great deal more data and stops people from tampering with your URL to try to find holes in your script.

Is that it? Well, almost. That tells you how to retrieve user data, but you should be sure to sanitize it so users do not try to sneak HTML or JavaScript into your database as something you think is innocuous. PHP gives you the strip_tags() function for this purpose. It takes a string and returns the same string with all HTML tags removed.

## Databases

The ease with which PHP can be used to create dynamic, database-driven websites is for many the key reason to use it. The stock build of PHP comes with support for MySQL, PostgreSQL, SQLite, Oracle, Microsoft SQL Server, ODBC, plus several other popular databases, so you are sure to find something to work with your data.

If you want to, you can learn all the individual functions for connecting to and manipulating each database PHP supports, but a much smarter idea is to use PEAR::DB. PEAR::DB is an abstraction layer over the databases that PHP supports, which means you write your code once, and—with the smallest of changes—it will work on every database server.

PEAR is the script repository for PHP and contains numerous tools and prewritten solutions for common problems. PEAR::DB is perhaps the most popular part of the PEAR project, but it is worth checking out the PEAR site to see whether anything else catches your eye.

## Introduction to PEAR::DB

To get basic use out of PEAR::DB, you need to learn how to connect to a database, run a SQL query, and work with the results. This is not a SQL tutorial, so we have assumed you are already familiar with the language. For the sake of this tutorial, we have also assumed you are working with a database called dentists and a table called patients that contains the following fields:

- ID—The primary key, auto-incrementing integer for storing a number unique to each patient
- Name—A varchar(255) field for storing a patient name
- Age—Integer
- Sex—1 for male, 2 for female
- Occupation—A varchar(255) field for storing a patient occupation

Also for the sake of this tutorial, we will use a database server on IP address 10.0.0.1, running MySQL, with username ubuntu and password a1m6z5. You will need to replace these details with your own—use localhost for the local server.
