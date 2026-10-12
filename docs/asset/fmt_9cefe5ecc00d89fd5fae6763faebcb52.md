
```php
$row = mysql_fetch_assoc($result);

echo "<h1>Submitted question details</h1>";
echo "<table border='0' cellspacing='0' cellpadding='5'>";
echo "<tr>";
echo "<td><b>Subject</b></td>";
echo "<td>" . $row['subject'] . "</td>";
echo "</tr>";
echo "<tr>";
echo "<td><b>Topic</b></td>";
echo "<td>" . $row['name'] . "</td>";
echo "</tr>";
echo "<tr>";
echo "<td><b>Question</b></td>";
echo "<td>" . $row['question'] . "</td>";
echo "</tr>";
echo "<tr>";
echo "<td><b>Answer</b></td>";
echo "<td>" . $row['answer'] . "</td>";
echo "</tr>";
echo "<td colspan=2>";
```

# allow 代码块

若要允许某条问题，请添加 `allow` 代码块：

```php
echo "</table>";
break;

case "allow":
	$validid = set_validid();
	
	$modqsql = "UPDATE questions SET active = 1 WHERE id = "
	.	$validid . "";
	$modq = mysql_query($modqsql);
	
	header("Location: " . $config_basedir .
	"adminmodquestions.php?func=main");
break;
```

此代码块更新该问题并将 `active` 字段设置为 `1`，以将该问题设为已启用状态。随后页面重定向至 `adminmodquestions.php` 的主代码块。

# deny 代码块

若要拒绝某条问题，该过程分为两个部分。第一部分询问用户是否确认希望拒绝该问题。参见图 9-13。

![](img/c75d0c4fa51711b62f211459ae794f3f_368_0.png)

图 9-13 在拒绝问题之前，请确认这是用户希望执行的操作。

添加此部分的代码：

```php
header("Location: " . $config_basedir .
"adminmodquestions.php?func=main");
break;

case "deny":
    require("header.php");

    $validid = set_validid();

    echo "<h1>Are you sure that you want to reject this question?</h1>";
    echo "<p><a href=" . $SCRIPT_NAME . "?func=denyconf&id="
    . $validid . ">Yes</a>] [<a href="" . $SCRIPT_NAME
    . "?func=main">No</a>]";
    break;
```

此代码块提供了两个链接。`No` 链接只是链接回当前脚本的主部分，而 `Yes` 链接则链接到 `denyconf` 部分。

# denyconf 代码块

为了确认拒绝某条问题这一冷酷而现实的操作，请添加 `denyconf` 代码块：

```php
echo "<p><a href=" . $SCRIPT_NAME . "?func=denyconf&id="
. $validid . ">Yes</a>] [<a href="" . $SCRIPT_NAME
. "?func=main">No</a>]";
break;
case "denyconf":
    $validid = set_validid();

    $delsql = "DELETE FROM questions WHERE id = " . $_GET['id']
    . "";
    $delq = mysql_query($delsql);

    header("Location: " . $config_basedir .
    "adminmodquestions.php?func=main");
    break;
```

此代码块从 `questions` 表中删除该问题，然后重定向回主部分以显示其他经过审核的问题。

最后，关闭 `switch` 语句并添加 `footer` 文件：

```php
header("Location: " . $config_basedir .
"adminmodquestions.php?func=main");
break;
}

require("footer.php");
?>
```

# 管理主题

主题是本项目管理内容的核心基础，与第 4 章博客项目中的 `Categories` 分类非常相似。管理主题自然只应由管理员执行。如果你将主题的权限交给普通用户，可能会发生任何事情。

添加和删除主题的能力是重要的功能组成部分，但删除操作需要格外小心。使用 MySQL 中的 `InnoDB` 表时，任何意外删除主题的操作都会导致该主题下的所有子主题 `topics` 和问题 `questions` 一并被删除。因此，在处理此部分时请务必非常小心。

## 添加主题

向数据库添加主题就像创建一个表单并将表单内容添加到数据库中一样简单。创建名为 `addsubject.php` 的新文件，并添加以下代码：

```php
<h1>Add a new subject</h1>
<form action="<?php echo $SCRIPT_NAME; ?>" method="post">
<table cellpadding="5">
<tr>
<td>Subject</td>
<td><input type="text" name="subject"></td>
</tr>
<td>Owner</td>
<td>
```

此代码添加了表单和表格以布局表单元素。在添加主题文本框后，显示一个下拉框，以便选择主题所有者：

```php
<td>Owner</td>
<td>
<select name="owner">
<option value="0">-- No Owner --</option>
<?php
$sql = "SELECT * FROM users ORDER BY username ASC;";
$result = mysql_query($sql);

while($row = mysql_fetch_assoc($result)) {
echo "<option value=" . $row['id'] . " >" . $row["username"] . "</option>";
}
?>
</select>
```

创建了一个下拉框，并添加第一个条目返回值为 `0` 以提供“无所有者”选项。下拉框中的其他条目从查询结果中添加。

完成表单：

```php
            ?>
            </select>
            </td>
        </tr>
        <tr>
            <td>Description Blurb</td>
            <td><textarea name="blurb" cols=50 rows=10></textarea></td>
        </tr>
        <tr>
            <td></td>
            <td><input type="submit" name="submit" value="Add Subject!"/></td>
        </tr>
    </table>
</form>
```

表单完成后，到了处理的时候。跳转到文件开头并添加以下代码：

```php
<?php

session_start();

require("db.php");
require("functions.php");

if(isset($_SESSION['SESS_ADMINUSER']) == FALSE) {
    header("Location: " . $config_basedir . "adminlogin.php");
}
```

首先保护该页面，使其仅管理员可以访问。检查 `Submit` 按钮是否被点击并开始处理：
