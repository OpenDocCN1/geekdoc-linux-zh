# Chapter 8

```
$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

//query
$res =& $db->query('SELECT * FROM testtable');

//display number of rows
echo "There were " . $res->numRows() . " rows found.";

//display one column of results, or by row number
while ($row =& $res->fetchRow()) {
    echo $row[0] . "\n";
}

//display more than one field of results
//also switching AssocIative mode
while ($res->fetchInto($row, DB_FETCHMODE_ASSOC)) {
    echo $row['field1'] . "," . $row['field2'] . "\n";
}
?>
```

This was just a sample of this package. There is so much more you can do with it, such as getting the resultsets from multiple queries, and automatically preparing and executing commonly used SQL statements.

# HTML_CSS and HTML_Page

These are the packages that allow you to dynamically create your CSS stylesheets and easily incorporate them into a new HTML page. HTML_Page can also perform other functions for you, but this example focuses on creating a new CSS stylesheet:

```
<?php
require_once('HTML/CSS.php');
require_once('HTML/Page.php');

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt verdana');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();
```

192