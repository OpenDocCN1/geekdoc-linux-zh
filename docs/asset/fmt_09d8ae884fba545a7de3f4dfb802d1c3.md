
**图 16-2 向目录表插入数据**

由于我们省略了 `ID`，MySQL 会自动创建一个。这是由于我们将该列定义为 `AUTO_INCREMENT`。`VALUES` 关键字让服务器知道我们正准备发送之前命令中承诺的值。注意使用单引号包围文本，这是 SQL 的标准写法。

为了检查一切是否进展顺利，图 16–3 显示了如果你在 MySQL 客户端内部从 `catalog` 表中选择所有内容将得到的输出。我是通过输入得到这个输出的：

**图 16-3 SELECT * FROM catalog**

| ID | Name | Price |
| :--- | :--- | :--- |
| 1 | Toothbrush | 1.79 |
| 2 | Comb | 0.95 |
| 3 | Toothpaste | 5.39 |
| 4 | Dental Floss | 3.50 |
| 5 | Shampoo | 2.50 |
| 6 | Conditioner | 3.15 |
| 7 | Deodorant | 1.50 |
| 8 | Hair Gel | 6.25 |
| 9 | Razor Blades | 2.99 |
| 10 | Brush | 1.15 |

| 10 rows in set (0.01 sec)

## 第 16 章数据库集成

```sql
SELECT * FROM catalog;
```

最后一步是编写一个 PHP 脚本，获取表的内容并将其封装成 HTML 表格。在图 16–4 中，我选择将所有 HTML 代码放在内联 `print` 语句中。开头这几行简单的代码——

**图 16–4 从查询创建 HTML 表格**

```php
<?

//start HTML page

print("<HTML\n");

print("<HEAD>\n");

print("<TITLE>Figure 16-4</TITLE>\n");

print("</HEAD>\n");

print("<BODY>\n");

// connect to server

$mysql_link = mysql_connect("localhost", "httpd");

// select the 'store' database

mysql_select("store", $mysql_link);

// get everything from catalog table

$query = "SELECT * FROM catalog ";

$mysql_result = mysql_query($query, $mysql_link);

// start table

print("<TABLE border=\"1\">\n");

// create header

print("<TR>\n");

print("<th>ID</th>\n");

print("<th>Name</th>\n");

print("<th>Price</th>\n");

print("</TR>\n");

// get each row

while($row = mysql_fetch_row($mysql_result)) {

  print("<TR>\n");

  print("<td>".$row[0]."</td>\n");

  print("<td>".$row[1]."</td>\n");

  print("<td>".$row[2]."</td>\n");

  print("</TR>\n");

}

print("</TABLE>\n");

print("</BODY>\n");

print("</HTML>\n");

?>
```

## 第16 章 数据库集成

```php
print("<A HREF=\"page.php3?session=$session\">next</A>");
```

用于将 `session` 发送到下一个页面。我使用这种技术是因为它可以兼容所有浏览器，甚至是 Lynx。PHP 会将 Cookies 转换为变量。

另一种方法是使用 cookie。其方式与 GET 和 POST 表单变量相同。因此，你可以创建一个名为 `session` 的 cookie。区别在于，由于 cookie 可能只存在于标头 `headers` 中，你必须在发送任何 HTML 代码之前先将它们发送给浏览器。如果你想采用这种策略，请查看第 8 章中的 `setcookie` 函数。

这两种方法在互联网上都被广泛使用。查看任何电子商务网站即可。为了演示，我将一种使用 GET 变量的策略。第一步是创建一个表来存储 `session` 标识符。图 16-5 是在 MySQL 数据库中创建简单 `session` 表的 SQL 代码。

该表以一个八字符的字符串作为键值。每当用户移动到新页面时，我们都会更新 `LastAction` 列。这样，我们就可以清理所有看起来未被使用的 `session`。每次访问我们的页面都会触发清理所有 30 分钟内无操作的 `session`。然后我们需要测试每个访问者是否拥有 `session` 标识符。如果他们没有，我们就创建一个。如果他们有一个，我们需要检查它以确保其有效性。

当你第一次加载图 16-6 时，它会为你创建一个 `session`。每次点击“刷新页面（Refresh Page）”链接都会脚本检查 `session`。如果 `session` 标识符不在 `session` 表中，则该 `session` 标识符将被拒绝，并创建一个新的。你可以通过删除浏览器地址框中的一个字符来尝试使用一个无效的 `session` 标识符。

下一个逻辑步骤是添加另一个表，用于存储你需要的关于浏览你网站的人的信息。其中一列应该用于存储来自 `session` 表的 `session` 标识符。我把这个留给你们作为练习。

### 图 16-5 创建 Session 表

```sql
CREATE TABLE session (
  ID VARCHAR(8) NOT NULL,
  LastAction DATETIME,
  PRIMARY KEY (ID)
);
```

### 图 16-6 检查 ID

```php
/*
 ** 使用 session 标识符的演示
 */

// 生成一个 session id
function SessionID($length=8)
{
    /*
     ** 设置可能字符的池
     */
    $Pool = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    $Pool .= "abcdefghijklmnopqrstuvwxyz";
    for($index = 0; $index < $length; $index++) {
        $sid .= substr($Pool, (rand()%strlen($Pool)), 1);
    }
    return($sid);
}

// 为生成器种子
rand(time());
// 开始 HTML 页面
print("<HTML>\n");
print("<HEAD>\n");
print("<TITLE>Figure 16-6</TITLE>\n");
print("<HEAD>\n");
print("<BODY>\n");
// 建立数据库连接
$mysql_link = mysql_connect("localhost", "httpd", "");
mysql_select_db("store", $mysql_link);
// 清理任何旧 session
$Query = "DELETE FROM session ";
$Query .= "WHERE LastAction < '";
$Query = date("Y-m-d H:i:s", (time()-108000));
$Query .= " ";
mysql_query($Query, $mysql_link);
// 检查 session
if(isset($session))
{
    if(mysql_num_rows($mysql_result))
    {
        // session 存在，更新最后操作
        $Query = "UPDATE session ";
        $Query .= "SET LastAction = now() ";
        $Query = "WHERE ID='$session' ";
        mysql_query($Query, $mysql_link);
        print("Session recognized!<BR>\n");
    }
    else
    {
        // session 无效，通知用户并将其删除
        print("Bad Session ID ($session)!<BR>\n");
        $session = " ";
    }
}
// 如果 session 为空，我们需要创建它
if($session == "")
{
    // 没有 session，所以创建一个
    $session = SessionID(8);
    // 将 session 插入数据库
    $Query = "INSERT INTO session ";
    $Query = "VALUES ('$session', now()) ";
    mysql_query($Query, $mysql_link);
}
print("You session identifier $session<BR>\n");
print("<A HREF=\"16-6.php?session=$session\">");
print("Refresh Page;");
print("</A><BR>\n");
// 关闭页面
print("</BODY>\n");
print("</HTML>\n");
?>
```

## 在数据库中存储内容

存储在数据库中的信息不仅限于短字符串，例如图 16-4 中 32 字符的项目名称。你可以创建 64K 的 `blob`，这足够存储一个相当大的 Web 页面。这种做法的优点是页面存在于一个结构化的环境中。它们可以通过数字来识别，并且仅使用这些数字就可以建立它们之间的关系。缺点是，由于信息现在数据库中，你不能直接将文件加载到你喜欢的编辑器中。你必须平衡成本和收益；大多数 网站都需要将每部分内容存储在数据库中。

将内容放在数据库中非常有意义的情况是公告板系统，即 BBS。该系统存储的消息不仅仅是 Web 页面。每条消息都有自己的标题、创建时间和作者。此外，由于每条消息都可以赋予一个唯一的标识符，我们可以在父子树结构中关联消息。用户可以创建一个新线程，并产生许多其他消息。消息可以以这种层级结构显示，以便浏览。对于所有与数据库相关的系统，第一步都是创建一个表。图 16-7 创建了一个表来存储消息。每条消息都有标题、帖者的姓名、发布消息的时间、父节点和正文。父节点可能是 0。

```sql
CREATE TABLE Message (
  ID INT NOT NULL AUTO_INCREMENT,
  Title VARCHAR(64),
  Poster VARCHAR(64),
  Created DATETIME,
  Parent INT,
  Body BLOB,
  PRIMARY KEY(ID)
);
```

### 图 16-7 表

### 图 16-8 简单的 BBS (Leon's BBS)

```php
print("<HTML>\n");
print("<HEAD>\n");
print("<TITLE>Figure 16-8</TITLE>\n");
print("<HEAD>\n");
print("<BODY BGCOLOR=\"FFFF\">\n");
// 连接到服务器
$mysql_link = mysql_connect("localhost", "httpd", "");
// 将消息标题显示为链接
// 查看正文
print("<LI><A HREF=\"16-8.php?messageID=$messageID\">");
print("$messageTitle</A><BR>\n");
// 显示此消息的子消息
showMessages($messageID);
RowCount++;
print("</UL>\n");
/*
 输出一个用于添加消息的表单，
 并给定父 id
*/
function postForm($parentID)
{
    print("NAME\"");
    print("SIZE\"");
    print("MAX=\"64\" VALUE=\"$title
}
/* 执行操作 */
if($ACTION != "")
{
    if($ACTION == "POST") {
        $inputTitle = ere_replace("'", "", $_POST['inputTitle']);
print("<A HREF=\"16-8.php?\">");
print("List of Messages</A><BR>");
    }
else
{
    print("<2>List Messages</n");
    // 获取整个列表
    showMessages(0);
    postForm(0);
}
print("</BODY>\n");
print("</HTML>\n");
?>
```

无论采用哪种模式，都会显示一个添加消息的表单。如果在显示消息列表时添加消息，该消息将添加到根层级。如果在用户正在查看某条消息时添加消息，则会被视为一条回复。新消息将成为所查看消息的子元素。

这个 BBS 虽然简单，但核心功能完备备。更复杂的解决方案可能仅允许经过身份验证的用户添加消息，或者在管理员批准之前保持消息的私密状态。

## 生成图形

本章内容

-   动态按钮
-   即时生成图形

![](img/490647a2fc8fbc7034b6e56593c58845_511_0.png)

## 第 17 章

本章探讨了如何使用第 12 章描述的 GD 扩展函数生成图形。意识到即时创建图形涉及的问题是非常重要的。首先，这在 CPU 时间上是相对昂贵的。在大多数情况下，动态图形的灵活性并不值你为服务器带来的额外负担。

另一个问题是，使用 PHP 函数制作美观的图形并不容易。像阴影这样的常用技术几乎是不可能实现的。你将在后续示例中看到，创建一个简单的扁平图表需要花费大量工作。

最后，虽然对文本有充分的支持，但你在文字处理器中会期待的功能并不存在。文本不会在行尾换行。没有行间距、间距或下降部 `descenders` 的概念。

尽管如此，在某些情况下生成图形是有意义的。本章包含了一些真实的示例，你只需稍作修改即可开始使用。

## 动态按钮

封装在 `<a>` 标签中的图像是一种常见的导航设备。这种方法允许你创建类似于操作系统创建的按钮，甚至是奇幻的图标，而不是简单的纯文本。在大多数情况下，最好将这些留作用最喜欢的图形编辑器创建的图形，因为更改之间的时间相对较长。另一方面，如果你有一个经常变化的按钮，那么用 PHP 动态创建它可能是有意义的。按钮的内容、标签需要在 PHP 中以字符串的形式可用。它可以是一个设置变量赋值的语句，也可以是从文件或数据库中检索的值。

通过插图可以使这个想法变得清晰。许多企业网站都有新闻稿板块。你的客户想要的不仅仅是文本链接列表，而是每条发布稿都有一个燃烧报纸的图形，所有这些都位于“热烈出炉”的标题下。每份正在燃烧的日报上方都有带有新闻稿标题的文本。对于每月只发布一份新闻稿的小公司，你手手创建这些图形会更好。而对于每周发布一份新闻稿的公司，自动化该过程就变得有意义了。你可以将新闻稿放入数据库，并在用户查看新闻稿列表时即时生成图形。这种方法的一个优势是，如果 CEO 发现你在网站上放了燃烧的报纸，你可以进行细微修改，让图形变成带有新闻标题的公司徽标 `logo`。

严肃地说，你必须考虑与动态创建图形相关的权衡。你不想为了节省 15 分钟而让每条新闻稿的下载时间都增加 30 秒。如果你已经在 Web 领域工作了一段时间，你就知道在整个站点中重用图形，因为浏览器会缓存它们。第一个页面加载可能需要更长时间，但每个后续页面都会更快，因为图形已经加载了。动态图形当然可以被缓存，但浏览器使用的是 URL。GET 变量是 URL 的一部分，所以

```php
http://www.site.com/button.php?label=home&from=1
```
和
```php
http://www.site.com/button.php?label=home&from=2
```
创建了两个相同的图形，但从浏览器缓存来说它们是不同的。这些只是动态按钮的一些问题。为了真正理解这个过程，我将提供一个示例并描述这些步骤。图 17-1 是创建一个带有文本标签的 GIF 按钮的脚本。按钮是矩形的，带有一些高亮和阴影。标签应用了下投影效果，并在垂直和水平方向上居中。

**图 17-1** 按钮

![](img/490647a2fc8fbc7034b6e56593c58845_514_0.png)

```php
/*
 GIF button
 ** 根据变量
 * 变量创建一个图形化按钮。
 */
// 如果未给出则设置参数
if(!isset($ButtonWidth))
{
    $ButtonWidth = 100;
}
if(!isset($ButtonHeight))
{
    $ButtonHeight = 30;
}
```

```php
if(!isset($ButtonLabel))
{
    $ButtonLabel = "CLICK";
}
if(!isset($ButtonFont))
{
    $ButtonFont = 5;
}
// 创建图像
```
