

![](img/d9230b719dc0efd80851f363d8c6f571_823_0.png)

## 798 了解 Perl 概述

默认情况下，`open` 函数以读取模式打开文件。你可以在文件名的开头添加特殊字符来指示其他类型的访问方式。`<` 前缀表示打开文件进行写入，而 `>` 前缀表示打开文件进行追加。下面是一个短脚本，它读取 `/etc/passwd` 文件并创建一个新的输出文件 `output`，其中列出了所有缺少 shell 的用户（这些用户的密码条目每行末尾都有 `:` 结尾）：

```perl
#!/usr/bin/perl
# 读取 /etc/passwd 并创建一个没有任何 shell 的用户列表

open (PWFILE, "/etc/passwd");
open (RESULT, ">output"); # 打开文件进行写入

while (<PWFILE>)
    if ($_ ~ /\n/) print RESULT $_;

close PWFILE;
close RESULT;
```

执行此脚本后，你发现在当前目录下有一个名为 `output` 的文件。以下是在 Fedora Core 系统上运行此脚本时的输出文件内容：

news:x:9:13:etc/news

### 带有管道前缀的文件名

一个有趣的前缀是管道字符——竖线 (`|`)。如果你在调用 `open` 时使用以 `|` 开头的文件，文件名的其余部分将被视为命令。Perl 解释器会执行该命令，你可以使用管道向该命令发送输入。接的 Perl 脚本使用 `mail` 命令向用户列表发送消息：

```perl
#!/usr/bin/perl
# 向用户列表发送邮件

foreach ("root", "naba") {
    open (MAILPIPE, "| mail -s Greetings $_");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

如果文件名以管道字符 (`|`) 结尾，则文件名将作为命令执行；你可以使用角括号（<>`）读取命令的输出，如下例所示：

```perl
open (PSPIPE, "ps ax |");
while (<<PSPIPE>)
{
```

## 799 了解 Perl 概述

# 处理 ps 命令的输出
# 此示例简单地回显每行
print $_;

### 子程序

尽管 Perl 包含了大量的内置函数，但你也可以以子程序的形式添加自己的代码模块。事实上，Perl 自带了一系列这类“程序中的程序”。下面是一个展示了 Perl 中子程序语法的简单脚本：

```perl
#!/usr/bin/perl
sub hello
# 从 @_ 数组中创建参数的局部副本
local ($first, $last) = @_;

print "Hello, $first $last\n";
```

```perl
$a = "Jane";
$b = "Doe";

&hello($a, $b);          # 调用子程序
```

当你运行上述脚本时，它会显示以下输出：

Hello, Jane Doe

注意关于子程序的以下几点：

- 子程序在数组 `@_`（`@` 符号，其后跟下划线字符）中接收参数。
- 子程序中使用的变量默认是全局的。使用 `local` 函数来创建一组变量。
- 通过在名称前放置 ampersand (`&`) 来调用子程序。因此，通过输入 `hello` 来调用子程序 `hello`。

如果你愿意，可以将子程序放在它自己的文件中。例如，`hello` 子程序可以存在名为 `hello.pl` 的文件中。当你将子程序放在文件中时，记住在文件末尾添加返回值——只需在末尾输入 `1;` 即可返回 1。因此，`hello.pl` 文件内容如下：

```perl
sub hello
{
# 从 @_ 数组中创建参数的局部副本
local ($first, $last) = @_;
print "Hello, $first $last\n";
return 1; # 返回值
}
```

## 800 理解 Perl 包（Packages）和模块

然后，你必须编写使用 `hello` 子程序的脚本，如下：

```perl
#!/usr/bin/perl
require 'hello.pl'; # 包含有子程序的文件

$a = "Jane";
$b = "Doe";

&hello($a, $b); # 调用子程序
```

此脚本使用函数来包含包含 `hello` 子程序的 `hello.pl` 文件。

### Perl 中的内置函数

Perl 拥有近 200 个内置函数（也称为 Perl 函数），包括类似于 C 运行时库的函数，以及访问操作系统的函数。你真的需要查阅函数列表，以体会 Perl 可用功能的广度。我在书中没有足够的空间来涵盖这些函数，但你可以通过浏览器指向以下地址来了解 Perl 内置函数：

www.perldoc.com/perlin5.8.0/pod/perlfunc.html

该地址将你连接到 Perl 5.8.0 文档页面，让你对 Perl 内置函数有一个概述。在该上，点击函数名称可以查看关于该函数的更详细信息。

你也可以在 Fedora Core 系统上通过在终端窗口输入命令来阅读 Perl 函数手册：

```bash
man perlfunc
```

该命令显示函数的文本型帮助页。（我认为你会发现基于 Web 的文档要好用得多。）

### 理解 Perl 包和模块

Perl 包（package）是一种将数据和子程序分组的方法。本质上，它是一种使用变量和子程序名称的方法，而不会与程序其他部分使用的名称冲突。包的概念从 Perl 4 版本开始就存在了。尽管你可能没有意识到，但当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。

## 801 理解 Perl 包和模块

包提供了一种控制命名空间的方法——命名空间指的是变量和子程序名称的集合。尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 模块遵循特定指南。你可以定义自己的包。

### 包

Perl 包是一种将数据和子程序组合在一起的方法。本质上，它是一种使用变量和子程序名称的方法，而不会与程序其他部分使用的名称冲突。包的概念从 Perl 4 版本开始就存在了。

包提供了一种控制命名空间的方法——命名空间指的是变量和子程序名称的集合。尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 模块遵循特定指南。你可以定义自己的包。

Perl 包是一种将数据和子程序组合在一起的方法。本质上，它是一种使用变量和子程序名称的方法，而不会与程序其他部分使用的名称冲突。包的概念从 Perl 4 版本开始就存在了。

包提供了一种控制命名空间的方法——命名空间指的是变量和子程序名称的集合。尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，其他 Perl 包位于 Perl 库中（在 `/usr/lib/perl/X.Y.Z` 目录下）。5.8 模块遵循特定指南。你可以定义自己的包。

## 802 理解 Perl 包和模块

ctime 定义在 `ctime.pl` 文件中。该包包含了将二进制时间转换为字符串的 ctime 子程序。下面的简单程序使用了 ctime 包：

```perl
#!/usr/bin/perl -w
# 使用 ctime.pl 中 ctime 包
require 'ctime.pl';

# 调用 ctime 子程序
$time = ctime(time());

# 打印时间字符串
print $time;
```

如你所示，此程序使用 require 函数将 `ctime.pl` 文件引入程序。当你运行此程序时，它会打印格式化的当前日期和时间，如下所示：

Jan 24 16:40:17 2004

注意此脚本的第一行使用了 `-w` 选项。该选项会导致解释器对 Perl 中任何错误的结构打印警告信息。在调用 Perl 解释器的行上包含 `-w` 选项是一个好主意。

![](img/d9230b719dc0efd80851f363d8c6f571_828_0.png)

```bash
perl -c filename
```

### Perl 模块

Perl 5 将包的概念向前推进了一步，引入了模块，模块是一种遵循特定指南并设计为可重用的包。每个模块都是定义在与包同名但扩展名为 `.pm` 的文件中的包。每个 Perl 对象都作为模块实现。例如，CGI 对象（用于 Web 服务器）通过 CGI 模块实现，存储在命名的 `CGI.pm` 文件中。

