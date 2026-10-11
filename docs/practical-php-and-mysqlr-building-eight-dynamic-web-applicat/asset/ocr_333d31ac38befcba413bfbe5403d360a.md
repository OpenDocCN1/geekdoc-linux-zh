Jump to the beginning of the page (before the form) and start adding the code to process the form:

```
```php
<?php

session_start();

include("config.php");
include("functions.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbname, $db);
$validid = pf_validate_number($_GET['id'], "redirect", "index.php");
```
```

After the usual introductory code, protect the page from users who are not logged in:

```
```php
$validid = pf_validate_number($_GET['id'], "redirect", "index.php");

if(isset($_SESSION['USERNAME']) == FALSE) {
  header("Location: " . _HOST_NAME
. "/login.php?ref=images&id=" . $validid);
}
```
```

Select the user_id from the items table for the current item. This is required so you can check that the owner of the item-not a random user-is accessing the page.

```
```php
if(isset($_SESSION['USERNAME']) == FALSE) {
  header("Location: " . _HOST_NAME
. "/login.php?ref=images&id=" . $validid);
}

$$heitemsql = "SELECT user_id FROM items WHERE id = " . $validid . "";
$$heitemresult = mysql_query($$heitemsql);
$$heitemrow = mysql_fetch_assoc($$heitemresult);
```
```

Check if the current user owns the item by checking if the data from the query matches the USERID session variable. If not, redirect the user:

```
```php
$heitemresult = mysql_query($$heitemsql);
$heitemrow = mysql_fetch_assoc($$heitemresult);

if($$heitemrow['user_id'] != $_SESSION['USERID']) {
  header("Location: " . $conf['base_dir']);
}
```
```

To process the form, you use a new PHP superglobal called $_FILES, which you can use to access uploaded files. When a file is uploaded, it contains a number of different attributes, such as the file name, size, type, and so on.