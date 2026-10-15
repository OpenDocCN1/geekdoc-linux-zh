
```php
require("header.php");
echo "<h1>Add a delivery address</h1>";

if(isset($_GET['error']) == TRUE) {
    echo "<strong>Please fill in the missing information from the form</strong>";
}

echo "<form action=" . $SCRIPT_NAME . " method='POST'>";

if($_SESSION['SESS_LOGGEDIN'])
{
?>
    <input type="radio" name="addselectBox" value="1" checked>Use the address from my account</input><br>
    <input type="radio" name="addselectBox" value="2">Use the address below:</input>
<?php
}
?>
    <table>
        <tr>
            <td>Forename</td>
            <td><input type="text" name="forenameBox"></td>
        </tr>
        <tr>
            <td>Surname</td>
            <td><input type="text" name="surnameBox"></td>
        </tr>
        <tr>
            <td>House Number, Street</td>
            <td><input type="text" name="addlBox"></td>
        </tr>
        <tr>
            <td>Town/City</td>
            <td><input type="text" name="add2Box"></td>
        </tr>
        <tr>
            <td>County</td>
            <td><input type="text" name="add3Box"></td>
        </tr>
        <tr>
            <td>Postcode</td>
            <td><input type="text" name="postcodeBox"></td>
        </tr>
        <tr>
            <td>Phone</td>
            <td><input type="text" name="phoneBox"></td>
        </tr>
    </table>
    <br>
    <input type="submit" value="Continue">
</form>

<?php
require("footer.php");
?>
```

在表单显示之前，一个 `if` 语句会检查是否存在错误 `GET` 变量。如果存在，则显示错误消息。随后脚本检查用户是否已登录，如果是，则添加两个单选按钮，以便用户在注册地址和其他地址之间进行选择。

将光标移至文件开头并添加以下代码：

```php
<?php
    session_start();
    require("db.php");

    $statussql = "SELECT status FROM orders WHERE id = " .
    $_SESSION['SESS_ORDERNUM'];
    $statusres = mysql_query($statussql);
    $statusrow = mysql_fetch_assoc($statusres);
    $status = $statusrow['status'];
?>
```

第一步是确定订单的当前状态。如果用户已经通过了结账流程中的地址阶段，则重定向页面到支付屏幕。通过搜索 `orders` 表中与 `SESS_ORDERNUM` 匹配的记录来获取状态。然后，将 `$status` 变量设置为正确的状态。

> **注意**
>
> 请记住，状态可以是以下值中的任意一个：
>
> | 值 | 描述 |
> | :---- | :---------- |
> | 0     | 用户仍在购物。 |
> | 1     | 用户已完成地址输入。 |
> | 2     | 用户已付款。 |
> | 10    | 管理员已确认订单。 |

如果状态设置为 `1`，表示用户已输入地址，页面将重定向到支付屏幕。如果状态为 `2` 或更高，则表示订单已完成。将页面重定向到网站的基础 URL：

```php
if($status == 1) {
    header("Location: " . $config_basedir . "checkout-pay.php");
}

if($status >= 2) {
    header("Location: " . $config_basedir);
}
```

开始处理表单：

```php
if($status >= 2) {
    header("Location: " . $config_basedir);
}

if($_POST['submit'])
{
    if($_SESSION['SESS_LOGGEDIN'])
    {
        if($_POST['addselecBox'] == 2)
        {
            if(empty($_POST['firstnameBox']) ||
               empty($_POST['surnameBox']) ||
               empty($_POST['add1Box']) ||
               empty($_POST['add2Box']) ||
               empty($_POST['add3Box']) ||
               empty($_POST['postcodeBox']) ||
               empty($_POST['phoneBox']) ||
               empty($_POST['emailBox']))
            {
                header("Location: " . $basedir . "checkout-address.php?error=1");
                exit;
            }
        }
    }
}
```

第一个嵌套的 `if` 语句检查用户是否已登录。然后检查用户是否选择了第二个单选按钮（使用下面的地址）。如果是，则检查表单字段是否为空。如果为空，页面将重新加载并附带 `error` `GET` 变量，以便显示错误消息。

如果表单不为空，将地址添加到 `delivery_addresses` 表并更新 `orders` 表：

```php
$addsql = "INSERT INTO delivery_addresses (firstname, surname, add1, add2, add3, postcode, phone, email) VALUES("
. strip_tags(addslashes($_POST['firstnameBox'])) . ", "
. strip_tags(addslashes($_POST['surnameBox'])) . ", "
. strip_tags(addslashes($_POST['add1Box'])) . ", "
. strip_tags(addslashes($_POST['add2Box'])) . ", "
. strip_tags(addslashes($_POST['add3Box'])) . ", "
. strip_tags(addslashes($_POST['postcodeBox'])) . ", "
. strip_tags(addslashes($_POST['phoneBox'])) . ", "
. strip_tags(addslashes($_POST['emailBox'])) . ")";
mysql_query($addsql);

$setaddrsql = "UPDATE orders SET delivery_add_id = " . mysql_insert_id() . ", status = 1 WHERE id = " . $_SESSION['SESS_ORDERNUM'];
mysql_query($setaddrsql);
```
