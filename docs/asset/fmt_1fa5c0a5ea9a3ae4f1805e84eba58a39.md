
`-O`（或 `--remote-name`）选项是绝对要求的。如果不使用它，`curl` 会将下载输出写入到标准输出（`STDOUT`），这意味着你的终端将迅速充满无法使用的乱码。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们对 `curl` 的了解仅仅冰山一角。它的帮助页面（man page）虽然没有 `wget` 那么长，但也充满了如果你想充分利用 `curl` 时所需要阅读的有用信息。请将其视为必读。

# 结

本章中的命令是我个人最喜欢的一些，因为它们让我能够完成其他情况下会极其乏味、不安全或困难的任务。所有这些命令让网络成为你数据、程序和想象力的另一个途径，而这正是 Linux 闪光的地方。通过让用户免费使用如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 促进了创新和安全，这在许多人被迫使用的其他操作系统上是不可能的。投入学习 `ssh`，这样你就可以安全地连接到其他计算机，掌握 `rsync` 实现安全自动备份，并依靠 `wget` 和 `curl` 以尽可能高效的方式下载所需内容。你会庆幸自己这么做的！

# 第 16 章 Windows 网络

`Samba` 是世界上最重要的开源项目之一，因为它让 Linux（以及其他 Unix 机器，如 Mac OS X）可以使用服务器区块（`SMB`），这是所有 Microsoft Windows 机器使用的网络协议。通过 `Samba`，Unix 机器可以连接并挂载 Windows 机器上的共享，并连接到 Windows 机器上的共享打印机打印。Unix 机器还可以建立基于 `Samba` 的打印机和文件共享供 Windows 机器连接和使用。事实上，`Samba` 如此有用，以至于你甚至不需要 Windows 机器。你可能会选择在 Linux 机器网络上实现 `Samba` 文件和打印机共享，因为它工作得非常出色。

许多优秀书籍涵盖了如何在服务器上设置 `Samba`，因此我们不会介绍管理类命令，如 `smbd`、`smbcacl` 或 `smbpasswd`（确实，普通用户可以运行它们来更改自己的密码，但在实践中几乎总是由 `Samba` 服务器管理员运行），或者如何配置 `smb.conf`。相反，本章假设你已经在 Windows、Linux 或 Mac OS X 机器上设置了 `SMB` 共享。你将专注于客户端工作：如何找到这些共享的位置，如何连接这些共享，以及如何在你的硬盘上挂载共享。

**提示**：关于设置和管理 `Samba` 的一些优秀书籍

- `Sams Samba Unleashed`, ISBN: 0672318628; Steve Litt 著
- `Sams Teach Yourself Samba in 24 Hours`, 第2版, ISBN: 0672322692; Gerald Carter 著
- 位于 `http://samba.org/samba/docs/man/Samba-HOWTO-Collection/` 的官方 `Samba`-3 `HOWTO` 和参考指南非常出色。

## 发现工作组的主浏览器

```
nmblookup -M [Master Browser]

nmblookup -S [NetBIOS name]

nmblookup -A [IP address]
```

`Samba` 服务器实际上使用两个守护进程：`smbd` 提供共享可用，`nmbd` 将标识使用 `SMB` 机器的 `NetBIOS` 名称映射到其 IP 地址，从而使查找和浏览 `SMB` 共享成为可能。你现在将专注于与 `nmbd` 通信的命令，用于获取有关你查询的 Windows 工作组的概览信息。

**注意**：以下示例假设你使用的是 Windows 工作组，而不是域。工作组本质上是一小组机器，它们通过工作组成员的自我身份标识来识别为相互所属。域使用中央服务器（或大型网络中的几台服务器）来验证想要加入网络的计算机和用户。域是庞大、棘手复杂的怪兽，你最好参考本文提到的书籍。

要找到你工作组的主浏览器（Master Browser），请使用带有 `-M` 选项的 `nmblookup` 命令：

```
nmblookup -M [Master Browser]
```

要找到特定机器的 `NetBIOS` 名称，使用 `-S` 选项：

```
nmblookup -S [NetBIOS name]
```

要找到与 `NetBIOS` 名称关联的 IP 地址，使用 `-A` 选项：

```
nmblookup -A [IP address]
```

## 查询和映射 NetBIOS 名称与 IP 地址

```
nmblookup -T
```

你可以使用 `nmblookup` 作为快速查找任何通过 `Samba` 共享文件和打印机的方法。在命令后加上 `-T` 选项，后面跟上 `"*"`（是的，你必须包含引号，告诉 shell 你没有将 `*` 作为代表当前工作目录文件的通配符）。

```bash
$ nmblookup -T "*"

querying * on 192.168.1.255

192.168.1.151 *<0>

192.168.1.104 *<0>

192.168.1.10 *<0>
```

此局域网上有三台开启 `Samba` 共享的机器。要找出其中哪些是主浏览器（Master Browsers），请参考上一节；要列出每台计算机提供的共享列表，请继续下一节。

## 列出机器的 Samba 共享

```
smbclient
```

通过上一节概述的命令，你已经知道某台机器上有 `Samba` 共享，但你并不知道这些共享是什么。`smbclient` 命令是一个多功能工具，可用于连接到共享并对其操作；然而，在更简单的层面，它也可以列出计算机上可用的共享。只需使用 `-L`（或 `--list`）选项，后跟 `NetBIOS` 名称或 IP 地址。当提示密码时，直接按回车即可。

```bash
$ smbclient -L ELIOT

Password:

Anonymous login successful Domain=[TURING] OS=[Unix] Server=[Samba 3.0.14a-Ubuntu
```

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| print$ | Disk | 打印机驱动程序 |
| documents | Disk | 共享演示文稿 |
| IPC$ | IPC | IPC 服务 |
| ADMIN$ | IPC | IPC 服务 |

在这种情况下，你可以看到所有匿名登录可用，或者在服务器的 `smb.conf` 文件中被标记为可浏览的共享。如果你想查看你的可用共享，请添加 `-U`（或 `--user`）选项，后跟你在 `Samba` 服务器上找到的用户名。

**注意**：你的 `Samba` 用户名可能与你在 Linux（或 Windows 或 Mac OS）服务器上的用户名不同。你需要在 `Samba` 服务器上查看。

```bash
$ smbclient -L ELIOT -U scott

Password:

Domain=[ELIOT] OS=[Unix] Server=[Samba 3.0.14a-Ubuntu]
```

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| print$ | Disk | 打印机驱动程序 |
| documents | Disk | 共享演示文稿 |
| IPC$ | IPC | IPC 服务 |
| ADMIN$ | IPC | IPC 服务 |
| scott | Disk | 目录 |

登录后，你现在可以看到一个新的共享 `scott` ——该用户的家目录。这还告诉你你可以登录，进入下一节，在其中登录并实际使用共享上的内容。

> **提示**：如果你想测试在 `Samba` 服务器上创建的共享，极好的方法是在该机器上打开 shell，然后输入：

```bash
$ smbclient -L localhost
```

当提示密码时，按回车。通过这种方式你可以快速查看添加的新共享是否可用。当然，如果你没有将共享设置为开放浏览，你将需要使用 `-U` 选项登录用户。

## 使用类 FTP 客户端访问 Samba 资源

在知道 `Samba` 服务器上的可用共享后，你可以登录并开始使用它们。使用 `smbclient` 命令，格式如下：

```bash
smbclient //server/share -U username
```

你不能直接登录服务器；相反，你需要登录服务器上的某个共享。要访问密码保护的项目（建议对你的共享进行密码保护），你需要指定用户。要访问服务器 `ELIOT` 上的 `documents` 共享，使用：

```bash
$ smbclient //eliot/documents -U scott

Password:
```
