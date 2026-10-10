
输出确实提供了一些关于正在发生的事情的线索：每一行显示关于一个网络数据包的信息。每一行都以时间戳开头，随后是数据包的详细信息（例如来源和去向等信息）。我并没有在此处试图解释这些细节，但你可以通过执行 **man tcpdump** 来了解更多关于部分细节的信息（更重要的是，查看 *tcpdump* 的其他用途）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_0.png)

如果在 Debian 中未安装 *tcpdump*，请键入 `apt-get install tcpdump` 进行安装。

在 Linux 中，你可以使用另一种名为 Ethereal 的数据包嗅探器。要了解有关 Ethereal 的更多信息，请访问 `www.ethereal.com`。

## 在启动时配置网络

每次启动系统时自动启动网络是合乎情理的。要实现这一点，各种启动脚本必须包含相应的命令。除了配置网络（在安装期间或稍后使用网络配置工具）之外，你不需要做其他特殊操作。然而，如果网络在启动时出现异常，你可以通过检查本节中提到的文件来排除故障。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_1.png)

在 Debian、MEPIS、Ubuntu 和 Xandros 中，`/etc/network/interfaces` 文件描述了系统中可用的网络接口，而 `/sbin/ifup` 命令在系统启动时激活这些接口。以下是来自 Debian 系统的典型 `/etc/network/interfaces` 文件内容：

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
# The loopback network interface
auto lo
iface lo inet loopback
# The primary network interface
auto eth0
iface eth0 inet dhcp
```

`auto eth0` 行表示你可以通过使用命令 `ifup -a`（由系统启动脚本调用）在初始化时启用以太网接口。`iface eth0 inet dhcp` 行标识该以太网是一个由动态主机配置协议（DHCP）配置的 TCP/IP 网络接口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_2.png)

在 Fedora Core 中，网络激活脚本使用 `/etc/sysconfig` 目录中的一组文本文件来激活网络接口。例如，脚本会检查 `/etc/sysconfig/network` 文件中定义的变量，以决定是否激活网络。在 `/etc/sysconfig/network` 中，你看到 NETWORKING 变量的一行如下所示：

```bash
NETWORKING=yes
```

只有当 **NETWORKING** 变量设置为 *yes* 时，网络才会激活。`/etc/sysconfig/network-scripts` 目录中的许多脚本激活特定的网络接口。例如，激活以太网接口 eth0 的配置文件是 `/etc/sysconfig/network-scripts/ifcfg-eth0`。典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件包含以下内容：

```bash
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=00:08:74:E5:C1:06
ONBOOT=yes
TYPE=Ethernet
```

**DEVICE** 行提供网络设备名称。**BOOTPROTO** 变量设置为 *dhcp*，表示 IP 地址是通过使用 DHCP 动态获取的。**ONBOOT** 变量表示此网络接口是否在 Linux 启动时激活。如果你的计算机有以太网卡并且你希望在启动时激活 eth0 接口，**ONBOOT** 必须设置为 *yes*。当然，`/etc/sysconfig/network-scripts` 目录中的配置文件 *ifcfg-eth0* 仅在您的计算机拥有以太网卡且 Linux 内核已检测到并加载了该卡的特定驱动程序的条件下才有效。

在 SUSE 中，网络信息保存在 `/etc/sysconfig/network` 目录中，文件名以 *ifcfg* 开头。对于以太网接口，配置文件名以 *ifcfg-eth*-id- 开头，后跟以太网卡的唯一硬件地址。以下是典型以太网配置文件中的关键行：

```bash
BOOTPROTO='dhcp'
STARTMODE='auto'
```

**BOOTPROTO='dhcp'** 行表示该接口是使用 DHCP 设置的，而 **STARTMODE='auto'** 意味着该接口在系统启动时初始化。

# 第四卷

# 互联网

第五个浪潮
作者：Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_336_0.png)

> “在互联网出现之前，我们只是在当地吹牛。但现在，有了我们的网站，我们在全球各地都在吹牛。”

# 内容概览

- 第 1 章：在 Linux 中发送电子邮件和即时消息 ......313
- 第 2 章：浏览网页 ......333
- 第 3 章：阅读新闻组和 RSS 源 ......345
- 第 4 章：使用 FTP ......361

## 第 1 章：在 Linux 中发送电子邮件和即时消息

### 本章内容

- 理解电子邮件
- 盘点邮件阅读器和 IM（即时消息）客户端
- 介绍 Evolution
- 介绍 Thunderbird
- 介绍 KMail
- 使用 Gaim 和 Kopete 进行即时消息

电子邮件（e-mail）是互联网的主要组成部分。电子邮件之所以很棒，是因为你可以与互联网上的任何人交换消息和文档。人们使用互联网的最常见方式之一就是通过电子邮件与朋友、熟人、亲人和陌生人保持联系。你可以向数千英里外的朋友发送消息，并在几分钟内收到回复。基本上，你可以从互联网主机向世界上任何地方发送消息，并且该消息通常会在几分钟内到达目的地——这是传统邮件（也称为*蜗牛邮件*，名副其实）无法做到的。

我热爱电子邮件，因为它让我可以在不进行*电话捉迷藏*游戏的情况下进行沟通，那种游戏中两个人可以无限次地给对方留言，却从未成功取得联系。当我发送电子邮件消息时，它会在收件人的邮箱中等待，以便收件人在方便时阅读。我想我更喜欢相反的情况——当人们给我发邮件时，我可以在*我*方便的时候阅读并回复。

Linux 附带了几个邮件客户端——也称为*邮件阅读器*——可以从你的互联网服务提供商（ISP）下载邮件。你也可以使用这些邮件客户端阅读和发送电子邮件。在本章中，我提到了 Linux 中可用的几个邮件客户端，并简要介绍其中几个。当你熟悉一个后，你就可以轻松使用任何邮件阅读器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_339_0.png)

还有一种*保持联系*的方式，更符合当今年轻一代的需求。我指的是 IM——即时消息。IM 基本上是一对一的聊天，Linux 包含用于 AOL Instant Messenger（或 AIM）的 IM 客户端，以及其他即时消息协议，如 Jabber、ICQ、MSN Messenger、Yahoo!、Gadu-Gadu、IRC（互联网中继聊天）和 SMS（短消息服务或短信）。我在本章中简要描述了一些 IM 客户端。

## 理解电子邮件

电子邮件消息是发送给*主机*上的用户名的（*主机*只是在线计算机的优雅名称）。这意味着如果 John Doe 以用户名 `jdoe` 登录，发给他的电子邮件地址为 `jdoe`。唯一其他需要的信息是收件人系统的全限定域名，以唯一标识收件人。因此，如果 John Doe 的系统名为 `someplace.com`，他的完整电子邮件地址变为 `jdoe@someplace.com`。有了这个地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

### MUA 和 MTA 如何工作

两种类型的邮件软件如下：

- **邮件用户代理（MUA）**是邮件阅读器的优雅名称——一个用于读取邮件消息、撰写回复和创建新消息的客户端。通常，邮件用户代理通过使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是*邮政协议第 3 版*，IMAP4 是*互联网消息访问协议第 4 版*。Linux 附带邮件用户代理，如 Balsa、Thunderbird、KMail 和 Evolution。
- **邮件传输代理（MTA）**是实际发送和接收邮件消息文本的邮件服务器的优雅名称。用于邮件传输的具体方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用*简单邮件传输协议*（SMTP）来递送邮件。Linux 包含 `sendmail`，这是 TCP/IP 网络中强大且流行的邮件传输代理。

图 1-1 展示了当 Alice 向 Bob 发送电子邮件消息时 MUA 和 MTA 如何协同工作。（如果你不知道的话，使用 *Alice* 和 *Bob* 来解释电子邮件和加密是惯例——随便拿起一本关于加密的书，你就能看到我的意思。）你可能已经知道这一点，但互联网总是被绘制成云朵——互联网的边界如此模糊，云朵似乎很适合代表它。（或者是因为没人知道它从哪里开始，到哪里结束？）

