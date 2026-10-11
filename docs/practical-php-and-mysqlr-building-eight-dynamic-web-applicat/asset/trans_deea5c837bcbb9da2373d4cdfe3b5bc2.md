

```php
<td><textarea name="about" rows="10" cols="50"><?php echo $row[ 'about' ] ?></textarea></td>
</tr>
<tr>
<td></td>
<td><input type="submit" name="submit" value="Modify details"></td>
</tr>
</table>
</form>
</php>
}
?>
```

完成后的表单外观应如图 10-6 所示。

![](img/c75d0c4fa51711b62f211459ae794f3f_421_0.png)

**图 10-6** 一个简单的表单，允许更改项目设置。

# 管理下载

在项目管理中，最重要的功能之一就是查看不同版本和可用下载的能力。这不仅是一个基本功能，而且相当复杂，因为同一页面呈现了两种不同类型的功能（管理版本和管理发行版）。在开始编写页面代码之前，退后一步确定该功能应如何工作。这将使理解代码变得更容易。

下载的管理是在图 10-7 所示的界面中进行的。

| 添加新版本 |
|---|
| **0.2** | 无发行版！ | 添加新发行版 |
| **0.1** | [X] Tarball | 添加新发行版 |
| | [X] Debian 包 | |

![](img/c75d0c4fa51711b62f211459ae794f3f_422_0.png)

在表格内，可以看到版本号、发行版以及添加新内容的链接。与其点击链接跳转到另一个页面来添加版本或发行版，不如用表单替换链接更合理。因此，当你点击“添加新版本”链接时，你会看到如图 10-8 所示的结果。

![](img/c75d0c4fa51711b62f211459ae794f3f_422_1.png)

![](img/c75d0c4fa51711b62f211459ae794f3f_422_2.png)

类似地，当你点击“添加新发行版”链接时，你会看到如图 10-9 所示的结果。

![](img/c75d0c4fa51711b62f211459ae794f3f_422_3.png)

![](img/c75d0c4fa51711b62f211459ae794f3f_422_4.png)

代码的复杂性并不具体体现在困难或复杂的语句上，而在于大量检查不同条件并相应处理的嵌套块。建议先添加完整的代码，然后再重新阅读其工作原理的说明。

创建一个名为 *project_admin/downloads.php* 的新文件，并开始添加代码。首先显示图 10-7 中所示的界面（你可以稍后处理表单）：

```php
$versql = "SELECT * FROM homeproject_releaseversions WHERE
 project_id = ' . $_SESSION['SESS_PROJECTID'] . ' ORDER BY id DESC";
 $verresult = mysql_query($versql);
 $vernrmrows = mysql_num_rows($verresult);

 echo "<h1>Manage Downloads</h1>";
```

首先选择与当前项目相关的所有版本。打开表格并添加第一行：

```php
echo "<h1>Manage Downloads</h1>";

echo "<table border=1 cellpadding=5>";

echo "<tr><td colspan=3>";
```

第一行可以包含“添加新版本”链接或添加版本的表单。如果用户点击链接，会将一个 *addver* GET 变量发送到页面。因此，检查此变量是否存在。如果存在，显示表单；否则，显示链接：

```php
echo "<tr><td colspan=3>";
if($_GET['addver']) {
  echo "<form action=" . SCRIPT_NAME . "?func=downloads"
  method="POST">";
  echo "<strong>New Release Number: ";
  echo "<input type="text" name="version">";
  echo "<input type="submit" value="Add" name="versubmit">";
  echo "</form>";
} else {
  echo "<a href=" . SCRIPT_NAME . "?func=downloads&addver=1>"
Add a New Version</a>";
}

echo "</td></tr>";
```

完成第一行后，遍历版本。首先，检查查询是否返回了任何版本：

### 注意

#### 获取正确的提交按钮

表单中的 Submit 按钮命名为 *versubmit*。此页面有两个 Submit 按钮（一个用于版本，一个用于发行版），你需要能够区分点击了哪一个。

```php
echo "</td></tr>";

if($vernumrows == 0) {
  echo "<tr><td colspan=2>This project has no versions or releases.</td></tr>";
}
```

如果没有行存在，则显示一条消息，表明没有版本或发行版。如果存在行，则显示它们：

```php
echo "<tr><td colspan=2>This project has no versions or releases.</td></tr>";
} else {
  while($vverrow = mysql_fetch_assoc($verresult)) {
    echo "<tr>";
    echo "<td><strong>" . $verrow['version'] . "</strong></td>";
    echo "<td>";
```

```php
$relesql = "SELECT homeproject_releasefiles.id, homeproject_releasefiles.filename, homeproject_releasefiles.date, homeproject_releasetypes.type FROM homeproject_releaseversions INNER JOIN homeproject_releasefiles ON homeproject_releasefiles.version_id = homeproject_releaseversions.id INNER JOIN homeproject_releasetypes ON homeproject_releasetypes.type_id = homeproject_releasetypes.id WHERE homeproject_releaseversions.id = '" . $verrow['id'] .
"';
$relresult = mysql_query($relesql);
$relnumrows = mysql_num_rows($relresult);
```

在这种情况下，你在第一个单元格中添加版本号，然后运行查询以收集该版本可用的发行版。此查询通过执行内连接将 *homeproject_releaseversions*、*homeproject_releasefiles* 和 *homeproject_releasetypes* 表连接在一起，返回每个版本的 *id*、*filename*、*date* 和 *type*。

检查是否返回了任何发行版，并相应显示：

```php
$relnumrows = mysql_num_rows($relresult);

if($relnumrows == 0) {
    echo "No releases!";
}
else {
    while($relerow = mysql_fetch_assoc($releresult)) {
        echo "<a href='' . $SCRIPT_NAME
. "?func=deleteRelease&relid=" . $relerow['id'] . "' target='_blank'>";
        echo $relerow['file'];
    }
}
```

在每个发行版旁边，添加一个 X 链接，以便用户可以删除发行版。此链接指向 `deleteRelease` 块并传递发行版的 id。（该块稍后讨论。）

在第三个单元格中，显示“添加新发行版”链接或表单。当链接被点击时，地址栏中会添加一个名为 `addRelelver` 的 GET 变量，其值设置为版本 id。如果当前行的版本 id 与 `addRelelver` 的值相同，则点击的是当前行上的链接。因此，你需要显示表单：

```php
echo "</td>";
echo "<td>";
if($GET['addRelelver'] == $verrow['id']) {
    $typesql = "SELECT * FROM homeproject_releasetypes;";
    $typesresult = mysql_query($typesql);
    echo "<form action='' . $SCRIPT_NAME
. "?func=download&ver=" . $verrow['id'] . "' method='POST' enctype='multipart/form-data'>";
    echo "<select name='type'>";
    while($typesrow = mysql_fetch_assoc($typesresult)) {
        echo "<option value='" . $typesrow['id'] . "'>" . $typesrow['type'] . "</option>";
    }
    echo "</select>";
    echo "<input type='file' name='releasefile'>";
    echo "<input type='submit' value='Add' name='relsubmit'>";
    echo "</form>";
} else {
    echo "<a href='' . $SCRIPT_NAME
. "?func=download&addRelelver=" . $verrow['id'] . "' target='_blank'>Add a New Release</a>";
}
```

当显示表单时，选择框包含 `homeproject_releasetypes` 表中类型的列表。Submit 按钮名为 `relsubmit`，这样你就可以确定用户点击的是版本还是发行版 Submit 按钮。

关闭剩余代码：

```php
echo "<a href=\"" . $SCRIPT_NAME
. "?func=downloads&addrelver=\" . $verrw['id']
. "">Add a New Release</a>";
}
echo "</td>";
echo "</tr>";
}
echo "</table>";
}
```

完成主要界面部分后，你可以专注于处理表单。跳到文件开头，开始添加代码：

```php
<?php
require_once('../project_functions.php');
pf_protect_admin_page();

$upload_dir = $config_projectdir . $_SESSION['SESS_PROJECTPATH']
. "/releases/";
```

在保护页面后，你设置了一个名为 `$upload_dir` 的变量。此变量指定了发行版上传的位置。你希望将文件上传到项目目录中的 `releases` 目录，以便你可以连接 `$config_projectdir` 和 `SESS_PROJECTPATH` 变量，然后添加 `releases` 目录。

开始处理版本表单：

```php
$upload_dir = $config_projectdir . $_SESSION['SESS_PROJECTPATH']
. "/releases/";
if($_POST['versubmit']) {
  $adds q1 = "INSERT INTO homeproject_releaseversions(project_id,
  version) VALUES("
  . $_SESSION['SESS_PROJECTID']
  . ", '" . $_POST['version'] . "')";
  mysql_query($addsql);
  header("Location: " . $config_projectadminbasedir
  . basename($SCRIPT_NAME) . "?func=downloads");
}
```

