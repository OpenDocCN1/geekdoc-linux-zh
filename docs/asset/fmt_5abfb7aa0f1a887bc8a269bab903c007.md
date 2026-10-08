
`package timelocal`

`package` 声明的作用是，后续的名称都将被视为 `timelocal` 包的一部分。如果你想在一个包中定义变量和子程序，可以在文件开头使用 `package` 语句。例如，`timelocal.pl` 文件在一个名为 `timelocal` 的包中定义了许多子程序和变量。在 Perl 5 中，这种包声明的效果是，后续的变量和子程序名都位于 `timelocal` 的包中。如果你想在另一个包中引用变量或子程序，可以使用 `Package::Variable` 语法。正如你所猜的，双冒号比单引号更具可读性。Perl 5 引入了这种，`Package` 是包名，`Variable` 是该包中的变量名。有一个名为 `ctime` 的包，它在 `ctime.pl` 文件中定义。该包包含了 `ctime` 子程序，它可以将二进制时间转换为字符串。

要在程序中使用该包，只需将文件名作为 `require` 函数的参数。例如，使用 `ctime` 包的程序如下：

```
#!/usr/bin/perl -w

# 使用在 ctime.pl 中定义的 ctime 包

require 'ctime';

# 调用 ctime 子程序

$time = ctime();

# 打印时间字符串

print $time;
```

该程序通过 `require` 函数将 `ctime.pl` 文件引入。当你运行此程序时，它应该打印格式化后的日期和时间：

Sun Nov 19 15:41:09 2000

注意，`-w` 选项允许 Perl 解释器对脚本中的错误打印警告。建议在调用 Perl 解释器的行包含 `-w` 选项。

### Perl 模块

Perl 5 进一步扩展了包的概念，引入了模块——遵循特定指南且设计用于重用的包。每个模块定义在与包同名的文件中，扩展扩展为 `.pm`。每个 Perl 对象都作为模块实现。例如，一个 CGI 对象作为 CGI 模块实现，存储在 `CGI.pm` 文件中。

Perl 5 自带许多模块。你可以在 Perl 5 安装目录的 `lib` 子目录下找到这些模块。对于 Perl 版本 5.6.1，Perl 模块位于 `/usr/lib/perl5/5.6.1` 目录（路径的最后部分是 Perl 版本号）。寻找以 `.pm` 结尾的文件。

## 使用模块

你可以调用 `require` 函数或 `use` 函数将 Perl 模块引入程序。例如，名为 `Cwd` 的 Perl 模块（在 `Cwd.pm` 文件中定义）提供了一个 `getcwd` 子程序，用于返回当前目录。你可以调用 `require` 函数引入 `Cwd` 模块，并如下调用 `getcwd`：

```
require Cwd; # 不需要完整文件名

$curdir = Cwd::getcwd();

print "Current directory = $curdir\n";
```

## 第 24 章：Shell 和 Perl 脚本

763

第一行将 `Cwd.pm` 文件引入此程序——你不需要指定文件的文件名；`require` 函数会自动在模块名称后添加 `.pm` 以确定要包含哪个文件。第二行显示了你如何调用 `Cwd` 模块中的子程序。当你使用 `require` 包含一个模块时，必须使用 `Module::subroutine` 格式来调用每个子程序。

如果你用 `use` 函数代替 `require` 来重写这个示例程序，它需要以下格式：

```
use Cwd;

$cwdir = getcwd(); # 不需要 Cwd: 前缀

print "Current directory = $cwdir\n";
```

最大的区别在于，你不再需要用模块名前缀（如 `Cwd::`）来限定子程序。

你可以使用 `require` 或 `use` 来在程序中包含模块。在使用这些函数时，你需要理解以下细微差别：

- 当通过调用 `require` 包含模块时，该模块仅在程序运行时调用 `require` 函数时才被包含。对于通过 `require` 函数包含的模块，你必须使用 `Module::subroutine` 语法来调用任何子程序。
- 当通过调用 `use` 包含模块时，模块在 `use` 语句被处理后立即包含在程序中。因此，你可以像调用程序内部的一部分一样调用模块中的子程序和变量。你不需要为子程序和变量添加 `Module::` 前缀。

你可能希望坚持使用 `use Module;` 语法在程序中包含模块，这让你在调用模块中的子程序时使用更简单的语法。

## 在 Perl 5 中使用对象

对象是一个数据结构，以及操作该数据的函数集合。每个对象都是类的实例，类定义了对象的类型。例如，一个矩形类可以拥有矩形的四个顶点作为数据；以及诸如计算矩形面积和绘制矩形的函数。那么，每个矩形对象都可以是矩形类的实例，具有不同的四个顶点坐标。从某种意义上说，对象是类的实例。

实现对象数据操作的函数（或子程序）被称为方法（methods）。这是借鉴最早面向对象编程语言之一 Smalltalk 的术语。

类还暗示了继承的概念。你可以通过扩展现有类的数据或方法（或两者都扩展）来定义一个新的对象类。继承的一个常见用途是表示不同对象类之间的“是一种”（IS A）关系。以几何形状为例，因为圆形“是一种”形状，而矩形“是一种”形状，你可以说圆形类和矩形类继承自形状类。在这种情况下，形状类被视为父类或基类。

面向对象编程的基本思想是，你可以将对象的数据和相关方法（子程序）封装成一个黑盒。程序仅通过公开的方法访问对象，而无需知道方法的内部工作机制。通常，程序员可以创建一个对象，调用其方法来获取或设置属性（这是对象数据的另一种说法），并销毁对象。本节将向你展示如何在 Perl 5 中使用对象。掌握这些知识后，你将能够利用对象作为你 Perl 程序的构建模块。

## 理解 Perl 对象

Perl 5 通过使用模块来实现对象，模块在文件中封装了数据和子程序。Perl 5 提供了以下简单的对象模型：

- 对象由引用（reference）表示（对象实现为指向哈希的引用）。
- 类是一个 Perl 模块，提供处理对象的方法。
- 方法是一个 Perl 子程序，它期望对象引用作为第一个参数。

对象的实现必须遵循某些规则，并在代表类的模块中提供某些方法。然而，在你的 Perl 程序中使用对象时，你并不真的需要了解关于对象的实现的细节。你只需要知道在使用对象时必须遵循的步骤。

## 创建和访问 Perl 对象

一个实用的 Perl 对象是 Lincoln Stein 的 CGI 对象，它由 Perl 模块 `CGI.pm` 实现。该模块随 Perl 分发一起，位于 `/usr/lib/perl5/6.1` 目录（针对 Perl 版本 5.6）。

正如名称所示，CGI 对象用于为万维网 服务器编写通用网关接口（CGI）应用程序。CGI 程序接受用户提交的查询，并返回一个带有响应的超文本标记语言（HTML）文档（这是用户在 Web 浏览器中看到的文档）。

当你创建一个 CGI 对象时，它会自动解析用户通过 HTML 表单提交的查询字符串。（这些你在许多 Web 页面上看到的表单；你基本上可以通过这些表单填写并提交信息。）CGI 对象提供了访问用户在表单上输入的参数的方法、创建网页所需的头部的方法以及为 CGI 程序返回的网页生成 HTML 代码。

要使用 CGI 对象，请遵循以下通用步骤：

1. 在程序中放置以下行以包含 CGI 模块：
   `use CGI;`
   你必须在创建 CGI 对象之前包含此行。

2. 创建 CGI 对象，请使用以下语法：
   `$query = new CGI;`
   其中 `$query` 是指向对象的引用。

3. 按照以下示例调用方法：
   `print $query->header;` // 发送 HTTP 头部
   `print $query->start_html("Title of document");`
   `print $query->end_html();` // 结束 HTML

要使用 CGI 对象，请遵循以下通用步骤：

- 1. 在程序中放置以下行以包含 CGI 模块：
   `use CGI;`
   你必须在创建 CGI 对象之前包含此行。
- 2. 创建 CGI 对象，请使用以下语法：
   `$query = new CGI;`
   其中 `$query` 是指向对象的引用。
- 3. 按照以下示例调用方法：
   `print $query->header;` // 发送 HTTP 头部
   `print $query->start_html("Title of document");`
   `print $query->end_html();` // 结束 HTML

## 使用 English 模块

Perl 包含一些具有奇怪名称的特殊变量，例如 `$_` 表示最后一个参数，`$` 表示对应最后错误的错误消息。要使用 English 模块，请在程序中包含以下行：
`use English;`

之后，你可以将 `$_` 称为 `$ARG`，将 $$` 称为 `$ERR`（这些“英语”名称可能仍然有点晦涩）。

766 第五部分：Red Hat Linux 编程

以下程序使用了 English 模块并打印了几个变量：

```perl
#!usr/bin/perl -w

# File: english.pl

use English;

if($PERL_VERSION ge v5.6.0)

{

    print "Perl version 5.6.0 or later\n";

} else

{

    print "Perl version prior to 5.6.0\n";

}

print "Perl executable = $EXECUTABLE_NAME\n";

print "Script name = $PROGRAM_NAME\n";
```

当我运行此脚本时，输出如下：

```
./english.pl
Perl version 5.6.0 or later
Perl executable = perl
Script name = ./english.pl
```

English 模块非常实用，因为它让你编写 Perl 脚本时可以使用有意义的名称引用变量。要学习更多关于 Perl 特殊变量的内容，请在 shell 提示符输入 `man perlvar`。

### 总结

脚本或解释型程序通常用于自动化 Linux 中的各种任务。本章重点关注使用 Bash——Bour Again shell——以及 Perl 脚本语言编写脚本。

通过阅读本章，你学习了以下内容：

- Shell 脚本无非是文件中的一系列 Linux 命令。通常，你需要在脚本文件的开头放置一个特殊行，并使其具有可执行权限。然后你就可以在 shell 提示符处输入其名称来运行脚本。
- 当你的 Red Hat Linux 系统启动时，存储在 `/etc` 目录下各种子目录中（例如 `/etc/init.d`）的 shell 脚本会执行许多初始化任务。
- 有许多内置 shell 命令可以在 shell 脚本中使用。你已经熟悉了一些内置命令，如 `cd` 和 `pwd`，但本章描述了更多内置 shell 命令。
- Perl 是一种流行的脚本语言，出现在本书的附带 CD-ROM 光中。你可以使用 Perl 在你的 Red Hat Linux 系统上编写强大的脚本。
- Perl 包含了与其它编程语言（如 C）相当的功能。Perl 的一个强大特性是能够使用正则表达式并在文件中搜索搜索模式的出现情况。
- Perl 5 是 Perl 的最新版本（也是 Red Hat Linux 自带的版本），包含了许多实用的功能。一个关键特性是 Perl 模块（module），它是遵循某些指南的子程序包。模块使得在 Perl 中实现对象成为可能。
- 你可以从 Perl 存档网络（CPAN）下载最新版本的 Perl（以及 Perl 文档），地址为：`http://www.perl.com/CPAN/`。

## 第 25 章

### Tcl/Tk 脚本编写

**本章内容**

- 了解 Tcl/Tk
- 理解 Tcl 语法
- 编写 Tcl 脚本
- 使用 Tk 为 Tcl 脚本构建图形界面
- 通过示例学习使用 Tcl/Tk

如果你已经是一名 C 和 X Window 系统程序员，你将惊讶于使用 Tcl（工具命令语言）及其相关的 X 工具包创建图形应用程序是如此简单——它们统称为 Tcl/Tk（读作 "tickle/tee kay"）。Tcl 是一种类似于 Perl 的脚本语言。Tcl 最大的优势是它的 X 工具包 Tk，它使你能够开发带有图形界面的脚本。

当我开始使用 Tcl/Tk 时，我发现只需要几行 Tcl/Tk 代码就能创建一个图形界面，这感到非常惊喜。对于新手来说，Tcl/Tk 脚本看起来仍然相当复杂，但如果你用过基于 C 的工具包（如 Xt 和 Motif）编写程序，你就能体会到 Tcl 的高级性。在 Tcl 中创建按钮等用户界面组件比在 Motif 中简单得多。在 Tcl 中你仍然需要处理许多细节，例如如何布局用户界面的组件，但你可以比调用 Motif 库的 C 程序更快地看到结果。

如果你从未编写过程序，请不要跳过这一章。本章的示例将教你 Tcl 和 Tk 的基础知识。当你看到如何快速地使用 Tcl/Tk 解释器创建带有图形界面的应用程序后，你一定会成为 Tcl/Tk 的支持者。

## 介绍 Tcl

Tcl 的创建者 John Ousterhout 意图将其一种简单的、可嵌入的脚本语言，其解释器可以与任何 C 程序链接，以便该 C 程序可以使用 Tcl 脚本。“嵌入式*（embeddable）一词指的是 Tcl 的这种属性：任何 C 程序使用 Tcl 解释器并运行 .tcl 脚本的能力。

## Tcl/Tk 从何而来？

John Ousterhout 在伯克利加州大学就读期间创建了 Tcl 和 Tk。Tcl 首次于 1989 年；Tk 随后于 1991 年出现。Tcl/Tk 免费供无限制使用，包括商业用途。本书时，当前的 Tcl 版本为 8.3；Tk 也是 8.3。本书的第一张附带 CD-ROM 包含了 Tcl/Tk。

以下章节提供了 Tcl、其语法以及一些重要命令的概述。由于 Tcl 是 Tcl 工具包的基础，在跳到 Tk 之前，你应该先熟悉 Tcl，尽管 Tcl 无疑更有趣，因为你可以用它创建图形界面。

## 你的第一个 Tcl 脚本

在第 24 章中，你学习了如何编写 shell 脚本和 Perl 脚本。用同样的方式编写 Tcl 脚本。与 Perl 不同，Tcl 包含一个 shell——一个 Tcl 命令的交互式解释器。Tcl shell 的名称是 `tcl`；它应该在 `/usr/bin` 目录下。

当你登录时，PATH 环境变量应该包含 `/usr/bin` 目录。因此，你可以通过输入 `tcl` 来启动 Tcl shell。下一行会出现一个百分号 (%)；这是 Tcl shell 的提示符。要查看你拥有的是哪个版本的 Tcl，请在 Tcl shell 提示符处输入 `info tclversion`。Tcl shell 通过打印 Tcl 的版本来响应：

```
tcl
% info tclversion
8.3
%
```

现在你可以交互式地尝试以下 Tcl 程序，它将在标准输出（显示屏）上打印 Hello, World!：

```
% puts "Hello, World!"
Hello, World!
% exit
```

输入 `exit` 退出 Tcl shell (`tclsh`)。

请注意，我在之前的章节中没有显示 shell 提示符，但在本章的列表中显示了 Tcl 提示符 (%)。这是因为 Tcl 提示符看起来与 Bash 提示符不同，这应该告诉你你没有在 Bash 中工作。

Tcl shell 会立即处理你输入的 Tcl 命令并显示结果；然后提示你进行下次输入。此时，你可以输入 `exit` 退出 Tcl shell。

## 第 25 章：Tcl/Tk 脚本编写

### More Tcl

本节提供了 Tcl、其语法以及一些重要命令的概述。由于 Tcl 是 Tcl 工具包的基础，在跳到 Tk 之前，你应该先熟悉 Tcl，尽管 Tcl 不无疑更有趣，因为你可以用它创建图形界面。

### 你的第一个 Tcl 脚本

在第 24 章中，你学习了如何编写 shell 脚本和 Perl 脚本。用同样的方式编写 Tcl 脚本。与 Perl 不同，Tcl 包含一个 shell——一个 Tcl 命令的交互式解释器。Tcl shell 的名称是 `tcl`；它应该在 `/usr/bin` 目录下。

当你登录时，PATH 环境变量应该包含 `/usr/bin` 目录。因此，你可以通过输入 `tcl` 来启动 Tcl shell。下一行会出现一个百分号 (%)；这是 Tcl shell 的提示符。要查看你拥有的是哪个版本的 Tcl，请在 Tcl shell 提示符处输入 `info tclversion`。Tcl shell 通过打印 Tcl 的版本来响应：

```
tcl
% info tclversion
8.3
%
```

现在你可以交互式地尝试以下 Tcl 程序，它将在标准输出（显示屏）上打印 Hello, World!：

```
% puts "Hello, World!"
Hello, World!
% exit
```

输入 `exit` 退出 Tcl shell (`tclsh`)。

请注意，我在之前的章节中没有显示 shell 提示符，但在本章的列表中显示了 Tcl 提示符 (%)。这是因为 Tcl 提示符看起来与 Bash 提示符不同，这应该告诉你你没有在 Bash 中工作。

Tcl shell 会立即处理你输入的 Tcl 命令并显示结果；然后提示你进行下次输入。此时，你可以输入 `exit` 退出 Tcl shell。

要准备 Tcl 脚本，请按照以下步骤操作：

1. 使用文本编辑器输入以下行：

```tcl
#!/usr/bin/tcl

puts "Hello, World!"
```

2. 使文件变为可执行：

```bash
chmod +x hello.tcl
```

3. 运行脚本：

```bash
./hello.tcl
```
