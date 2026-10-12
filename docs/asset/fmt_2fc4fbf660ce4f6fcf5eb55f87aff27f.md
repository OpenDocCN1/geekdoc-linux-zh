
`$ sudo dpkg --list "apache2"`

```
Desired-unmark/Install/Remove/Purge/Hold

/Failed-config/Half-installed

| Err--(none)/Hold/inst-required-X-both-problem (Status,Err: uppercase)

|/ Name Version Description

=================================================

apache2                  <none> (no description available)

apache-common           2.2.14-ubuntu4 (generation, scalable, extendable web...

apache2-doc             2.2.14-ubuntu4 (documentation for apache2

apache2-modules         <none> (no description available)

apache2-mpm-prefork     <none> (no description available)

apache2-mpm-thread      <none> (no description available)

apache2-mpm-worker      <none> (no description available)

pn-utils            <none> (no description available)
```

在以下示例中，`apache2` 软件包的期望状态为已清除（`p`），且状态为未安装（`n`），这意味着该软件包未安装，但在系统中留有配置文件。`apache-common` 软件包的期望状态为已移除（`r`），且当前（`r`）仅安装了配置文件（`c`）。对于 `apache2-doc`，第一个 `i` 表示软件包的期望状态为已安装，第二个 `i` 表示软件包的当前状态为已安装（软件包已安装在系统中）。对于 `apache2-modules`，软件包期望状态为未知（`u`）且未安装（`n`）。更多关于 `--list` 命令的示例请参见第 536 页。

### 表 13-1 dpkg 表示软件包为

| 字母 Desired（选择状态） | |
|---|---|
| `u` (unknown) | dpkg 未知 |
| `i` (installed) | 将要安装 |
| `r` (remove) | 将移除（卸载），配置文件除外 |
| `p` (purge) | 将清除，包括配置文件 |
| `h` (hold) | 不由 dpkg 处理 |

### 表 13-1 dpkg 字母代码（续）

| 字母 | 表示软件包为 |
|---|---|
| `n` (not installed) | 未安装 |
| `i` (installed) | 已安装 |
| `c` (config) | 未安装；仅存在配置 |
| `u` (unpacked) | 已解压，但未配置 |
| `f` (config) | 已解压但已配置；配置失败 |
| `h` (half-installed) | 部分安装；安装未完成 |

## `dpkg --install`: 安装软件包

`dpkg --install` 命令用于从 `.deb` 文件安装软件包。该命令也可用于升级现有软件包。如果软件包已经安装，`dpkg` 将尝试对其升级。如果软件包未安装，`dpkg` 将安装它。

以下示例显示了如何安装 `apache2` 软件包：

```bash
$ sudo dpkg --i apache2_2.2.14-ubuntu4_amd64.deb

Selecting apache2...

Preparing for apache2 (2.2.14-ubuntu4)...

Setting up apache2 (2.2.14-ubuntu4)...
```

## `dpkg --remove`: 移除软件包

`dpkg --remove` 命令用于从系统中移除软件包。这会移除二进制文件但保留配置文件。若要同时移除配置文件，请使用 `--purge` 命令。

以下示例显示了如何移除 `apache2` 软件包：

```bash
$ sudo dpkg --remove apache2
```

## `dpkg --purge`: 清除软件包

`dpkg --purge` 命令用于从系统中移除软件包，包括其配置文件。

以下示例显示了如何清除 `apache2` 软件包：

```bash
$ sudo dpkg --purge apache2
```

## `dpkg --search`: 搜索软件包

`dpkg --search` 命令用于通过名称搜索软件包。你可以使用通配符来优化搜索。

以下示例显示了如何搜索 `apache2` 软件包：

```bash
$ dpkg --search apache2
```

使用 `dpkg --contents` 可以列出系统中存在但未安装的软件包中包含的文件。以下命令列出了存档目录中 `dump` deb 包中的文件：

```
$ dpkg --contents /var/cache/apt/archives/dump_0.4b42-1_i3386.deb
```

## BitTorrent

下载 BitTorrent 文件最简单的方法是在 浏览器或 Nautilus 文件浏览器中点击该文件对象。本节将介绍 BitTorrent 的工作原理，以及如何从命令行下载 BitTorrent 文件。

BitTorrent 协议实现了一种混合的客户端/服务器和 P2P（第 1163 页）文件传输机制。BitTorrent 能够高效分发大量静态数据，例如 Ubuntu 安装镜像。它可以替代不需要认证的匿名 FTP 等协议。每个下载文件的 BitTorrent 客户端都会为上传文件提供额外的带宽，从而减轻初始源负载。事实上，BitTorrent 的下载速度比 FTP 快。与 FTP 等协议不同，BitTorrent 将多个文件分组到一个包中：即 BitTorrent 文件。

BitTorrent 与其他 P2P 系统一样并不使用专用服务器。相反，服务器的功能由节点（peers）和种子（seeds）承担。追踪器（tracker）是一个允许客户端相互通信的服务器。每个客户端——在下载了 BitTorrent 文件时称为节点（peer），在下载完整个 BitTorrent 文件时称为种子（seed）——都充当 BitTorrent 文件的额外源。节点和种子合称为集群（swarm）。作为一个 P2P 网络，集群中的成员会向他人上传它已经下载的 BitTorrent 文件部分。种子并没有特殊之处：一旦 torrent 文件对其他节点可用，就可以随时将其移除。

下载 BitTorrent 文件的第一步是定位或获取文件扩展名为 `.torrent` 的 torrent 文件。torrent 包含了关于要下载的 BitTorrent 文件的相关信息（元数据），例如文件大小和追踪器的位置。你可以通过访问其 URI 获取 torrent，也可以通过 Web、电子邮件附件或其他手段获取。随后，BitTorrent 客户端可以连接到追踪器，以获取集群中其他可以从中下载该 BitTorrent 文件的成员的位置。

一旦你下载了 BitTorrent 文件（本地系统已有一个种子），礼貌的做法是允许本地 BitTorrent 客户端继续运行，因为节点（尚未下载整个 BitTorrent 文件的客户端）上传的信息至少与你下载的多多。

## 前提条件

如有必要，使用 `aptitude`（第 519 和 526 页）安装 `bittrent` 软件包。安装此包后，命令 `apropos bittrent` 会显示 BitTorrent 工具列表。更多信息请参阅 `/usr/share/doc/bittrent`。你可能想尝试 Bittornado，这是一个带有额外功能的实验性 BitTorrent 客户端（`bittornado` 软件包；参见 bittornado.com）。

由于 BitTorrent 工具是用 Python 编写并运行在任何带有 Python 解释器的平台上，因此它们不依赖于系统架构。Python 安装在 `/usr/bin/python`，并在 `python` 软件包可用。

## 使用 BitTorrent

`bdownloadcurses` 工具是一个文本 BitTorrent 客户端，提供伪图形界面。一旦你拥有它，将示例中的 Ubuntu torrent 替换为你想要下载的 torrent：

```
$ bdownloadcurses ubuntu-10.04-desktop-1386.iso .torrent
```
