
`sayHello($hello, $world);` // 你猜对了 - 打印 Hello World

`echo ($a);` // 输出 11

`echo ($b);` // 输出 20

`?>`

# 第 16 章

函数的默认方式是按值传递参数，也就是说，对传递的参数本地副本的修改不会反映在调用函数中。例如，如果变量 `Shell` 的值被更改为 `echo Hello`，这只会在 `SayHello` 函数中生效。调用函数中的变量 `Shell` 将保持不变，不会被值 `Hello` 改变。

然而，函数也可以按引用传递。这意味着，如果按引用传递的变量在被调用函数中被修改，该更改将反映在调用函数中。我们在函数定义中在参数前加上 `&` 字符，表示它是一个按引用传递的变量。下面的示例说明了这一点：

```php
<?php

function sayHello(&$first, &$last) {
  $first = "Hello";
  $final = $first.$last; // 这行拼接了两个字符串
  echo ($final);
}

$Shell = "Hello "; $Sword = "World";
SayHello($Shell, $Sword); // 如果你猜对了 - 打印 Hello World
?>
```

## 数组

我们在 PHP 中使用数组来存储多个相同数据类型的值，就像在其他编程语言中一样。区别在于 PHP 数组功能强大得多。PHP 可以通过两种方法对数组索引——数值索引和关联字符串索引。在数值索引中，我们使用变量值的位置来索引数组，而在关联索引中，我们分配一个字符串作为值来索引数组。当我们查看接下来的示例时，这一点将会变得更加清晰。

PHP 数组还补充了几个内置函数，可以使用这些函数来操作它们。因此，我们可以使用 `current()` 函数来获取数组中当前元素的值。以下是 PHP 数组的一些示例：

```php
<?php
$Color[0] = "violet";
$Color[1] = "indigo";
$Color[2] = "blue";
$Abbreviations['ps'] = "Post Script";
$Abbreviations['etc'] = "Et Cetera";
$Abbreviations['PHP'] = "Personal HomePage tools";
echo($Color[0]); // 打印字符串 violet;
echo($Abbreviations["PHP"]); // 打印 Personal HomePage tools
?>
```

## 使用 PHP 创建 Web 接口

### 在 DVD 项目中使用 PHP

在之前的章节中，我们初步进入了 PHP 的世界，并在某种程度上探索了该语言的安装和语法。在本章其余部分，重点是使用 PHP 和 PostgreSQL 来构建 PHP 程序，该程序将为 DVD 店项目提供一个接口。

### HTTP、HTML 和 PHP

到此时你可能已经疑惑，我们需要某种机制来从显示的 HTML 页面中接受用户输入。我们通常使用 HTML 表单来获取用户输入，因此我们需要一种机制来获取表单元素（HTML 表单中的文本框）的值，以便其供 PHP 表单元素使用。为了方便这一点，一个与表单元素同名的 PHP 变量将包含该表单元素的值。下面的脚本说明了这一点：

```html
<HTML>
<BODY>
<FORM ACTION="form.php" METHOD=GET>
Who goes there? :
<INPUT TYPE=TEXT name=username>
<BR>
<INPUT TYPE=SUBMIT>
</FORM>
</body></HTML>
```

下面的脚本是 `getform.php` 文件，用于处理通过 GET 提交的表单：

```html
<HTML>
<BODY>
<?php
echo("Hmm, So you are " . $_username);
?>
</body></HTML>
```

![](img/930f7611cac03a5cd5573f4bb94fd7b9_598_0.png)

我们处理后的表单看起来像这样：

![](img/930f7611cac03a5cd5573f4bb94fd7b9_599_0.png)

我们看到，HTML 表单中的表单变量名可以作为名为 `$_username` 的 PHP 变量供 PHP 脚本使用。

数据可以通过两种方式返回到服务器。首先，将数据编码在 URL 中并使用 GET 方法将其发送到网络服务器。假设一个 HTML 表单获取了用户的姓名，并需要将其传递给 PHP 脚本，以便脚本对其进行操作。GET 将生成一个发送到网络服务器（从而发送给脚本）的 URL，它看起来类似于：

`http://example.net/egofind.php?user=incognito`

PHP 脚本可以访问变量 `user` 的值，并发现它是 'incognito'。我们将在开发过程中学习如何编码字符串。

我们还可以使用 POST 方法，它不涉及编码 URL 来将数据传回 PHP 脚本。POST 通常用于我们需要发送大量数据的情况，且发送的数据通常会更改服务器上现有的数据存储。为了说明目的，让我们整合一个 HTML 表单和脚本，使用 POST 方法来实现与之前相同的功能：

```html
<html>
<FORM ACTION='get.php' METHOD=POST>
Who goes there?:
<INPUT TYPE=TEXT NAME=yourname>
<BR><BR>
<INPUT TYPE=SUBMIT>
</FORM>
<body>
</</html>
```

### 使用 PHP 创建 Web 接口

我们可以使用下面所示的 PHP 脚本来处理通过 POST 方法提交的表单。

```php
<?php
echo ("Hmm, so you are " . $_yourname);
?>
```

GET 用于处理通过 POST 方法提交的表单（注：原文此处可能有误，应为POST）。

GET 通常用于发送小量数据，在 URL 中可见。如果存在连接，则它是不安全的。这些变量在脚本之间传递。我们稍后会看到。

应用程序

我们现在开始构建 PHP 应用程序。通过浏览器访问数据库，并释放（放弃）这些。变量在脚本之间保持。

### 登录

- 从用户获取姓名并使用用户名进行身份验证。
- 获取用户 ID 并使用用户名登录。
- 后续脚本将需要它们。
- 登录后提供检查状态和搜索选项。

### 预留状态

- 检查成员是否有预留。如果是，显示详情。
- 如果没有，予以提示。

### 搜索标题

- 搜索表单——对标题进行查询。
- 调用搜索函数获取匹配。
- 每个匹配允许用户预订。

## 预订标题

- 检查用户是否有预订——如果有，显示错误信息。
- 获取要预订的日期。执行不能提前 7 天预订的规则。
- 再次检查可用性；如果不可，显示错误信息。
- 如果可用，为用户预订该标题。

## 取消

- 调用数据库访问函数取消用户对该标题的预订。代码如下。脚本包含了数据库访问函数。你会注意到其中一些函数没有在主程序中使用。它们只是为了说明目的，并以便读者可以使用它们扩展应用程序。在尝试运行此代码之前，请确保已完成并安装了第 4 章的代码。

`storefunctions.php`

在这里我们定义并分配了一些仅用于数据库访问的变量。`db_name` 变量是数据库名称，必须与 DVD 商店其他接口使用的数据库相同。数据库用户由变量 `Sdb_user` 定义：

```php
<?php
// dvdstorefunctions.php
// Global Variables
$Shost="localhost";
$Sdb_name="dvd_store";
$Sdb_user="dvd_user";
$Sdb_password="";
$Serr_msg="";
$Sdb_conn;
```

`dvd_open_db()`

该函数打开到数据库的持久连接。持久连接节省了每次访问数据库时初始化连接的开销。持久连接是在特定脚本执行结束时不关闭的连接。当请求数据库连接并启用了持久连接时，PHP 会检查是否存在预先连接，如果是，则使用该连接；如果不是，则初始化一个新的：

```php
function dvd_open_db() {
    global $Sdb_conn, $Serr_msg;
    global $Shost, $Sdb_name, $Sdb_user, $Sdb_password;
```

```php
// 打开持久化数据库连接
if (($db_conn = pg_pConnect("host=$host dbname=$db_name user=$db_user password=$db_password")) == false) {
```
