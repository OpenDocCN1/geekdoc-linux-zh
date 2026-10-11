
在此示例中，NFS 驱动器是服务器 `mmcune` 上的目录 `/mnt/home/alisa`。`rsize` 和 `wsize` 为 4096 字节，并设置了 `hard` 和 `intr` 选项。`dump` 和 `fsck` 都被设置为 0，因为这不是本地驱动器。

## 16.3 在 Windows 上使用 NFS

任何版本的 Windows 都没有内置 NFS 支持，尽管有许多附加程序允许 Windows 充当 NFS 服务器或客户端。两个著名的商业软件包是 Hummingbird 的 NFS Maestro 和 NetManager 的 Chameleon NFS。微软还为 Windows NT 制作了一个“Windows for UNIX”附加包。还有十几个其他软件包，每个包都有其优缺点。我不会涵盖所有它们，但我将为你提供一个如何实现 NFS 的概述。大多数为 Windows 制作 NFS 软件的公司都提供评估版，因此你可以在决定是否使用之前先查看该软件包。

我将介绍微软的“Windows for UNIX”附加包，因为这个包经常安装在 NT 机器上，并且在混合 Windows 和 Linux（或 UNIX）环境中是必须的。

### 16.3.1 在 Windows NT 上设置 NFS 服务器

要在 Windows NT 机器上创建 NFS 共享，请控制面板并选择要共享的驱动器或目录。NT 上的驱动器在 NFS 共享中显示为 `/drive/`。例如，NT 上的 `D:` 盘在 NFS 共享中显示为 `/D/`。你可以使用别名（`aliases`）使名称更易于管理。例如，共享驱动器 `/D/public/user/share` 可以别名为 `share` 以便于记忆。别名的唯一问题是，别名在生效之前需要重启服务器。

你还可以在 NFS 共享上设置客户端组。这简化了 NFS 共享的管理，因为它允许以组为单位对用户进行管理。请注意 `sec`

### 16.3.2 设置 NFS 客户端

在 Windows 上设置 NFS 客户端。使用 Windows for UNIX 附加包。首先，在控制面板中选择。在 NFS 共享上，使用 Network Information Services (`NIS`) 或 NFS Daemon (`NFSD`)。首先，设置 NFS 客户端。如果你使用 `NIS`，选择。下一步，选择 NFS 客户端。像 Linux 客户端一样，硬挂载通常更好。Windows NFS 客户端也支持版本 3。如果 NFS 服务器支持版本 3，这将提供显著的性能提升。缺点是 NFS 服务器崩溃会导致。

名称映射在混合 Windows 和 Linux 环境中非常重要。Linux 区分大小写，而 Windows 将它们视为相同。例如，Linux 会认为 `Sample.txt` 和 `sample.txt` 是不同的文件名，但 Windows 会认为它们是相同的文件。有几种方法设置名称映射，但最简单的方法让 Windows 客户端在读取时忽略大小写。

NFS 客户端支持服务器上的符号链接（`symbol links links` 符号链接指向另一个文件的文件。它类似于 Windows 上的快捷方式。它可以指向本地文件，甚至是另一台机器。默认情况下，Windows 客户端不会解析或删除未解析链接。它不允许重命名或删除符号链接。除非你有理由，否则不要更改。重命名或删除符号链接除非你理解符号链接的工作原理。例如，如果你删除一个符号链接并创建一个同名的文件，它就不再是符号链接。你将有两个文件，而不是一个指向另一个文件。

### 16.3.3 使用 Windows 连接到 NFS 服务器

你可以通过在客户端输入 `show mounts <servername>` 来查找服务器上的 NFS 共享。然后可以使用 Windows 语法或 UNIX 语法连接到共享。例如，服务器 `mmcune` 上的 `home` 共享可以从命令行以两种不同的方式挂载。这样做是为了兼容 UNIX 和 Windows 系统。

```
use * \mmcune\home (使用 Windows 语法)
```

```
use * mmcune:/home (使用 UNIX 语法)
```

一旦完成，共享看起来和用起来就像系统上的任何其他网络驱动器一样。

Windows 和 Linux 的模型是不同的。Windows 用户可以属于多个组，而 Linux 用户一次只能属于一个组。这通常不会引起任何问题，但在某些情况下，它可能会导致问题。如果这是一个问题，你可以使用 `chgrp` 来更改组 ID。

Windows for UNIX 提供了名称映射服务。它作为标准服务运行，并将 UNIX ID (`UIDs`) 映射到 Windows ID (`SIDs`)。它在下表中的表中维护映射：

| Windows Username | Windows Domain | UNIX Username | UNIX Domain | UID/GID |
| :--- | :--- | :--- | :--- | :--- |
| JohnDoe | Indwinds | Johnd | Indux | 1090/2 |
| Maryjane | Indwinds | Maryj | Indux | 223/1 |

Windows 有几种商业化的 NFS 实现。它们的优势是可以在 Windows 95/98 下运行。其中一些商业程序包括 Hummingbird Maestro (`http://www.hummingbird.com/products/nfs/`)、NetManager (`http://www.netmanage.com/products/`)、Omni NFS (`http://www.xlink.com`) 和 Access NFS (`http://www.ssc.com`)。如果你想尝试，这些商业程序在他们的网站上提供了演示。

有一个免费的 Windows NFS 实现叫做 `NFSnt`。它没有商业程序那样的功能，但非常易于安装。它在 `http://www.com` 可以找到。它是开源的，因此可以。

# 在 Linux 上设置 NIS 服务器

用于共享 NFS 挂载。对于 Windows 客户端来说，该 NFS 共享 `own` 就像服务器上的普通共享。

对于 Windows NT，你将需要诸如 Hummingbird NFS Maestro Gateway、Access NFS Gateway 和 Reflections NFS Gateway 等程序。这些程序允许 Windows 机器通过运行网关软件的 Windows NT 机器连接到 NFS 导出。

## 16.3.5 NFS 安全

有许多广泛使用的工具可以利用 NFS 的安全漏洞。任何与外部的连接都应该通过防火墙或其他安全设备进行。

这不一定是 NFS 的功能，但是一个良好的通用安全策略。编辑 `/etc/inetd.conf` 文件并注释掉任何你不需要的服务。任何服务都代表着潜在的安全风险。例如，`logind` 和 `rexec` 允许你登录并执行远程程序。如果这些很方便但你不需要，请注释掉下面的代码：

```
#shellstreamtcpnowaitaitroot/usr/sbin/tcpd.rshd
```

```
#loginstreamtcpnowaitaitroot/usr/sbin/tcpd.rlogind
```

```
#execstreamtcpnowaitaitroot/usr/sbin/tcpd.rexec
```
