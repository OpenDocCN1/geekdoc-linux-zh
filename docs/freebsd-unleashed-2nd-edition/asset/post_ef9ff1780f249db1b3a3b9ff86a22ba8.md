
# Using PHP to Provide Database-Driven Content to Web Pages

You may be wondering whether writing your own Web applications from scratch is the only way to include database-driven content in your dynamic pages, or if there's a better and cleaner way, such as using Microsoft's ASP or Macromedia's ColdFusion. The answer is yes, there is. It's called PHP, which originally stood for "Personal Home Page" but now is itself the official name of an open-source HTML preprocessing framework that has become very widely used throughout the Unix Web-hosting world. PHP's official Web site is www.php.net.

PHP consists of commands that can be embedded into HTML, and they are parsed out in much the same way that server-side includes are parsed in .shtml files, as you saw in Chapter 25. A PHP file has the extension .php, .php3, or .php4, and Apache is reconfigured at installation time to recognize those files and pass them through the PHP module before serving their content to the user.

This chapter's discussion of PHP will be brief, but it should be enough to get you started. If you've already become familiar with the more difficult concepts presented by database design, SQL, and Perl/Python connectivity, then PHP in this series of conceptual phases should be like dessert after a long meal.

## Installing PHP

The PHP project is maintained and driven forward by the Apache Software Foundation, which means PHP and Apache are very closely intertwined in their operation. PHP is installed as an Apache module, mod_php4, which links to libraries that harness the Zend processing engine upon which PHP is based.

PHP can be installed from the ports or packages. The name of the package is mod_php4, and if you choose to install it from the ports, it's located in /usr/ports/www. When you type make, you are presented with a list of options to compile into PHP. Select support for either MySQL, PostgreSQL, or both, depending on which database you're using. You can also choose to enable support for the GD imaging library, mcrypt encryption, OpenSSL, XML, and other add-ons. Unless you already know you have need for these, you can ignore these additional options.

> **NOTE**
> If you're running Apache 2.0, you will want to define the WITH_APACHE2 environment variable before typing make. See Chapter 11, "Customizing the Shell," for details on setting environment variables.

At the end of the installation process, the automated installer script will modify your httpd.conf file to enable recognition of .php and .php4 files and assign them to the PHP handler. You may wish to examine the httpd.conf file after this and make sure nothing has been accidentally broken in the process.

## Flow Control and Programming Techniques

The tag format for PHP commands is <?php ... ?>. A number of internal PHP commands can go between these two bookend tags; you can use echo() to print text, you can perform string operations on variables (including the HTTP connection variables, such as HTTP_USER_AGENT), and you can do flow control. For instance, the following if statement can be used to print different blocks of HTML code depending on the state of a variable:

```
<?php
if ($a > $b) {
?>
<B>A is greater than B.</B>
<?php
} else {
?>
<B>B is greater than or equal to A.</B>
<?php
}
?>
```

The syntax for naming and assigning variables is very like Perl. PHP includes such Perl-like control structures as foreach, while, and do...while, although the equivalent to Perl's *elsif* is *elseif*. There is also an array context, although the prefix for an array is $, as for a scalar. Also, as with Perl, PHP's variable types do not have to be declared by the programmer but are handled internally and derived from context. Lines of PHP code end with a semicolon (;).

Within a <?php ... ?> block, you can define variables and functions on as many lines as you want; you can almost pretend that it's a Perl program. Anything in a <?php ... ?> block will be parsed out of the HTML file it's embedded in and then replaced with the output from any functions you call. You can put PHP code blocks wherever you like throughout the file.

## Interfacing with the Database

For the purposes of this chapter, what interests us is how to make PHP interact with MySQL and PostgreSQL. Fortunately, the methods for doing this are very similar to the Perl-based techniques we have already covered.

The initial MySQL database connection is set up using the *mysql_connect* and *mysql_select_db* functions, as follows:

```
$conn = mysql_connect("localhost", "frank", "<frank's password>");
mysql_select_db("PictureArchive");
```

For PostgreSQL, the database setup commands are as follows:

```
$conn = pg_connect("dbname=PictureArchive user=frank password=<frank’s password>");
```

A large number of connection options can be specified in the **mysql_connect** or **pg_connect** argument string, whether in the **parameter=value** format shown in the PostgreSQL example or the ordered list of values for the MySQL example (either format will work for either database). Because PostgreSQL depends to a certain extent on environment variables, you can set the defaults for many of these options by defining them in the environment for the Web server. Use Apache’s **SetEnv** directive to set these in **httpd.conf** or a **.htaccess** file, as shown here:

```
PGHOST=localhost
PGPORT=7890
PGDATABASE=PictureArchive
PGUSER=frank
PGPASSWORD=<frank’s password>
```

For MySQL, PHP has a number of functions, such as **mysql.default_user**, **mysql.default_password**, and **mysql.connect_timeout**, that can be set within the global PHP configuration file, **/usr/local/etc/php.ini**. Note that this file must be copied or renamed from **php.ini-dist** before it will be read.

Once your database connection is set up, you can then issue a query in much the same way as you have seen in earlier examples, using **mysql_query** or **pg_query** as follows (note that the two functions take the database connection identifier and the query in reverse order from each other):

```
<?php
$result = mysql_query("SELECT * FROM Users",$conn)
  or die("Invalid query");
?>
```

```
<?php
$result = pg_query($conn, "SELECT * FROM Users")
   or die("Invalid query");
?>
```

PHP operates in autocommit mode for both databases. As soon as you issue a **mysql_query** or **pg_query** command, the query is submitted, and you can then begin to work with the results in **$result**:

```
while($rowdata = mysql_fetch_row($result)) {
print "$rowdata[0]: $rowdata[1]<BR>\n";
}
```

This syntax is very Perl like. If you look through the PHP documentation at `http://www.php.net/manual/`, under the headings “MySQL Functions” and “PostgreSQL Functions,” you will find a large number of well-documented functions that operate very similarly to the Perl database interfaces with which you are already familiar.

The biggest advantages of PHP over homegrown Perl or Python scripts are that because the server-processed code is all embedded into plain HTML files, you can maintain the layout of your pages with much more ease. You can edit the HTML in these main files without the danger of breaking permissions or disabling the executable code. And because the files are parsed internally by Apache, you will see a significant decrease in processing overhead, because starting up individual CGI processes for each page view is a very expensive way for a server to run.

## Security Concerns

PHP potentially opens your system up to a large number of security weaknesses. PHP is susceptible to many of the same exploits that threaten CGI programs, and it has a few new areas of susceptibility of which you should be aware.

The files that include database connection passwords, whether the HTML/PHP files themselves or include files, are subject to access by local users writing CGI programs to access the files’ contents. To address this problem, you will need to take the same precautions you would take with a Perl or Python connectivity setup (as explained earlier in this chapter). Similarly, issues exist with virtual hosting and PHP files that are executed outside the main server root in the users’ `public_html` directories (if you choose to allow it; a tightly secured server will run all PHP scripts from within the restricted `/cgi-bin` directory and not allow regular users to run them). Because all PHP files are parsed and executed with the same permissions and ownership, one user’s actions can potentially affect other users’ database code or files. Again, you will want to review your security policy: How much do you trust your local users?

Perfect security is a myth, and security and convenience are mutually exclusive. The more lenient you are in allowing users access onto your system, the less safe you are from malicious activity by your own users. Fortunately, for the purposes of database connectivity, the only sector from which to fear an attack is your local users, because most Web-enabled database systems don’t have their database back ends open to nonlocal connections. However, those local users can cause a great deal of trouble if you’ve allowed them onto the system.

Refer to the online PHP security documentation at `http://www.php.net/manual/en/security.php` for a thorough discussion of the ways in which a PHP server can be attacked and compromised.
