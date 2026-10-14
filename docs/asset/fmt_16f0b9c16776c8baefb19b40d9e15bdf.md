
$iteration=$ENV("QUERY_STRING");

$again=$iteration + 1;

# 输出内容类型

print "Content-type: text/html\n\n";

# 开始输出

print<<10;End_of_page;

<HTML>

<HEAD><TITLE>Back Again?</TITLE>

<META HTTP-EQUIV="Refresh"

CONTENT="10; URL=http://unix.yasd.com/book-bin/backagain.cgi?$again">

</HEAD>

<BODY>

```
第 6 章 -- 动态页面
```

<h1>你曾在这里</h1>

```html
<FONT COLOR="#FF0000" SIZE=5>$iteration </font> 次!
```
```html
</FONT>
</BODY>
</HTML>
```
End_of_page

```
exit(0);
```

告知 Web 页面阅读器他们已经经过了若干次自动刷新循环并不很有用。然而，你可以添加增加此概念实用性的内容。下一个示例在文档末尾添加了信息，即在特定时间，指定为 Webmaster的人员已登录系统或注销系统。此外，CGI 程序直接从浏览器调用，而不是由 HTML 文档启动。列表 6.12 显示了 Perl 代码。

## 列表 6.12 访问时间并生成 HTML 文档的 CGI 程序 (backagain.cgi)

```perl
#!/usr/local/bin/perl
#
# backagain2.cgi
#
# 该应用程序根据嵌入文档的
# 刷新响应头由服务器调用。
# 该程序的每次迭代都会测试
# webmaster 是否在位，并将此信息
# 添加到文档中
#
# 首先获取时间并赋值给变量
($sec, $min, $hour, $date, $month, $year) = localtime(time);
```

```perl
# 接下来，检查 webmaster
open(MASTER, "/usr/bin/w -h shelleyp |");
read(<MASTER,$result,200);
if (index($result,"shelleep") >= 0) {
    $status = "logged in.";
} else {
    $status = "logged out.";
}
close(MASTER);
# 输出内容类型
print "Content-type: text/html\n\n";
# 开始输出
print<<10;End_of_page;
<HTML>
<HEAD><TITLE>Back Again?</TITLE>
<META HTTP-EQUIV="Refresh"
CONTENT="10; URL=http://unix.yasd.com/book-bin/backagain.cgi?$again">
</HEAD>
<BODY>
```

```html
<h1>You have been here</h1>
<FONT COLOR="#FF0000" SIZE=5>$iteration </font> times!
```

```html
</FONT>
</BODY>
</HTML>
```
End_of_page

```
exit(0);
```

## 第 6 章 -- 使用动态页面

接下来，你可以输出一个数据块。你需要定义数据对象的内容类型，在这种情况下是 `gif`（用于 GIF 文件）。该类型也可以是 `text/html`（用于 HTML 格式）或 `jpeg`（用于 JPEG 文件），如下所示：

```
print "Content-type: image/gif\n\n";
```

实际输出相对简单。对于图形，使用 Perl 的 `open` 命令打开图形文件；使用 `print` 打印文件；最后关闭文件，如下：

```
open(GRAPHIC, $member);
print <GRAPHIC>;
close(GRAPHIC);
```

最后，你必须再次打印边界字符串以刷新缓冲区并确保内容显示，如下代码所示：

```
print "\n-appboundary\n";
```

如果你记得这些语句中的每一个语句，CGI 应用程序就会按照你的预期运行。你可以修改数据块的类型，并在循环中打开并打印数据块来实现动画。图 6.13 展示了一个使用五个 GIF 文件执行相对简单动画的服务器应用程序。

**图 6.13**：此图显示了在 HTML 文档加载后立即使用服务器推送（server push）加载图像的结果。

图 6.14 展示了相同的页面，但现在的图形不同。大约每隔 3 秒，服务器会将一个数据块加载到 GIF 中。图中显示的图像实际上是加载的第四张图像。

**图 6.14**：此图显示了在 Web 页面文档加载几秒后使用服务器推送加载图像的结果。

要创建图中所示的效果，你需要同时创建一个 CGI 应用程序和一个 HTML 文档。列表 6.13 显示了该 CGI 应用程序的 Perl 代码。

### 列表 6.13 用于实现服务器推送创建动画的 CGI 应用程序 (nph-dynamic.cgi)

```perl
#!/usr/local/bin/perl
#
# dynraphic.cgi
```

# 此应用程序使用服务器推送来
# 更改 HTML 文档中显示的图形。

#
# 创建图形数组

```perl
$|=1;
$count=1;
@grapharray = ("one.gif","two.gif","three.gif","four.gif","five.gif");
# 文件开始时，nph-
# 应用程序需要 HTTP 指令
print "HTTP/1.0 200 Okay\n";
print "Content-type: multipart/x-mixed-replace;boundary=appboundary\n\n";
print "---appboundary\n";
while ($count <= 10) {
    foreach $member (@grapharray) {
        print "Content-type: image/gif\n\n";
        open(<GRAPHIC>, $member);
        close(<GRAPHIC>);
        print "\n-appboundary\n";
        sleep 3;
    }
    $count++;
}
```

## 第 6 章 — 使用动态页面

Perl 代码包含了在本章之前讨论过的语句。每个 GIF文件的文件名被加载到数组中。打印 HTTP 响应头和 MIME 类型。接下来，创建了一个循环 10 次的外层循环。最后，创建了一个内循环；该循环遍历包含 GIF 文件名的数组，并依次访问每个文件。每个名称都用于打开并打印图形。文件关闭后，打印边界字符串以结束数据块。此过程对每个 GIF 文件都会发生。当内层循环结束时，外层循环将再次运行。

此文件可以直接从浏览器运行，但单独一个图形并没有太大帮助。要将此服务器推送动画嵌入 HTML 文档中，实际上通过 `IMG` 标签调用应用程序。列表 6.14 显示了图 6.13 和 6.14 中所示文档的 HTML。

### 列表 6.14 用于创建内联动画的 HTML 文档 (dyngraphic.html)

```html
<HTML>
<HEAD></HEAD>
<BODY BGCOLOR="#FFFFFF">
<IMG SRC="../book-bin/nph-dyngraphic.cgi">
<p>
<H1> 使用服务器推送的内联动画</H1>
<p>
<H2>Ooooh. Ahhhh. 动画。</H2>
</BODY>
<HTML>
