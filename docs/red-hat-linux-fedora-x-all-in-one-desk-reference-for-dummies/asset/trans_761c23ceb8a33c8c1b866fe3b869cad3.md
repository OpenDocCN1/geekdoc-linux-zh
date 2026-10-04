

# 确定你是否安装 Perl 5.8

现在，再次尝试 perl 命令。如果你仍然遇到错误，说明你可能没有安装 Perl。你可以通过以下步骤从随附 DVD-ROM 安装 Perl：

- 以 root 身份登录。
- 将随附 DVD-ROM 插入 DVD-ROM 驱动器。如果你在 GNOME 或 KDE 图形环境中工作，DVD-ROM 会自动挂载。否则，请输入以下命令挂载 DVD-ROM：
mount /mnt/cdrom

```
mount /mnt/cdrom
```

- 输入以下命令切换目录到 Red Hat 软件包所在的位置：cd /mnt/cdrom/Fedora/RPMS

```
cd /mnt/cdrom/Fedora/RPMS
```

- 输入以下 rpm（Red Hat 软件包管理器）命令安装 Perl：
-ivh perl*

```
rpm -ivh perl*
```

在系统上安装好 Perl 后，运行以下命令查看其版本号：

```
perl -v
```

以下是该命令的典型输出：

This is perl, v5.8.3 built for i386-linux-thread-multi

Copyright 1987-2003, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, can be found on this system using 'man perl' or 'perldoc perl'. If you have access to the Internet, point your browser at http://www.perl.com/. the Perl Home Page.

这告诉你你拥有 Perl 版本 5.8，补丁级别 3，并且 Perl 的创始人 Larry Wall 拥有版权（请注意，Perl 是在通用公共许可证下免费分发的）。

你可以通过将万维网浏览器指向全面 Perl 存档网络 (CPAN) 获取最新版本的 Perl。以下地址将你连接到离你最近的 CPAN 站点：

![](img/d9230b719dc0efd80851f363d8c6f571_807_0.png)

```
www.perl.com/CPAN/
```

# 编写你的第一个 Perl 脚本

Perl 具有许多 C 的特性。正如你可能知道的，大多数关于 C 的书籍都以一个在终端上显示 Hello, World! 的示例程序开始。Perl 是一种解释型语言，你可以直接从命令行完成此任务。如果你输入

```
perl -e 'print "Hello, World!\n";
```

Perl 的响应如下：

Hello, World!

该命令使用 perl 程序的 -e 选项，将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，下面的一行构成了 Perl 程序：

print "Hello, World!\n"

将此行转换为 Perl 脚本

（注：原文此处可能存在断句，根据上下文意为“为了将此行转换为 Perl 脚本”）

要尝试此 Perl 脚本，请遵循以下步骤：

- 1. 使用文本编辑器在名为 hello.pl 的文件中输入并保存以下几行：
   #!/usr/bin/perl
   # This is a comment.
   print "Hello, World!\n"
- 2. 使用以下命令使 hello.pl 文件具有执行权限：
   chmod +x hello.pl
- 3. 在 shell 提示符处输入以下内容运行 Perl 脚本：
   ./hello.pl
它显示了以下输出：
   Hello, World!

太棒了！你编写并尝试了你的第一个 Perl 脚本。

注意 Perl 脚本的第一行以 #! 开头，后跟 perl perl 程序的路径。如果脚本的第一行以 #! 开头，shell 会简单地剥离 #!，将脚本文件名添加到末尾并运行脚本。因此，如果脚本文件名为 hello.pl 且第一行是 #!/usr/bin/perl，shell 将执行以下命令：

![](img/d9230b719dc0efd80851f363d8c6f571_808_0.png)

# 获取 Perl 概述

```
 /usr/bin/perl hello.pl
```

大多数编程语言（包括 Perl）都有一些共同特性：

- **变量（Variables）**存储不同类型的数据。你可以将每个变量视为数据的占位符——类似于一个邮箱箱，有一个名称和存储数据的空间。变量的内容是它的值。
- **表达式（Expressions）**使用操作符组合变量。一个表达式可能会相加几个变量；另一个可能会提取字符串的某部分。
- **语句（Statements）**执行某些操作，例如为变量赋值或打印字符串。
- **流程控制语句（Flow-control statements）**允许语句根据某些表达式的值以不同的顺序执行。通常，有 for-do、while 和 if-then-else 语句。
- **函数（Functions）**（也称为子程序或例）允许你将多个语句分组并给它们起一个名称。使用此功能，你可以通过调用代表这些语句的函数来执行相同的语句集。通常用于 for-
- **包和模块（Packages and modules）**允许你将多个语句分组并给它们起一个名称。使用此功能，你可以通过调用代表这些语句的函数来执行相同的语句集。通常用于 for-
- **关联数组（Associative arrays）**是键值对。每个变量都有一个名称。使用此功能，你可以通过调用代表这些语句的函数来执行相同的语句集。通常用于 for-

基础语法

在 Perl 中，脚本是语句的集合。每个语句必须以分号 (;) 结束。文件末尾不需要分号。以下是常见的 Perl 关键字：

- if-else: 条件语句
- while, for: 循环语句
- sub: 定义函数
- print: 输出文本到屏幕
- return: 从函数返回值
- my: 声明局部变量
- global: 声明全局变量
- array: 有序列表
- hash: 关联数组
- string: 字符串
- integer: 整数
- boolean: 布尔（真或假）
- float: 浮点数

标可以存储单个值，例如数字或文本。每个变量以美元符号 ($开头。你甚至可以在不初始化的情况下使用变量；数字的默认值为零，字符串的默认值为空。如果你想查看标是否定义，使用 defined 函数：

```
print "Name undefined!\n" if !(defined $name);
```

如果 $name 已定义，表达式 (defined $name) 为 1。你可以通过 undef 函数“取消”变量，例如：

```
undef $name;
```

# 获取 Perl 概述

变量根据上下文求值。以下是一个初始化并打印几个变量的脚本：

```
#!/usr/bin/perl
$title = "Fedora Core All-One Reference";
$count1 = 650;
$count2 = 238;
```

$total = $count1 + $count2;

```
print "Title: $title -- $total\n";
```

当你运行上述 Perl 程序时，它产生以下输出：

Title: Fedora Core All-One Reference -- 888 pages

正如 Perl 语句所示，当两个数值值相加时，使用的是数值值；但当打印 $total 变量时，它的表示显示出Perl 的另一个有趣方面是它会评估双引号 ("") 中的变量。然而，如果你在单引号 ('...') 内写一个字符串，Perl 会原样保留它。如果你写成

```
print "Title: $title -- $total\n";
```

在双引号内包含引号，且不换行。

一个有用的变量是 $_（美元符号后跟划线字符）。这个特殊变量被称为默认参数。Perl 解释器根据上下文确定 $_ 的值。当 Perl 解释器从标准输入读取输入时，$ 持有当前输入行；当解释器搜索特定的文本模式时，$ 持有默认搜索模式。

数组

在 Perl 中，数组是标量的集合。数组名称以 @ 符号开头。与 C 语言一样，数组下标从 0 开始。你可以使用索引访问数组元素。Perl 动态分配数组空间。

