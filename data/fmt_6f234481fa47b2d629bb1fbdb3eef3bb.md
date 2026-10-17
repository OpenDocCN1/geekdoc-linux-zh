
```
host fantasia {
  hardware ethernet 08:00:27:07:26:c0:a5;
  fixed-address fantasia.fugue.com;
}
```

# You can declare a class of clients and then do address allocation

# based on that. The example below shows a case where all clients

# in a certain class gets addresses on the 10.17.224/24 subnet, and all

# other clients get addresses on the 10.0.29/24 subnet.

```
class "foo" {
  match if substring (option vendor-class-identifier, 0, 4) = "SUNW";
}

shared-network 224-29 {
  subnet 10.17.224.0 netmask 255.255.255.0 {
    option routers rtr-224-1.example.org;
  }
  subnet 10.0.29.0 netmask 255.255.255.0 {
    option routers rtr-29-1.example.org;
  }
}
```

# 第 15 章

# 设置邮件服务器

本章涵盖的主题：

- 使用消息传输代理 (MTA)
- 将 Postfix 设置为 SMTP 服务器
- 配置 Dovecot 用于 POP 和 IMAP
- 后续步骤

很难想象没有电子邮件的互联网。尽管即时消息、推文和短信等新的通信技术已经确立了自己的地位，但电子邮件仍然是互联网上一种重要的通信手段。为了配置互联网邮件服务器，Red Hat 提供了 Postfix 作为默认邮件服务器。在学习此邮件服务器如何工作之前，本章将对互联网邮件领域进行简要介绍。

## 使用消息传输代理 (MTA)

三个组件在互联网邮件代理 (MTA) 的过程中起着关键作用。MTA 使用简单邮件传输协议 (SMTP) 与互联网上的其他 MTA 交换邮件消息。如果用户向互联网上另一个域的用户发送邮件消息，则由 MTA 负责联系另一个域的 MTA 并消息投递到那里。要查找 MTA 如何服务其他域，可以使用 DNS MX 记录。

接收到消息后，MTA 会检查其是否为最终目的地。如果是，它将把消息投递给本地消息投递代理 (MDA)，由 MDA 负责将消息投递到用户的邮箱中。如果 MTA 本身不是最终目的地，则 MTA 将消息中继到最终目的地的 MTA。

中继是邮件投递中的热点问题。通常，MTA 不为任何人中继消息，只为经过身份验证的用户或以某种方式已知的用户。如果为所有人中继消息，这可能意味着 MTA 被互联网上的垃圾邮件发送者滥用了。

如果由于某些原因，MTA 无法将消息投递给另一个 MTA，它会将其队列，即 MTA 将消息存储在本地目录中并尝试之后投递。作为管理员，你可以刷新队列，这意味着你可以告诉 MTA 现在发送所有队列中的消息。

在投递时，有时会出现 MTA 联系了外部 MTA 并将消息投递那里后，又收到了该消息的情况。这一过程被称为退回（bouncing）。通常，如果消息不符合接收方 MTA 的规则，则会被退回；但如果目标用户不存在，也会被退回。或者，如果 MTA 简单配置为在消息无法投递时生成错误。

## 了解邮件投递代理 (MDA)

接收到消息后，MTA 通常会将其投递给邮件投递代理。这是负责将消息投递给目标用户的软件组件。通常，MDA 将消息投递到接收者的本地邮件存储中，在 Red Hat Enterprise Linux 中，默认路径为 `/var/spool/mail/$USER`。在 Postfix 邮件服务器中，MDA 以本地程序的形式存在。

你应该意识到，MDA 只是将消息投递到接收者可以找到的地方的软件部分。它不是 POP 或 IMAP 服务器，后者是邮件解决方案的补充，使用户更方便地获取消息（如果他们不在运行 MDA 的同一台机器上）。在互联网早期，消息接收者登录到运行 MDA 的机器上；而现在，用户在工作时从远程桌面获取消息已很常见。为了方便，你需要一个允许用户下载消息的 POP 服务器，或者一个允许用户在线时连接到邮件服务器并读取消息的 IMAP 服务器。

## 理解邮件用户代理 (MUA)

最后，邮件消息到达邮件用户代理 (MUA)。这是用户用于读取消息或编写新消息的邮件客户端。作为邮件服务器管理员，你通常不太关心 MUA。安装 MUA 是用户的责任，它允许他们能够在计算机、平板电脑或智能手机上进行工作。流行的 MUA 有 Outlook、Evolution 和 Linux 命令行工具 Mutt，你将在本章中用到它。

## 将 Postfix 设置为 SMTP 服务器

设置 Postfix 邮件服务器可以很简单，取决于你具体想对它做什么。如果你只想为本地投递启用 Postfix，你只需要设置几个安全参数并了解少量的管理命令即可。如果你想设置 Postfix 以将邮件投递到互联网上的其他域，那么情况会稍微复杂一些。

在这两种情况下，你的大部分工作都将在 `/etc/postfix/main.cf` 文件中完成。这是 Postfix 的配置文件，你可以在此调整该文件中提供的许多参数中的一些。

为了排查消息投递过程的故障，`/var/log/maillog` 文件是一个重要信息源。在该文件中，你将找到关于消息投递过程的状态信息，通过阅读该文件，你通常就能发现遇到问题的原因。

# 第 15 章 - 设置邮件服务器

在两种配置场景中，你将使用的另一个常见任务是检查邮件队列。邮件队列是由于某些问题尚未发送的消息列表。作为管理员，你可以使用 `mailq` 命令检查邮件队列的当前内容，或使用 `postfix flush` 命令刷新整个邮件队列。这意味着你告诉 Postfix 处理当前邮件队列中的所有消息并将其投递。

（注：原文中存在大量 OCR 重复和重叠内容，已根据逻辑结构进行清理和翻译）

## 练习 15.2：向外部用户发送消息

在本次练习中，你将向另一台计算机上的用户发送邮件消息。这意味着两个 Postfix 实例需要相互通信。请确保遵循所有指令，以确保所有前提条件已正确设置。

1. 在主机机上，使用 `virsh list`。如果你执行了之前所有的练习，将看到一个名为 `testvm` 的虚拟机。使用 `virsh start testvm` 启动该虚拟机。
2. 在主机机上，使用 `virt-manager` 启动虚拟机。在虚拟机上打开控制台，并记下其 IP 地址。
3. 在主机机和虚拟机上，编辑 `/etc/hosts` 文件，并包含主机机和虚拟机的一行。这样做的目的是为了这两者可以相互解析。
4. 在虚拟机上，使用 `useradd` 创建名为 `lisa` 的用户。
5. 在主机机上，使用 `su - linda` 成为 `linda` 并启动 Mutt。在 Mutt 界面，输入 `m` 开始编写新邮件消息。在字段中输入 `lisa@testvm.example.com`。在主题（Subject）字段中输入 `test message 1`。在邮件消息中输入一些文本，然后按 `y` 发送。

# 第 15 章 设置邮件服务器

## 练习 15.2（续）

6. 在 testvm 上打开一个 shell，以 root 身份使用 `yum -y install mutt` 安装 Mutt。接下来，使用 `su - lisa` 登录为 lisa 并启动 Mutt。你会发现 lisa 的邮箱是空的， linda 从另一台机器发送的消息尚未发送。

到目前就这些了。正如你所注意到的，你还无法发送消息。你将在下一节中学习如何修复这个问题。

## 基础配置

如上一个练习所示，默认安装后，你的 Postfix 邮件服务器无法接收来自其他计算机的消息。也就是说，默认情况下，Postfix 只绑定到环回 IP 地址。你可以使用 `netstat -tulpen | grep 25` 来验证这一点。在列表 15.1 中，你可以看到该命令的结果所示。

列表 15.1：默认情况下，你的 Postfix 服务器仅绑定到环回地址。

```
[root@hnl ~]# netstat -tulpen | grep 25
tcp 0 0 127.0.0.1:0.0.0.0:* LISTEN 0 18453 2561/master
tcp 0 0 :::* LISTEN 0 18456 2561/master
```

要配置 Postfix 进行基本的邮件传递，你需要向外部开放服务器，确保它绑定到环回端口以外的端口。为了做到这一点，必须更改 `/etc/postfix/main.cf` 文件中的一个参数。你可以在列表 15.2 中看到该文件的内容。

列表 15.2：`/etc/postfix/main.cf` 的部分内容
