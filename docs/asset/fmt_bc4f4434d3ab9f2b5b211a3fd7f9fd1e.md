
- 3. 保存文件并退出编辑器。
- 4. 使用 `chmod` 命令赋予该文件执行权限。
- 5. 通过输入 `./perlsort3.pl numberlist` 并按回车键测试程序。你的屏幕应该与图 9–8 相似。

![](img/b5f7722b7c2983a215c7726aaada19f9_359_0.png)

图 9-8 `perlsort3.pl` 的输出

`persort3.pl` 程序使用一个排序子程序，该程序以数值而非文本方式比较 `$a` 和 `$b`。程序还初始化了数组元素索引，从第一个元素 0 开始。`while` 循环：

```perl
while (<>) {
  $somelist[$x] = $_;
  $x++;
}
```

工作原理与之前描述的相同，即从文件中读取并将行存储在数组中。

# 使用 Perl 排序 339

排序子程序：
```perl
{
  if ($a < $b) {-1; }
  elsif ($a == $b) {0; }
  else {+1; }
}
```

比较从 `while` 循环顺序传递给它的两个数字。如果 `$a` 中的值小于 `$b` 中的值，子程序返回 -1。如果 `$a` 等于 `$b`，子程序返回 0。否则，子程序返回 +1。

现在看看使用太空船运算符如何为你节省编写代码的时间。

# 使用 Perl 的太空船运算符

- 1. 使用你喜欢的编辑器创建程序 `persort4.pl`。输入以下代码。
```perl
#!/usr/bin/perl
# 程序名: persort4.pl
# 目的: 使用太空船运算符
# (<=>) 数排序
# 语法: persort4.pl filename <Enter>
=====================================================================
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
  $a <=> $b;
}
```
- 2. 保存文件并编辑。
- 3. 使用 `chmod` 命令赋予该文件执行权限。
- 4. 通过输入 `./persort4.pl numberlist` 并按回车键测试程序。你的屏幕应该显示按升序排列的数字，类似于 `persort3` 的结果：

```
tom@localhost]$ ./persort4.pl numberlist
100
101
120
121
122
130
```

![](img/b5f7722b7c2983a215c7726aaada19f9_360_0.png)

# 第9章 节 B Perl 与 CGI 编程

在 `persort4.pl` 程序中，注意 `persort3` 的那些代码变化。

现在你对 Perl 更加熟悉，可以学习如何创建一个网页。

## 节 B

# 创建交互式网页

完成本节后，你应该能够：

- 设置一个 HTML 网页
- 使用 Perl 和 CGI 脚本让你的网页具有交互性
- 使用 X Window 和 Netscape 获取网页

## 设置网页

在本节中，你将体验 Web 文档和基于 Perl 的编程。这两种编程只是开始，因为关于这些领域有大量的书籍。本章的目的是帮助你体验它们，了解它们的用途，并激励你寻求更多体验

你可以使用 HTML（超文本标记语言）创建网页。HTML 是一种创建带有编码标签文档的格式。当在 Web 浏览器（如 Netscape 或 Internet Explorer）查看文档时，标签赋予了文档特殊属性。属性的示例包括前景和背景颜色、字体大小和颜色以及图片的放置。此外， HTML 允许你在文档中放置超链接。超链接是文本或对象，点击后加载另一个文档并在浏览器中显示。

在你使用 HTML 创建网页后，然后将网页发布在 Web 服务器上。Web 服务器是运行的 Web 服务器软件，例如连接到互联网的 Apache。Web 服务器让其他人可以通过互联网访问 HTML 文档。

你可以使用 Linux 系统的环回网络功能测试 HTML 文档。环回功能允许你的 UNIX 或 Linux 系统访问其自身的内部网络配置。更重要的是，通过环回你不需要连接到任何网络。它可以模拟真实的网站，因此你可以对新页面进行测试和开发。

# 第9章 节 B Perl 与 CGI 编程

![](img/b5f7722b7c2983a215c7726aaada19f9_363_0.png)

**图 9-9** 简单网页

浏览器会自动换行文本，因此你不需要担心页面宽度。然而，要使文本居中，请使用 `<CENTER>(此处文本)</CENTER>`。要从左右边距缩进，请使用 `<BLOCKQUOTE>(此处文本)</BLOCKQUOTE>`。要更改颜色，请使用 `<FONT COLOR="RGB\(此处文本)</FONT>`，其中 RGB 是 RGB 颜色代码。**RGB 颜色代码**是由三个数字组成的集合，用于指定颜色的红、绿、蓝分量。例如，代码 512218 指定红色分量为51，绿色分量为22，蓝色分量为18。数字越大，颜色分量越强烈。

这是另一个 HTML 文件的示例。

```
<HTML>
<HEAD><TITLE>UNIX Programming Tools</TITLE></HEAD>
<BODY>
<H1><CENTER>My UNIX Programming Tools</CENTER></H1>
<H2>Languages</H2>
<P>Perl</P>
<P>Shell Scripts</P>
<P>C and C++</P>
<H2>Editors</H2>
<P>Emacs</P>
<H2>Other Tools</H2>
<P>awk</P>
<P>sed</P>
</BODY>
</HTML>
```

图 9-10 显示了文件在 Web 浏览器中显示的样子。

![](img/b5f7722b7c2983a215c7726aaada19f9_364_0.png)

**图 9-10** UNIX 编程工具网页

现在你已经有了关于创建网页的一些常知识，需要学习如何使用 Perl 和 CGI 来让它们具有交互性。

# CGI 概述

Perl 是 **CGI（通用网关接口）编程**最常用的语言。CGI 是一种协议（或一组规则），规定了浏览器和服务器之间通信的方式。任何从服务器发送或接收信息的脚本都需要遵循 CGI 指定的标准。因此，用 Perl 编写的脚本遵循 CGI 协议。CGI Perl 脚本专门编写用于通过你的网页输入、处理和返回信息，即，让你的网页具有交互性的功能。

为了让你的 HTML 文档接受输入（特别是在适用 CGI 规则的地方），请在输入区域之前加上关于你想要输入内容的描述。例如，如果你让用户输入成本，将使用以下代码：

```
Total Cost? <INPUT TYPE=text NAME=cost SIZE=10>
```
