
`ldapsearch` 命令的作用正如你所期望的：它从命令行查询 LDAP 目录。同样，`-x` 表示使用简单身份验证，不过在这种情况下你不需要提供任何凭据，因为你只是从目录中读取。`objectclass=*` 搜索指定返回任何 `objectclass` 的条目，因此搜索将返回目录中的所有条目。

你可以修改搜索使其更具体。例如：

```
ldapsearch -x 'cn=Ni*'
```

该命令返回所有常用名称以 Ni 开头的人员。如果你的搜索得到结果，就准备好配置客户端了。

> TIP
>
> OpenLDAP 对其文件需要特定的权限。`/var/lib/ldap` 目录应由用户 `ldap` 和组 `ldap` 所有，权限为 600。如果遇到问题，请尝试运行 `chmod 600 /var/lib/ldap`。

## Configuring Clients

虽然 Ubuntu 附带了多种邮件客户端，但这里没有足够的篇幅涵盖所有。于是，我们讨论两种最常用的客户端：默认的 Evolution 和 Thunderbird。两者都是功能强大的消息解决方案，因此都与 LDAP 配合良好。在两者中，Thunderbird 似乎更容易配置。我们过去在 Evolution 上遇到过各种问题，而在 Thunderbird 上却能第一次就成功。

### Evolution

要为 Evolution 配置 LDAP，请点击 New 按钮旁边的箭头并选择 Address Book。会出现一个新屏幕，其第一个选项提示你输入要创建的地址簿类型。选择 On LDAP Servers。

对于 Name，只需输入 Address book，对于 Server，输入你的 LDAP 服务器的 IP 地址（如果你在服务器上工作，则为 `127.0.0.1`），如图 26.1 所示。将端口保持为 389，这是 `slapd` 的默认值。切换到 Details 选项卡，并将 Search Base 设置为你的地址簿的 DN——例如 `ou=People,dc=hudzilla,dc=org`。将 Search Scope 设置为 Sub，以便 Evolution 执行全面搜索。完成后，点击 Add Address Book。

虽然 Evolution 现在已配置为使用你的目录，但它还不会立即用于电子邮件地址自动补全。要启用它，请转到 Tools 菜单并点击 Settings。从左侧出现的选项中，点击 Autocompletion 并从列表中选择你的 LDAP 服务器。点击 Close，然后创建一个新的电子邮件消息。如果一切正常，输入某人姓名的一部分应该会弹出一个包含 LDAP 匹配项的框。

![](img/e464b828c497c99e41f61d4c55f1c0db_644_0.png)

FIGURE 26.1 Configuring Evolution to use LDAP for addresses is easy for anonymous connections.

### Thunderbird

Thunderbird 的配置比 Evolution 稍微容易一些，并且通常工作得更好，特别是对于具有多个 CN 的条目。要启用自动补全，请转到 Edit 菜单，点击 Preferences，然后从顶部选项卡中选择 Composition。

在 Addressing 子选项卡中，勾选 Directory Server 复选框并点击其右侧的 Edit Directories 按钮。从出现的对话框中，点击 Add 以添加新目录。你可以随意命名，因为这只是用于显示目的。如图 26.2 所示，将 Hostname 字段设置为你的 LDAP 服务器的 IP 地址（如果你在服务器上工作，则为 `127.0.0.1`）。将 Base DN 设置为你的地址簿的 DN（例如 `ou=People,dc=hudzilla,dc=org`），并将端口号保持为 389。连续点击三次 OK 返回主界面。

现在，点击 Write 创建一封新的电子邮件消息，并在 To 框中输入用户的几个首字母。如果一切正常，Thunderbird 应该会弹出一个包含 LDAP 匹配项的框。

![](img/e464b828c497c99e41f61d4c55f1c0db_645_0.png)

FIGURE 26.2 Thunderbird's options are buried deeper than Evolution's, but it does allow you to download the LDAP directory for offline use.

## Administration

在你设置好 LDAP 服务器和客户端后，它们在外部没有变化之前几乎不需要维护。具体来说，如果目录中的某人换工作、更改电话号码、结婚（更改姓氏），离职等等，你需要能够更新目录以反映这些变化。

OpenLDAP 附带了一系列用于操作目录的工具，其中你已经见过 `ldapadd`。除此之外，你可以使用 `ldapdelete` 删除目录中的条目，以及使用 `ldapmodify` 修改条目。两者使用起来都很困难，但在其 man 手册中有适量的文档。

一个更聪明的选择是使用 `phpLDAPadmin`，这是一款 LDAP 管理工具，允许你完全通过网页浏览器添加和修改条目。你可以在 http://www.phpldapadmin.com 了解更多信息并下载产品试用。

## 参考

- <http://www.openldap.org> — OpenLDAP 项目的主页，你可以在此下载软件的最新版本并结识其他用户。
- <http://www.kingsmountain.com/ldapRoadmap.shtml> — 一组遍布互联网的优秀链接和资源，解释了 LDAP 及其父协议 X.500 的各个方面。
- <http://ldap.perl.org/> — Perl 与 LDAP 交互库的家园，提供全面的文档帮助你入门。
- <http://www.ldapguru.com/> — 全球 LDAP 管理员的巨大门户。从专门针对 LDAP 的论坛到专门为 LDAP 管理员提供的职位，该网站很可能就是你所需要的一切。

关于 LDAP 的权威书籍是 *LDAP System Administration*（O’Reilly），ISBN：1-56592-491-6。对于任何 Linux LDAP 管理员的书架来说，这绝对是必备之作。如需更一般的阅读，请尝试 *LDAP Directories Explained*（Addison-Wesley），ISBN：0-201-78792-X。它对 Microsoft Active Directory LDAP 实现的关注更强一些。

# 第四部分：编程 Linux

## 本部分内容

- 第 27 章 使用 Perl 619
- 第 28 章 使用 Python 641
- 第 29 章 编写 PHP 脚本 659
- 第 30 章 Ubuntu 的 C/C++ 编程工具 693

# 第 27 章：使用 Perl

Perl（Practical Extraction and Report Language 的缩写，或视说话对象而定为 Pathologically Eclectic Rubbish Lister），一种强大的脚本工具，使你能够管理文件、创建报表、编辑文本，并在使用 Linux 时执行许多其他任务。Perl 已包含在 Ubuntu 中，可以被视为发行版不可或缺的一部分，因为 Ubuntu 依赖 Perl 为许多类型的软件服务、日志活动和软件工具提供支持。如果你从本书光盘进行完整安装，你会发现在 `/usr/bin` 和 `/usr/sbin` 目录下安装了近 150 个用 Perl 编写的软件工具。

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

## 使用 Perl 与 Linux

尽管最初设计为数据提取和报表生成语言，但 Perl 吸引了许多 Linux 系统管理员，因为它可用于创建填补 shell 脚本和编译 C 程序能力之间空白的实用程序。Perl 相对于其他 UNIX 工具的另一个优势是它可以处理和从二进制文件中提取数据，而 `sed` 和 `awk` 则不能。

> **注意：** 在 Perl 中，“有不止一种方法可以做到”。这是 Perl 的非官方座右铭，经常被提及，通常缩写为 `TIMTOWTDI`。
