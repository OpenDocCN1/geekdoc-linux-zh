so, a variable called $VALIDAUCTION is set to 1 (the capitalization of the variable is used only to make it stand out in the code). $VALIDAUCTION is checked later to determine if the auction is valid (still available to bid on).

Add the name of the item in a second-level heading tag:

```
```php
if($rowepoch > $nowepoch) {
    $VALIDAUCTION = 1;
}

echo "<h2>" . $itemrow['name'] . "</h2>";
```
```

Now run a query to get any images that are associated with an item:

```
```php
echo "<h2>" . $itemrow['name'] . "</h2>";

$imagesql = "SELECT * FROM images WHERE item_id = " . $validid . ";";
$imageesult = mysql_query($imagesql);
$imagenumrows = mysql_num_rows($imageesult);
```
```

The next query returns the highest bid and the number of bids for the item:

```
```php
$imagenumrows = mysql_num_rows($imageesult);

$bidsql = "SELECT item_id, MAX(amount) AS highestbid, COUNT(id) AS number_of_bids FROM bids WHERE item_id="
    . $validid . " GROUP BY item_id";
$bidresult = mysql_query($bidsql);
$bidnumrows = mysql_num_rows($bidresult);
```
```

The preceding query is similar to the one used in index.php to get the same information.

Display the information from the queries:

```
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
```