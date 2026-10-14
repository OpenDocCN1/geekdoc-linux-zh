
# 第 16 章 -- 子程序定义

## 子程序原型

Perl 5.0 引入了声明有限原型的能力。这种能力允许早期检测参数数量的错误。原型的主要用途是编写模块，因为它们指定了参数的数量。

## `my()` 和 `local()` 的作用域问题

使用 `my()` 声明的变量是块部的，对该块之外的所有上下文完全隐藏。块局部变量必须以字母数字（或下划线）开头。通过 `local()` 声明的变量是动态的。通常，你应该使用 `my` 代替 `local()`，因为它更快更安全。此规则的例外包括全局变量、文件句柄以及对符号表的直接操作。格式变量通常使用 `local`，以便其他变量当前值对子程序可见。

## Perl 库

Perl 4.0 标准库有31个文件。这些文件在 Perl 5.0 中被一组基于 `require()` 的标准模块（下节）所取代。包机制本身提供了一种将命名空间划分为单元的方法。当这种机制与存储可以通过 `require()` 加载的子程序套相结合时，就创建了一个库。

## 库的创建

库本质上是包中的子程序集合。将库设置为库文件是一个相当直接的过程。将子程序放在单独的文件中，并在文件顶部添加包声明。库文件名和包名应该相同。然后在文件末尾添加一行

```
1;
```

（这样当被 `require()` 函数包含时它就会返回 `TRUE`）。

### 第 16 章 -- 子程序的定义

```perl
# 库文件 (Perl 4)

package filtest;

sub main::filtest {

    local($fil) = @_

    -f $fil && print "File $fil is a normal file.\n";

    -d $fil && print "File $fil is a directory.\n";

}
```

在 Perl 5.0 中，优先使用 `main::mysub` 而不是 `main'mysub` 来显式指定包名，但在 Perl 5.0 中你应该考虑创建一个模块（module）而不是库。

## 库的调用

要使用库，请使用 `require()` 来引用库名。Perl 在尝试定位此文件时，会搜索 `@INC` 变量指定的所有目录。要包含上一节中指定的示例库文件，请使用以下代码：

```perl
#!/usr/bin/perl -w

#
require "filtest";

&filtest("/usr/bin/");

&filtest("/usr/etc/passwd");
```

## 标准 Perl 4.0 库

以下是标准 Perl 4.036 库中的文件，这些文件已被 Perl 5.0 模块取代：

| abbrev.pl | getcdw.pl |
| :--- | :--- |
| assert.pl | getopt.pl |
| bigfloat.pl | getops.pl |
| bigint.pl | importenv.pl |
| bigrat.pl | look.pl |
| cacheout.pl | newgetop.pl |
| chat2.pl | open2.pl |
| complete.pl | perldb.pl |
| ctime.pl | pwd.pl |
| dumpvar.pl | shell.pl |
| exceptions.pl | stat.pl |
| fastcwd.pl | syslog.pl |

## 模块 (Perl 5.0)

Perl 5.0 采用了一种用于管理复用代码的新结构。模块的功能比 Perl 4.0 中基于包（package）的库多得多，后者仅提供了将命名空间划分为多个包的方法。

你可以通过两种主要的概念方式创建 Perl 5.0 模块。一种方法是使用子程序集合的基本概念，并增加有助于控制哪些子程序是强制性或可选的特性。另一种方法是使用 Perl 5.0 的新面向对象特性，使模块成为类的定义，以便类的实例可以隐式地调用库中的子程序（方法）。你可以结合这两种方法来生成混合模块。

面向对象的特性将“包”的概念扩展到了包含“类”的概念。子程序充当构造函数和析构函数，创建作为类成员的对象，并在最后一个对象消失时删除这些对象。其他子程序提供了将对象映射到类的方法。这样的包可以是一个简单的包，如果它提供了作为类对象方法的子程序，那么它也可以是一个类。当你使用 `@ISA` 数组时，任何包都可以从另一个包类继承方法。模块仅仅是用于处理类中对象的子程序。

解释面向对象编程的概念背景超出了本书的范畴，但在结合上下文描述标准模块时，需要提到这些概念，因为正因为这些概念，我们才使用这些特性。

## 标准模块列表

本节列出了 Perl 5.02 中的标准模块和实用模块（Pragmas）。所有这些模块都应该位于 Perl 库路径 (`@INC`) 中，应具有 `.PM` 扩展名，并包含它们自己的文档。实用模块（Pragmas）不包含子程序或类，而是作为在引用时触发的编译指令。

> 注意
> 存在许多其他模块。请参见附录 B“Perl Web Reference”获取其他非标准 Perl 模块的信息。

某些 Perl 模块是用 C 语言而不是 Perl 开发的。这些模块被称为扩展模块。由于确保这些模块在所有操作系统上正常工作存在，它们不像下表列出的标准模块那样标准化：

| 模块名称 | 描述 |
| :--- | :--- |
| AnyDBFile | 提供对外部数据库的访问 |
| AutoLoader | 按需加载子程序的特殊方式 |
| AutoSplit | 为 AutoLoader 设置模块的特殊方式 |
| Benchmark | 用于基准测试的时间代码 |
| Carp | 跨模块报告错误 |
| Config | 报告 Perl 安装时的编译器选项 |
| Cwd | 操作当前目录的函数 |
| DB_File | 提供对 Berkeley DB 文件的访问 |
| Devel::SelfStub | 允许自动加载方法的正确继承 |
| diagnostics | 启用诊断警告 |
| DynaLoader | 链接到 C 库的模块使用 |
| English | 允许使用长变量名 |
| Env | 允许访问环境变量 |
| Exporter | 模块导出子程序的标准方式 |
| ExtUtils::Liblist | 检查 C 库 |
| ExtUtils::Maker | 为扩展模块创建 make |
| ExtUtils::Manifest | 帮助维护 MANIFEST 文件 |
| ExtUtils::Miniperl | 由 ExtUtils::Maker 生成的 make 使用 |
| ExtUtils::Mbookstrap | 由 ExtUtils::Maker 生成的 make 使用 |
| Fcntl | 提供对 C fcnt.h 的访问 |
| File::Basename | 根据各种操作系统的规则解析文件名 |
| File::Check | 执行文件检查 |
| File::Find | 查找文件 |
| File::Path | 创建目录 |
| FileHandle | 提供句柄 |
| Getopt::Long | 命令行选项 |
| Getopt::Std | 标准选项 |
| I18N::Collate | 允许排序 |
| I18N::Unicode | 允许 Unicode 支持 |
| IPC::Open | 进程通信 |
| IPC::Open3 | 进程通信 |
| integer | 算术 |
| Net::Ping | 网络测试 |
| overload | 允许重载 |
| POSIX | 标准函数 |
| Safe | 安全代码 |
| SelfLoader | 自动加载方法 |
| sig | 信号处理程序 |
| Socket | Socket 访问 |
| strict | 强制严格变量 |
| Text::Abbrev | 缩写 |
| Test::Harness | 运行测试 |

```perl
filtest1("/etc/passwd");
```

以下明确要求使用 `filtest2()`：

```perl
use FilTest qw(filtest2);

filtest1("/etc/passwd");

filtest2("/etc/passwd");
```

以下代码未将子程序名称导入到当前命名空间：

```perl
use FilTest ();
```

即使使用空列表来避免导入任何名称，模块中的子程序仍然可以通过在子程序名中显式引用 `FilTest` 程序包来访问。下面的示例说明了如何直接访问这些子程序：

```perl
use FilTest ();

FilTest::filtest1("/etc/passwd");

FilTest::filtest2("/etc/passwd");
```
