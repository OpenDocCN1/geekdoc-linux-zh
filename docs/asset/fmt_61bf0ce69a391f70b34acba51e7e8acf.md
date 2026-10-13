
`echo "Failed to create backup copy"`

`fi`

```
```

此脚本说明了 `if-then-else` 结构的语法，并展示了 `cp` 命令的退出状态如何被 `if` 结构用于决定后续操作。如果 `cp` 脚本调用 `vi` 编辑文件；否则脚本显示消息并退出。

不要忘记结束 `if` 结构的 `fi`。忘记 `fi` 是 Bash 脚本中常见的错误源。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_264_0.png)

在 Bash 脚本中，控制结构——如 `if`、`case`、`for` 和 `while`——取决于命令的退出状态以决定下一步做什么。当任何命令执行时，它会返回一个退出状态，这是一个指示命令是否成功的数值。按照惯例，退出状态为零表示命令执行成功。（是的，你读没错：零表示成功。）非零退出状态表示命令执行出现问题。

你可能会如下方式一个脚本，在用 `vi` 编辑器打开文件之前先创建文件的备份副本：

```
#!/bin/sh

if cp "$1" "$1"

then

  vi "$1"

else

  echo "Failed to create backup copy"

fi
```

此脚本说明了 `if-then-else` 结构的语法，并展示了 `cp` 命令的退出状态如何被 `if` 结构用于决定后续操作。如果 `cp` 脚本调用 `vi` 编辑文件；否则脚本显示消息并退出。

不要忘记结束 `if` 结构的 `fi`。忘记 `fi` 是 Bash 脚本中常见的错误源。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_264_0.png)

在 Bash 脚本中，控制结构——如 `if`、`case`、`for` 和 `while`——取决于命令的退出状态以决定下一步做什么。当任何命令执行时，它会返回一个退出状态，这是一个指示命令是否成功的数值。按照惯例，退出状态为零表示执行成功。（是的，你读没错：零表示成功。）非零退出状态表示命令执行出现问题。

在 Bash 中，`test` 命令告诉你文件是否存在或是否可读。使用这种表示法，你编写脚本如下：

```
#!/bin/sh

if [ -f "$1" ]

then

    vi "$1"

else

    echo "No such file"

fi
```

另一个常见的控制结构是 `for` 循环。以下脚本列出了从一到十的数字：

```
#!/bin/sh

sum=0

for i in 1 2 3 4 5 6 7 8 9 10

do

    sum=`expr $sum + $i`

done

echo "Sum = $sum"
```

# Bash 中的内置函数

Bash 有几十个内置函数，包括 `cd` 和 `pwd`。本章没有足够的空间涵盖内置函数，但你可以通过 `man bash` 从在线手册中获取更多信息。

# 第 6 章：Linux 命令的秘密 237

# Perl 脚本语言

官方上 Perl 代表 Practical Extraction Language（实用提取语言）。Perl 由 Larry Wall 创建，用于从文本文件中提取信息并使用这些信息准备报告。用 Perl 语言编写的程序由 `perl` 解释并执行。这本书的配套光盘包含了 `perl`；它应该安装在系统的 `/usr/bin` 目录下。Perl 可用于多种计算机系统，如 Linux。

## 我有 Perl 吗？

在继续 Perl 教程之前，检查你的系统是否安装了它。输入以下命令：

```
which perl
```

该命令告诉你会在 `PATH` 环境变量列出的目录中找到指定的程序。如果安装了 `perl`，你应该看到以下输出：

```
/usr/bin/perl
```

如果 `which` 命令抱怨在当前 `PATH` 中找不到该程序，这并不意味着你没有安装 `perl`。你可能没有将 `/usr/bin` 目录加入 `PATH`。检查确保 `/usr/bin` 在

# 第二部分：运行 Linux

在 `PATH` 中：可以输入 `echo $PATH` 或查看由 `which` 命令显示的消息（此消息包含 `PATH` 中的目录）。如果 `/usr/bin` 不在 `PATH` 中，使用以下命令重新定义 `PATH`：

```
PATH=$PATH:/usr/bin; export PATH
```

现在再次尝试 `perl` 命令。如果你仍然遇到错误，你可能没有安装 Perl。你可以按照以下步骤从随附的 CD-ROM 安装 Perl：

- 1. 以 root 身份登录。
- 2. 将随附的 CD-ROM 插入光驱驱动器，并使用以下命令挂载 CD-ROM：

```
mount /dev/hdc /cdrom 替换为你的 CD-ROM 器的设备名称。
```

- 3. 输入以下命令切换目录到 Red Hat 软件包所在的路径：

```
cd /mnt/cdrom/RedHat/RPMS
```

- 4. 输入以下 `rpm`（Red Hat 软件包管理器）命令安装 Perl：

```
rpm -i perl*
```

如果你的系统中已安装了 `perl`，输入以下命令获取其版本号：

```
perl -v
```

以下是该命令的典型输出：

```
This is perl. version 5.004_01
```

```
Copyright 1987-1997. Larry Wall
```

Perl 仅可以根据艺术许可（Artistic License）或 GNU 通用许可证（GNU General Public License）的条款复制，这些许可可以在 Perl 4.0 源代码中找到。

此输出告诉你你拥有 Perl 版本 5.004，补丁级别为 01，并且 Perl 的创始人 Larry Wall 拥有版权。Perl 一直通过 GNU 通用许可证自由分发。

随附的 CD-ROM 包含 5.004_01 Perl。你可以通过将浏览器指向全面的 Perl 存档网络（CPAN）来获取最新版本的 Perl。以下地址将你连接到附近的 CPAN 站点：

```
http://www.perl.com/CPAN/
```

## 你的第一个 Perl 脚本

Perl 有许多 C 的特性，正如你所知，大多数关于 C 的书籍都以一个在终端显示 Hello, World! 的示例程序开始。因为 Perl 是一种解释语言，你可以直接从命令行完成此任务。如果你输入：

```
perl -e 'print "Hello. World!\n';
```

系统响应为：

```
Hello, World!
```

该命令使用 `perl` 程序的 `-e` 选项将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，下面这一行构成了 Perl 程序：

```
print "Hello. World!\n";
```

要将此行转换为脚本，你必须将该行放在文件中，并以一个运行 `perl` 程序的指令开头（正如你在 shell 脚本中所做的那样，你将如 `#!/bin/sh` 的行放在 Bourne shell 脚本开头以处理脚本）。

要尝试 Perl 脚本，请遵循以下步骤：

- 1. 使用文本编辑器（如 `vi` 或 `emacs`）将以下行保存到名为 `hello` 的文件中：
  `#!/usr/bin/perl`
  `# This is a comment.`
  `print "Hello. World!\n";`
- 2. 使用以下命令使 `hello` 文件具有可执行权限：
  `chmod +x hello`
- 3. 在 shell 提示符处输入以下内容来运行 Perl 脚本：
  `hello`
  `Hello, World!`

就这样！你刚刚编写并尝试了你的第一个 Perl 脚本。

> 注意，Perl 脚本的第一行以 `#!` 开头，后面跟着 `perl` 程序的完整路径。如果脚本的第一行以 `#!` 开头，shell 会剥离 `!`，在末尾附加脚本名称并运行脚本。因此，如果脚本文件名为 `hello` 且第一行是 `#!/usr/bin/perl`，shell 将执行以下命令：

```
/usr/bin/perl hello
```
