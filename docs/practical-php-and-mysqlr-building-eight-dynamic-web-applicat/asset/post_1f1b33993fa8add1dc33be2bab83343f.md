
If $bidnumrows has no rows, the startingprice field from the first query is displayed (if there are no bids, the starting price should be displayed). If there are bids, the highest bid is displayed ($bidrow['highestbid']) from the last query. Both prices are formatted.

**NOTE: Formatting Prices**

When you use a FLOAT to store a price in the database, the trailing zeros are removed by default. To reformat the price with zeros, use the PHP function sprintf(). The function takes two arguments: the formatting string and the value to format. The formatting string takes a value such as %.2f, which asks for two decimal places (.2) on a floating point number (f).

Finally, display and format the dateends field:

```php
}
echo "</td>";

echo "<td>" . date("D jS F Y g:iA",
  strtotime($row['dateends'])) . "</td>";
echo "</tr>";
}
echo "</table>";
require("footer.php");
?>
```

## Viewing Item Details and Placing Bids

The next page is linked from the name of the item on the page you just created. This script has two primary purposes:

- To display information about the item, including images of it.
- To allow a user to bid on the item.

To place a bid, you need to check if the user is logged in, and if so, display a form into which she can type a bid amount. The page then checks that the amount is legitimate and adds the bid to the bids table.

Create a new file called `itemdetails.php` and add the usual introductory code:

```php
<?php
session_start();
include(config.php);
include(functions.php);
$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);
$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir);
```

Create a query to grab the item information:

```php
$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir);
require(header.php);
$itemsql = "SELECT UNIX_TIMESTAMP(dateends) AS dateepoch, items.* FROM items WHERE id = '" . $validid . "'";
$itemresult = mysql_query($itemsql);
$itemrow = mysql_fetch_assoc($itemresult);
```

In index.php, only items that were newer than the date and time were returned by the `MySQL_NOW()` function. For completeness, the page checks this with PHP rather than `MySQL`.

Inside the query, the `UNIX_TIMESTAMP()` command converts the dateends field into the number of seconds since the epoch. The query is then executed, and a row is stored in the `$itemrow` array.

Check to see if the current item has ended:

```php
$itemrow = mysql_fetch_assoc($itemresult);
$nowepoch = mktime();
$rowepoch = $itemrow['dateepoch'];
if($rowepoch < $nowepoch) {
    $VALIDACTION = 1;
}
```

The `mktime()` function stores the seconds since the epoch for the current time in the `$nowepoch` variable. The `$rowepoch` variable then stores the epoch returned from the row. A check is made to see if `$rowepoch` is greater than `$nowepoch` and if so, a variable called $VALIDAUCTION is set to 1 (the capitalization of the variable is used only to make it stand out in the code). $VALIDAUCTION is checked later to determine if the auction is valid (still available to bid on).

Add the name of the item in a second-level heading tag:

```php
if($rowepoch > $nowepoch) {
    $VALIDAUCTION = 1;
}

echo "<h2>" . $itemrow['name'] . "</h2>";
```

Now run a query to get any images that are associated with an item:

```php
echo "<h2>" . $itemrow['name'] . "</h2>";

$imagesql = "SELECT * FROM images WHERE item_id = " . $validid . ";";
$imageesult = mysql_query($imagesql);
$imagenumrows = mysql_num_rows($imageesult);
```

The next query returns the highest bid and the number of bids for the item:

```php
$imagenumrows = mysql_num_rows($imageesult);

$bidsql = "SELECT item_id, MAX(amount) AS highestbid, COUNT(id) AS number_of_bids FROM bids WHERE item_id="
    . $validid . " GROUP BY item_id";
$bidresult = mysql_query($bidsql);
$bidnumrows = mysql_num_rows($bidresult);
```

The preceding query is similar to the one used in index.php to get the same information.

Display the information from the queries:

```php
$bidnumrows = mysql_num_rows($bidresult);

echo "<p>";

if($bidnumrows == 0) {
    echo "<strong>This item has had no bids</strong>
    - <strong>Starting Price</strong>: " . $config_currency
    . sprintf('%.2F', $itemrow['startingprice'])";
}
else {
    $bidrow = mysql_fetch_assoc($bidresult);
```

```php
echo "<strong>Number Of Bids</strong>: "
. $bidrow['number_of_bids'] . "
- <strong>Current Price</strong>: " . $config_currency
. sprintf('%2f', $bidrow['highestbid']);
}
```

If no rows were counted in `$bidnumrows`, the page displays not only text that indicates no bids were placed but also the starting price. When rows are present, the page displays both the number of bids and the highest bid price.

Display the date when the auction ends:

```php
echo "<strong>Number Of Bids</strong>: "
. $bidrow['number_of_bids'] . "
- <strong>Current Price</strong>: " . $config_currency
. sprintf('%2f', $bidrow['highestbid']);
}
```

```php
echo " - <strong>Auction ends</strong>: "
. date("D J S F Y g.iA", $rowepoch);
```

Display any images of the item:

```php
echo " - <strong>Auction ends</strong>: "
. date("D J S F Y g.iA", $rowepoch);

echo "</p>";

if($imagenumrows == 0) {
  echo "No images.";
}
else {
  while($imagerow = mysql_fetch_assoc($imageresult)) {
    echo "<img src="./images/" . $imagerow['name'] ."" width="200">";
  }
}
```

The `$imagenumrows` variable is checked to see if any rows were returned. If not, the text No images displays. If rows were returned, the `while` loop displays each image.

Add the item description. Use the `nl2br()` function to ensure that any whitespace lines are added:

```php
}

echo "<p>" . nl2br($itemrow['description']) . "</p>";
```

You can now start work on adding the bid entry box. This functionality should be available only if the user is logged in. First, display a heading to indicate the bidding area:

```php
echo "<p>" . nl2br($itemrow['description']) . "</p>";

echo "<a name='bidbox'>";
echo "<h2>Bid for this item</h2>";
```

The anchor in this code is used when the user is not logged in, clicks the link to log in, and is then redirected to the bidding area.

To see if the user is logged in, check the USERNAME session variable:

```php
echo "<h3>Bid for this item</h3>";

if(!isset($_SESSION['USERNAME']) == FALSE) {
    echo "To bid, you need to log in. Login"
    "<a href='login.php?id=' . $validid . '&ref=addbid'>here</a>.";
}
```

If the user is not logged in and the isset() function returns FALSE, the user can click the link to log in. The login link adds the id of the item and a variable called ref as GET variables. This is the same technique used in the forums project.

Run the code if the user is logged in:

```php
echo "To bid, you need to log in. Login"
"<a href='login.php?id=' . $validid . '&ref=addbid'>here</a>.";
} else {
    if($VALIDAUCTION == 1) {
        echo "Enter the bid amount into the box below.";
        echo "<p>";

        switch($_GET['error']) {
            case "lowprice":
                echo "The bid entered is too low.
Please enter another price.";
                break;
            case "letter":
                echo "The value entered is not a number.";
                break;
        }
}
```

```php
?>
```

If $VALIDAUCTION is equal to 1, a switch statement checks the value of the error GET variable, and the page displays the relevant error.

Add the form:

```php
<?php echo pf_script_with_get($SCRIPT_NAME);
?> method="post">
 <table>
 <tr>
 <td><input type="text" name="bid"/></td>
 <td><input type="submit" name="submit" value="Bid!"/></td>
 </tr>
 </table>
 </form>
```

If $VALIDAUCTION is not set to 1, inform the user that the auction has ended:

```php
<?php
} else {
 echo "This auction has now ended.";
}
```

After the bid box, it is helpful to list a history of bids and the users who placed them:

```php
} else {
 echo "This auction has now ended.";
}
$historysql = "SELECT bids.amount, users.username FROM bids,
 users WHERE bids.user_id = users.id AND item_id = "
 . $validid . " ORDER BY amount DESC";
$historyresult = mysql_query($historysql);
$historynumrows = mysql_num_rows($historyresult);

if($historynumrows >= 1) {
 echo "<h2>Bid History</h2>";
 echo "<ul>";
 while($historyrow = mysql_fetch_assoc($historyresult)) {
 echo "<li>" . $historyrow['username'] . " - "
 . $config_currency . sprintf('%.2f', $historyrow['amount']) . "</li>";
 }
 echo "</ul>";
}
```
