
Usenet 软件已移植到非 Unix 系统，因此 netnews 用户群体已经大幅增长。Netscape 在其 Web 浏览器中包含了一个名为 Netscape News 的图形界面，你可以使用它来阅读新闻。按照 Unix 传统，netnews 组的类别呈层次结构组织。顶层有诸如 comp、misc、rec、sci、soc 和 talk 等标识。这些缩写分别代表计算机、杂项、娱乐、科学、社会问题和谈论讨论。

顶层通常有一个区域类别，包含有关当地活动的信息。新类别不断增加。新闻组名称类似于域名，但像 Solaris 文件名一样从左到右读取。例如，`talk.politics`、`soc.singles`、`rec.racing` 等只是其中几个新闻组。

使用 Usenet 需要耐心，但你肯定会找到你需要的内容，并在途中结识一些有趣的人。有 netnews 存档，你可以在那里找到几乎任何问题的答案，因为其他人可能曾经问过同样的问题。你可以阅读 Usenet 新闻来了解新工具和服务。`comp.os.Unix` 层次结构始终对 Unix 用户很有吸引力。人们会在那里宣布免费软件的可用性，并提供如何获取副本以供自己使用的说明。

在互联网上有一些关于 Solaris 8 问答的优秀资源。`comp.unix.solaris` 论坛是一个关于 Solaris 8 信息和讨论的 Usenet 组。它还允许你贡献你的知识来帮助有其他疑问的人。你可能能够为他们提供一两个答案。

除了 Usenet，还有其他在互联网上查找和分享有关 Solaris 信息的方法。由 Casper Dik 维护的 Solaris 8 FAQ 是通用信息的绝佳来源。最新版本位于 `www.win5.uva.nl/pub/solaris/solaris8/`。

对于 Intel 用户，有一个名为 `alt.solaris.x86` 的论坛站点，该站点信息丰富且对初学者友好。没有任何问题被认为是不重要的而不被回答。SPARC 和 Intel 平台都有可用的 FAQ 站点，可以通过 `www.sunhelp.org/faq/sunadm.html` 访问。

有关最新的 Solaris 2 FAQs，包括 HTML 版本和其他有趣的资源，请联系 `ftp://ftp.win5.uva.nl/pub/solaris`。

提问和寻找答案的另一个选项是使用邮件列表。Sun Manager's List 是一个著名的列表，包含问题、答案以及之前查询的摘要。几乎涵盖了所有与 Solaris 相关的主题。还有一个 x86 邮件列表，为对 Solaris 8 相对陌生的用户提供了绝佳的提示、技巧和忠告。如果你在特定的硬件配置上遇到困难，这是一个很好的资源。

有关 Solaris 帮助资源的更多信息，请参阅第 1 章“Solaris 8 操作系统”。

# Apache

Apache 项目是一个由志愿者团队共同管理的软件开发项目。他们遍布世界各地，使用互联网和万维网进行沟通，这是一个核心小组，创建了一个商业的、自由源代码的 HTTP Web 服务器实现及相关文档。基于 NCSA httpd 服务器，Apache 现在是一个完全重写的服务器，具有相当高的安全性。

Solaris 8 的发行版包含一个 Apache Web 服务器版本供你使用。如果你没有操作系统的发行版，或者你决定需要最新版本，Apache Web 服务器可以从 Apache 组免费获得（`www.apache.org`）。这将让你获得所有最新的错误修复和当前安全功能。版本 2 的预发布版现在已在互联网上供开发者下载。Apache 免费的主要原因之一是，用户通常通过建议功能增强和错误修复，以及在公共新闻组中积极支持他人来做出贡献。个人的努力通常很少，但所有人投入的组合产生了一个非常强大的产品。虽然用户仍在使用 1.3.20 版，但版本 2 很快就会准备好供公众使用。版本 2 有许多新的增强功能，使其更加稳健。

如果你决定下载 Apache，请务必执行以下操作：

1. 获取一个有效的 IP 地址。
2. 获取一个用于你的 Web 服务器的主机名。
3. 让你的 Web 服务器添加到域名服务器中。
4. 如果你计划支持 CGI 或 servlets，请使用单独的机器作为 Web 服务器。
5. 检查你的系统，确保它具有编译 Apache 所需的组件。
6. 确定编译后 Apache 应安装的目录。
7. 确定哪些模块应被编译进 Apache。

在确认系统具备编译所需的所有组件后，配置您的 Apache Web 服务器至关重要。当您使用 `configure` 命令时，Apache 会自动处理此过程：

```
$ ./configure --prefix=\[install_dir\] --enable-module=<module-name>
```

如果您希望启用多个模块，请输入多个 `enable-module` 语句，如下例所示：

```
$ ./configure --enable-module=<module-name> --enable-module=<module-name> --enable-module=<module-name> ...
```

如果您不需要任何额外的模块且仅使用默认设置，您可以使用带有 `--prefix` 选项的 `configure` 命令。

在 `configure` 命令完成后，使用以下命令编译 Apache：

```
$ make
```

在输入 `make` 命令时，请务必确保您位于解压分发包所在的目录中。如果您使用的是 Sun make 工具，可能需要使用完整路径，如下例所示：

```
$ /usr/ccs/bin/make
```

该命令将导致 Apache 连同其所有默认模块一起进行编译。完成后，`src` 目录中会出现一个名为 `httpd` 的单个文件。

现在，您可以使用以下命令安装 Apache：

```
$ make install
```

这会将 `httpd` 可执行文件以及配置文件复制到安装目录中。如果出现错误消息，可能是您的权限不足。如果是这种情况，请以 root 身份执行该命令：

```
$ su root -c '/usr/ccs/bin/make install'
```

此命令完成后，您的系统中就安装了 Apache。此时，您应该对其进行彻底测试，以确保其正常工作。您应考虑让 Apache 随系统启动而运行。有一个名为 `bin` 的子目录，其中包含一个名为 `apachectl` 的脚本。该脚本可用于启动和停止 Apache。将 `apachectl` 脚本的一个副本放置在 `/etc/init.d` 目录中。这会将 Apache 集成到启动过程中。请以 root 身份使用以下命令：

```
# cp /hm/httpd/bin/apachectl /etc/init.d
```

如果您安装到了其他目录，请更改该命令以使用正确的路径名称。

复制 `apachectl` 脚本后，将目录更改为 `/etc/rc3.d`，然后发出以下 root 命令：

```
# ln -s ../init.d/apachectl S85apachectl
```

当系统启动并达到运行级别 3 时，此链接将自动启动 Apache。如果您希望 Apache 自动关闭，可以发出以下 root 命令创建另一个链接：

```
# ln -s ../init.d/apachectl K15apachectl
```

由于您仍然位于 `/etc/rc3.d` 目录中，当系统达到级别 3 时，Apache 将被停止然后启动。您需要在 `rc0.d`、`rc1.d`、`rc2.d` 和 `rc5.d` 中放置 kill 命令。

此时，通过发出以下 root 命令测试 Apache Web 服务器的启动是明智之举：

```
# /etc/init.d/apachectl start
```

如果脚本失败，请检查是否已为 `apachectl` 文件设置了可执行位。您可能忘记将启动文件复制到 `/etc/init.d`。如果是这种情况，请切换到安装 Apache 的目录并发出以下 root 命令：

```
# ../bin/apachectl start
```

这将启动 Web 服务器。您可以使用 `telnet` 命令对其进行测试：

```
$ telnet localhost 80
```

您将看到以下输出：

```
Trying 127.0.0.1
Connected to localhost.
Escape character is '^'.
```

虽然您不会收到提示符，但您的终端光标将位于空行的开头。这表明您已连接到 Web 服务器。但是，如果您收到“连接被拒绝”的消息，请检查进程列表，以确保 Apache 已正常启动。

以下示例可用于测试 Web 服务器：

```
GET / HTTP/1.0
```

输入此行后，按两次 Return（回车）。在第二次按 Return 后，您将看到一个 HTML 页面在屏幕上滚动。HTTP 响应头和部分页面内容如下所示：
