EXAMPLE 6-3 Continued

```
```php
echo "<a href='" . $config_basedir . "login.php'>Login</a>";
}
?>
</div>
<div id="main">
```

```

Take a moment to review the following interesting points about *header.php*:

+   At the top of the file, a check is made for a session variable called SESS_CHANGEID. If it exists, the session is unset (deleted) and the session id is regenerated. Later, when the order is complete, SESS_CHANGEID is created when the session system should be reset.

+   A check is made to see if the SESS_LOGGEDIN variable exists. If it does, it indicates the user is currently logged in, and his username and a Logout link are displayed. The username is stored in SESS_USERNAME; this variable is created in login.php, which is covered later.

+   The same *stylesheet.css* file from the previous projects in the book is used here.

A file called *bar.php* is also included in the header file. This file contains the list of categories shown in Example 6-4.

EXAMPLE 6-4 Although the code in *bar.php* could have been added to *header.php*, you can use this file to cleanly add other content if needed.

```
```php
<h1>Product Categories</h1>
<ul>
<?php
$catsql = "SELECT * FROM categories";
$catres = mysql_query($catsql);
while($catrow = mysql_fetch_assoc($catres))
{
    echo "<li><a href='" . $config_basedir . "/products.php?id=' . $catrow['id'] . "'>" . $catrow['name'] . "</a></li>";
}
?>
</ul>
```

```