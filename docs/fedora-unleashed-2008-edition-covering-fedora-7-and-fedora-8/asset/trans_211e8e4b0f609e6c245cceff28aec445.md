

## 配置客户端

虽然 Fedora 自带了一些电子邮件客户端，但这里没有足够的空间来涵盖所有客户端。因此，我们将讨论最常使用的两个客户端：默认的 Evolution 和 Thunderbird。两者都是功能强大的消息解决方案，并且都与 LDAP 配合良好。在这两者中，Thunderbird 似乎更容易配置。我们在某些场景下遇到过 Evolution 的问题，而 Thunderbird 却能一次性正常工作。

## Evolution

要配置 Evolution 使用 LDAP，请点击 **New**（新建）按钮旁边的箭头，并选择 Address Book（地址簿）。会出现一个新屏幕，其第一个选项会提示你选择要创建的地址簿类型。请选择 **On LDAP Servers**（在 LDAP 服务器上）。

在 Name（名称）字段中，只需输入 **Address book**（地址簿）；在 Server（服务器）字段中，输入你的 LDAP 服务器的 IP 地址（如果你是在服务器上操作，则输入 **127.0.0.1**），如图 24.1 所示。端口保持为 389，这是 LDAP 的默认值。切换到 Details（详细信息）选项卡，将 Search Base（搜索基）设置为你地址簿的 DN——例如，`ou=People,dc=hdzilla,dc=org`。将 Search Scope（搜索范围）设置为 Sub，以便 Evolution 执行全面搜索。最后，点击 Add Address Book（添加地址簿）。

![](img/34e72348d53ca54c2a1d9c871316691b_586_0.png)

> 图 24.1 配置 Evolution 以使用 LDAP 处理地址对于匿名连接来说很容易。

虽然 Evolution 现在已配置为使用你的目录，但它还不会立即将其用于电子邮件地址的自动补全。要启用此功能，请转到 Tools（工具）菜单并点击 Settings（设置）。在左侧出现的选项中，点击 Autocompletion（自动补全），并从列表中选择你的 LDAP 服务器。点击 Close（关闭），然后创建一个新的电子邮件消息。如果一切正常，输入某人姓名的一部分应该会自动弹出一个包含 LDAP 匹配结果的框。

## Thunderbird

Thunderbird 比 Evolution 稍微容易配置一些，并且通常运行得更好，特别是对于具有多个 CN 的条目。要启用自动补全，请转到 Tools（工具）菜单，点击 Options（选项），然后在左侧选项卡中选择 Composition（撰写）。

勾选 Directory Server（目录服务器）复选框，并点击其右侧的 Edit Directories（编辑目录）按钮。在出现的对话框中，点击 Add（添加）以添加新目录。你可以给它任何名称，因为这仅用于显示目的。如图 24.2 所示，将 Hostname（主机名）字段设置为你 LDAP 服务器的 IP 地址（如果你是在服务器上操作，则为 127.0.0.1）。将 Base DN（基础 DN）设置为你地址簿的 DN（例如，`ou=People,dc=duzilla,dc=org`），并将端口号保持为 389。点击 OK（确定）三次以返回主界面。

![](img/34e72348d53ca54c2a1d9c871316691b_587_0.png)

现在，点击 Write（撰写）创建新的电子邮件消息，并在 To（收件人）框中输入用户的前几个字母。如果一切正常，Thunderbird 应该会弹出一个包含 LDAP 匹配结果的框。

## 管理

在 LDAP 服务器和客户端设置好之后，除非外部情况发生变化，否则它们需要很少的维护。具体来说，如果你目录中的某人换了工作、改了电话号码、结婚（改了姓氏）、辞职或类似情况，你需要能够更新目录以反映这些变化。

OpenLDAP 附带了一组用于操作目录的工具，你已经认识了其中的 ldapadd。除此之外，你可以使用 ldapdelete 删除目录中的条目，使用 ldapmodify 修改条目。这两个工具都很难使用，但它们的 man 手册页提供了中等程度的文档说明。

一个更智能的选择是使用 phpLDAPadmin，这是一个 GPL 许可的 LDAP 管理工具，允许你完全通过 Web 浏览器来添加和修改条目。你可以了解更多并在 [http://www.phpldapadmin.com/](http://www.phpldapadmin.com/) 下载该产品进行尝试。

## 参考

- [http://www.openldap.org/](http://www.openldap.org/) — OpenLDAP 项目的主页，你可以在这里下载最新版本的软件并结识其他用户。
- [http://www.ingsmountain.com/ldapRoadmap.shtml](http://www.ingsmountain.com/ldapRoadmap.shtml) — 一组来自互联网各处的优秀链接和资源，解释了 LDAP 及其父协议 X500 的各个方面。
- [http://ldap.perl.org/](http://ldap.perl.org/) — 用于与 LDAP 交互的 Perl 库的主页，提供全面的文档帮助你入门。
- [http://www.ldapguru.com/](http://www.ldapguru.com/) — 面向全球 LDAP 管理员的大型门户。从专注于 LDAP 的论坛到专门针对 LDAP 管理员的工作机会，这个网站很可能就是你所需的一切。
- 关于 LDAP 的权威书籍是 *LDAP System Administration*（O'Reilly 出版），ISBN: 1-56592-491-6。它是任何 Linux LDAP 管理员书架上必不可少的读物。
- 对于更一般的阅读，可以尝试 *LDAP Directories Explained*（Addison-Wesley 出版），ISBN: 0-201-78792-X。不过，该书更侧重于 Microsoft 的 Active Directory LDAP 实现。

## 第五部分

## Linux 编程

- 第 25 章 使用 Perl 563
- 第 26 章 使用 Python 579
- 第 27 章 编写 PHP 脚本 599
- 第 28 章 Fedora 的 C/C++ 编程工具 629
- 第 29 章 Mono 641

## 第 25 章

## 使用 Perl

### 本章内容

- 在 Linux 中使用 Perl
- Perl 变量和数据结构
- 运算符
- 条件语句
- 循环
- 正则表达式
- 访问 Shell
- 模块和 CPAN
- 参考

Perl（Practical Extraction and Report Language 或 Pathologically Ecclectic Rubbish Lister，取决于你问谁！）是一个强大的脚本工具，你可以在使用 Linux 时用它来管理文件、创建报告、编辑文本以及执行许多其他任务。Perl 包含在 Fedora 中，可以被视为该发行版的重要组成部分，因为 Fedora 在许多类型的软件服务、日志活动和软件工具中依赖于 Perl。如果你从本书的 DVD 进行完整安装，你会发现几乎 150 个用 Perl 编写的软件工具安装在 /usr/bin 和 /usr/sbin 目录下。

Perl 并不是最容易学习的编程语言之一，因为它的设计旨在灵活性。本章展示了如何在你的系统上创建和使用 Perl 脚本。你将看到 Perl 程序长什么样子、语言的结构如何，以及在哪里可以找到预写代码的模块来帮助你自己编写 Perl 脚本。

### 在 Linux 中使用 Perl

虽然 Perl 最初被设计为数据提取和报告生成语言，但它吸引了许多 Linux 系统管理员，因为它可用于创建实用工具，填补 shell 脚本功能和编译后的 C 程序之间的空白。Perl 相对于其他 Unix 工具的另一个优势是它可以处理和从二进制文件中提取数据，而 sed 和 awk 做不到。

> **注意**
>
> 在 Perl 中，“完成一件事永远不止一种方法。”这是 Perl 的非官方座右铭，它经常出现，通常缩写为 TIMTOWTDI。

你可以在 shell 命令行上使用 Perl 来执行单行 Perl 程序，但通常程序（通常以 .pl 结尾）作为命令运行。这些程序通常可以在任何计算机平台上工作，因为 Perl 已被移植到几乎所有操作系统。安装 Fedora 时默认提供 Perl，你可以在随本书提供的 DVD 上找到其 RPM 文件。

Perl 程序用于支持许多 Fedora 服务，例如系统日志记录。例如，logwatch.pl 程序每天早晨 4:20 由你系统上的 crond（调度）守护进程运行。其他由 Perl 支持的 Fedora 服务包括：

- 用于本地和网络备份的 Amanda
- 使用 faxrunq 程序的传真排队
- 由 Perl 文档过滤程序支持的打印
- 使用 sensors -detect Perl 程序的硬件传感器监控设置

### Perl 版本

截至撰写本文时，当前的生产版本 Perl 是 5.8.8（即 Perl 版本 5.8，补丁级别 8）。你可以从 http://www.perl.com/ 下载代码并从源代码自行构建。你偶尔会在 Fedora 中找到更新版本的 RPM 格式 Perl，你可以通过更新系统来安装它们。

你可以通过在 shell 提示符下输入 `perl -v` 来确定你安装的 Perl 版本。如果你正在安装最新的 Fedora 发行版，你应该拥有最新版本的 Perl。

### 一个简单的 Perl 程序

本节介绍一个简单的示例 Perl 程序，帮助你开始使用 Perl。虽然对于经验丰富的 Perl 黑客来说这很微不足道，但对于希望了解更多关于 Perl 的新用户来说，一个简短的示例是必要的。

为了向你介绍 Perl 编程的绝对基础知识，代码清单 25.1 说明了一个打印简短消息的简单 Perl 程序。

```
LISTING 25.1     一个简单的 Perl 程序

#!/usr/bin/perl
print 'Look at all the camels!\n';
```

将其输入并保存到一个名为 trivial.pl 的文件中。然后使用 chmod 命令使该文件可执行（参见以下侧栏），并在命令提示符下运行它。

