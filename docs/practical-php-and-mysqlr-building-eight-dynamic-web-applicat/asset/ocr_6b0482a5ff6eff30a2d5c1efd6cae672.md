as the hour, and 30 as the minute. With these numbers, the valid date would be 2005-12-10 11:30. The sprintf() function (which you used earlier to pad prices with zeros) was used again, this time to ensure that single digits have a leading zero (so 1 would become 01 and so on). This is important for the date to be a valid MySQL date.

Construct the query to insert the data:

```
$concatdate = $_POST['year']
          . "-" . sprintf("%02d", $_POST['day'])
          . "-" . sprintf("%02d", $_POST['month'])
          . "-" . $_POST['hour']
          . ":" . $_POST['minute']
          . ":00";

$itemsql = "INSERT INTO items(user_id, cat_id, name,
startingprice, description, dateends) VALUES("
          . $_SESSION['USERID']
          . ", " . $_POST['cat']
          . ", " . addslashes($_POST['name'])
          . ", " . $_POST['price']
          . ", " . addslashes($_POST['description'])
          . ", " . $concatdate
          . ");";

mysql_query($itemsql);
$itemid = mysql_insert_id();

header("Location: " . $config_basedir .
     "/addimages.php?id=" . $itemid);
```

Within the query, a new function called addslashes() was wrapped around the boxes that accept input in the form of letters. This helps to prevent input errors.

Finally, a header redirect jumps to the addimages.php page and passes it a GET variable, called id, with the insert id.

Earlier in the code, you made a check to see if the date was valid. If the date was invalid, reload the page and pass the error flag:

```
header("Location: " . $config_basedir . "/addimages.php?id=" .
$itemid);
} else {
header("Location: " . $config_basedir .
"/newitem.php?error=date");
}
```