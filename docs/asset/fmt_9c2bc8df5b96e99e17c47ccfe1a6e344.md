
Mason 为 Mason Request 对象提供了广泛的 API。该 API 允许你访问和更改缓存信息、检查组件调用栈、直接调用组件（例如 `$m->comp()`）、使用 `&...&` 的长版本以及更多功能。详细请参阅 `www.masonhq.com/docs/manual/Request.html`。

## 11.9.4 组件类 API

Mason 提供了方法来检查和报告生成网页时所使用的组件。详细信息请参阅 `www.masonhq.com/docs/manual/Component.html`。

## 11.9.5 顶层组件

Mason 有一个功能，即使请求的页面、甚至目录不存在，也可以创建网页。换句话说，假设用户请求 `www.example.com/reports/2002/March/`。在正常情况下，Apache 会提供 `reports/2002/March/` 目录下的 `index.html` 文件。然而，在这个示例中，`2002` 目录并不。而且，Mason 也没有。那么，发生什么什么？

配置妥当的 Mason 会搜索 `index.html`，如果没有找到，它将开始在目标目录向上目录树中搜索 `dhandlers`（即默认处理器）。例如，对于上述要查找的目录，Mason 会按顺序查找以下内容：

```
/reports/2002/March/index.html
/reports/2002/dhandler
/reports/dhandler
/dhandler
```

找到第一个文件即被使用。假设没有找到 `/reports/2002/March/index.html` 和 `/reports/2002/dhandler`，找到的第一个是 `/reports/dhandler`。该文件被用于生成 HTML。其内容如下：

```html
<_header %>
<h1>Report for %month%</h1>
<%report_contents %>
<_footer %>
```

```perl
<init>
# 获取路径
my $arg = $m->handler;
# 分割年份和月份
my($year,$month) = split("/",$arg); # 获取报告内容所需的任何操作
# 也许从数据库读取
my $report_contents = 'All the good content of the report';
</init>
```

`<init>` 部分首先执行的代码抓取了 `/reports/` 下的内容——在这种情况下，`2002/March`。这个文本存储在 `$arg` 中，然后通过斜杠分割并存储在 `$month` 中。然后，通过某些方式（也许查询了数据库或文件），`2002 report` 被读取并存储在 `$report_contents` 中。然后，在文件的顶部，我们调用 `_header` 组件来构建头部；然后创建一个带有月份和年份的 `<h1>` 标签。报告的内容包含了 `<%report_contents %>`，最后是 `_footer` 组件。正如该示例所示，根据报告，我们可以拥有：

```
www.example.com/2002/March
www.example.com/2002/February
www.example.com/2002/January
www.example.com/2002/December
www.example.com/2001/November
```

关于 `dhandlers` 的更多信息，请参阅 `www.masonhq.com/docs/manual/Devel.html#initialization_and_cleanup`。与本书中的许多其他主题一样，我们可以再写一本书来详细描述 Mason 的所有功能；我们在这里只是触了皮毛（80/20 原则）。虽然这些并非必不可，但当你进一步深入了解如何使用 Mason 开发网站时，你可能想要探索以下主题。

## 11.1 总结

`$report_contents` 包含了，最后是 `_footer` 组件。正如该示例所示，根据报告，我们可以拥有：

```
www.example.com/2002/March
www.example.com/2002/February
www.example.com/2002/January
www.example.com/2002/December
www.example.com/2001/November
```

# 第12章 PHP

在这些示例中我们没有使用 XML，因此不需要使用 `<?php ... ?>` 语法。此外，由于我们喜欢的 HTML 编辑器是 we 和 emacs，我们不需要 `<script>` 语法（我们不使用 FrontPage 或其他的 HTML 编辑器——如果你在使用，请相应做好计划）。我们在示例中使用第一种风格。

## 12.3 配置

如果你按照第 2 章的建议安装了 Linux，那么 Apache 已经为 PHP 配置好了。要使用 PHP，只需将 PHP 文件命名为 `.php` 扩展名。

你可能会注意到，这种方法与 Emberry 和 Mason 的方法相反，在那些项目中我们决定不为这些文件使用单独扩展名。逻辑是不提供过多关于网站的信息，并保持整个网站 URL 的简洁（所有页面都通过 `.html` 扩展名访问）。但由于 Apache 默认配置使用 `.php` 文件，出于纯粹的懒惰，我们将坚持这样做（这是优秀程序员的优点之一）。

有一种方法可以配置 Apache，使得目录下的所有 `.html` 文件都由 PHP 处理。更多信息请参阅文档。

## 12.4 几个快速示例

我们将从两个快速示例开始。为 PHP 工作创建一个新目录并进入目录：

```
$ mkdir /var/www/html/php
$ chmod a+rx /var/www/html/php
$ cd /var/www/html/php
```

创建一个名为 `hello.php` 的 PHP 文件：

```php
<html>
<head>
<title>Hello, world! with PHP</title>
</head>
<body bgcolor="#ffffff">
<?php echo "hello, world!" ?>
</body>
</html>
```

> ⁴ 记住权限，644。

要查看此文件的结果，请加载以下 URL 之一：`http://localhost/php/hello.php` 或 `www.opensourcewebbook.com/php/hello.php`。结果可以在图 12.1 中看到。

PHP 代码嵌入在 HTML 的 `<? ... ?>` 标签中。在这个示例中，PHP 代码简单地显示（`echo`）字符串“hello, world!”。`echo` PHP 语句输出一个会在浏览器中渲染的字符串。

现在已经完成了 PHP 必经的“hello, world!”示例，请尝试一个可以完成大量工作的内置函数：`phpinfo()`。将此代码放在 `phpinfo.php` 中。

```php
<html>
<head>
<title>PHP Information</title>
</head>
<body bgcolor="#ffffff">
<?php phpinfo() ?>
</body>
</html>
```

`phpinfo()` 函数构建了一个页面，其中包含了关于 PHP 如何构建、PHP 环境等大量有用信息。要查看结果，请加载以下 URL 之一：`http://localhost/php/phpinfo.php` 或 `www.opensourcewebbook.com/php/phpinfo.php`。该操作的结果可以在图 12.2 中看到。

## 12.5 语言语法

与其他我们学过的语言（以及大多数易用语言）一样，PHP 对空白字符不敏感。因此，这条语句：

```php
<$title="PHP is cool";echo <title> $title</title>;
```

如果写成这样可能会更清晰：

```php
<?php
$title = "PHP is cool";echo "<title> $title</title>";
```

PHP 中的变量名对大小写敏感——`sa` 与 `SA` 不同。函数名（包括用户定义的函数）对大小写敏感——`rose()` 等于 `ROSE()` 和 `Rose()`。
