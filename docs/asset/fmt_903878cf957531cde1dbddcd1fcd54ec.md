
| PID TTY STAT TIME COMMAND |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ? | S | 0:05 | [5] |
| 2 | ? | SWN | 0:00 | [ksoftirqd/0] |
| 3 | ? | SW | 0:00 | [events/0] |
| 4 | ? | SW | 0:00 | [blockd/0] |
| 5 | ? | SW | 0:00 | [pdfflush] |
| 6 | ? | SW | 0:00 | [pdfflush] |
| 8 | ? | SW | 0:00 | [aio/0] |
| 7 | ? | SW | 0:00 | [kswapod] |
| 9 | ? | SW | 0:00 | [kseriod] |
| 13 | ? | SW | 0:00 | [kjjournal] |
| 98 | ? | SW | 0:00 | [thudbd] |
| 222 | ? | SW | 0:00 | [usb-storage] |
| 223 | ? | SW | 0:00 | [scsi_eh_0] |
| 759 | ? | SW | 0:00 | [journal] |
| 2177 | ? | S | 0:00 | [/sbin/dhclient -1 -q -lf] |

```
/var/lib/dhcp/dhclient-eth0.pid -cp /var/run/dhclient-eth0 -cf /etc/dhclient.conf eth0
2226 ? S 0:00 syslog -m 0
2230 ? S 0:00 klod -x
2258 ? S 0:00 portmap
2278 ? S 0:00 rpc.statd
... lines deleted ...
```

即使只有一个用户登录，系统上也能运行这么多程序，这真令人惊讶，不是吗？

正如你所猜的，你可以从 Shell 提示符做任何事情，但这确实需要一些适应。

### 关机

当你准备好关闭 Fedora Core 时，必须以有序的方式进行。即使你是 Fedora Core PC 的唯一用户，后台还有其他几个程序在运行。此外，像 Linux 这样的操作系统会尝试优化向磁盘写入数据。由于磁盘访问相对缓慢（与访问内存位置所需的时间相比），数据通常保留在内存中并分大块写入磁盘。因此，如果你简单地关闭电源，就有某些文件没有更新的风险。

任何用户（你甚至不需要登录）都可以从桌面或图形登录界面关机。选择主菜单（Main Menu）→注销（Log Out）。会出现一个注销框，提供重启或停止系统或直接注销的选项。要关机系统，只需选择关机（Shutdown），并点击确定（OK）。系统将有序地关机。

如果你在图形登录界面，点击屏幕底部关机（Shutdown）标签。然后另一个对话框会要求你确认是否真的想停止系统。点击是（Yes）按钮。系统将有序关机。

当系统关机时，你会看到关于进程关闭的消息。你可能会对有这么多进程感到惊讶，即使没有人在系统上显式运行任何程序。如果你的系统在关机时没有自动断电，你可以手动关闭电源。

![](img/d9230b719dc0efd80851f363d8c6f571_124_0.png)

> 注意，关机和重启系统*不需要 root 权限*。

# 第 5 章：Core 安装

**在本章中**

- 加入 BitTorrent
- 刻录 Core CD
- 准备 Core DVD
- 网络安装 Core

你是否曾希望过通过 BitTorrent 刻录 Core？关于 Core DVD 你好奇吗？你想知道通过网络安装 Core 如何？好吧，有一些项目可以帮助你下载 Core。第一个项目是加入 BitTorrent 并下载必要的。事实上，一旦你尝试它，你会发现通过 BitTorrent 获取 Core 比通过 FTP 容易。BitTorrent 是一种下载文件的协议。你不需要理解该协议就能使用 BitTorrent。你只需要知道你在下载文件，同时也分享给其他人。这种共享方式让 BitTorrent 成了一种非常有吸引力的 Core 下载方式。在使用 BitTorrent 之前，你需要做一些事情。第一个项目是加入 BitTorrent 并下载 Core 的 CD 镜像。

## 加入 BitTorrent

要加入 BitTorrent，你需要以下内容：

- 一台运行 Red Hat Linux 或 Fedora Core 的 PC —— 你使用该系统来运行 BitTorrent。如果你在 PC 上运行 Microsoft Windows，仍然可以使用 BitTorrent；只需查看 `bitconjurer.org/` 上的信息。
- 确保你的 Linux 系统已安装了 Python 2。如果没有，插入配套 DVD，挂载它，并输入 `rpm -ivh /mnt/cdrom/Fedora/RPMS/python-2*.rpm` 来安装 Python 2。
- 网络连接，带宽越高

### 需要遵循的步骤

你有三个高级别的步骤需要遵循：

1. 在系统上下载并安装 BitTorrent 客户端。
2. 调整你的系统防火墙设置，开放 BitTorrent 用于向他人发送文件的 TCP 端口 `6881` 到 `6999`。
3. 运行 BitTorrent 客户端开始文件传输。

我将在后续章节详细描述这三个高级步骤。

### 下载并安装 BitTorrent 软件

确保你的互联网连接正常。然后按照以下步骤操作：

1. 运行 Mozilla 浏览器并访问 `torrent.duke.edu/btmps`，点击一个 RPM 文件下载适用于 Red Hat Linux 或 Fedora Core 的 BitTorrent 软件。对于 Core，下载带有 `fc1`（代表 Fedora Core 1）或 `rh90`（名称中代表 Red Hat 9.0 —— 这些版本运行在 Fedora Core 上）的版本。将下载的 RPM 文件保存到系统的目录中并记住保存位置。
2. 打开终端窗口并切换到保存 BitTorrent RPM 文件的目录，然后安装 BitTorrent 软件。

输入以下命令安装 BitTorrent：

```
rpm -ivh bitstorrent*.rpm
```

### BitTorrent 入门教程

如果你没有在 `torrent.dulug.duke.edu/btrprms/` 找到正确的 BitTorrent RPM 文件，你始终可以从 BitTorrent 官方主页 `bitconjur.org/BitTorrent/` 下载文件。例如，要下载并安装 BitTorrent 3.3，请打开终端并输入以下命令：

```
wget http://bitconjur.org/BitTorrent/BitTorrent-3.3.tar.gz
tar -xzf BitTorrent-3.3.tar.gz
```

在这种情况下，BitTorrent 软件被安装在当前目录下的 `BitTorrent-3.3` 子目录中，你需要从该子目录运行 BitTorrent 客户端。

### 打开 BitTorrent 使用的入站 TCP 端口

通常，你的系统运行着防火墙，限制了对许多端口的访问。然而，BitTorrent 需要你开启 TCP `6881` 到 `6999` 端口，以便 BitTorrent 客户端能够连接你的系统并请求更新。要打开 TCP `6881` 到 `6999` 端口，请在终端窗口中输入以下命令：

```
iptables -I RH-Firewall-1-INPUT --protocol tcp --dport 6881:6899 -i eth0 -j ACCEPT
```

此命令假设你的系统通过以太网接口连接互联网，且接口为 `eth0`（第一块网卡）。请将 `eth0` 更改为你系统的外部网络接口名称。例如，如果是第二个网卡，接口则为 `eth1`。对于拨号连接，接口为 `ppp0`。

### 开始 BitTorrent 传输

要下载 BitTorrent，你必须运行 BitTorrent 客户端。使用 URL 下载 torrent，torrent 指你想要下载的文件集合。该 URL 还标识了追踪器（tracker）——该服务器将你的系统 BitTorrent 客户端与其他提供你想要的文件部分的客户端连接起来。反之，追踪器也允许其他客户端从你的系统请求该 torrent。

按照以下步骤下载 Fedora Core torrent 之一：

- 1 访问 `torrent.dulug.duke.edu` 上的 Fedora Core 追踪器。

你可以在该网站上找到不同的 torrent 文件列表。找到你想要的文件。例如，如果你计划刻录 Fedora Core CD，你需要 Fedora Core 二进制操作系统镜像的 torrent。

## 102 加入 BitTorrent

- 2 打开终端窗口并切换到你想要存储计划下载的文件的目录。
- 3 运行 BitTorrent 客户端。

输入以下命令，其中 `tfile` 替换为你想要的 torrent 文件名：
