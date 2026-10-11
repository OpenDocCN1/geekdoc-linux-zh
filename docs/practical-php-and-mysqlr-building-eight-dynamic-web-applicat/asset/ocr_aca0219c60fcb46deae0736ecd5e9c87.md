```
```
}
if($_POST['submit']) {
	$db = mysql_connect($dbhost, $dbuser, $dbpassword);
	mysql_select_db($dbdatabase, $db);

	$catsql = "INSERT INTO categories(name) VALUES('" . $_POST['cat'] .
	"');";
	mysql_query($catsql);

	header("Location: " . $config_basedir);
}

    In this code, the database connection details are added and an INSERT query is
    made to the `categories` table in which the data from the form is added. The query is
    executed, and the page redirects.

    Add the `else` that contains the form:

    header("Location: " . $config_basedir);
}
else {
	require("header.php");
```
?>
```

```
```
<h2>Add a new category</h2>

<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">

    Finally, after the form, add the closing code:

    </table>
    </form>

<?php
```
}
```

```
```
require("Footer.php");
```
?>
```

# ## Adding Forums

This page adds forums to a particular category. The logic behind this script is simple: You present the user with a form in which she can select a category from a drop-down box. The data is then added to the forums table.