
静态路由指定针对特定网络或主机的信息应该发送到与默认网关不同的网关。通过这种方式，可以为从互联网提供商到互联网的所有流量定义静态路由。

# 我们现在到了哪里？

在本章中，我们学习了 TCP/IP 和路由的基本概念。将这些理论知识应用于实践，在下一章中我们将学习如何连接 Linux 到互联网。

# 第十七章

## 将 Linux 连接到互联网

- 什么是 PPP？
- 必要的硬件和软件
- 你的第一次连接
- 自动化互联网连接

将 Linux 系统（或者说任何计算机系统）连接到互联网是一个复杂的话题，可能需要对系统的网络环境有深入了解。尽管如此，对于许多用户来说，这个过程非常简单，Windows 和 Linux 都能上手。

在本章中，我们将首先快速查看 PPP 及其在互联网中的作用。接下来我们将回顾连接互联网所需的硬件和软件。然后，我们将演示手动建立 PPP 连接的步骤，最后通过学习如何自动化这些连接来结束。

## 什么是 PPP？

互联网用户可能对 PPP 这个缩写很熟悉，因为他们在互联网提供商处的账户类型就是 PPP 账户。然而，许多用户并不真正理解 PPP 是什么。

PPP 代表点对点协议（Point-to-Point Protocol），提供一种让 TCP/IP 扩展到模拟调制调器连接的方法。通过这种方式，你使用 PPP 连接到互联网，成为互联网提供商网络的一部分，成为互联网上真正的主机，并拥有 IP 地址。

## 必要的硬件和软件

在本章中，我们将讨论最常见的互联网连接场景：将调制调器连接到提供动态分配 IP 地址 PPP 连接的互联网提供商。

为了让 PPP 正常工作，需要进行一些准备。在让 PPP 正常工作之前，硬件和软件需要到位并完成配置。需要考虑的三个关键部分：

- 调制调器需要安装、配置并正常工作。
- PPP 支持需要编译到 Linux 内核中。
- 需要安装 PPP 软件。

### 调制调器

由于 PPP 是为拨号连接设计的，因此调制调器是 PPP 过程中不可或缺的一部分。

在第 15 章“使用外设”中，我们讨论了调制调器以及如何安装、测试并使其正常工作。请参考该章节让您的调制调器运行起来，并进行测试连接以确保一切正常。

要配置 PPP，您需要知道调制调器连接的速度，以及它在 Linux 中使用的设备（可能是 `/dev/modem` 或 `/dev/cuao0` 到 `/dev/cuao3` 之间的之一）。

### 内核中的 PPP

Linux 内核设计得非常灵活。它可以被编译以包含（或排除）从串口鼠标到 PPP 等网络设施的许多技术支持。

为了在 Linux 中建立 PPP 连接，内核必须包含 PPP 支持。在大多数 Linux 发行版中（包括许多版本的红帽 Linux），由该发行版安装的默认内核已内置了 PPP 支持。

您可以通过观察操作系统启动时滚过屏幕的消息来检查是否存在该支持。如果您看到类似下面的这些行：

```
PPP: version 2.2.0 (dynamic channel allocation)
PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
PPP line discipline registered.
registered device ppp0
ppp: ppp line discipline successfully unregistered
```

那么 PPP 已经编译到您的内核中了。如果您发现消息滚动得太快，可以使用 `dmesg` 命令查看启动消息中包含 PPP 消息的部分：

```bash
$ dmesg | more
```

如果您发现需要重新编译内核，应该访问本书书的网站 `http://linux.just.com/`。重新编译内核是一个高级话题，许多用户并不会遇到。为了完全理解它并在重新编译中成功，您需要理解它的复杂性。正因如此，这是本书的范围。在网站上，您将找到讨论重新编译内核的参考链接，它们可以帮助您完成这一过程。

### 安装 PPP 软件

大多数 Linux 发行版在完整或默认安装时都会安装 PPP 软件。红帽 Linux 5 也不例外。

使用两个程序建立 PPP 连接：`/usr/sbin/pppd` 和 `/usr/sbin/chat`。在红帽 5 中，这些是 `ppp-2.3.3-2` 软件包的一部分，您可以使用 `rpm` 检查它们是否已安装：

```bash
$ rpm -q ppp
ppp-2.3.3-2
```

如果您缺少 `pppd` 或 `chat`，在继续之前需要安装一套新的 PPP 软件。

如果您正在运行红帽 5，请将红帽 CD-ROM 挂载到合适的位置（例如 `/mnt/cdrom`），然后使用 `rpm` 安装 `ppp-2.3.3-2.i386.rpm` 包：

```bash
$ rpm -i ppp-2.3.3-2.i386.rpm
```

或者，您可以从 Sun 的 Linux 存档下载 PPP 的最新源码，目录为 `ftp://sun.edu/pub/Linux/system/serial/ppp`。PPP 的当前版本是 2.3.4，文件名是 `ppp-2.3.4.tar.gz`。

您需要在合适的位置使用以下命令解包：

```bash
$ tar xzvf ppp-2.3.4.tar.gz
```

然后仔细阅读 `README.linux` 文件。安装新的 PPP 包不仅涉及编译软件，还需要升级您的 Linux 内核源码并重新编译 Linux 内核以匹配正在安装的 PPP 软件版本。

详细介绍这一过程将占据一整章，因此最好留给文档。如果您不幸地运行着一个不包含 PPP 的 Linux 发行版，而且您没有足够的信心（或足够的冒险精神）来自己安装 PPP，那么最好的建议是安装一个新的 Linux 发行版，例如此书附带的那个。

## 您的第一个 PPP 连接

现在我们已经有了必要的软件和硬件，准备好讨论我们第一个连接的细节。首先，有必要理解它是如何工作的。

在 Linux 中，PPP 连接由 `pppd` 建立和维护。但 `pppd` 假设您的调制调器与互联网提供商的调制调器之间已经建立了连接，所有必要的登录都已完成，并且互联网提供商的系统也在尝试在同一个调制调器连接之上建立 PPP 连接。

这听起来有很多条件，但实际上并没有那么糟糕。在几乎每个互联网提供商的系统中，连接过程如下：

1. 建立调制调器连接。
2. 发生登录过程。
3. 一旦用户通过身份验证，互联网提供商就开始通过发送本地机器的 IP 地址尝试建立 PPP 连接。

### 建立连接

为了建立连接，我们需要使用 `chat` 程序。在几乎每个互联网提供商的系统中，连接过程如下：

1. 建立调制调器连接。
2. 发生登录过程。
3. 一旦用户通过身份验证，互联网提供商就开始通过发送本地机器的 IP 地址尝试建立 PPP 连接。

服务商的计算机将向你显示一个命令提示符，你需要在其中输入命令来启动 PPP。在这种情况下，你需要创建一个额外的配对。

对于我们的示例，完整的脚本如下：

```
** DT1234567 CONNECT ** Username: tester Password: testpassword
```

要配合聊天程序（通常位于 `/usr/sbin/` 中）使用它，我们只需将脚本作为参数提供给 `chat` 即可：

```
/usr/sbin/chat ** ATDT1234567 CONNECT ** Username: tester:
-> testpassword
```

但注意，你不想在命令行中输入这些内容并按回车。如果没有与 `pppd` 集成并通过该程序获得调制调的访问权限，调制调将尝试在控制台中进行交互。你可以利用此测试你的脚本，只需在命令提示符处输入命令即可。当你看到 `ATDT1234567` 时，输入 `CONNECT`，然后输入 `Username:`；你应该响应 `tester`。接着输入 `Password;`；你应该响应 `testpassword`。

如果你需要解决聊天脚本中的问题，请尝试在 `chat` 命令中添加 `-v` 标志。这会导致脚本的输出出现在系统日志中，你可以在那里分析结果以发现问题。

一旦你有了可以工作的脚本，就需要将其与 `pppd` 集成。我们将使用一些 `pppd` 选项来实现此。`pppd` 应用程序还有许多额外选项，可以在 `pppd` 的 man 页中找到。我们使用的选项如下：

- `-connect`：用于指定在正在使用的串口线上建立连接的程序或命令。在这种情况下，我们使用此选项来指定聊天程序及其脚本。
- `-default`：`pppd` 的默认行为是根据主机名确定本地机器的 IP 地址。如果互联网提供商分配了动态 IP 地址，则使用默认设置告诉 `pppd` 从正在连接的远程机器获取 IP 地址。
- `-defaultroute`：此选项告诉 `pppd` 向系统路由表添加默认路由，并将远程系统作为默认网关。当连接中断时，该条目会被移除。

`pppd` 命令的结构为：

`pppd device-name device-speed options`

如果我们使用设备 `/dev/modem` 进行连接，且调制调最高压缩速度为 57600bps（换句话说，一个 14.4Kbps 的调制调），我们将使用以下命令与聊天程序连接：

```
$ ppp /dev/modem 57600 connect /usr/bin/chat ** ATDT1234567 CONNECT
** Username: tester Password: testpassword' noipdefault
** defaultroute
```

当下发此命令时，调制调应该拨号，并在连接后进行身份验证并建立 PPP 连接。如果此过程成功，应该发生两件事。

首先，执行不带标志或参数的 `ifconfig` 命令应返回接口列表，其中包含一个类似于下面的 PPP 接口：

```
pp0
Link enc:Point-to-Point Protocol
inet addr:194.209.60.101 P-t-P:194.209.60.97
Mask:255.255.255.0
```

```
UP EPOPOINT RUNNING MTU:1500 Metric:1
RX packets:10 errors:0 dropped:0 overruns:0
TX packets:11 errors:0 dropped:0 overruns:0
```

其次，路由表中应添加条目，以创建通过远程机器的默认路由（请检查使用不带标志或参数的 `route` 命令）：

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use |
| --- | --- | --- | --- | --- | --- | --- |
| Kernel IP routing table | | | | | | |
| Iface | | 255.255.255.0 | 0 | 0 | 0 | |
| dul.paus.ch | * | | | | | |
| ppp0 | | 0.0.0.0 | UG | 0 | 0 | 0 |
| default | dul.paus.ch | | | 0 | 0 | 0 |
| ppp0 | | | | | | |

在这个示例中，`dul.paus.ch` 是 PPP 连接中的远程机器，并作为默认网关。

## 使用 PAP 身份验证连接

使用 PAP 身份验证连接与我们刚刚处理过的文本提示示例遵循相同的基本原理，不同之处在于提供用户名和密码的方法。

第一个主要区别是，我们不是在命令行中作为 PAP 脚本的一部分提供用户名和密码。相反，我们在特殊的 secrets 文件中创建条目，该文件在 PAP 身份验证过程中使用。在 Red Hat Linux 5 中，该文件是 `/etc/ppp/pap-secrets`。默认情况下，该文件的权限使得只有 root 用户可读可写。其他用户没有该文件的读取权限。

该文件中条目的格式为：

```
username device/interface password
```

例如，如果我们使用上面部分中的用户名和密码，我们的条目可能是：

```
tester * testpassword
```

`*` 表示此密码可用于任何接口的连接。如果我们仅有一个 PPP 接口 (`ppp0`)，我们可以限制 ppp0 的使用。

对于拨号脚本（dial script），我们假设在本章之前的 PAP 示例是我们想要连接 Internet 的方式。

一旦创建了脚本，你将希望使用 `chmod` 命令让它们具有可执行权限：

```bash
$ chmod 700 dial hangup
```

`700` 权限使得该脚本只有 root 用户可以读取、写入和执行，其他人均无法操作。这将能够正常工作，因为在建立 PPP 连接时你需要以 root 身份运行。

### 拨号脚本 (The Dial Script)

拨号脚本应该如下：

```sh
#!/bin/sh
/usr/bin/pppd /dev/modem 57600 connect \
/usr/bin/chat "" ATDT1234567 CONNECT '\'
noipdefault defaultroute user tester
```

第一行告诉 Linux 通过 Bourne Shell（即 `/bin/sh`）处理该脚本。你会发现你的 `pppd` 命令被分成了三行。我们这样做是为了使脚本更具**可读性**，并缩短单行的长度。第一行和第二行末尾的反斜杠 `\` 表示换行处的换行符不应被视为行结束，命令将在文件的下一行继续。

### 挂断脚本 (The Hangup Script)

挂断脚本应该如下：

```sh
#!/bin/sh
kill `cat /var/run/ppp0.pid`
```

与拨号脚本一样，我们首先指定该脚本应由 Bourne Shell 处理。接下来，我们以一种与之前学习略不同的方式杀死进程。

我们利用这样一个事实：`pppd` 进程会将进程 ID（PID）写入到一个文件中，该文件在大多数现代 Linux 系统中通常位于 `/var/run/`。文件名由设备名加上 `.pid` 扩展组成。如果你只有一个现代设备和一个 PPP 连接处于活动状态，你可以假设设备是 `ppp0`，并将 `/var/run/ppp0.pid` 直接写入你的脚本中。

`cat` 命令简单地在标准输出显示 `ppp0.pid` 文件的内容。我们将 `cat` 命令放在这里，是为了将 `cat` 命令的结果（即 `pppd` 进程的进程 ID）传递给 `kill` 命令。

但如果你有多个 PPP 接口并想要指定挂断哪一个，会发生什么呢？对挂断脚本进行快速修改即可实现这一点：

```sh
#!/bin/sh
kill 'cat /var/run/$1.pid'
```

在这里我们将 `ppp0` 替换为 `$1`。`$1` 表示脚本的第一个参数的值应该放在此位置。现在我们可以将接口名称作为参数传递给脚本。执行 `$ hangup ppp1` 将挂断正在用于 `ppp1` 接口的调制解调器。

## 我们将如何继续？

在本章中，我们迈出了大的一步。我们将 Linux 系统从桌面上孤立计算机的状态中解放出来，并通过 PPP 连接将它们连接到世界。

在接下来的章节中，我们将利用这种新能力，查看 Netscape Communicator——它是 Linux 平台领先的 Web 浏览器和 Internet 客户端。

之后，在第 19 章中，我们将查看 Linux 提供的丰富的电子邮件软件，以便你可以选择最符合你邮件使用风格的一个。

# 第十八章

## 使用万维网 (Using the World Wide Web)

- Linux 浏览器概览
- 安装和使用 Netscape Communicator
- 安装和使用 Xmosaic
- 安装和使用 Lynx

# 第 18 章 • 使用万维网

现在我们的 Linux 系统已经正确连接到 Internet，我们大多数人最想做的第一件事就是出去浏览万维网（World Wide Web）。

在本章中，我们将对 Linux 可用的许多种 Web 浏览器进行简要游览，然后仔细查看三个浏览器：Netscape Communicator、Xmosaic 和 Lynx。

Netscape Communicator 是 Netscape 推出的最新免费 Web 浏览器和 Internet 客户端。这个全功能包适用于 Windows、Macintosh 以及几乎所有可以想象的 Unix 变体 Linux。

在 Netscape Communicator 的图形化浏览器之后，Xmosaic 值得一看，因为它是今天图形化浏览器的“祖父”。在任何人听说过 Netscape 之前（可能甚至在 Marc Andre 构思它之前），Mosaic 就已经通过将基于文本的超文本系统变为图形化，在悄悄地改变着万维网。Mosaic 诞生于 Unix 和 X 世界，后来进入了 Windows 世界，因此在 X 环境下查看 Mosaic 真正是在观察我们今天所知的 Web 从何处开始。

最后，我们将查看 Lynx，它是 Unix 文本浏览器的事实性标准。Lynx 的历史比 Netscape 或 Mosaic 都要长，可以追溯到 Web 技术仍被用于在简单的文本超文本系统中传递少量科学信息的时期。Lynx 一直在进化，并与几乎每个 Linux 发行版一起发布。虽然它缺乏 Netscape Communicator 那种华丽的图形和图标驱动的界面，但对于快速上网、查看信息并离线来说，Lynx 更胜一筹。

## Linux 浏览器概览
