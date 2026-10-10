
安装工具、支持和文档。实际的邮件服务器软件本身是相同的。

## SMT 与 POP

SMT 不是 POP。POP 也不是 SMT。既然我们把这一点弄清楚了，让我们澄清一下这一切的含义：

- SMT 是仅用于发送消息的传输协议。用户无法连接到 SMT 服务器来读取他们的邮件。
- 邮局协议（POP）则正好相反。客户端可以使用 POP 从 POP 服务器上读取邮件，但客户端主机不能使用 POP 服务器来发送电子邮件。有关 POP 的更多信息，请参见第 16 章。

经常让一些人感到困惑的是，运行 SMT 服务器软件的机器与运行 POP 服务器软件的机器可以是同一台机器。这是因为 SMT 使用端口 25 接受连接，而 POP（具体来说是版本 3）在端口 110 接受连接。

## 推荐读物

Sendmail 最大的特性之一也是其最大的问题：可配置性。（有人甚至可能认为整个基于 UNIX 的操作系统也是如此。）显然，我们无法在本章中涵盖关于 Sendmail 的一切；相反，我们为您提供设置最常见配置所需的信息，并希望能提供足够的基础知识，使您能够有信心去探索更复杂的设计。

如果您决定接受深入了解 Sendmail 的挑战，不妨看看那本真正权威的著作：《*Sendmail, Second Edition*》（O'Reilly & Associates，1997 年）。这本书由 Sendmail 的主要开发者 Eric Allman 合著。这本书的缺点在于它非常巨大——超过 1100 页。这不是一本入门读物！然而，如果您在任何时候在互联网讨论论坛上发布关于 Sendmail 的问题，请做好心理准备，至少会有一个人告诉您去买这本书。（由于封面上有一只老鼠的图片，这本书也被戏称为“老鼠书”。）

您的书架上可能还有另外一两本关于系统管理的书籍——否则我就太天真了——这些书也涵盖了 Sendmail。您可能发现我涵盖的内容与它们之间有一个区别：我不会详细介绍 sendmail.cf 配置文件中所有命令的细节。这是因为大多数配置选项都可以通过使用随 Sendmail 提供的配置宏来完成。宏不仅对您更友好，也更容易让您的继任者了解您对系统做了什么，而不必担心他们的升级会破坏您所做的某些细微（未文档化）的调整。如果您确实决定深入研究 sendmail.cf 文件的格式，请务必明白，仅仅几页内容是不足以让您完全掌握并正确处理的。

认真研究与配置文件中定义的规则集。**一如既往，请运用良好的系统管理员常识，并在进行更改之前备份任何文件。**

## 查找和安装 SENDMAIL

大多数 Linux 发行版都预装并预配置了 Sendmail，用于简单的服务器配置。虽然这意味着您在初始部署时不需要处理安装 Sendmail 的问题，但这并不意味着您永远不需要升级！本节将介绍下载干净版本的 Sendmail 源代码、编译它并将其安装的过程。

### 下载 Sendmail

查找 Sendmail 的最佳地点是其主站点 http://www.sendmail.org 或列在该网页上的镜像站点之一。截至本文撰写时，Sendmail 的最新版本为 8.9.3。我们将以下载和编译它为例进行说明。

Sendmail 网站实际上是一个相当令人印象深刻的有用信息集合，涉及 Sendmail 的各个方面。您将找到 Sendmail 常见问题解答、指向有用电子文档的指针，以及当然，指向该软件商业版本的链接，位于 http://www.sendmail.com。我强烈建议您阅读一遍常见问题解答，即使您并不理解所有内容，或者甚至还没有需要回答的问题。这样，当您确实遇到一个问题时，您将对可以在网站上找到什么帮助有更好的了解。

Sendmail 的最新版本可以在 ftp://ftp.sendmail.org/pub/sendmail 找到。包含 Sendmail 8.9.3 的文件是 ftp://ftp.sendmail.org/pub/sendmail/sendmail.8.9.3.tar.gz。

与我们下载的其他软件包类似，您应该将其下载到一个有足够空间进行解包和编译的目录中。/usr/local 目录通常很适合这样做。在此示例中，我们假设我们在这个目录下工作。

解压源代码归档的命令是

```bash
[root@ford src]# tar -xfz sendmail.8.9.3.tar.gz
```

这将创建目录 /usr/local/src/sendmail-8.9.3 以包含所有源代码。

### 编译 Sendmail

Sendmail 的开发者在使 Sendmail 尽可能容易编译方面做得非常出色，尤其考虑到 Sendmail 支持的平台数量。要开始这个过程，请确保您位于 /usr/local/src/sendmail-8.9.3/src 目录中。在那里，输入

```bash
[root@ford src]# ./Build
```

这将生成 Sendmail 二进制文件及相应的手册页。

此时，安装新版本 Sendmail 的工作已完成约 25%。剩下的过程要求我们构建一个配置文件，这个过程并没有我们希望的那么直观。但优点仍然大于缺点，这解释了 Sendmail 的持续成功。

### 周边程序

Sendmail 附带几个小型程序，有助于管理系统或在其内置功能之上提供额外的安全功能。在本节中，我们将逐步了解理解、编译和安装这些程序的过程。

**MAILSTATS** Sendmail 可以维护其性能和吞吐量统计信息。为了以人类可读的形式呈现这些信息，您需要使用 mailstats。该程序随 Sendmail 源代码树提供，位于 *mailstats* 子目录中。要编译和安装此程序，进入 *mailstats* 目录并输入

```bash
[root@ford mailstats]# ./Build; ./Build install
```

**MAKENAP** 为了提高性能，Sendmail 将其许多表保存在数据库格式中。这当然需要有一个工具将这些表（由我们使用文本编辑器创建）转换为数据库格式。Makenap 就是那个工具。它随 Sendmail 源代码树提供，位于 *makenap* 子目录中。要编译和安装此程序，进入 *makenap* 目录并输入

```bash
[root@ford makenap]# ./Build; ./Build install
```

**PRALIASES** Sendmail 别名文件允许您为用户创建替代电子邮件地址，等等。（请参见本章后面关于 `/etc/aliases` 的部分。）虽然我找不到这个工具任何真正好的用途，特别是因为别名文件是以人类可读格式保存的，但确实可以不使用 praliases 来转储别名文件。praliases 程序包含在 Sendmail 源代码分发中，位于 *praliases* 子目录中。要编译和安装它，进入 *praliases* 目录并输入

```bash
[root@ford praliases]# ./Build; ./Build install
```

**SMRSH** smrsh 工具（以及 Sendmail 中相应的功能）是帮助保护 Sendmail 的好方法。它本质上限制了 Sendmail，使其只能运行放置在特殊目录中的程序。如果程序不在那里，它就不能被运行。这防止了外部人员试图向 Sendmail 发送虚假信息以执行恶意操作。强烈建议您编译、安装并配置该功能以在 Sendmail 中使用。

要编译和安装它，进入 *smrsh* 目录并输入

```bash
[root@ford smrsh]# ./Build; ./Build install
```

