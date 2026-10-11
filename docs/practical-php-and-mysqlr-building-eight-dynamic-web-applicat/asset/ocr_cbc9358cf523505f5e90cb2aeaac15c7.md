If $bidnumrows has no rows, the startingprice field from the first query is displayed (if there are no bids, the starting price should be displayed). If there are bids, the highest bid is displayed ($bidrow['highestbid']) from the last query. Both prices are formatted.

**NOTE**
**Formatting Prices**
When you use a FLOAT to store a price in the database, the trailing zeros are removed by default. To reformat the price with zeros, use the PHP function sprintf(). The function takes two arguments: the formatting string and the value to format. The formatting string takes a value such as %.2f, which asks for two decimal places (.2) on a floating point number (f).

Finally, display and format the dateends field:

```
```
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
```

# Viewing Item Details and Placing Bids

The next page is linked from the name of the item on the page you just created. This script has two primary purposes:

+   ■ To display information about the item, including images of it.
+   ■ To allow a user to bid on the item.

To place a bid, you need to check if the user is logged in, and if so, display a form into which she can type a bid amount. The page then checks that the amount is legitimate and adds the bid to the bids table.