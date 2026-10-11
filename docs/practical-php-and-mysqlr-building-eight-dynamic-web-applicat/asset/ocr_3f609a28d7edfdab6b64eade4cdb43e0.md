If no rows were returned, it means the entered bid is the first bid entered (no others bids have been previously entered). Next, a check is made to see if the starting price is greater than the entered bid. If it is, a header redirect is made to the same page, but the error GET variable is added with a value of lowprice.

When previous bids exist, ensure the current highest bid is not higher than the entered bid:

```
```
} else {
    $checkbidrow = mysql_fetch_assoc($checkbidresult);
    if($checkbidrow['highestbid'] > $_POST['bid']) {
        header("Location: " . $config_basedir . "itemdetails.php?id=" .
            $validid . "&error=lowprice#bidbox");
    }
}
```
```

If highestbid is higher than the bid entered, a header redirect is made.

With the checks out of the way, run the INSERT query to actually add the bid to the bids table:

```
```
header("Location: " . $config_basedir .
    "/itemdetails.php?id=" . $validid .
    "&error=lowprice#bidbox");
}$$

$sql = "INSERT INTO bids(item_id, amount, user_id) VALUES("
    . $validid
    . ", " . $_POST['bid']
    . ", " . $_SESSION['USERID'] . ")";
mysql_query($sql);
```
```

Close the block and prepare to add the rest of the code:

```
```
. "");"
mysql_query($sql);

header("Location: " . $config_basedir .
    "itemdetails.php?id=" . $validid);

} else {
```
```

Finally, at the bottom of the file, add a curly bracket to close the else block:

```
```
echo "</ul>";
}
}
```
```

```
require("footer.php");
```