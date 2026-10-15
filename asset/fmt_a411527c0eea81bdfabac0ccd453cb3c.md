
### sub numbers

```perl
{
  if ($a < $b)
    {-1; }
  elsif ($a == $b)
    { 0; }
  else
    {+1; }
}
```

- 3. 保存文件并退出编辑器。
4. 使用 `chmod` 命令授予文件执行权限。
5. 通过输入 `./perlsort.p3 numberlist` 并按回车来测试程序。你的屏幕应该类似于图 9-17。

![](img/6ed9bb33c68863516b7a954081187e3b_357_0.png)

`persort.p3` 程序使用语句 `$x = 0;` 来初始化变量 `$x`，使其包含指向数组的索引。每个数组的第一个元素都是 0 (0)。在 `while` 循环中，

```perl
while (<>)
{
  $somelist[$x] = $_;
  $x++;
}
```

文件中的下一行会自动复制到 `$_` 变量中。赋值语句 `$somelist[$x] = $_;` 将 `$_` 变量的内容复制到数组的一个元素中。元素由变量 `$x` 决定，该变量用作下标。赋值操作发生后，执行以下语句 `$x++;`

`++` 运算符对其参数加 1，该语句递增变量 `$x`。第一个名字 Aaron 被存放在 `$somelist[0]`，Alice 被存放在 `$somelist[1]`，依此类推。

语句 `$sortedlist = sort @somelist;` 对数组 `@somelist` 进行排序，将按字母顺序排列的名称放入 `sortedlist`。

## 使用 Perl 数值字段

数值字段排序需要一个子程序，你可以在要排序的数据之间定义比较条件（例如大于、小于或等于）。排序例程被反复调用，每次调用传递两个要比较的元素。标量变量 `$a` 和 `$b` 存储与较大值进行比较的值。使用比较操作，将返回一个 -1、0 或 +1 的返回码，取决于 `$a` 是否小于或大于 `$b`，如演示代码所示：

```perl
sub numbers
{
  if ($a < $b) { -1; }
  elsif ($a == $b) { 0; }
  else { +1; }
}
```

在对数字排序时，你需要指示 Perl 使用此子程序作为比较函数，而不是内置的 ASCII 升序排序（默认值）。要实现这一点，将子程序名放在关键字 `sort` 和待排序的条目列表之间：

```perl
$sortednumbers = sort numbers 101, 87, 34, 12, 1, 76;
```

该语句指示 Perl 排序列表中的值，但使用子程序来确定它们的顺序。输出是数值顺序，而不是 ASCII 顺序。

## Perl 和 CGI 编程

`$a` 和 `$b` 的数值比较非常频繁，以至于 Perl 的创始人 Larry Wall 开发了一个专门用于数值排序的 Perl 运算符 `<=>`。这种排序运算符被称为太空船运算符，减少了编码需求。为了说明节省的代码，将下一个使用太空船运算符的排序子程序与上一个进行比较：

```perl
sub numbers
{
  $a <=> $b;
}
```

此子程序产生与第一个 if-else 语句相同的结果。Perl 允许更紧凑的表示法：内联块，它看起来如下：

```perl
@sortednumbers = sort { $a <=> $b } @numberlist;
```

该语句使用块 `{ $a <=> $b }` 作为排序例程。它消除了对单独子程序的需求。让我们查看 Perl 程序如何对数值数据排序。

使用 Perl 进行数值排序：
1. 创建文件 `numberlist`，包含数据 130, 100, 121, 101, 120 和 122。
2. 使用你喜欢的编辑器创建 `persort.p3` 程序。输入此代码：
```perl
#!/usr/bin/perl
# 程序名: persort.p3
# 目的: 使用子程序进行数值排序。文件名在命令行输入。
# 语法: persort.p3 filename <回车>
$x = 0;
while (<>)
{
  $somelist[$x] = $_;
  $x++;
}
@sortedlist = sort numbers @somelist;
print @sortedlist;
sub numbers
{
  if ($a < $b)
    {-1; }
  elsif ($a == $b)
    { 0; }
  else
    {+1; }
}
```
- 3. 保存文件并退出编辑器。
4. 使用 `chmod` 命令授予文件执行权限。
5. 通过输入 `./perlsort.p3 numberlist` 并按回车来测试程序。你的屏幕应该类似于图 9-17。

## 总结

- Perl 被广泛用作强大的工具。
- Perl 有三种数据类型：标量、数组和哈希表。
- 标量是一个简单的变量，例如数字。标量变量以 `$` 开头。
- 数组是标量的有序列表，通过下标访问，从 `[0]` 开始。数组名称以 `@` 开头。
- 哈希表是无序的键值对集合，你可以通过键访问。哈希变量以 `%` 开头。

- 7. `$` 字符位于：
a. 数组名称
b. 标量变量名
c. 哈希名称
d. 常量

- 8. `@` 字符位于：
a. 数组名称
b. 标量变量名
c. 哈希名称
d. 常量

- 9. `%` 字符位于：
a. 数组名称
b. 标量变量名
c. 哈希名称
d. 常量

- 10. 假设一个程序包含以下代码：
`@food = ("$fruit", "steak", "bread", "vegetables" );`
在同一程序中，下一语句将打印什么？
`print("$food[2]");`
a. fruit
b. steak
c. bread
d. vegetables

- 11. 假设此代码存在于程序中：
`%food = ("$fruit", 5, "steak", 10, "bread", 15, "vegetables", 20 );`
在同一程序中，下一语句将打印什么？
`print("$food{'bread'}");`
a. 5
b. 15
c. steak
d. bread

## 练习

- 1. 编写一个 Perl 脚本打印 "Hello Perl"。
- 2. 编写一个 Perl 脚本对内存数组中的 1, 8, 15, 1000, 12 进行排序。
- 3. 使用练习 2 中的数字创建文件 Ex2numbers。编写一个 Perl 脚本使用空格运算符排序并显示 Ex2numbers。
- 4. 编写一个带有哈希变量的 Perl 脚本。哈希变量应包含以下姓名和电话号码：

Jean James 555-9898
Rhonda Smith 555-0982
Joe Milner 555-8944
Greg Jones 555-0716

程序应该显示每个人的电话号码。

## 发现练习

- 1. 修改程序 `perlcom.p`（在本章较之前开发），使其统计文件中所有非注释的行。
- 2. 编写一个 Perl 程序，统计学生文件（在本章较之前创建）中以字母 A 开头的记录数。
- 3. 编写一个 Perl 程序，将英寸值转换为厘米值并显示结果。（1 英寸 = 2.54 厘米。）
- 4. 编写一个 Perl 程序，使用 `while` 循环显示 1 到 12 的数值及其平方。
- 5. 编写一个 Perl 程序要求用户输入两个数值。将值存储在 `$x` 和 `$y` 中。如果 `$y` 不为 0，则将 `$x` 除以 `$y` 并显示结果。如果 `$y` 为 0，则显示错误消息，表示除零是不可能的。

## 课程 B 目标

在本节中你将：
- 为万维网创建一个 HTML 文档
- 使用 Perl 和 CGI 脚本使你的网页具有交互性
- 使用 X-Window 和 Netscape 获取网页

# 创建交互式网页

# 设置网页

你可以使用 HTML（超文本标记语言）创建网页。HTML 是一种创建嵌入 `tags`（标签）代码文档的格式。当在 Web 浏览器（如 Netscape Navigator 或 Internet Explorer）中查看文档时，标签会赋予文档特殊属性。属性示例包括前景颜色和背景颜色、字体大小和颜色以及图形图像的放置。此外，HTML 标签允许你在文档中放置超链接。超链接是文本或对象，点击它后会加载另一个文档并在浏览器中显示。

在使用 HTML 创建网页后，你将该页面发布在 Web 服务器上。Web 服务器是连接到 Internet 并运行如 Apache 等 Web 服务器软件的系统。Web 服务器允许其他用户通过 Internet 访问 HTML 文档。

你可以使用 Linux 系统的环回（loopback）网络功能来实验和测试 HTML 文档。环回允许你的 UNIX 或 Linux 系统访问其自身的外部网络内部网络配置。要使用环回，你不需要连接到任何网络。重要的是，环回可以模拟真实的 Web 网站，因此你可以对你的新网页进行测试和开发。建议对新网页进行单机测试：在充分测试你的工作成果后，你就可以将文档传输到任何 Web 服务器，并知道它们已准备好运行。

> 要运行本节中的网页和 CGI 程序，你必须在你的 Linux 计算机上安装 Apache Web 服务器程序。（安装 Apache 的说明请参见附录 C。）

# 创建网页

你可以使用可视化 HTML 编辑器（如 Netscape Composer 或 Microsoft FrontPage）来创建网页。这些程序允许你以“所见即所得”的方式图形化地构建网页。如果你没有可视化 HTML 编辑器，你只需要一个文本编辑器。你通过输入文本和所需的嵌入标签来创建 HTML。这里是一个 HTML 文件示例。

```
<HTML>
<HEAD><TITLE>My Simple Web Page</TITLE></HEAD>
<BODY>
<h1>A Simple Web Page</h1>
This is a web page with no frills!
</BODY>
</HTML>
```

所有包含尖括号 `<>` 内的特殊代码都是标签。第一个标签 `<HTML>` 标识文件为 HTML 文档。注意对应的 `</HTML>`。

## 第 9 章，B 节

信息被编码在 FORM 标签中。FORM 标签指定了如何获取要传输的信息。有两种方法：GET 和 POST。GET 方法在 URL 内部传输数据。POST 使用 HTTP 请求体部分来传递参数。（在本章中你将使用 POST 方法。）

你可以下载数百个已经写好的脚本，并将它们用于你自己的页面应用程序中。其中一些脚本是免费的，例如在这些演示中使用的 `subparseform.lib`。它是从 `http://www.cook-wood/perl` 下载的。

- 其他免费 Perl CGI 脚本的来源：
- `http://www.worldwidemart.com/scripts`
- `http://www.extropia.com`
- `http://www.awsdm.com/scripts`

- 这些网站提供了有用的 Perl 信息和常见问题（FAQ）的解答：
- `http://www.perl.com`（一个巨大的网站，汇集了大量信息）
- `http://language.perl.com/faq/index.html`
- `http://language.perl.com/info/documentation.html`

在为 Dominion Consulting 创建网页之前，你将首先看到网页在 UNIX 中是如何工作的。

## 要查看示例网页：

1. 创建一个存储 HTML、CGI 脚本和 Perl 脚本的子目录，输入 `cd /home/http/cgi-bin`，按回车，输入 `mkdir <你的用户名>`，然后按回车。例如，如果你是用户 Ellen，你将创建目录 `/home/http/cgi-bin/ellen`。

注意：确保 `/home/http/cgi-bin` 目录具有足够的访问权限（通常由系统管理员完成）。要在你自己的 PC 上执行此操作，请以超级用户身份登录，输入 `chmod 755 /home/http/cgi-bin` 然后按回车。

2. 将工作目录更改到第 1 步中创建的新目录。

3. 你的教师或技术支持人员获取将以下程序和脚本复制到新目录的说明：
   `project.html`
   `project.cgi`
   `subparseform.lib`

4. 启动 X-Window 系统（Microsoft Windows 的 UNIX 等效物）以运行 Netscape 浏览器。输入 `startx` 然后按回车。你的屏幕应该类似于图 9-21。

![](img/6ed9bb33c68863516b7a954081187e3b_368_0.png)
图 9-21: X-Window 系统

5. 在 X-Window 中，你可以从命令行执行 Netscape。你可以在 Terminal（终端）窗口访问命令行。要打开 Terminal 窗口，点击图 9-22 所示的 Terminal 图标。

![](img/6ed9bb33c68863516b7a954081187e3b_368_1.png)
图 9-22: Terminal 图标

6. Terminal 窗口出现，如图 9-23 所示。点击 Terminal 窗口内部使其激活。

![](img/6ed9bb33c68863516b7a954081187e3b_369_0.png)
**图 9-23：** Terminal 窗口

你将在浏览器中查看 `projest.html` 文件，但你必须先修改该文件，使其知道其 CGI 脚本的位置。将 `projest.html` 文件加载到你任选的编辑器中。文件内容所示。

```html
<!-- Program Name: projest.html -->
<HTML><HEAD><TITLE>Dominion Project Analysis</TITLE></HEAD>
<BODY>
<H2>Average Profit per Project Calculation</H2>
<FORM METHOD=POST ACTION="http://localhost/cgi-bin/projest.cgi">
Total cost of projects last year? <INPUT TYPE=text NAME=projest SIZE=10>
Number of Projects? <INPUT TYPE=text NAME=projects SIZE=10>
Project revenue received? <INPUT TYPE=text NAME=revenue SIZE=10>
<HR><INPUT TYPE=submit NAME=submit VALUE=Submit>
<INPUT TYPE=reset NAME=reset VALUE="Start over">
</FORM></body></html>
```

必须修改加粗行。将名称 "ellen" 改为你的登录名。例如，如果你的登录名是 sam，你将该行修改为：

```html
<FORM METHOD=POST ACTION="http://localhost/cgi-bin/sam/projest.cgi">
```

保存文件并编辑编辑器。

2. 现在你必须执行 Netscape 浏览器来查看示例网页。打开 Netscape Communicator，输入 `netscape` 并按回车。出现 Netscape 启动界面，如图 9-24 所示。

3. 注意：如果这是你第一次访问 Netscape，可能需要点击启动界面右下角的 Accept（接受）按钮。

4. 点击 Location（位置）文本框，按 Del 删除当前文本，然后输入 `file:/home/httpd/cgi-bin/<你的用户名>/projest.html` 作为你网页的地址。例如，如果你是 Ellen，输入 `file:/home/httpd/cgi-bin/ellen/projest.html`。

![](img/6ed9bb33c68863516b7a954081187e3b_370_0.png)
图 9-24: Netscape 启动界面

10. 按回车。出现 `projest.html` 网页的启动界面，如图 9-25 所示。

![](img/6ed9bb33c68863516b7a954081187e3b_371_0.png)
图 9-25: 由 projest.html 生成的网页

这是 `projest.html` 文件。

要确认你想使用 Common Gateway Interface（通用网关接口），点击确认界面上的 Submit 按钮。（如果你点击 Next 按钮，以后可以避免确认界面。） Perl 执行程序，Apache 服务器将网页传回 Netscape 浏览器进行显示。现在的/cgi 响应界面应该类似于图 9-26。点击 Submit 按钮让 Apache 使用 Common Gateway Interface 运行 `projest.cgi` 脚本。

![](img/6ed9bb33c68863516b7a954081187e3b_372_0.png)
图 26: Perl/CGI 响应界面

这是生成此页面的源码。

```perl
#!/usr/bin/perl
# Program name: projest.cgi
require "subparseform.lib";
&Parse_Form;
$projectcost = $formdata{'projectcost'};
$projects = $formdata{'projects'};
$revenue = $formdata{'revenue'};
$average = $projectcost / $projects;
$average = sprintf("%.2f", $average);
$grossprofit = $revenue - $projectcost;
print "Content-type: text/html\n";
```
