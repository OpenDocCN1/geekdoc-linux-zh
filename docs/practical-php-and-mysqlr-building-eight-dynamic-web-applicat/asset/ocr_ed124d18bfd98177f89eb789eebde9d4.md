Create *config.php* and add the code shown in Example 11-1.

# EXAMPLE 11-1 Nothing new here; just the same ‘ol config file.

```
```
<?php

$dbhost = "localhost";
$dbuser = "root";
$dbpassword = "";
$dbdatabase = "news";

$config_basedir = "http://localhost/sites/readallaboutit/";
?>
```
```

Create *db.php* and add the database connection code in Example 11-2.

# EXAMPLE 11-2 This is the same connection code used in previous projects.

```
```
<?php

require("config.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
?>
```
```

In this project, you use the *functions* file from previous projects. Copy it over or create *functions.php* and add the same code from Example 11-3.

# EXAMPLE 11-3 These functions add slashes to input and validate numeric GET variables.

```
```
<?php

function pf_fix_slashes($string) {
if (get_magic_quotes_gpc() == 1) {
return($string);
}
else {
return(addslashes($string));
}
}

function pf_check_number($value) {
if(issset($value) == FALSE) {
$error = 1;
}
```
```