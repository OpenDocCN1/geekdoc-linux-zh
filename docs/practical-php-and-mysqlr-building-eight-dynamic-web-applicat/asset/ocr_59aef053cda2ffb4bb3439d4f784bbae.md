```
if($_POST['paypalsubmit'])
{
    $supsql = "UPDATE orders SET status = 2, payment _type = 1 WHERE id = " . $_SESSION['SESS_ORDERNUM'];
    $upres = mysql_query($supsql);

    $itemsmsql = "SELECT total FROM orders WHERE id = " . $_SESSION['SESS_ORDERNUM'];
    $itemsres = mysql_query($itemsmsql);
    $row = mysql_fetch_assoc($itemsres);
```

The `orders` table is updated to reflect the completion of the order. The `status` field is changed to 2 and the `payment_type` field is set to 1 (PayPal). A query then gets the total price from the order so that the PayPal link can be constructed later.

Reset the order session:

```
$row = mysql_fetch_assoc($itemsres);
if($_SESSION['SESS_LOGGEDIN'])
{
    unset($_SESSION['SESS_ORDERNUM']);
}
else
{
    session_register("SESS_CHANGEID");
    $_SESSION['SESS_CHANGEID'] = 1;
}
```

If the user is logged in, the SESS_ORDERNUM session variable is removed with `unset()`. If not, a new session variable called SESS_CHANGEID is created. The next time `header.php` is loaded, the code at the top of `header.php` will regenerate the new session and id.

Redirect to www.paypal.com with the payment details:

```
$_SESSION['SESS_CHANGEID'] = 1;
}

header("Location: https://www.paypal.com/ cgi-bin/webscr?cmd=_xclick&business= you$40youraddress.com&item_name=" . urlencode($config_sitename)
    . "+Order&item_number=PROD" . $row['id'] . "&amount=" . urlencode(sprintf('%.2f', $row['total']))) . "&no_note=1&currency_code=GB&l c=GB&submit.x=41&submit.y=15");
```