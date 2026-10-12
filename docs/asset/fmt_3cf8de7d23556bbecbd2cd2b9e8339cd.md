
```php
echo "<h3>Bid for this item</h3>";

if(!isset($_SESSION['USERNAME']) == FALSE) {
    echo "To bid, you need to log in. Login"
    "<a href='login.php?id=' . $validid . '&ref=addbid'>here</a>.";
}
```

如果用户未登录且 `isset()` 函数返回 `FALSE`，用户可以点击链接登录。登录链接将物品的 `id` 和一个名为 `ref` 的变量作为 `GET` 变量添加。这与论坛项目中使用的技术相同。

如果用户已登录，则运行代码：

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

如果 `$VALIDAUCTION` 等于 `1`，`switch` 语句检查 `error` `GET` 变量的值，并显示相应的错误。

添加表单：

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

如果 `$VALIDAUCTION` 未设置为 `1`，告知用户拍卖已结束：

```php
<?php
} else {
 echo "This auction has now ended.";
}
```

在出价框之后，列出出价历史及进行出价的用户很有帮助：

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

前面的代码创建了一个查询，按降序返回出价金额和用户名。然后进行检查，判断行数是否大于或等于 `1`。如果是，则显示出价历史。

最后，添加页脚：

```php
echo "</ul>";
}
require("footer.php");
?>
```

主页面完成后，添加处理出价的代码。在 `itemdetails.php` 的开头添加此代码：

```php
$validid = pf_validate_number($_GET['id'], "redirect", $config_basedir);

if($_POST["submit"]) {
if(is_numeric($_POST["bid"]) == FALSE) {
header("Location: " . $config_basedir . "/itemdetails.php?id=" . $validid . "&error=letter");
}
```

检查出价是否为数值。如果不是，页面将重定向。在出价被接受之前，添加以下查询以获取一些信息：

```php
header("Location: " . $config_basedir
. "/itemdetails.php?id=" . $validid . "&error=letter");
}

$theitemsql = "SELECT * FROM items WHERE id = " . $validid . "";
$theitemresult = mysql_query($theitemsql);
$theitemrow = mysql_fetch_assoc($theitemresult);

$checkbidsql = "SELECT item_id, max(amount) AS
highestbid, count(id) AS number_of_bids FROM
bids WHERE item_id=" . $validid . " GROUP BY item_id";
$checkbidresult = mysql_query($checkbidsql);
$checkbidnumrows = mysql_num_rows($checkbidresult);
```

检查是否返回了任何出价：

```php
$checkbidresult = mysql_query($checkbidsql);
$checkbidnumrows = mysql_num_rows($checkbidresult);

if($checkbidnumrows == 0) {
if($theitemrow['startingprice'] > $_POST['bid']) {
header("Location: " . $config_basedir
. "/itemdetails.php?id=" . $validid . "&error=lowprice&bidbox");
}
}
```

如果没有返回行，这意味着输入的出价是第一个出价（之前没有其他人出价）。接下来，检查起拍价是否大于输入的出价。如果是，则执行 `header` 重定向到同一页面，但添加了值为 `lowprice` 的错误 `GET` 变量。

如果之前存在出价，确保当前最高出价不高于输入的出价：

```php
} else {
    $checkbidrow = mysql_fetch_assoc($checkbidresult);
    if($checkbidrow['highestbid'] > $_POST['bid']) {
        header("Location: " . $config_basedir . "itemdetails.php?id=" .
            $validid . "&error=lowprice#bidbox");
    }
}
```

如果 `highestbid` 高于输入的出价，则执行 `header` 重定向。

既然检查已经处理完毕，运行 `INSERT` 查询以实际将出价添加到 `bids` 表中：

```php
header("Location: " . $config_basedir .
    "/itemdetails.php?id=" . $validid .
    "&error=lowprice#bidbox");
}

$sql = "INSERT INTO bids(item_id, amount, user_id) VALUES("
    . $validid
    . ", " . $_POST['bid']
    . ", " . $_SESSION['USERID'] . ")";
mysql_query($sql);
```

关闭代码块并准备添加其余代码：
