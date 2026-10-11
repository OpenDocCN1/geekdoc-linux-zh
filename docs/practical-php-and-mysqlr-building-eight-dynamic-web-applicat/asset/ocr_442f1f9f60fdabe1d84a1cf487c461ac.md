```
```
else if($POST['chequesubmit'])
{
    $sql = "UPDATE orders SET status = 2, payment_type = 2 WHERE id = 
    '$_SESSION['SESS_ORDERNUM']';
    $res = mysql_query($sql);
```
```

Here you again update the orders table, but this time the `payment_type` is `2` instead of `1`.

Reset the order as you did previously:

```
```
$res = mysql_query($sql);
if($SESSION['SESS_LOGGEDIN'])
{
    unset($SESSION['SESS_ORDERNUM']);
}
else
{
    session_register("SESS_CHANGEID");
    $SESSION['SESS_CHANGEID'] = 1;
}
```
```

Finally, display the details of where the user should send the check:

```
```
$SESSION['SESS_CHANGEID'] = 1;
? >

require("header.php");
?>
<h1>Paying by cheque</h1>
Please make your cheque payable to
<strong><?php echo $config_sitename; ?> </strong> .
<p>
Send the cheque to:
<p>
<?php echo $config_sitename; ?><br>
22, This Place,<br>
This town,<br>
This county,<br>
FG43 F3D.<br>
</p>
? >
}
```
```

The processing is now complete

Open the block to display the form. Before you reach the form, however, add the `showcart()` function to summarize the current cart: