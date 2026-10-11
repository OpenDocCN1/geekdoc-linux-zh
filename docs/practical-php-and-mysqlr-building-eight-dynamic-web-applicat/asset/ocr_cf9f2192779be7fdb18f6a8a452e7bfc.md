Create a new file called `itemdetails.php` and add the usual introductory code:

```
```php
<?php
session_start();
include(config.php);
include(functions.php);
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir);
```
```

Create a query to grab the item information:

```
```php
$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir);
require(header.php);
$itemsql = "SELECT UNIX_TIMESTAMP(dateends) AS dateepoch, items.* FROM items WHERE id = '" . $validid . "'";
$itemresult = mysql_query($itemsql);
$itemrow = mysql_fetch_assoc($itemresult);
```
```

In index.php, only items that were newer than the date and time were returned by the `MySQL_NOW()` function. For completeness, the page checks this with PHP rather than `MySQL`.

Inside the query, the `UNIX_TIMESTAMP()` command converts the dateends field into the number of seconds since the epoch. The query is then executed, and a row is stored in the `$itemrow` array.

Check to see if the current item has ended:

```
```php
$itemrow = mysql_fetch_assoc($itemresult);
$nowepoch = mktime();
$rowepoch = $itemrow['dateepoch'];
if($rowepoch < $nowepoch) {
    $VALIDACTION = 1;
}
```
```

The `mktime()` function stores the seconds since the epoch for the current time in the `$nowepoch` variable. The `$rowepoch` variable then stores the epoch returned from the row. A check is made to see if `$rowepoch` is greater than `$nowepoch` and if