# CHAPTER 7  Building an Online Auction Site



Create a new <div> and add a table to list the items:

```
```php
$result = mysql_query($sql);
$numrows = mysql_num_rows($result);

echo "<h1>Items available</h1>";
echo "<table cellpadding="5">";
echo "<tr>";
    echo "<th>Image</th>";
    echo "<th>Item</th>";
    echo "<th>Bids</th>";
    echo "<th>Price</th>";
echo "</tr>";
```
```

Determine if any items are available by checking the value of $numrows:

```
```php
echo "<th>Bids</th>";
echo "<th>Price</th>";
echo "</tr>";

if($numrows == 0) {
    echo "<tr><td colspan=4>No items!</td></tr>";
}
```
```

If $numrows is equal to 0 (no rows were returned), the text No items! is displayed in the table.

If items were returned and $numrows is greater than 0, you can iterate through each item and display them in the table:

```
```php
if($numrows == 0) {
    echo "<tr><td colspan=4>No items!</td></tr>";
}
else {
    while($row = mysql_fetch_assoc($result)) {
        $imagesql = "SELECT * FROM images WHERE item_id = " . $row['id'] . " LIMIT 1";
        $imageresult = mysql_query($imagesql);
        $imagenumrows = mysql_num_rows($imageresult);

        echo "<tr>";
        if($imagenumrows == 0) {
            echo "<td>No image</td>";
        }
        else {
            $imageorow = mysql_fetch_assoc($imageresult);
            echo "<td><img src="./images/" . $imageorow['name'] . " width='100'></td>";
        }
```
```