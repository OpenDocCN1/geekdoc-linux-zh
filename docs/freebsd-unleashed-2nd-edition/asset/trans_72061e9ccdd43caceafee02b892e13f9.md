
# 使用 PHP 为网页提供由数据库驱动的内容

你可能在疑惑，是否从零开始编写自己的 Web 应用程序是动态页面中包含由数据库驱动的唯一方式，还是说有更好、更简洁的方法，比如使用 Microsoft 的 ASP 或 Macromedia 的 ColdFusion。答案是肯定的，确实有。这就是 PHP，它最初代表“个人主页”（Personal Home Page），但现在它本身已成为一个开源 HTML 预处理框架的官方名称，在 Unix Web 托管领域得到了非常广泛的应用。PHP 的官方网站是 www.php.net。

PHP 由可以嵌入到 HTML 中的命令组成，它们的解析方式与 .shtml 文件中服务器端包含（server-side includes）的解析方式非常相似，正如你在第 25 章中所见。PHP 文件的扩展名为 .php、.php3 或 .php4，Apache 在安装时被重新配置以识别这些文件，并在向用户提供内容之前将它们通过 PHP 模块进行处理。

本章对 PHP 的讨论将较为简略，但足以让你入门。如果你已经熟悉了数据库设计、SQL 以及 Perl/Python 连接性中提出的较难概念，那么在这一系列概念阶段中，PHP 就像是漫长餐后的一道甜点。

## 安装 PHP

PHP 项目由 Apache Software Foundation 维护并推动向前发展，这意味着 PHP 和 Apache 在操作上紧密交织在一起。PHP 是作为 Apache 模块 mod_php4 安装的，它链接到利用 Zend 处理引擎的库，PHP 正是基于该引擎构建的。

可以从端口（ports）或软件包（packages）安装 PHP。该软件的包名为 mod_php4，如果你选择从端口安装，它位于 /usr/ports/www 目录中。当你输入 make 时，会提供一个用于编译到 PHP 中的选项列表。根据你正在使用的数据库，选择支持 MySQL、PostgreSQL 或两者皆可。你还可以选择启用对 GD 图像处理库、mcrypt 加密、OpenSSL、XML 以及其他附加组件的支持。除非你已明确知道需要这些功能，否则可以忽略这些额外选项。

> **注意**
> 如果你正在运行 Apache 2.0，需要在输入 make 之前定义 WITH_APACHE2 环境变量。有关设置环境变量的详细信息，请参阅第 11 章“自定义 Shell”。

在安装过程结束时，自动化安装脚本会修改你的 httpd.conf 文件，以启用对 .php 和 .php4 文件的识别，并将其分配给 PHP 处理器。你可能希望在此之后检查 httpd.conf 文件，确保过程中没有意外破坏任何配置。

## 流程控制和编程技巧

PHP 命令的标签格式为 <?php ... ?>。在这两个端点标签之间可以放置许多内部 PHP 命令；你可以使用 echo() 打印文本，可以对变量执行字符串操作（包括 HTTP 连接变量，如 HTTP_USER_AGENT），并且可以执行流程控制。例如，下面的 if 语句可以根据变量的状态打印不同的 HTML 代码块：

```
<?php
if ($a > $b) {
?>
<B>A is greater than B.</B>
<?php
} else {
?>
<B>B is greater than or equal to A.</B>
<?php
}
?>
```

变量的命名和赋值语法非常类似于 Perl。PHP 包含诸如 foreach、while 和 do...while 等类似 Perl 的控制结构，尽管 Perl 中 *elsif* 的等价物是 *elseif*。还有一种类数组上下文，尽管数组的前缀是 $，与标量相同。此外，与 Perl 类似，PHP 的变量类型无需由程序员声明，而是由内部处理并从上下文中推导出来。PHP 代码行以分号 (;) 结尾。

在 <?php ... ?> 块中，你可以在任意多行中定义变量和函数；你几乎可以假装这是一个 Perl 程序。<?php ... ?> 块中的任何内容都会从嵌入的 HTML 文件中解析出来，然后替换为你调用的任何函数的输出。你可以将 PHP 代码块放置在文件中的任意位置。

## 与数据库接口

就本章目的而言，我们感兴趣的是如何让 PHP 与 MySQL 和 PostgreSQL 交互。幸运的是，实现此功能的方法与我们已经介绍过的基于 Perl 的技术非常相似。

初始的 MySQL 数据库连接使用 *mysql_connect* 和 *mysql_select_db* 函数设置，如下所示：

```
$conn = mysql_connect("localhost", "frank", "<frank's password>");
mysql_select_db("PictureArchive");
```

对于 PostgreSQL，数据库设置命令如下：

```
$conn = pg_connect("dbname=PictureArchive user=frank password=<frank’s password>");
```

可以在 **mysql_connect** 或 **pg_connect** 的参数字符串中指定大量的连接选项，无论是 PostgreSQL 示例中显示的 **parameter=value** 格式，还是 MySQL 示例中有序的值列表（两种格式均可用于任何数据库）。由于 PostgreSQL 在一定程度上依赖于环境变量，你可以通过在 Web 服务器环境中定义它们来设置许多这些选项的默认值。使用 Apache 的 **SetEnv** 指令在 **httpd.conf** 或 **.htaccess** 文件中设置这些值，如下所示：

```
PGHOST=localhost
PGPORT=7890
PGDATABASE=PictureArchive
PGUSER=frank
PGPASSWORD=<frank’s password>
```

对于 MySQL，PHP 有许多函数，如 **mysql.default_user**、**mysql.default_password** 和 **mysql.connect_timeout**，这些可以在全局 PHP 配置文件 **/usr/local/etc/php.ini** 中设置。注意，必须先将此文件从 **php.ini-dist** 复制或重命名后，它才会被读取。

一旦你的数据库连接设置完成，你就可以像在早期示例中那样发出查询，使用 **mysql_query** 或 **pg_query**，如下所示（注意这两个函数接收数据库连接标识符和查询的顺序是相反的）：

```
<?php
$result = mysql_query("SELECT * FROM Users",$conn)
  or die("Invalid query");
?>
```

```
<?php
$result = pg_query($conn, "SELECT * FROM Users")
   or die("Invalid query");
?>
```

PHP 对这两个数据库均运行在自动提交（autocommit）模式下。一旦你发出 **mysql_query** 或 **pg_query** 命令，查询就会提交，然后你就可以开始在 **$result** 中处理结果：

```
while($rowdata = mysql_fetch_row($result)) {
print "$rowdata[0]: $rowdata[1]<BR>\n";
}
```

这种语法非常类似 Perl。如果你查阅 `http://www.php.net/manual/` 上的 PHP 文档，在“MySQL Functions”和“PostgreSQL Functions”标题下，你会发现大量文档完善且功能与你已经熟悉的 Perl 数据库接口非常相似的函数。

PHP 相对于自研 Perl 或 Python 脚本的最大优势在于，由于服务器处理的代码全部嵌入到纯 HTML 文件中，你可以更容易地维护页面的布局。你可以编辑这些主文件中的 HTML，而没有破坏权限或禁用可执行代码的危险。而且，由于文件由 Apache 内部解析，由于为每次页面查看启动单独的 CGI 进程对于服务器来说是一种成本高昂的运行方式，因此你会看到处理开销显著减少。

## 安全顾虑

PHP 潜在地将你的系统暴露给大量的安全弱点。PHP 容易受到许多威胁 CGI 程序的相同漏洞的影响，它还有一些你需要意识到的新的易受攻击领域。

包含数据库连接密码的文件，无论是 HTML/PHP 文件本身还是包含文件，都可能被编写 CGI 程序以访问文件内容的本地用户访问。为了解决这个问题，你需要采取与 Perl 或 Python 连接设置相同的预防措施（如本章前面所述）。类似地，虚拟主机以及在执行主服务器根目录之外的用户 `public_html` 目录中执行的 PHP 文件也存在问题（如果你选择允许的话；一个紧密安全的服务器将仅在受限的 /cgi-bin 目录内运行所有 PHP 脚本，而不允许普通用户运行它们）。由于所有 PHP 文件都以相同的权限和所有权进行解析和执行，一个用户的操作可能会影响其他用户的数据库代码或文件。再次强调，你需要审查你的安全策略：你多么信任你的本地用户？

完美安全是一种神话，安全和便利性是相互排斥的。你允许用户访问系统的程度越宽松，你就越难防范来自你自身用户的恶意活动。幸运的是，就数据库连接的目的而言，唯一需要担心攻击的领域是你的本地用户，因为大多数启用 Web 功能的数据库系统并不开放其数据库后端给非本地连接。但是，如果你允许这些本地用户进入系统，他们可能会造成很大的麻烦。

请参阅 `http://www.php.net/manual/en/security.php` 上的在线 PHP 安全文档，其中详细讨论了 PHP 服务器可能被攻击和利用的方式。

