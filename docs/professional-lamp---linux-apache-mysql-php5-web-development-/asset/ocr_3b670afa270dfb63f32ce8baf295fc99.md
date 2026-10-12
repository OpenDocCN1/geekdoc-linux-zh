# # Site Security

Now, if the script is called with that access_level added, it doesn’t matter if the user is truly an administrator or not — the$access_level variable will be set to 10 automatically when the script begins, thanks to register_globals and PHP not requiring variable initialization.

Luckily, it’s relatively easy to avoid such pitfalls. Make sure you code withregister_globals disabled, use the proper $_GET and $_POST superglobals, initialize possibly unsafe variables, and make sure error_reporting is set to E_ALL when developing and testing the site.

If you cannot disable register_globals in php.ini, you can use a .htaccess file to turn it off, if properly enabled in Apache:

```
php_flag register_globals off
```

# ## SQL Injection Attacks

Another dirty-data attack, but with a far higher potential for damage, is the SQL Injection Attack. Used in conjunction with a register_globals attack, or just using a normal web form, SQL injection attacks are simply the insertion of malicious SQL statements in the place of what should normally be innocuous data.

SQL injection preys on a lack of input scrubbing and data validation — data that is blindly used in a PHP-built SQL query. Take the following example that would access the WebAuth database you created earlier in the chapter:

```
<?php

$username = $_POST['username'];

$conn = mysql_connect(AUTH_DB, AUTH_USER, AUTH_PASS);
mysql_select_db(AUTH_DB, $conn);

$sql = "SELECT * FROM Users WHERE username='$username'";
mysql_close($conn);

?>
```

Looks harmless enough, right? You’d expect it to happily take whatever username was sent from the form and look up all columns related to that specific username. The problem with this code lies in the SQL query. Notice how the $username variable is not validated, scrubbed, or prepared in any way before sending it to the database. Under most circumstances, you might not notice anything wrong, and it would rarely if ever throw an error.

However, things turn nasty quickly, when the following value is entered in the username field of the sending form:

```
'; DELETE FROM Users; SELECT 'Own3d' AS username FROM Users WHERE '=''
```

Look carefully at what is going on with this value. It begins by terminating the part of the query before the $username variable is appended, deletes all information from the Users table, and then performs a query of the attacker’s choosing, just to close out the query and match up the final apostrophe.