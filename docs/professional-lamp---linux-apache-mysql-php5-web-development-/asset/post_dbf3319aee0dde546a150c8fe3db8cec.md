
portability. DB should work on your standard configuration, but if you're having compatibility issues, there are others you can try. In fact, PEAR dedicates an entire category of packages for dealing with databases which can be found http://pear.php.net/packages.php?catpid=7&catname=Database.

In the next few examples, you are going to need the following information:

- `MySQL` your database type
- `testdatabase` : Database name
- `testtable` : Database table
- `username` User accessing database
- `password`: User's password
- `localhost` : Server name
- `field1` , `field2` : Fields you will be querying

This will help you “fill in the blanks” when customizing your installation of the package.

## Connecting to a Database

In order to connect to the database, you have to pass your new database object the proper Data Source Name (DSN). The syntax is as follows:

```
<?php
require_once("db.php");

$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
  die($db->getMessage());
}

echo "Connected successfully. Now what?";
?>
```

As you can see, this is all that it takes to connect and, more important, report any errors that may have occurred in the process. Again, feel free to visit the official PEAR documentation for detailed instructions on the various options you can set when connecting to the database, such as the port number or protocol. This documentation is available http://pear.php.net/manual/en/package.database.db.intro-connect.php. Now try querying the imaginary fields from the imaginary tables.

## Querying the Database

To query the database, you need to pass along the table name and your desired filter, so you type the following:

```
<?php
require_once("db.php");

$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

//query
$res =& $db->query("SELECT * FROM testtable");

//display number of rows
echo "There were " . $res->numRows() . " rows found.";


//display one column of results, or by row number
while ($row =& $res->fetchRow()) {
    echo $row[0] . "\n";
}

//display more than one field of results
//also switching Associative mode
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
require_once("HTML/CSS.php");
require_once("HTML/Page.php");

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt verdana');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();

$p->setTitle("Testing the CSS");

$p->addStyleDeclaration($css, 'text/css');
$p->addBodyContent("<h1>Wow, this background is really bright</h1>");
$p->addBodyContent("<p>This should wake you up.</p>");

$p->display();
?>
```

Using simple *if* or *switch* statements, you can use something like this to dynamically create a stylesheet based on a person’s authorization level, the type of browser or operating system being used, the time or day, or anything else you can think of.

# HTML_QuickForm

The purpose of this package is to create HTML forms quickly and easily. It is easy to use, but relatively robust, and allows for quite a bit of customization on your part. Take a look at a quick example:

```
<?php
require_once("HTML/QuickForm.php");

//create a new form object
$form = new HTML_QuickForm('firstForm');

//add two input fields; this is completely customizable
$form->addElement('text', 'name', 'Your full name:', array('size' => 50, 'maxlength' => 255));
$form->addElement('text', 'email', 'Your email address:', array('size' => 50, 'maxlength' => 255));

//add a submit button
$form->addElement('submit', null, 'Send');

//add validation rules of our choosing
//using addRule('field to be validated', 'error_message to be displayed',
// 'validation type',
$form->addRule('name', 'Empty Name Field', 'required', null, 'client');
$form->addRule('email', 'Empty Email Address', 'required', null, 'client');
$form->addRule('email', 'Incorrect Format for Email Address', 'email', null, 'client');

//check to make sure input followed all our rules
//if so, put all form elements into an array for us
//for sake of example, let's print the values
if ($form->validate()) {
	$elements=$form->exportValues();
	print_r($elements);
	exit;
}

//show the form
$form->display();
?>
```

With this little script, you have created a user form, validated required fields (and an email field as well), and collected the input into a tidy little array for your use. You can set as many rules as you wish to have your script make sure required fields are entered, whether they are of the correct format (numeric, alphabetical, and so on), and as you saw previously, check for things such as a correctly formatted email field. You can also set default values and anything else you can accomplish with forms (such as uploading files and using images for "submit" buttons).

# HTML_Table

You can easily output a table of data with this package, either with data obtained from the resultset of a database query or data that’s just sitting in an array somewhere waiting for you to emancipate it. Take a quick look at an example that illustrates just how easy this package is to use:

```php
require_once ("HTML/Table.php");

//Set up attributes for our table, using common HTML attributes as
//array keys and their values as array values
$attributes = array("width" => "50%", "border" => "1");

//create a new table object
$table = new HTML_Table($attributes);

//configure table
//AutoGrow is for an unknown number of rows
//AutoFill inserts text for every empty cell
//Because we are pretending not to be sure how big our table will be, we
//will set this option to true.
$table->setAutoGrow(true);
$table->setAutoFill("-");

//get some data for our table
$rows = array(
    "0" => array("Number One", "Number Two", "Number Three"),
    "1" => array("Numero Uno", "Numero Dos", "Numero Tres"),
);

//populate the table
for($nr = 0; $nr < count($rows); $nr++) {
    //the header row comes first
    $table->setHeaderContents($nr+1, 0, (string)$nr);
    for($i = 0; $i < 3; $i++) {
        if("" != $rows[$nr][$i])
        //the cell contents come next
            $table->setCellContents($nr+1, $i+1, $rows[$nr][$i]);
    }
}
//set background for every other row
//skip the first row so we use a value of 1 to start
$altRow = array("bgcolor"=>"#FFFFCC");
$table->altRowAttributes(1, null, $altRow);

//set header info for each cell of the table
//based on coordinates. 0,0 is top left cell.
//the third value is the contents to be shown
$table->setHeaderContents(0, 0, " ");
$table->setHeaderContents(0, 1, "Field 1");
$table->setHeaderContents(0, 2, "Field 2");
$table->setHeaderContents(0, 3, "Field 3");

//set attributes for the header rows and first column
//first row and column = 0.
$shrAttrs = array("bgcolor" => "#FFFF4D");
$table->setRowAttributes(0, $shrAttrs, true);
$table->setColAttributes(0, $shrAttrs);

//send it to the browser
echo $table->toHTML();
?>
```

You can imagine how easy it would be to create a table based on user input, or results from a database, and the level of customization you would realize by changing a few variables here and there.

# What Else Is There?

Take a gander at the full list of PEAR packages (available http://pear.php.net/packages.php ) where you will begin to appreciate the breadth and depth of the PEAR community. There are so many great packages available, this book just doesn't have the space to cover all of them. To give a brief list of the more useful topics available, besides the ones we discussed in this chapter:

- Benchmarking
- Caching
- Configuration
- Encryption
- Event
- File Formats
- File System
- Gtk Components
- HTTP
- Images
- Internationalization
- Logging
