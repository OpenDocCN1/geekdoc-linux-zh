

## 加密密码

在 Windows 98 和 Windows NT Service Pack 3 之前，密码在网络上传输时没有任何加密。微软改变了这种行为，而最初这破坏了 Samba，因为用户无法连接到 Samba 控制的服务器。为了解决这个问题，存在两种解决方案——要么强制 Windows 机器向 Samba 发送明文密码，要么启用 Samba 处理加密密码。

更改 Windows 机器的行为可能相当繁琐，这取决于你的网络规模。例如，如果你的网络上只有三台 Windows 机器，你可以轻松地更改它们的默认行为。但是，如果你有一个庞大的 Windows 机器网络，将它们的行为更改以适应你的需求就会相当困难。要在 Windows 机器上禁用加密密码，你必须更改其注册表中的一个值。

如果你查看 /usr/doc/packages/samba，你会找到以下文件：

- NT4_PlainPassword.reg
- Win95_PlainPassword.reg
- Win2000_PlainPassword.reg
- Win98_PlainPassword.reg

将适合你的系统的文件复制到软盘上并从 Windows 中双击它。这将编辑你的注册表并更新以禁用加密密码。你还应该在 smb.conf 的 global 部分添加参数 encrypt passwords = no。Samba 现在应该可以正常工作了。

第二个解决方案是强制 Samba 使用加密密码。你需要做的第一件事是在 smb.conf 的 global 部分设置 encrypt passwords = yes。然后，对于你希望连接到非访客共享的每个用户，使用 smbpasswd 命令将其添加到 Samba 中。例如，要将用户 John 添加到允许的用户中，输入以下内容：

```
# smbpasswd john
```

该命令会要求你为该用户输入两次密码。就这样，John 可以使用此密码连接到 Samba，该密码将被加密发送。请记住，你应该为系统上的所有用户执行此操作。

> TIP 你可以使用 smbpasswd 命令将更多用户添加到你的 Samba。添加的用户不必是系统的一部分；你可以将新用户添加到 Samba 而不添加到你的 SuSE Linux 系统。因此，新用户将不像真正的用户那样拥有主目录。

## OS 级别、本地主控和首选主控

为了理解这些选项，你需要学习几个概念。在 SMB/CIFS 网络中，每台机器都有一个 NetBIOS 名称，用于定义它对其他机器。例如，我们的机器称为 Shadow。当一台机器想要知道当前在线的所有其他机器的名称时，它通常会向担任本地主控角色的机器发送请求。本地主控是一台保存当前在线所有机器名称列表的机器。该列表会发送给需要此信息的任何机器。本地主控维护该列表并不断根据网络上的任何更改对其进行更新。

你可以让你的 Samba 服务器充当本地主控。但是，为了使一台机器成为本地主控，它必须赢得选举。当这台机器加入网络时，它必须挑战当前本地主控进行选举，赢得选举的机器将成为本地主控。网络上的任何机器都可以随时要求选举。当一台机器要求选举时，它需要广播有关自己的一些信息：

- 它使用的选举协议的版本
- 机器上的操作系统版本
- 机器是否设置了首选主控位
- 机器在线的时间长度
- 机器的主机名

当一台机器要求选举时，只有在以下情况为真时它才会获胜：

- 该机器使用最高版本的选举协议。这现在不是那么重要，因为 Windows 机器使用协议版本 1。因此，这将是平局，并将进行到下一个选项。
- 该机器具有最高的 OS 版本。如果平局，则进行到下一个选项。
- 该机器的首选主控位已打开。如果平局，则进行到下一个选项。
- 该机器的在线时间比挑战者更长。如果平局，则进行到下一个选项。
- 该机器的主机名在字母顺序上排在前面。

现在你知道了选举是如何进行的，让我们看看如何准备你的 Linux 机器以赢得或输掉选举。第一个选项，如你所见，不会有所帮助，因为所有机器在协议版本上都会平局。下一个选项是 OS 版本。OS 版本有特殊代码，如表 15.1 所示。

### 表 15.1 不同类型 Windows 操作系统宣布的 OS 版本

| Operating System | OS Version |
|---|---|
| Microsoft Windows NT 4.0 | 33 |
| Microsoft Windows NT 3.51 | 32 |
| Microsoft Windows NT Workstation 4.0 | 17 |
| Microsoft Windows NT Workstation 3.51 | 16 |
| Microsoft Windows 98 | 2 |
| Microsoft Windows 95 | 1 |
| Microsoft Windows 3.1 for Workgroups | 1 |

要参加选举，你应该告诉 Samba 成为本地主控。这是通过在 smb.conf 的 global 部分添加 local master = yes 来完成的。现在，如果你希望 Samba 总是赢得选举，在 smb.conf 的 global 部分输入 os level = 34。这样，Samba 永不会输，因为它将具有最高的 OS 版本。如果你希望 Samba 在 Windows NT 机器在线时不充当本地主控，设置 os level = 31。这样，Samba 将击败所有机器，除了运行 Windows NT 的机器。如果你希望 Samba 大多数时候都输掉，设置 os level = 1。

最后，如果你想与 Windows NT 正面竞争，可以设置 os level = 33 和 preferred master = yes。这样，如果 Windows NT 机器不是首选主控，Samba 肯定会获胜。

## 为同一台机器创建多个 NetBIOS 别名

Samba 允许你在 Windows 网络上创建多台机器。这在你需要出于组织目的创建单独的机器时很有用。例如，你可以除了主机器之外再创建一个名为 Backup 的机器。需要备份文件的用户可以使用 Backup，而其他需要访问你在机器上的主目录的用户可以使用原始机器。

例如，假设你的机器称为 Shadow，并且你想要创建另外两台名为 Machine1 和 Machine2 的机器。你需要做的第一件事是为每个新机器创建一个单独的 smb.conf 文件。这些文件将是 smb.conf.machine1 和 smb.conf.machine2。在你的主 smb.conf 文件中，修改你的 global 部分：

```
[global]
workgroup = HOME
netbios aliases = machine1 machine2
include = /etc/smb.conf.%L
... Rest of smb.conf file unmodified ...
```

你告诉 Samba 的第一件事是你希望它使用的 NetBIOS 别名。下一个条目告诉 Samba 将额外的 smb.conf 文件包含到你的配置中。文件的名称将取决于访问了哪个 NetBIOS 别名。%l 将被别名替换。因此，如果用户访问 Machine1，include 行将解析为 include = /etc/smb.conf.machine1。这就是你为该别名之前创建的文件。

你现在需要重新启动你的 Samba 守护进程：

```
# /sbin/init.d/smb reload
```

就这样了。如你在图 15.5 中所见，当你使用 Windows 机器浏览网络时，你应该看到三台机器，Shadow、Machine1 和 Machine2。它们各自具有单独的配置，但它们都在同一台物理机器上。

FIGURE 15.5
多亏了 NetBIOS 别名，你能够在网络上创建多台机器。这些被称为虚拟机器。

![](img/659f91d9da7b29976c0625e2e9628511_340_0.png)

## 处理旧版 Windows 客户端

旧的 Windows 客户端，例如 Windows for Workgroups (WFWG)，与新版本大不相同。一个主要区别是文件名存储的方式。在 WFWG 中，文件名长八个字符，后跟一个点和三个字符表示文件扩展名，例如 command.com。如果你使用 Samba 与这些机器一起使用，你可能会遇到一些问题。最基本的问题是 Linux 使用长文件名，这会让 WFWG 客户端感到困惑。然而，这个问题可以很容易地修复。

首先，你应该创建一个名为 smb.conf.WFWG 的新 smb.conf 文件（请注意 WFWG 的大小写）。在此文件中，输入以下内容：

```
[global]
case sensitive = no
mangle case = yes
mangled names = yes
default case = upper
preserve case = no
short preserve case = no
```

