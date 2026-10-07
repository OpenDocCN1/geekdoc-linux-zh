
此命令使用了 `rsync` 的多个选项，并将它们放在一个快速易于运行的脚本中。你可以从命令行使用 `sudo sh ./backup.sh` 运行脚本，或者作为自动的 cron 任务运行。

以下是发生操作的概述。基本上，`rsync` 被告知要执行：以下是各个选项：

- `-force`: 强制删除。
- `-ignore-errors`: 告诉即使有 I/O 错误也继续。
- `-delete`: 删除目录。
- `-delete-excluded`: 也删除被排除的目录。
- `-exclude-from=/home/matthew-exclude.txt`: 防止备份文件中列出的文件。
- `-backup`: 在删除之前创建备份。
- `--backup-dir='+Y-%m-%d'`: 为日期创建一个备份目录。
- `-av`: 使用归档模式和详细模式。
- `/`: 表示源目录。
- `/media/externaldrive/backup/Seymour`: 设置备份的目标地。

## 配置文件的版本控制

能够快速方便地执行此操作具有巨大的权力和优势；不再需要文件编辑器记住关于谁、何时、甚至如何编辑了文件的技术细节。当问题发生时，文件只需恢复到之前的状态即可。版本控制系统还能通知用户每次保存时每个文件在何时以及如何发生了什么变化。

对配置文件使用版本控制系统意味着每次更改配置时，这些更改都会被记录和跟踪。这使得能够发现入侵者（如果配置被未经授权的人更改以重置，例如更改 Apache 的设置以便允许入侵者在你的服务器上运行恶意的 Web 服务或站点）、从错误和故障中恢复，并轻松发现软件升级在配置中启用或包含的新功能和设置。

许多旧且著名的工具都能完成此任务，例如 `changelelograck` 就是一个很好的例子。所有此类工具都能让跟踪配置更改的工作变得更加简单、快速，但随着版本控制系统的进步，它们提供的额外作用非常小。与其使用其中任何工具，你认为学习一个现代且良好的版本控制系统会更好。有一个例外值得讨论，因为它能够与你的软件软件包管理器协同工作，这节省了你每次运行包管理器时都要将更改提交到版本控制系统的任务。这个例外就是 `etckeeper`。

`etckeeper` 获取 `/etc` 目录的所有内容，并将其配置文件存储在版本控制仓库中。你可以通过编辑 `etckeeper.conf` 来配置程序，将数据存储在 Git、Mercur、Bazaar 或 Subversion 仓库中。此外，`etckeeper` 会自动连接到 Ubuntu 的 APT 软件包管理工具，并在软件包升级期间自动提交对 `/etc` 及其文件的更改。在运行 Fedora 等 Linux 发行版时，也可以跟踪 Yum 等其他包管理器。它还会跟踪版本控制系统不易跟踪的文件元数据，例如 `/etc/shadow` 中的权限。

> 注意
> 使用任何版本控制系统跟踪包含密码等敏感数据的文件都存在安全风险。被跟踪的文件和版本控制系统本身应该受到与敏感数据本身同级别的对待。

默认情况下，`etckeeper` 使用 Git。在 Ubuntu 上，这被改为 Bazaar `bz`，因为这是 Ubuntu 开发者使用的版本控制系统。由于这是可配置的，我们在这里只提到步骤，留给你根据自己喜好的特定版本控制系统进行调整。

首先，编辑 `/etc/etckeeper/etckeeper.conf` 以使用你所需的设置，如要使用的版本控制系统、使用的包管理器，以及是否每天自动提交更改。从 Ubuntu 仓库安装 `etckeeper` 后，必须从命令行启动它：

```
matthew@seymour:-$ etckeeper init
```

## 第 17 章 备份

如果你仅使用 `etckeeper` 来跟踪使用 APT 更新软件时对 `/etc` 做的更改，那么你什么都不需要做。如果你手动编辑文件，请确保使用你的版本控制命令来提交这些更改，或者使用以下命令：

```
matthew@semour:- etckeeper commit "Changed prompt style"
```

引号中的消息应该反映刚刚完成的更改。这使得读取日志和查找准确更改变得容易得多。

恢复可回滚的文件随后直接使用你的版本控制系统完成。例如，假设你对 `/etc/bash.bashrc`（设置 bash shell 默认值的文件）进行了更改。你在某处读到过如何更改提示符，但不喜欢那个结果。然而，由于更改正在被跟踪，你可以将其回滚到之前的版本。由于 bzr 是 Ubuntu 中 etckeeper 的默认值，你检查日志以找到以下更改的提交号：

```
revno: 2

committer: matthew <matthew@semour>

branch nick: semour etc repository

tstamp: Pri 2021-07-16 11:08:22 -0700

message:

 Changed /etc/bash.bashrc

revno: 1

committer: matthew <matthew@semour>

branch nick: semour etc repository

tstamp: Pri 2021-07-16 11:00:16 -0700

message:

 Changed /etc/bash.bashrc
```

如果你知道更改是在最近的修订中完成的（用 `revno 2` 表示修订版本号），你可以恢复到：

```
matthew@semour:- bzr revert -revision 2 /etc/bash.bashrc
```

今天，程序员、系统管理员和开发者使用版本控制备份他们的点文件（dotfiles）。点文件是用户 `/home` 目录下的配置文件和目录，所有这些文件都以点开头，例如 `.bashrc`。这些文件并不一定会被软件备份，它们通常由高技术水平的人根据自己的喜愿进行定制，因此备份它们是一个好主意。版本控制系统被广泛用于 Ubuntu 的程序 `dotdee` 对包含 `.d` 且存储在 `/etc` 中的不同类型文件或目录执行此操作。你可以在第 9 章“管理设置”中找到关于 `dotdee` 的更多信息。

## 系统救援

总会有需要进行系统救援工作的时候。这种需求出现在系统甚至无法启动 Linux 导致你无法恢复任何文件时。这个问题最常见与引导程序或分区表有关，但也可能是关键系统文件被无意删除或损坏了。

## 第 18 章

## 网络

开源技术通用（特别是 Linux）的优势之一是它可以毫不费力地跨多个网络环境和互联网。得益于标准互联网协议 TCP/IP 的强力支持，Linux 可以与所有 UNIX 变体通信，包括 macOS、Windows（借助 Samba）、NetWare `IPX`，甚至是如 DCNet 和 Banyan VINES 等较旧协议。大多数组织使用 Linux 作为互联网网关，允许许多不同的客户端通过 Linux 访问互联网，并通过电子邮件和即时消息进行通信。最重要的是它对 IPv6 的内置支持，这在商业/企业世界中已成为一项重大的更新。可以说，无论你遇到什么种网络协议，Linux 都能以某种方式与之工作。

本章涵盖了网络连接性，而大多数网络不可避免地会以某种形式连接到互联网。你将学习如何正确完成基础工作，包括在 Ubuntu 中配置和管理网络接口卡（NIC）以及其他网络服务。你还将了解如何从命令行管理网络服务——这在你可能受限于命令行提示符时非常重要。我们还查看了针对入站和出站流量的连接选项，例如点对点协议（PPP）。

在本章中，我们重点关注文本接口和手动配置。我们还包含了 Ubuntu 中基本图形化网络管理的概述，这正变得越来越流行。图形用户界面（GUI）选项已变得更加稳定、有用且易理解，大多数桌面用户现在使用 GUI 与网络进行交互。然而，这是一本为想要学习系统原理的用户设计的，所以请卷起袖子，准备大干一场。

### 本章内容

- 建立基础：localhost 接口
- 使用 `ping`、`traceroute` 和 `mtr` 检查连接
- 使用 TCP/IP 联网
- IPv6 基础
- 网络组织
- 网络硬件设备
- 使用网络配置工具
- 动态主机配置协议
- 无线网络
- 越网络进入互联网
- 常见配置信息
- 参考文献

### 建立基础：localhost 接口

在成功连接到互联网或任何网络之前，首先需要就绪一个 localhost 接口，有时称为回环接口（loopback interface），通常称为 `lo`。TCP/IP 协议族（参见本章稍后提到的“使用 TCP/IP 联网”章节）使用此接口为你的计算机分配 IP 地址，并且 Ubuntu 分配 PPP 接口也需要它。

#### 检查回环接口的可用性

通常你不需要手动创建回环接口，因为 Ubuntu 会自动为你创建一个。要检查它是否处于启动状态，可以使用 `ip` 命令配合几个参数列出所有可网络接口，包括如果存在 `lo` 接口。此示例显示了信息：

```bash
$mathew@semour~$$ ip address

lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000

    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

    inet 127.0.0.1 scope host lo

        valid_lft preferred_lft forever

    inet6 ::/128 scope host

        valid_lft preferred_lft forever
```

你在示例中看到的内容是回环接口存在且活跃的证据。分配给 localhost 的 inet 号（通常为 127.0.0.1）广播掩码为 255.255.0.0。你也可以看到分配给 `lo` 的 IPv6 地址，即 `::/128`，称为 `inet6`。

> 注意
> 之前你使用现在已弃用的 `ifconfig` 检查了回环接口的可用性：
> ```
> $mathew@semour~$ ifconfig
> lo Link encap:Local Loopback
>     inet addr:127.0.0.1 Mask:255.255.0.0
>     inet6 addr::/128 Scope:Host
>     UP RUNNING MTU:16436 Metric:1
>     RX packets:270 errors:0 dropped:0 frame:0 carrier:0
>     TX packets:270 errors:0 dropped:0 collisions:0 txqueuel:0
>     RX bytes:20748 (20.7 KB) TX bytes:20748 (20.7 KB)
> ```
> `ifconfig` 仍然可用，但它正在消失，并且不再默认安装。如果你已经学会了 `ifconfig`，我们强烈建议花时间学习 `ip` 并取而代之。

#### 手动配置回环接口

localhost 接口的 IP 地址指定在一个文本配置文件中，Ubuntu 使用该文件记录各种网络范围的 IP 地址。该文件名为 `/etc/hosts`，通常在系统中都存在，即使它是空的。Linux 内核和其他工具使用此文件访问 IP 地址和主机名。如果你没有配置任何其他接口，你可能会发现文件看起来所示：

```text
127.0.0.1 localhost
127.0.0.1 seymour
```

```text
# 以下行对于支持 IPv6 的主机是理想的
::1 localhost ip6-localhost ip6-loopback
fe00::1 ip6-local
ff00::1 ip6-multcastprefix
ff00::1 ip6-multicast
```
