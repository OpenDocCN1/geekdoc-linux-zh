
- 处理字符串内字符位置和长度的函数和运算符，而不是字节位置。排除项是 `pack()`、`unpack()` 和 `vec()`，它们传统上通过字节或位数据的方式工作。

- `pack()`/`unpack()` 的 `c` 和 `C` 格式不会改变——它们仍然提取基于字节的信息。如果你想使用字符，请使用 `U` 格式。

- `chr()` 和 `ord()` 函数作用于多字节字符。

- 标量上下文下的 `reverse()` 函数按字符反转，而不是按字节反转。

# Unicode 字符转换

目前没有方便的内置机制可以将 Unicode 字符字符串转换为适用于任何设备打印的格式。要在简单（不支持 Unicode）的设备上为了显示而对其进行翻译，最简单的方法可能是使用 `tr///` 将 ASCII 范围之外的所有内容转换为问号：

```
tr\0-\x{0ffff}/\0-\xff/?/
```

这不是一个整洁的解决方案，如果你想将 Unicode 转换为 Mac-Roman（例如），它将无济于。对于那些你有特定目标（或源）字符集的情况，解决方案是使用 Gisle Aas 的 Unicode `:Map8` 模块。

该模块在内部支持大多数基础表外，还提供了许多标准字符表的访问权限，包括 Macintosh、PC 代码页（以在 DOS/Windows 3.11 中使用的 CP 开头的代码页）。它甚至包含了某些特定字体的表，包括 Adobe Zapf Dingbat 字体涵盖了 Mac 和 Windows 机器可用的大部分表意文字。

## 总结

Perl 原生支持 Unicode，允许你使用处理普通 Perl 字符串相同的方法和技术创建 Unicode 兼容字符串。除了在字符串中支持 Unicode 之外，你还可以

# Perl 与 Unicode 373

也创建变量、函数和其他。

## 下一步

在下一章中，我们将回到 Web 并创建一个留言簿应用程序，学习 Perl 处理不同的数据格式。

# 第 14 章

为你的网站创建一个留言簿

万维网的奇能力之一是它可以作为存储库。存储在任何地方都可以被检索——只要它是可访问的。Web 打开了道路。

到为止，你写的 Perl 程序提供了即时反馈。但一旦信息输入并显示，它就消失了；因为它没有存储在任何地方。

在本章中，你将设计一个留言簿网页，允许访问者输入自己的详情。你将编写 Perl 程序来获取单个访问者的留言，将其存储在磁盘文件中，并显示整个访问者名单。你还将学习网站安全基础，以及如何防止访问者无意或恶意输入可能破坏你的网站或系统的数据。

# 为你的网站创建一个留言板

```html
<BODY>
<CENTER>
<H1 ALIGN="CENTER">Perl-CGI 留言板</h1>
<HR>
```
```html
<TABLE WIDTH="50%">
    <TR>
        <TD><strong>名：</strong></TD><TD><strong>姓： </strong></TD>
    </TR>
    <TR>
        <TD><INPUT TYPE="text" NAME="first_name" SIZE="24" MAXLENGTH="30"> </TD>
        <TD><INPUT TYPE="text" NAME="last_name" SIZE="24" MAXLENGTH="30"> </TD>
    </TR>
    <TR>
        <TD><strong>城市：</strong></TD><TD><strong>州： </strong></TD>
    </TR>
    <TR>
        <TD><INPUT TYPE="text" NAME="city" SIZE="24" MAXLENGTH="30"> </TD>
        <TD><INPUT TYPE="text" NAME="state" SIZE="24" MAXLENGTH="30"> </TD>
    </TR>
    <TR>
        <TD><strong>国家：</strong></TD><TD><strong>电子邮箱： </strong></TD>
    </TR>
    <TR>
        <TD><INPUT TYPE="text" NAME="country" SIZE="24" MAXLENGTH="30"> </TD>
        <TD><INPUT TYPE="text" NAME="email" SIZE="24" MAXLENGTH="72"> </TD>
    </TR>
</TABLE>
```
```html
<strong>评论：</strong><BR>
<TEXTAREA NAME="comments" COLS="36" ROWS="6">
</TEXTAREA>
```
```html
<BR>
<P>
<INPUT TYPE="submit" VALUE="提交你的名字">
<INPUT TYPE="reset" VALUE="清除表单">
</P>
</FORM>
</CENTER>

</BODY>
</HTML>
```

![](img/6e99147f217994f89499215b2cff677f_405_0.png)

**图 14.2：** 你的留言板入口页面

此页面是如何在 HTML 中构建表格的一个很好的示例。注意顶部的表格声明：

```html
<TABLE WIDTH="50%">
<TR>
<TD><STRONG>名： </STRONG></TD><TD><STRONG
```
```html
姓： </STRONG></TD>
</TR>
<TR>
<TD><INPUT TYPE="text" NAME="first_name" SIZE="24" MAXLENGTH="30"> </TD>
<TD><INPUT TYPE="text" NAME="last_name" SIZE="24" MAXLENGTH="30"> </TD>
</TR>
<TABLE>
```

这段代码将表格的宽度设置为屏幕宽的 50%，然后对第一组文本字段的行和列进行格式化，在本例中是用于访问客的名字和姓。

> **提示**
>
> 使用百分比而不是固定值来设置表格宽度是一个好主意。你的访问者将使用各种屏幕，运行在不同的分辨率下。宽度设置为特定像素数量的 HTML 表格将根据显示分辨率而变大或变小——在极端情况下，它可能甚至无法显示在屏幕上。使用百分比宽度可确保你的表格能够比例地适应屏幕，无论访问者的设备如何。

文本字段被赋予了 `MAXLENGTH` 值；这些值防止用户在字段中输入过多的数据。注意，脚本仍然必须监控输入过量的数据，因为恶意用户可以从页面的私副本中移除 `MAXLENGTH` 值。尽管如此，`MAXLENGTH` 帮助大多数用户做正确的事。

## 添加留言条目

从留言板表单收集并归档条目在 Perl 中是一项简单的工作。让我们创建一个名为 `addguest.pl` 的程序，如列表 14.2 所示。

### 14.2：addguest.pl

```perl
#!/usr/bin/perl

use GuestBook;

# 从 STDIN 获取 POST 信息并将其放入
# $post_info 中。
```
![](img/6e99147f217994f89499215b2cff677f_406_0.png)
```perl
read (STDIN, $post_info, $ENV { 'CONTENT_LENGTH' });
```
```perl
@InfoArray = split (&/, $post_info);
```

# 遍历 `@InfoArray` 中的每个元素，分离出

# "variable=" 部分，然后将加号转换为空格，

#并将任何转义的十六进制字符转换回其真实的字符值

```perl
for ($n = 0; $n < @InfoArray; $n++)
{
    ($dummy, $temp) = split (/, $InfoArray[$n], 2);
    $temp =~ tr/+/ /;
    $temp =~ s/([\dA-Fa-f]{2})\/pack("C", ($1))/eg;
    $InfoArray[$n] = $temp;
}
```

现在我们将检查是否有内容要写入留言板。我们至少需要一个名或一个姓；否则我们将跳过我们写入这些内容的例程。

```perl
if ((length ($InfoArray[$FirstName]) != 0 || (length ($InfoArray[$LastName]) != 0)
```

# 将当前时间附加数组末尾。将当前时间放入数组中。

```perl
$InfoArray[$NumEntryTime] = time();
```

# 将数据打包成二进制结构，以追加模式打开留言板文件并写入磁盘。
