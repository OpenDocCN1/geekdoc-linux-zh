```
echo $bidrow['numberofbids'] . "</td>";
}

echo "<td>" . $config_currency;

if($bidnumrows == 0) {
    echo sprintf('%.2F', $row['startingprice']);
} else {
    echo sprintf('%.2F', $bidrow['highestbid']);
}
echo "</td>";
```

This query uses a few MySQL functions to determine the highest bid and the number of bids. To better explain this, read the SQL from left to right:

Select (SELECT) the item_id (item_id), use the MySQL MAX() function to find the highest value within the amount field and alias the field as highest bid (MAX(amount) AS highestbid). Use the MySQL COUNT() function to count the number of records and alias the field as numberofbids (COUNT(id) AS numberofbids) from the bids table (FROM bids), in which the item_id is equal to $row['id'] (WHERE item_id = $row['id']), and group the records by item_id (GROUP BY item_id).

If no rows are returned from the query, 0 is added to the table; otherwise, the value of numberofbids is added. $bidnumrows does not return 0 when no rows exist because if there are no bids, there are no entries in the bids table to count with the COUNT() function. As such, nothing is returned. Always remember in programming that 0 is a value, and it is often different to the concept of nothing.

The next column is the latest price. Before a value is displayed, the currency is added from the $config_currency field.

![](bbox=[0.08, 0.7, 0.2, 0.73])

# Dealing with Currencies

When dealing with monetary units such as prices, quotes, figures, and other numbers, never include the currency sign in the database. Currency is really just an additional piece of information that gives the number a context. If you want the currency symbol in the database, store the number and symbol as a VARCHAR.

Storing the price as a number and without the symbol allows you to do things such as taxes, addition expenses, currency conversion, and other calculations.