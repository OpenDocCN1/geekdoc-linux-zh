
## 运行 Zircon 1.18

如果你在安装期间接受了默认设置，二进制可执行文件现在位于 /usr/local/bin。每次运行此程序时都会出现一个小的启动画面，但第一次运行时还会出现一个通知窗口，告知你这是一个新版本。请注意，启动画面会遮挡大部分该窗口，因此你需要移动窗口以便能够点击 OK 按钮继续。幸运的是，这只会在安装后的首次执行时发生。

在尝试连接 IRC 服务器之前，你需要设置你的 Ircname 和 Nickname——只需高亮默认数值并覆盖输入即可。然后选择位于灰显的 Server information 按钮上方的按钮，选择 Other，然后输入你想要连接的 IRC 服务器名称。

鉴于 Zircon 具有大量功能，学习如何使用它的最佳方法是启动它并进行实验。实验时显示可能会变得相当繁忙，但最终会自行整理好，你就可以开始聊天了。

## X-Chat

X-Chat 是随 Red Hat 6.0 发行版默认安装的 IRC 客户端。它具有简洁美观的用户界面，并且默认安装了 IRC 服务器列表——当然，你可以根据需要添加、删除或更改此列表。

X-Chat 是一款功能齐全的客户端，它响应多种 ircII 命令，同时还通过界面上的按钮提供大多数命令的等效操作。X-Chat 主页位于 http://xchat.linuxpower.org 并提供额外的文档和信息可用。X-Chat 需要 X11 和 GTK+，可选 GNOME 和 Perl。

X-Chat 在 GPL 下发布。

## 获取 X-Chat

如前所述，X-Chat 已随 Red Hat 6.0 版本发行版默认安装，但对于想要更新或更喜欢自行安装的人来说，RPM 打包的二进制文件可以从 X-Chat 下载页面 http://xchat.linuxpower.org/download/ 获得。源代码也可在该位置获得，形式为 tarred 和 zipped 归档或 SRPM。

## 安装 X-Chat

在撰写本文时，最新版本是 1.2.1。如果你有较早版本（如随 Red Hat 6.0 安装的版本），升级非常值得。X-Chat 1.2.1 提供了改进的用户界面以及其他多项更改。

从下载页面下载 RPM 二进制文件并将其放置到合适的目录中。进入该目录并使用 Red Hat 软件包管理器安装，

```
rpm -ivh xchat-1.2.1-1.1386.rpm.
```

请注意，如果你已安装了 X-Chat 的先前版本，应使用命令

```
rpm -Uvh xchat-1.2.1-1.1386.rpm instead.
```

## 运行 X-Chat

如果你使用 GNOME 界面并且已安装了 X-Chat 的先前版本，可以从 GNOME 菜单运行 X-Chat。它出现在 Internet 子菜单中。

如果你之前未安装 X-Chat 并使用 RPM 安装了最新版本，二进制可执行文件位于 /usr/bin。这是在所有用户的默认 shell 搜索路径中。

当然，如果你从源码安装，需要阅读 makefile，如果你从 tarball 安装，二进制文件通常会出现在 tarball 放置的目录下、与程序同名的目录中。

启动 X-Chat 后，第一件事是选择一个昵称——默认是你的用户名——然后选择要连接的服务器。X-Chat 非常贴心地提供了全面的服务器列表供你选择，因此你不必在 WWW 上查找。如果你知道所需的服务器且列表中没有，可以使用 New Server 按钮添加它。

在选择服务器后点击 Connect 会连接到服务器，你通常会看到每日信息。此时昵称冲突将被提示。

## BitchX

根据主页 (http://www.bitchx.com) 的说法，“BitchX is a modified clone of the popular ircII client, and is available for almost all UNIX OS's...”。

BitchX 是另一款基于控制台的 IRC 客户端，为 ircII 提供了替代方案。因为它是基于控制台的，你不必担心启动 X——只需使用车库里那台只有能显示 80 × 25 的单色显卡的老 386 电脑即可！

请注意，文档未随程序一起安装，但你可以在 http://scripts.bitchx.com/bxf... 找到 FAQ 列表。

## 获取 BitchX

BitchX 可在 http://www.bitchx.com/download/ 以二进制或源码形式下载。像往常一样，我们建议你下载并安装二进制文件以求简单，但下载页面建议你自行下载源代码并编译，因为存在引入安全漏洞的可能性。

## 安装 BitchX

进入放置下载的 tarball 的目录，并使用命令 tar -xzf BitchX-75p3-Linux-glibc2-1386.tgz 解压，以在同一目录中创建二进制可执行文件。在运行它之前，需要为其设置执行位。

## 运行 BitchX

在放置 tarball 的目录中（并且在确保已设置执行位之后），输入 ./BitchX 即可开始！

BitchX 启动时会自动连接到服务器 irc.idle.net。如果你想指定不同的服务器，需要设置环境变量 IRCSERVER。bash shell 命令是 bash: $export IRCSERVER="server1:port1 server2:port2 server3:port3"。请注意，FAQ 给出了错误的命令 (setenv) 和错误的环境变量 (IRCSERVERS)。

## ICQ 和克隆

ICQ (I seek you) 是由 Mirabilis (http://www.icq.com) 开发的软件包，用于在比 IRC 更私密的环境中实现人对人及多方聊天。它还有便于查找他人的优点，并且对许多人来说比 IRC 更易于使用。

克隆，当然是提供与原版相同或类似功能的程序，但并非由原版程序的作者提供或编写。在 Linux 下，除了由 Mirabilis 发布 JavaICQ 之外，所有 ICQ 类型的程序都是克隆。

## ICQ、IP-Masquerading 和防火墙

在 ICQ 网站 http://www3.mirabilis.com/ 上，有关于如何配置防火墙以允许 ICQ 通信的全面讨论。

由于通信的实现方式，防火墙对 ICQ 构成了特定问题。实现需要建立 ICQ 讨论中涉及的各台计算机之间的通信线路。防火墙的目的是阻止这些通信线路的建立，因此需要单独的程序来绕过防火墙，同时尽量降低安全风险。

简而言之，如果你不想立即访问 Mirabilis 网站，过程相当简单。

要配置防火墙，你只需设置规则允许通过一小范围端口（例如 5000-5020）进行传入套接字连接。如何操作取决于防火墙的性质。你应在实施防火墙更改之前阅读并理解 Mirabilis 网站上的信息以及第 26 章，“Firewall Strategies，”中的内容。

## 配置 ICQ 客户端

要配置 ICQ 客户端，你必须告知客户端你正运行在非 socks 防火墙之后，并且可用端口范围如你修改防火墙时所指定。最后，你需要重新启动客户端，使其识别新设置，然后你就可以聊天、发送和接收文件和消息等。

## 来自 Mirabilis 的 JavaICQ

JavaICQ 是 ICQ 的 Java 实现。ICQ 主页位于 http://www.icq.com/。

你需要注意 JavaICQ 的最低要求为 10MB 硬盘空间和 32MB RAM。这是一个总 RAM 要求，因此 16MB 物理 RAM 加上 16MB 交换空间即可满足要求（前提是整个交换空间可供该应用程序使用）。

请注意，普遍的看法是该应用程序不必要地庞大且存在错误。由于这一声誉，许多 Linux 用户被劝阻使用它，但代码正由 Mirabilis 不断审查，改进正在逐步实施。

JavaICQ 的优点在于它由 Mirabilis 编写并发布，因此提供了可用的最大功能。Windows 版 ICQ 用户期望可用的功能在 JavaICQ 中大多可用，而克隆程序不一定实现所有功能。
