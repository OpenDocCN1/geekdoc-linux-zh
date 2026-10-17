
要查看此，请加载 `http://localhost/wml/define.html` 或 `www.opensourcewebbook.com/wml/define.html`。结果可以在图 6.9 中看到。关于定义标签的更多信息，请参见 `man wml1_p2.mp4h`。

![](img/9b05e38e58495be06a08eeb2b690634_209_0.png)

图 6.9 定义你自己的标签

## 6.10 编程代码——perl

WML 的一个很棒的特性是可执行的 Perl 代码（在 WML 中嵌入 Perl 代码=`perl!`: `HTML::Emperl`）8 嵌入 HTML 文档中，允许将任意计算的性能输出到 HTML 中。

可以使用 `< ... :>` 语法将 Perl 代码插入文档。对于一个简单的示例，请查看 `/var/www/html/wml/perl11.wml`：

```
<
print "Hello, world!"
>
```

> 8 见第 10 节。

### 第 6 章 网站元语言

构建 HTML 使用：

```
$ wmk eperl1.wml
wml -n eperl1.html perl
```

生成的 HTML 位于 `/var/www/html/wml/eper1.html`：

Hello, world!

我们确定你可以猜到它看起来是什么样，但为了证明你是的，请查看 `www.opensourcewebbook.com/wml/eper1.html` 或 `http://localhost/wml/eper1.html`。这个示例说明了块内的内容是由 `wmk` 输出的。

有些人（不是我们）会认为在块中打印文本很痛苦——为什么不直接显示块的内容？为了解决这个问题，WML 允许以下隐含打印：

```
"Hello, world!";
```

我们倾向于使用这种语法——我们想告诉 WML 何时输出我们的文本，但你可能不同意。没关系——Perl 允许任意计算。这个示例创建一个 Perl 变量并处理它，生成指向网站的链接。可以在 `/var/www/html/wml/eper2.wml` 找到代码分配了一个哈希变量 `%websites`，关于网站的信息。然后按键对哈希排序并打印 HTML。#176 第二部分 静态内容

通过以下命令生成 HTML：

```
$ wmk eperl2.wml
wml -n -o eperl2.html eperl2.wml
```

生成的 HTML 位于 `/var/www/html/wml/eper2.html`：

```
<a href="http://www.net/">net
<a href="http://google.com/">Google
<a href="http://hacking.com/">hacking
<a href="http://www.opensourcewebbook.com/">OS
```

现在有四个指向重要网站的链接。遵循这些链接，访问 `www.opensourcewebbook.com/wml/eper2.html` 或 `http://localhost/wml/eper2.html`。这在模板中非常有用——例如，生成面包屑导航（显示你在网站的位置并链接到其他页的列表），例如参见 `www.opensourcewebbook.com/contents/wml/` 开始“Page Path”。可以通过创建一个接受名为 `$(page)` 的变量来实现，其定义如下：

URI1:Text1:URI2:Text2:URI3:Text3:Other text

例如，使用此值：

/book1/:Book 1:/book1/chapter3/:Section 2

第一个对 `/book1/` 和 Book 1 变成如下所示的链接：

```
<a href="/book1/">Book 1
```

第二个对 `/book1/chapter3/` 和 Chapter 3 变成如下所示的链接：

```
<a href="/book1/chapter3/">Chapter 3
```

`$(page)` 的最后一个元素 Section 2 不是一对，因此它作为纯文本打印。此外，此示例演示了 `$(ROOT)` 的使用，它在 `.wrc` 文件中定义为 `-ROOT`。记得包含 `.wrc` 文件的目录（这里是 `/var/www/html/`）将是 HTML 文档的根目录。然后，

# 第 6 章 网站元语言 177

任何使用此变量的 WML 文件都会神奇地创建相对于包含 `.wml` 文件的目录。例如，如果文件在 `/contents/`，则：

```
<a href="$(ROOT)/sourcecode/">
```

变为：

```
<a href="../sourcecode/">
```

如果文件在 `/contents/wml/`，结果变为：

```
<a href="../sourcecode/">
```

查看 `/var/www/html/wml/breadcrumb.wml` 中的模板：

```
<html>
<head>
<title>Bread Crumb Example</title>
</head>
<body bgcolor="#ffffff">
  # 获取传入的页面信息
  my page_string = "$(page)";
  # 如果页面信息为空，则处理它
  if ($page_string ne "") {
    # 首先，打印一些红色文本
    print "<font color="#FF0000\"><b>Page Path - </b></font>";
    # 按冒号分割行，以防传递了
    # 多于 href:text1:href2:text2:final text
    # 循环构建链接
    my @page = split(:/, page_string);
    while (@page > 1) {
      my $href = "$(ROOT)". shift(@page);
      my $text = shift(@page);
      print "<a href=\"$href\"><font color="#999996\"><b>$text</b></font></a - ";
    }
    print "$page[0]";
  } else {
    print "No bread crumbs!\n";
  }
</body>
</html>
```

#178 第二部分 静态

`perl` 块中执行的第一件事是获取 WML 变量 `$(page)` 并将其转换为 Perl 变量 `$page_string = "$page"`。双引号是强制性的——如果不使用，Perl 将无法正确解释内容。代码接着检查字符串是否为空。如果是空字符串，代码只需打印“No bread crumbs.”。这对于真实的模板不是必要的，但会在测试代码时带给我们一种温暖的感觉。

处理页面始于打印一些 HTML 来显示红色文本 Page -。然后按冒号分割字符串：列表中仍有多个元素，模板输出 HTML 来构建链接。最后，打印最后一个文本，即没有配对的，这里存储在 `$page[0]`。

此处使用的代码是 `/var/www/html/wml/eper13.wml`（这全部应该是一行，在这里换行是为了适应页面）：

#use wml::breadcrumb page="/contents/contents/wml/:WML: Bread Crumbs

异常简单——只需使用一个语句。变量 `page` 被赋值为由冒号分隔的五个部分。因此，我们最后有两个链接和一些文本。

使用此命令构建 HTML：

```
$ wmk eperl13.wml
wml -n -o eperl13.html eperl13.wml
```

生成的代码位于 `/var/www/html/wml/eper13.html`。应该注意，以 `<font color=` 开始到 `<body>` 之前的行都是同一行，为了清晰起见进行了折：

```
<html>
<head>
<title>Bread Crumb Example</title>
</head>
<body bgcolor="#ffffff">
<font color="#FF0000"><b>Page Path - </b></font>
<a href="../contents/"><<font color="#999996"><b>/Contents/</b></font></a
<a href="../contents/wml/"><font color="#999996"><b>/WML/</b></font></a
</body>
</html>
```

### 第 6 章 网站元语言 (Website META Language)

![](img/9b05e38e58495be06a08eeb2b6906346_214_0.png)

图 6.10 面包导航

结果可以在图 6.10 中看到。要亲自查看，请访问 `www.opensourcewebbook.com/wml/eper13.html` 或 `http://localhost/wml/eper13.html`。
