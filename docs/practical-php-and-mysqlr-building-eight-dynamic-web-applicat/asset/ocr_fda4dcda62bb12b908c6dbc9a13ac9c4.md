# Logging In the Administrator

The login page for the administrator is fundamentally the same as the preceding page. Create a new file called admin.php and add the code shown in Example 5-3.

> **EXAMPLE 5-3** The administrator login page is virtually identical to the user login page.

```
```php
<?php
session_start();
require("config.php");
require("functions.php");
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
if($_POST['submit']) {
$sql = "SELECT * FROM admins WHERE username = '" . $_POST['username'] . "' AND password = '" . $_POST['password'] . "'";
$result = mysql_query($sql);
$numrows = mysql_num_rows($result);
if($numrows == 1) {
$row = mysql_fetch_assoc($result);
session_register("ADMIN");
$_SESSION['ADMIN'] = $row['username'];
switch($_GET['ref']) {
case "add":
header("Location: " . $config_basedir . "/addforum.php");
break;
case "cat":
header("Location: " . $config_basedir . "/addcat.php");
break;
case "del":
header("Location: " . $config_basedir);
break;
default:
header("Location: " . $config_basedir);
break;
```
```

continues