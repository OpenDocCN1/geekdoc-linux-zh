
在 `/var/lib/news` 目录中还有 INN history 文件。这些文件用于保持每个已发布到每个新闻组的文章的运行索引。保持这些文件不被篡改至关重要，因为如果它们与实际的新闻组文章不同步，新闻服务器在检索文章时就会出现问题。

history 文件有两个独立的部分：文本 history 文件和一组通过使用诸如常见的 Berkeley db 包之类的数据库程序创建的二进制索引文件。在启动 `innd` 守护程序之前，您必须创建这两组文件。

您使用 `/var/lib/news/bin/makehistory` 命令根据服务器上当前的新闻组文章（应该没有文章）创建文本 history 文件。Fedora Core 提供了一个空白的 history 文件。

创建文本 history 文件后，您创建二进制索引文件。您使用 `/usr/lib/news/bin/makedbz` 程序将文本 history 文件转换为二进制索引文件。`makedbz -i` 命令创建以下三个独立的二进制文件：

- `history.n.dir`
- `history.n.index`
- `history.n.hash`

您应该将这些文件重命名为标准的 history 文件名（`history.dir`、`history.index` 和 `history.pag`），以便 `innd` 程序能够识别它们。在 history 文件创建后，您终于可以启动新闻服务器了。

## 运行 innd

使用 `/var/lib/news/bin/inndstart` 程序是启动 `innd` 守护程序的最佳方式，进而启动其他 INN 包程序。必须从 news 用户 ID 运行 `inndstart` 程序。它在后台模式下启动 `innd` 程序以及 `controchan` 程序。

`innd` 程序在 NNTP TCP 端口上监听新闻源和新闻阅读器请求。如果远程新闻阅读器建立了连接，`innd` 程序会派生 active

用于对远程连接进行身份验证并处理新闻阅读器请求的程序。如果接收到的文章是控制文章，它们会被传递给 `controlchan` 程序进行处理。

Fedora Core 已精心配置了启动新闻服务器所需的 SystemV 文件；你可以以适当方式使用 `chkconfig`、`ntsysv`、`service` 或 `system-config-services` 来启动服务器。（有关详细信息，请参阅第 14 章“自动执行任务”。）以下是一个示例：

```
# /sbin/service inn start
```

当 `innd` 程序正在运行时，你可以使用 `ctlinnd` 程序来控制它，其语法如下：

```
ctlinnd [ -h ] [ -s ] [ -t timeout ] command [ argument...] 
```

`-s` 选项会抑制 `ctlinnd` 命令的任何输出。此选项通常用于批处理程序中。`-t` 选项指定等待服务器响应的时间长度（以秒为单位）。如果你通过慢速链路连接到服务器，或者连接到一个慢速服务器，你可以增加 `timeout` 的值。

命令参数定义了 `ctlinnd` 程序应对 `innd` 新闻服务器执行的操作。`-h` 选项会打印出所有可用于 `ctlinnd` 的命令参数摘要。目前，你可以使用 `newgroup` 命令创建一个新的本地新闻组，供新闻阅读器用于读取和发送消息：

```
$ ctlinnd newgroup local.linux.group y hoyt@maximumhoyt.com
```

`newgroup` 命令使用三个参数：

- 新新闻组的名称
- 用于定义要创建的新闻组类型的标志（`y` 代表常规开放组，`m` 代表受审核组）
- 新新闻组维护者的电子邮件地址

`ctlinnd` 程序应从 news 用户 ID 运行。如果命令成功，它将返回一个简单的 OK 消息。你可以使用 `ctlinnd` 命令检查新的新闻组是否已添加到新闻服务器中。

## 使用 cleanfeed 包过滤垃圾邮件

困扰 Usenet 新闻组系统的一个问题是垃圾 Usenet 消息的泛滥。垃圾邮件提供商通常试图将他们的消息发布到新闻组，以向大量被动受众强制推送消息。阻止垃圾邮件消息被发布到新闻组的最有效方法之一是使用 `cleanfeed` 包。`cleanfeed` 包是一个 Perl 脚本，在垃圾邮件到达你的新闻服务器之前将其过滤掉。你可以通过编辑 `/etc/news` 目录下的配置文件 `cleanfeed.conf` 来配置此软件。

本章中提供的新新闻组示例是专为封闭系统设计的，不需要过滤垃圾邮件。但你可以在 `http://www.exit109.com/~jeremy/news/cleanfeed/` 找到的常见问题解答（FAQ）中进一步了解 `cleanfeed`。

## 相关的 Fedora Core Linux 命令

你可以使用以下命令在 Fedora Core Linux 中管理新闻组和其他协作通信过程：

- `emacs`——首选的编辑环境，也可用于阅读 Usenet 新闻
- `innd`——INN 守护程序及其大量的相关命令
- `knode`——KDE 的图形化 Usenet 新闻阅读客户端
- `mozilla`——开源 Mozilla 浏览器的邮件和新闻组组件
- `pan`——一款易于使用的 GNOME 版 Usenet 新闻阅读器
- `pine`——一款基于文本的邮件客户端，也可阅读 Usenet 新闻
- `slrn`——一款基于文本的图形化 Usenet 新闻阅读器

## 参考

- [http://www.faqs.org/rfcs/rfc977.html](http://www.faqs.org/rfcs/rfc977.html)—RFC 977，即 NNTP 协议
- [http://www.faqs.org/rfcs/rfc1036.html](http://www.faqs.org/rfcs/rfc1036.html)—RFC 1036，即新闻消息的格式
- [http://www.list.org/](http://www.list.org/)—Mailman 邮件列表管理器的主页

# 第五部分

编程 Linux

# 本部分内容

| 章节 | 标题 | 页码 |
| :--- | :--- | :--- |
| 第 29 章 | 使用 Perl | 775 |
| 第 30 章 | 使用 Python 进行开发 | 801 |
| 第 31 章 | 编写 PHP 脚本 | 821 |
| 第 32 章 | Fedora 的 C/C++ 编程工具 | 865 |

# 第 29 章

# 使用 Perl

Perl（实用抽取和报告语言）是一种强大的脚本工具，你可以使用它来管理文件、创建报告、编辑文本，并在 Linux 中执行许多其他任务。Fedora 包含 Perl，并且可以将其视为发行版的组成部分，因为 Fedora 依赖于 Perl 来提供多种类型的软件服务、记录活动和软件工具。如果你从本书的 CD-ROM 进行完整安装，你会发现在 `/usr/bin` 和 `/usr/sbin` 目录下安装了近 150 个用 Perl 编写的软件工具。

随着 20 世纪 90 年代初万维网的诞生，Perl 迅速成为公共网关接口（CGI）编程的首选语言，CGI 用于扩展网站功能，使 Web 不仅仅是一个文档发布资源。随着最近开源运动的兴起，Perl 获得的媒体关注度几乎与 Linux 相当，尽管许多经验丰富的 Linux 用户使用 Perl 已经有很长一段时间了。

由于 Perl 是为灵活性而设计的，它可能不是最容易学习的编程语言。本章展示了如何在你的系统上创建和使用 Perl 脚本。你将看到 Perl 程序的样子，该语言的结构，在哪里可以找到预写的代码模块来帮助你编写自己的 Perl 脚本，以及几个使用 Perl 执行计算机系统中一些常见功能的示例。

本章还包括关于 Perl 的额外信息源；请参阅本章末尾的网站、书籍和在线期刊列表。成为 Perl 黑客的追求不必漫长而艰辛，但你将从 Perl 开发者社区其他成员提供的慷慨帮助中获益。Perl 在 Linux 系统上运行快速且高效，但学习如何编写良好的 Perl 程序需要付出一些努力。

## 本章内容

- 在 Linux 中使用 Perl
- Perl 变量和数据结构
- 运算符
- 条件语句：`if/else` 和 `unless`
- 循环
- 正则表达式
- 访问 Shell
- 开关
- 模块和 CPAN
- 代码示例
- 参考

## 在 Linux 中使用 Perl
