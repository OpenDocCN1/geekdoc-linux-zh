

一个更聪明的选择是使用 phpLDAPadmin，这是一款 LDAP 管理工具，允许你完全通过网页浏览器添加和修改条目。你可以在 http://www.phpldapadmin.com 了解更多信息并下载产品试用。

## 参考

- <http://www.openldap.org> — OpenLDAP 项目的主页，你可以在此下载软件的最新版本并结识其他用户。
- <http://www.kingsmountain.com/ldapRoadmap.shtml> — 一组遍布互联网的优秀链接和资源，解释了 LDAP 及其父协议 X.500 的各个方面。
- <http://ldap.perl.org/> — Perl 与 LDAP 交互库的家园，提供全面的文档帮助你入门。
- <http://www.ldapguru.com/> — 全球 LDAP 管理员的巨大门户。从专门针对 LDAP 的论坛到专门为 LDAP 管理员提供的职位，该网站很可能就是你所需要的一切。

关于 LDAP 的权威书籍是 *LDAP System Administration*（O’Reilly），ISBN：1-56592-491-6。对于任何 Linux LDAP 管理员的书架来说，这绝对是必备之作。如需更一般的阅读，请尝试 *LDAP Directories Explained*（Addison-Wesley），ISBN：0-201-78792-X。它对 Microsoft Active Directory LDAP 实现的关注更强一些。

## 第四部分：编程 Linux

### 本部分内容

- 第 27 章 使用 Perl 619
- 第 28 章 使用 Python 641
- 第 29 章 编写 PHP 脚本 659
- 第 30 章 Ubuntu 的 C/C++ 编程工具 693

## 第 27 章：使用 Perl

Perl（Practical Extraction and Report Language 的缩写，或视说话对象而定为 Pathologically Eclectic Rubbish Lister），一种强大的脚本工具，使你能够管理文件、创建报表、编辑文本，并在使用 Linux 时执行许多其他任务。Perl 已包含在 Ubuntu 中，可以被视为发行版不可或缺的一部分，因为 Ubuntu 依赖 Perl 为许多类型的软件服务、日志活动和软件工具提供支持。如果你从本书光盘进行完整安装，你会发现在 /usr/bin 和 /usr/sbin 目录下安装了近 150 个用 Perl 编写的软件工具。

Perl 并不是最容易学习的编程语言之一，因为它设计为灵活。本章展示如何在你的系统上创建和使用 Perl 脚本。你将看到 Perl 程序是什么样的，语言是如何结构的，以及在哪里可以找到预写代码模块来帮助你编写自己的 Perl 脚本。本章还包括几个使用 Perl 执行计算机系统上一些常见功能的示例。

### 本章内容

- 使用 Perl 与 Linux
- Perl 变量和数据结构
- 运算符
- 条件语句：if/else 和 unless
- 循环
- 正则表达式
- 访问 Shell
- 模块和 CPAN
- 代码示例
- 参考

### 使用 Perl 与 Linux

尽管最初设计为数据提取和报表生成语言，但 Perl 吸引了许多 Linux 系统管理员，因为它可用于创建填补 shell 脚本和编译 C 程序能力之间空白的实用程序。Perl 相对于其他 UNIX 工具的另一个优势是它可以处理和从二进制文件中提取数据，而 sed 和 awk 则不能。

> **注意：** 在 Perl 中，“有不止一种方法可以做到”。这是 Perl 的非官方座右铭，经常被提及，通常缩写为 TIMTOWTDI。

你可以在 shell 命令行上使用 Perl 执行单行 Perl 程序，但大多数情况下程序（通常以 .pl 结尾）作为命令运行。这些程序通常可在任何计算机平台上运行，因为 Perl 已移植到几乎所有操作系统。安装 Ubuntu 时默认提供 Perl，你可以在随书附带的 DVD 上找到其软件包文件。

Perl 程序用于支持多个 Ubuntu 服务，例如系统日志记录。例如，logwatch.pl 程序每天凌晨 4:20 由系统上的 crond（调度）守护进程运行。其他由 Perl 支持的 Ubuntu 服务包括以下内容：

- Amanda 用于本地和网络备份
- 使用 faxrunq 程序的传真排队
- 由 Perl 文档过滤程序支持的打印
- 使用 sensors-detect Perl 程序设置的硬件传感器监控

### Perl 版本

截至本文撰写时，Perl 的当前生产版本是 5.8.8（即 Perl 版本 5 点 8，补丁级别 8）。

你可以从 http://www.perl.com 下载代码并自行从源代码构建。你偶尔会在 APT 格式中找到适用于 Ubuntu 的更新版本，可以通过更新系统进行安装。参见第 7 章“管理软件”，了解如何快速获取 Ubuntu 可用更新列表。

你可以通过在 shell 提示符下输入 perl -v 来确定你安装的 Perl 版本是什么。如果你安装的是最新的 Ubuntu 发行版，你应该拥有最新版本的 Perl。

### 一个简单的 Perl 程序

本节介绍一个非常简单的示例 Perl 程序，帮助你开始使用 Perl。对于经验丰富的 Perl 黑客来说虽然微不足道，但对于想要了解更多关于 Perl 的新用户来说，一个简短的示例是必要的。

为了向你介绍 Perl 编程的绝对基础知识，清单 27.1 说明了一个简单的 Perl 程序，打印一条简短消息。

**清单 27.1：一个简单的 Perl 程序**

```
#!/usr/bin/perl
print "Look at all the camels!\n";
```

输入它并保存为名为 trivial.pl 的文件。然后使用 chmod 命令使文件可执行（参见以下边栏）并在命令提示符下运行它。

