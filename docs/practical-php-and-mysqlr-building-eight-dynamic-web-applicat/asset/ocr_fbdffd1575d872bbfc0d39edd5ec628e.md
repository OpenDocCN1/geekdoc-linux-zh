# ## Viewing a Specific Order

For the administrator to get the postal address for a particular order, she needs to view the specific details for the order. This next page lists the order information (order number, address, products purchased, payment method, and so on).

Create a new file called *adminorderdetails.php* and add the following code:

```
<?php
session_start();

require("config.php");
require("functions.php");

if(!isset($_SESSION['SESS_ADMINLOGGEDIN']) == FALSE) {
header("Location: " . $basedir);}

$validid = pf_validate_number($_GET['id'],
"redirect", $config_basedir . "adminorders.php");
require("header.php");

echo "<h1>Order Details</h1>";
echo "<a href='adminorders.php'>&lt;-- go back
to the main orders screen</a>";

$ordersql = "SELECT * from orders WHERE id = " . $validid;
$orders = mysql_query($ordersql);
$ordrow = mysql_fetch_assoc($orders);

echo "<table cellpadding=10>";
echo "<tr><td><strong>Order Number</strong>"
</td><td>" . $ordrow['id'] . "</td>";
echo "<tr><td><strong>Date of order</strong>"
<td><td>" . date('D jS F Y g.iA',
strtotime($ordrow['date'])) . "</td>";
echo "<tr><td><strong>Payment Type</strong></td><td>";
if($ordrow['payment_type'] == 1)
{
echo "PayPal";
}
else
{
echo "Cheque";
}
echo "</td>";
echo "</table>";
```