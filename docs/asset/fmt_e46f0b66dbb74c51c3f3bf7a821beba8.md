
## 第四部分：嵌入

## 服务器端包含

## 9.1 引言

服务器端包含（SSI）提供了一种将可执行代码嵌入网页的简单方法。SSI 的优点是使用简单且易于学习，而有时简单本身就是奖励。SSI 的主要缺点是由于其简单性，它的功能是有限的。

SSI 不是 CGI（见第 7 章）——也就是说，它不是通过执行来生成 HTML 文本的程序，因此使用它并不需要成为 Perl 黑客。相反，SSI 是一组可以嵌入 HTML 文件中并由 Apache 处理的指令。指令的格式如下：

```
<!--#directive param1="value" param2="value"...-->
```

这仅仅是一个带有 `#` 转义到 SSI 的 HTML 注释。除其他外，SSI 还允许你：

- 显示变量
- 包含文件内容
- 显示日期和文件名等信息
- 执行程序或命令
- 创建变量
- 使用简单的条件表达式

SSI 并非用于执行复杂的编程任务。它主要用于对基本信息进行简单的包含（因此得名如此）。

> ¹哥德尔再次抬起头 [Hofstadter 99]。

`http://www.example.com/a.shtml`

`www.example.com`

`GET /a.shtml HTTP/1.0`

![](img/9b05e38e58495be06a08eeb2b6906346_313_0.png)

图 9.1 SSI 工作原理

对于任何更复杂的内容，你在本书其他地方学到的内容是更好的选择。但你不需要用大炮来杀蚊子，所以如果我们需要拍掉蚊子，那么 SSI 也有一些实用的应用。

### 9.1.1 工作原理

如图 9.1 所示，当用户请求一个以 `.shtml` 扩展结尾的文件时，Apache 服务器会将该文本通过“服务器端包含”预处理器。该处理器会处理 SSI，将所有 SSI 指令转换为适当的文本。生成的文本随后会被发送回浏览器。

### 9.1.2 配置

如果你按照第 2 章的建议安装了 Linux，Apache 应该已经配置为支持 SSI。要进行检查，请确保 Apache 配置文件（`/etc/httpd/conf/httpd.conf`）中的这两行没有被注释：

```
AddType text/html .shtml
AddHandler server-parsed .shtml
```

这些指令添加了带有 `.shtml` 后缀的文件类型，其内容将（视为 HTML，且其文件在提供之前将由 Apache 服务器进行服务器端解析（或预处理）。所有以 `.html` 后缀结尾的文件都会经过预处理，因此不要将普通的非 SSI HTML 文件命名为 `.html` 扩展名——这只会减慢网络服务器的速度，因为它会预处理不需要预处理的文件。

一如既往，如果你更改了 Apache 配置文件，请重启服务器。

### 9.1.3 教程

学习 SSI 相对简单，我们可以在几页纸内对其重要方面进行简短的教程。SSI 由几个实现其功能的指令组成。

### echo 指令

`echo` 指令指示服务器在 HTML 文件的该点插入（显示）变量的值。它的语法如下：

```
<!--#echo var="variable"-->
```

可以被 `echo` 的变量有：

- `DOCUMENT_NAME`—文档名称
- `DOCUMENT_URI`—文档虚拟路径
- `DATE_LOCAL`—本地日期和时间
- `DATE_GMT`—格林威治标准时间的和
- `LAST_MODIFIED`—文档最后的修改日期
- `QUERY_STRING_UNESCAPED`—解码后的查询字符串，其中所有 shell 元字符都用反斜杠转义

让我们来看一个例子。首先，为 SSI 工作创建一个目录，并赋予适当权限：

```
$ cd /var/www/html
$ mkdir ssi
$ chmod a+rx ssi
$ cd ssi
```

将此示例命名为 `echo.html` 并确保它是可读的（使用 `chmod a+r echo.html`——请确保对本章中的所有示例都执行此）。在文件中放入以下代码：

```html
<html>
<head>
<title>服务器端包含: echo 指令</title>
</head>
<body bgcolor="#ffffff">
<h1>echo 指令示例</h1>
文件名: <b><!--#echo var="DOCUMENT_NAME"--></b>
<br>
URI: <b><!--#echo var="DOCUMENT_URI"/></b>
<br>
本地时间: <b><!--#echo var="DATE_LOCAL"/></b>
<br>
GMT: <b><!--#echo var="DATE_GMT"/></b>
<br>
最后修改时间: <b><!--#echo var="LAST_MODIFIED"/></b>
</body>
</html>
```

这里有几个 `echo` 指令，它们会产生如图 9.2 所示的网页。要亲自验证，请访问这些 URL 之一：`http://localhost/ssi/echo` 或 `www.opensourcewebbook.com/ssi/echo.shtml`。

![](img/9b05e38e58495be06a08eeb2b6906346_315_0.png)

图 9.2 `echo` 指令

### include 指令

`include` 指令允许你在当前文档中包含另一个文件的内容。如果你希望每个页面都有相同的页眉或页脚，这将非常方便。假设我们在 `header.html` 中有这样的内容：

```html
<html>
<head>
<title>服务器端包含: echo 指令</title>
</head>
<body bgcolor="#ffffff">
<h1>include 示例</h1>
```

假设我们在 `footer.html` 中有这样的内容：

```html
<hr>
<a href="http://www.opensourcewebbook.com/">www.opensourcewebbook.com</a>
```
