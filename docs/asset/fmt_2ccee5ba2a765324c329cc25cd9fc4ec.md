
在前面的示例中，`apache2` 软件包的期望状态为清除 (p)，状态为未安装 (n)，该软件包未安装在系统中，且系统上没有配置文件。`apache2-common` 软件包的期望状态为移除 (r)，且目前仅安装了其配置文件 (c)。对于 `apache2-doc`，第一个字母表示软件包的期望状态为安装，第二个字母表示软件包当前状态为已安装在系统中。对于 `apache2-modules`，软件包的期望状态为未知 (u)，且未安装 (n)。更多 `--list` 命令的示例请参见第602 页。

### 表 14-1 dpkg 字母代码

| 字母 | 表示软件包处于 |
|---|---|
| **期望（选择状态）** | |
| u (unknown) | dpkg 未知 |
| i (install) | 等待安装 |
| r (remove) | 将移除（卸载），但保留配置文件 |
| p (purge) | 将移除，包括配置文件 |
| h (hold) | 不由 dpkg 处理 |
| **状态 (软件包状态)** | |
| n (not installed) | 未安装 |
| i (installed) | 已安装 |
| c (config-files) | 未安装；系统中仅存在配置文件 |
| u (unpacked) | 已解压，但未配置 |
| f (failed-config) | 已解压但未配置；配置失败 |
| h (half-installed) | 部分安装；安装未完成 |

# dpkg --install: 安装软件包

`dpkg --install (-i)` 命令用于解压并设置（第599页）存储在 `.deb` 文件中的软件包。它不会从互联网上搜索并下载软件包。我们使用 `aptitude`（第592页）来实现这一目的。下面的示例显示了 dpkg 安装 `fptd` 软件包：

```
$ dpkg --install /var/cache/archives/ftp_0.17-16_i386.deb
Selecting previously deselected fptd package.
(Reading database ... 17365 files and directories currently installed.)
Unpacking fptd from .../archives/ftp_0.17-16_i386.deb) ...
Setting up fptd (0.17-16) ...
```

`dpkg --remove (-r)` 命令移除已安装的软件包，但保留其配置文件。如果你决定重新安装该软件包，保留这些文件可能会很有用。使用 `purge (-P)` 完全移除软件包，包括配置文件。以下命令显示了 `fptd` 软件包的状态（它已安装）：

```
$ dpkg --list fptd
Desired=Unknown/Install/Remove/Purge
Status=Not/Installed/Config-files/Unpacked/Failed-config/Half-installed
| Err=(none)/Hold/Reinst-required/X-both-problems (Status,Err: uppercase-bad)
|| Name Version Description
=================================================
ii fptd 0.17-24 FTP server
```

下一个命令移除 `fptd` 软件包，但保留其配置文件：

```
(Reading database ... 113325 files and directories currently installed.)
Removing fptd ...
```

```
$ dpkg --list fptd 显示 `fptd` 软件包的状态为 `rc`，表示它已被移除 (r)，但配置文件 (c) 仍然存在。
```

```
$ dpkg --list fptd
rc fptd 0.17-24 FTP server
```

最后，dpkg 清除了 `fptd` 软件包并显示状态为 `pn`（已清除，未安装）。

```
$ dpkg --purge fptd
(Reading database ... 113325 files and directories currently installed.)
Removing fptd ...
Purging configuration files for fptd ...
```

```
$ dpkg --list fptd
...
pn fptd <none> (no description available)
```

如果有软件包依赖于你正在移除的软件包，则命令将失败。在下一个示例中，dpkg 尝试移除 `apache2.2-common` 软件包但失败了，因为 `apache2-mpm-worker` 软件包依赖于 `apache2.2-common`：

```
# dpkg: Debian 软件包管理系统 60
sudo dpkg --remove apache2.2-common
dpkg: dependency problems prevent removal of apache2.2-common:
apache2-mpm-worker depends on apache2.2-common (=2.2.3-2.build1)
dpkg: error processing apache2.2-common (--remove)
dependency problems - not removing
Errors:
```

下一个命令移除 `apache2.2-common` 软件包，但保留其配置文件：

```
(Reading database ... 113325 files and directories currently installed.)
Removing apache2.2-common ...
```

```
$ dpkg --list apache2.2-common 显示 `apache2.2-common` 软件包的状态为 `rc`，表示它已被移除 (r)，但配置文件 (c) 仍然存在。
```

```
$ dpkg --list apache2.2-common
rc apache2.2-common 2.2.3-2.build1
```

最后，dpkg 清除了 `apache2.2-common` 软件包并显示状态为 `pn`（已清除，未安装）。

```
$ dpkg --purge apache2.2-common
(Reading database ... 113325 files and directories currently installed.)
Removing apache2.2-common ...
Purging configuration files for apache2.2-common ...
```

```
$ dpkg --list apache2.2-common
...
pn apache2.2-common <none> (no description available)
```

# BitTorrent 605

Tracker、peer（节点）、swarm（集群），BitTorrent 像其他 P2P 系统一样，并不使用专门的服务器。相反，服务器的功能由 tracker、peers 和 seeds（种子节点）共同承担。tracker 是一个允许客户端之间相互通信的服务器。每个客户端——当它下载了 BitTorrent 文件的一部分时被称为 peer，当它下载了整个 BitTorrent 文件时则被称为 seed——都充当了 BitTorrent 文件的额外来源。peers 和 seeds 合称为一个 swarm（集群）。在 P2P 网络中，集群中的成员会将它已经下载的 BitTorrent 文件上传给其他客户端。种子节点并没有特殊之处：一旦该 torrent 可以从其他种子处下载，它就可以随时被移除。

下载 BitTorrent 文件的第一步是定位或获取 torrent 文件，这是一个扩展名为 `.torrent` 的文件。torrent 包含了关于要下载的 BitTorrent 文件的相关信息（元数据），例如文件大小和 tracker 的位置。你可以通过访问 URI 获取 torrent，也可以通过 Web、电子邮件附件或其他手段获取。BitTorrent 客户端可以连接到 torrent，以获取 swarm 中其他成员的位置，从而从那里下载 BitTorrent 文件。

一旦你下载了 BitTorrent 文件（此时本地系统已成为一个 seed），良好的礼貌是允许本地 BitTorrent 客户端继续运行，以便 peers（尚未下载完整个 BitTorrent 文件的客户端）可以上传至少与你下载一样的信息。

## 前提条件

如有必要，请使用 `aptitude`（见第 585 页和第 592 页）安装 `bittorrent` 包。安装此包后，运行 `apropos bittorrent` 命令将显示 BitTorrent 工具程序列表。请使用 `/usr/share/doc/bittorrent` 获取更多信息。你可能想尝试 Bit Tornado，这是一个具有额外功能的实验性 BitTorrent 客户端（bittornado；访问 bittornado.com）。

由于 BitTorrent 工具程序是用 Python 编写的，可以在任何带有 Python 解释器的平台上运行，因此它们不依赖于系统架构。Python 安装在 `/usr/bin/python`，并包含在 Python 软件包中。

## 使用 BITTORRENT

`bdownloadcurses` 工具是一个提供图形界面的文本型 BitTorrent 客户端。一旦获取了 torrent，请执行如下命令，将示例中的 Ubuntu torrent 替换为你想要下载的 torrent：

```
$ bdownloadcurses gutsy-desktop-i386.iso.torrent
```

在上述命令中，torrent 指定了 BitTorrent 文件将保存为工作目录下的 `gutsy-desktop-i386.iso`。BitTorrent 文件的名称并不总是与 torrent 名称相同。在存在多个 torrent 的情况下，BitTorrent 文件可能存储在一个同样以 torrent 命名的目录中。图 14-1 显示了 `bdownloadcurses` 的运行情况。根据网络连接速度和种子的数量，下载大型 BitTorrent 文件可能需要几小时到几天不等。

### 606 第 14 章 下载与安装软件

![](img/556454b01d95450a92edff64b47580d6_652_0.png)

图 14-1 bdownloadcurses 正在处理 Ubuntu torrent

你可以通过按下键或 `CONTROL-C` 来停止下载 torrent。当你再次将 torrent 下载到相同位置时，下载将从上次中断的地方自动恢复。

### 确保你有足够的空间下载 torrent

某些 torrent 文件巨大。请确保你所在的分区有足够的空间来存放你正在下载的 BitTorrent 文件。

请查看 `bdownloadcurses` 页面以获取选项列表。最有用的选项之一是 `--max_upload_rate`，它限制了 swarm 从你处下载 torrent 时可以占用的带宽量。默认值为 0，意味着上传带宽没有限制。以下命令防止 BitTorrent 使用每秒超过 10 字节的上行带宽：

```
$ btdownloadcurses --max_upload_rate 10 gutsy-desktop-i386.iso.torrent
```

BitTorrent 通常允许 swarm 成员通过上传更多数据来获得更高的下载速率，因此如果你有空闲带宽，增加此值对你是有利的。你需要留出足够的上行带宽让你的 torrent 确认包能够通过，否则下载速度会变慢。默认情况下，`bdownloadcurses` 同时向最多七个其他客户端上传。你可以使用 `--max_uploads` 参数来更改此值，或者如果你通过调制解调器下载，请尝试设置 `--max_upload_rate 3 --max_uploads 2`。

BitTorrent 保存文件或多个文件的目录名称由 torrent 指定。你可以使用 `--saves` 选项指定不同的文件或目录。`btdmetainfo` 工具显示 Torrent 文件将保存的名称、大小、torrent 名称（元文件）以及其他信息：

```
$ btdmetainfo gutsy-desktop-i386.iso.torrent
btdmetainfo 2002107 - decode BitTorrent metainfo files
verno file: gutsy-desktop-i386.iso.torrent
info hash: 545738c65894f7ae5d4f7eb9a0f399796
file name: gutsy-desktop-i386
file size: 728713216 (1389 * 524288 + 477184)
```

## 安装非自由软件

（注：原文此处开始出现大量重复内容，已根据前文逻辑完成处理）

## wget: 非交互式下载文件

你可以通过以下命令行完成整个任务：

```
$ sudo ./configure && make && make install
```

逻辑“与”（AND）运算符 (`&&`) 允许在前一个命令返回成功退出状态时，才允许执行后续命令。

## wget: 非交互式下载文件

`wget` 工具是一个非交互式命令行，它使用 HTTP、HTTPS 或 FTP 从网络检索文件。在接下来的示例中，wget 下载了 Ubuntu 首页（命名为 `index.html`）到工作目录下的一个文件中：

```
$ wget http://www.ubuntu.com/
--14:58:48-- http://www.ubuntu.com/
=> 'index.html'
Resolving www.ubuntu.com... 82.211.81.158
Connecting to www.ubuntu.com|82.211.81.158|80...
HTTP request sent, awaiting response... 200 OK
Length: 13,112 (13K) [text/html]
100%[=================================>] 13,112    40.60K/s
14:58:49 (40.40 KB/s) - 'index.html' saved [13112/13112]
$
```

使用 `--recursive (-r)` 选项，wget 会下载你指定的 URI 下的目录层次结构。请谨慎使用此选项，因为它可能会下载大量数据（可能会完全填满你所在的分区）。`--background (-b)` 选项在后台运行 wget，并将其标准错误重定向到名为 `wget-log` 的文件中：

```
$ wget --recursive --background http://www.ubuntu.com
Continuing in background, pid 28839.
Output will be written to 'wget-log'.
$
```
