
这返回所有通用名称以 "Ni" 开头的人员。如果你得到了搜索结果，就就可以准备配置你的客户端了。

> 提示
> `OpenLDAP` 需要其文件的权限。`/var/lib/ldap` 目录应该由用户 `ldap` 和组 `ldap` 拥有，权限为 600。如果你遇到问题，请尝试运行 `chmod 600 /var/lib/ldap`。

# 配置客户端

虽然 Fedora 自带了一些电子邮件客户端，但没有足够的空间涵盖它们。我们将讨论两个最常用的客户端：默认的 `Evolution` 和 `Thunderbird`。这两者都是强大的消息传递解决方案，因此与 LDAP 配合得很好。在这两者中，`Thunderbird` 似乎更容易配置。在 `Thunderbird` 第一次运行成功的情况下，我们在 `Evolution` 上遇到过各种问题。

## Evolution

要为 `Evolution` 配置 LDAP，点击 `New` 按钮旁边的箭头并选择 `Address Book`。出现一个新屏幕，其第一个选项提示你要创建什么种类型的地址录。选择 `On LDAP Servers`。

对于 `Name`，输入 `Address book`，对于 `Server`，输入你 LDAP 服务器的 IP 地址（或者，如果你在服务器上操作），如图 24.1 所示。将端口保持为 389，这是 `slapd` 的默认值。切换到 `Details` 标签页，并将 `Search Base` 设置为你地址录的 DN——例如 `ou=People,dc=huddzilla,dc=org`。

## Thunderbird

如图 24.1 所示，Fedora 自带了一些电子邮件客户端，但没有足够的空间涵盖它们。我们将讨论两个最常用的客户端：默认的 `Evolution` 和 `Thunderbird`。这两者都是强大的消息传递解决方案，因此与 LDAP 配合得很好。在这两者中，`Thunderbird` 似乎更容易配置。在 `Thunderbird` 第一次运行成功的情况下，我们在 `Evolution` 上遇到过各种问题。

# 第五部分

# Linux 编程

本部分包含

- 第 25 章 使用 Perl 5 563
- 第 26 章 使用 Python 进行工作 579
- 第 27 章 编写 PHP 脚本 599
- 第 28 章 用于 Fedora 的 C/C++ 编程工具 629
- 第 29 章 Mono 641

# 第 25 章

# 使用 Perl

`Perl`（Practical Extraction and Report Language，或 Pathologically Eclectic Rubbish Lister，即病态怪异的杂物列表器，取决于你听谁说！）是一种强大的脚本工具，你可以在使用 Linux 时用它管理文件、创建报告、编辑文本并执行许多任务。它可以被认为是该发行版不可或缺的一部分，因为 Fedora 依赖 `Perl` 来处理许多类型的软件服务、活动记录和软件工具。如果你从本书的 DVD 进行完整安装，你会发现在 `/usr/bin` 和 `/usr/local/bin` 目录下安装了近 150 个用 `Perl` 编写的软件工具。

`Perl` 并不是最容易学习的编程语言，因为它的设计初衷是灵活性。本章将展示如何在你的系统上创建和使用 `Perl` 脚本。你将看到 程序 程序长什么样、该语言的结构，以及你可以在哪里找到预写代码的模块来帮助你编写自己的 `Perl` 脚本。

## 在 Linux 中使用 Perl

尽管 `Perl` 最初被设计为一种数据提取和报告生成语言，但它出现在许多 Linux 系统管理员面前，是因为它可以利用 shell 脚本的能力，而 shell 脚本无法弥补编译后的 C 程序之间的差距。`Perl` 相比其他 Unix 工具的另一个优势是，它可以从二进制文件中处理并提取数据，而 `sed` 和 `awk` 则不能。

> 在 `Perl` 中，“一件事有多种实现方法。”这是 `Perl` 的非官方格言，它出现的频率非常高，通常缩写为 `TIMTOWTDI`。

### 本章内容
- 在 Linux 中使用 Perl
- Perl 变量和数据结构
- 算符
- 条件语句
- 循环
- 正则表达式
- 访问 Shell
- 模块和 CPAN
- 引用

你可以在 shell 命令行中使用 `Perl` 执行单行 `Perl` 程序，但大多数情况下，程序（通常以 `.pl` 结尾）是作为命令运行的。这些程序通常工作于任何计算机操作系统平台，因为 `Perl` 已经移植到几乎每一个操作系统。安装 Fedora 时，默认就提供了 `Perl`，你可以在随书附带的 DVD 上找到你的 RPM 文件。

`Perl` 程序用于支持许多 Fedora 服务，例如系统日志。例如，`logwatch.pl` 程序每天早上 4:20 由系统上的 `cron`（调度）守护进程运行。受 `Perl` 支持的其他 Fedora 服务还包括：

- 用于本地和网络备份的 `Amanda`
- 使用 `faxxrund` 程序进行传真打印
- `Perl` 文档文件处理支持打印
- 使用 `sensors-detect` `Perl` 程序的硬件传感器监控设置

## Perl 版本

截至本文写作，`Perl` 的当前生产版本是 5.8.8（即 `Perl` 版本 5 点 8，补丁级别为 8）。你可以从 http://www.perl.com/ 下载代码并从源码编译。你偶尔会在 Fedora 的 RPM 格式中找到更新版本，可以通过更新系统来安装它们。

通过在 shell 提示符中输入 `perl -v` 来确定安装的 `Perl` 版本。如果你正在安装最新的 Fedora 发行版，你应该应该拥有最新版本的 `Perl`。

## 简单的 Perl 程序

本节介绍了一个非常简单的 `Perl` 程序，帮助你开始使用 `Perl`。尽管对于经验丰富的 `Perl` 黑客来说，简短示例不是必要的，但对于想要学习更多 `Perl` 的新用户来说是。

为了向你介绍 `Perl` 编程的绝对基础，列表 25.1 展示了一个显示消息的简单 `Perl` 程序。

列表 25.1 一个简单的 Perl 程序

```perl
#!/usr/bin/perl

print "Look at all the camels!\n";
```

输入该内容并保存为名为 `trivial.pl` 的文件。然后使用 `chmod` 命令将该文件设置为可执行（见下侧边栏），并在命令提示符运行它。

## 命令行错误

如果你收到消息 `bash: trivial.pl: command not found` 或 `bash: ./trivial.pl: Permission denied`，这意味着你要么输入了错误的命令，要么忘记使用 `chmod` 命令将 `trivial.pl` 设置为可执行：

```bash
$ chmod +x trivial.pl
```

你可以通过以下方式强制在当前目录执行命令：

```bash
$ ./trivial.pl
```

或者你可以像这样使用 `Perl` 运行程序：

```bash
$ perl trivial.pl
```

列表中的示例程序是一个两行的 `Perl` 程序。输入程序并运行它（使用 `Perl` 或将程序设为可执行）展示了如何创建你的第一个 `Perl` 程序，全球各地的 Linux 用户每天都在重复这一过程！

> `#!` 通常读作 she-bang，它是 sharp（音乐家对该字符的称呼）和 bang 的缩写，而 bang 是感叹号的另一个名称。这种符号也用于 shell 脚本。有关编写 shell 脚本的更多信息，请参考第 33 章“编写和执行 shell 脚本”。

`#` 行在技术上完全不属于 `Perl` 代码。`#` 字符表示屏幕行的其余部分是注释。注释是发给 shell 的消息，告诉它应该去哪里寻找寻找运行此程序的可执行文件。解释器会忽略注释行。

代码块（例如可能出现在循环内部）用大括号 `{}` 标识。例如，这是一个无限循环：

```perl
#!/usr/bin/perl

# a simple example to print a greeting

while (1) {
    print "hello there\n";
}
```

语句以分号 `;` 结束。一个 `Perl` 语句可以跨越多行，因为 `Perl` 不关心空格。

简单程序的第二行打印引号内的文本。`\n` 是换行的转义序列。

> 提示
> 使用 `perdoc` 和 `man` 命令是获取有关 `Perl` 信息的简单方法。要学习如何使用 `perdoc` 命令，输入：

```bash
$ perdoc
```

要获取 `Perl` 的介绍性信息，可以使用以下命令之一：

```bash
$ perdoc perl
$ man perl
```

要获取 `Perl` 文档的概述或目录，使用如下命令：

```bash
$ perdoc pertoc
```
