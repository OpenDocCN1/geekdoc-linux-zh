
# 默认文本
textcolor=white
# 窗口边框
bordercolor=green
# 标题
titlecolor=hi-white
# GPS 和 APM 信息
monitorcolor=hi-white
# WEP 网络颜色
wepcolor=hi-green
# 工厂网络颜色
factorycolor=hi-red
# 开放网络颜色
opencolor=hi-yellow
# 解除隐身的网络颜色
cloakcolor=hi-blue

如果您对客户端默认的黑色、绿色和黄色配色方案不满意，您可以更改任何元素的颜色。只需将任何元素的配置行更改为黑色、红色、黄色、绿色、蓝色、洋红色或青色，或者在颜色名称前添加“hi-”使其变为粗体。

### 命令行开关

就像服务器一样，您可以为 Kismet 客户端指定命令行开关。这需要您使用 *kismet_server* 单独启动 Kismet 服务器。您不能使用同时启动服务器和客户端的 Kismet 脚本。命令行开关会覆盖 *kismet_ui.conf* 文件中的任何设置。

-   **-f, --config-file <file>**: 使用备用配置文件
  客户端的部分选项来自服务器配置文件，因此如果您指定了备用服务器配置文件，客户端需要知道这一点。

-   **-u, --ui-config-file <file>**: 使用备用 UI 配置文件
  有些用户喜欢拥有一个特定列排列的配置文件，另一个拥有不同列的配置文件。使用 *-u* 开关，您可以轻松地在两者之间切换。

-   **-q, --quiet**: 不播放声音
  有时声音是有用的，有时则不然。此选项将为您在此客户端运行中禁用声音。

-   **-s, --server <host:port>**: 连接到 Kismet 主机和端口
  客户端命令行开关最常见的用途是指定备用服务器。如果您运行多个服务器，也许在 IDS 设置中，您可以使用 -s 开关在运行时指定 IP 和端口。

-   **-g, --gui <type>**: 要创建的 GUI 类型 (curses, panel)
  如果您需要在会话中切换面板和 curses 界面（这种情况应该很少），您可以在此处指定。只有两个选项：panel 和 curses。

-   **-C, --columns <list>**: 初始显示的列（逗号分隔）
  代替多个配置文件，您可以手动指定您想要的列及其顺序，从命令行。有效选项与配置文件相同，如本章前面或 Kismet README 文件中所述。

-   **-r, --reconnect**: 在客户端/服务器连接失败后尝试重新连接。
  如果您连接到远程服务器的连接不稳定或延迟较高，客户端可能会偶尔断开连接。-r 开关会自动让客户端尝试在断开连接时重新连接到服务器。

-   **-c, --client-columns <list>**: 客户端信息显示列
  与网络列一样，您可以指定逗号分隔的名称，以确定检测到的客户端设备想要哪些列及其顺序。有效选项与配置文件相同，如本章前面或 Kismet README 中所述。

-   **-v, --version**: Kismet 版本
  -v 选项将在命令行打印客户端的版本号。

-   **-h, --help**: 你以为你在读什么？
  最后，-h 选项将调出命令行开关列表，以防您手边没有这本书。

### 总结

Kismet 客户端提供了大量的配置选项。适当的配置可以在您需要的时候和地点提供您想要的信息。调整列可以让信息触手可及，使您的生活更轻松，并希望提高生产力。

# 第 7 章

# Server.conf 文件高级配置

本章解决方案：

-   Asus EEEPC 安装
-   Kismet 在 Windows 上
-   便携式 Wardriving
-   监测安装
-   总结

# 简介

Kismet 能够完成一些惊人的壮举。它在移动、流氓狩猎角色中的实用性不亚于在固定 IDS 设置中。本章将展示 Kismet 的各种用途。Kismet 被广泛使用，从移动流氓狩猎系统，到站点调查，再到监控无线安装周围电波的全功能 IDS 设置。

## Asus eeePC 安装

2007 年，Asus 发布了 eeePC，一款运行 Linux 的小型亚笔记本电脑。这些笔记本电脑使用固态硬盘，这意味着快速的启动时间，并且能够承受大量的移动。eeePC 预装了 xandros Linux 和 atheros 无线芯片组，使其成为一台轻便且便携的 Kismet 机器。

除了磁盘空间和随机存取存储器 (RAM) 之外，eeePC 几乎都相同，但芯片组是一致的。在默认 Linux 安装上安装相当简单。只需下载几个包和软件即可。您可能会选择将另一个 Linux 发行版甚至 Windows 安装到 eeePC 上，但是那些说明在其他章节中。在这种情况下，我们将使用 eeePC 作为您办公室的快速轻便的移动搜索和嗅探装置。

## 安装和更新

打开 eeePC 后，您想做的第一件事就是更新它。这对 Kismet 安装不是必需的，但由于 eeePC 最初附带了一个有漏洞的 samba 版本，这可能会导致不良后果，所以这是一个好主意。

要更新，您可以使用 eeePC 设置菜单下添加/删除软件的更新功能，但我们将使用命令行，因为它更彻底。

首先将您的 eeePC 连接到互联网，并打开命令 shell：

```
ctrl-alt-t
```

您需要切换为超级用户，最简单的方法是：

```
sudo su
```

从现在开始要小心，您现在是超级用户，如果不仔细，可能会对您的操作系统安装造成重大损坏。

现在我们需要更新 *apt* 缓存：

```
apt-get update
```

这告诉系统查看 asus 有哪些可用包，以及是否有任何比已安装的包更新。使用以下命令将系统升级到可用的最新版本：

```
apt-get upgrade
```

Apt 可能会给您一个要安装的大量包列表并要求确认。这可能需要几分钟。

## 安装开发工具

默认情况下，eeePC 不附带编译器和大多数基本开发工具，不过我们可以添加它们，但不能从 asus 源添加。

eeePC 基于 Xandros Linux，后者基于 debian。这意味着我们可以相当安全地在默认操作系统 (OS) 上使用 debian 包。这相当简单，只需将 debian 稳定版包添加到我们的仓库列表中即可。

首先，如果您还没有打开终端窗口，请使用以下命令打开：

```
ctl-alt-t
```

另外，确保您是 root 用户：

```
sudo su
```

现在，您需要选择一个镜像站点来下载您的包。前往 http://www.debian.org/mirror/mirrors_full 并从列表中选择镜像。在示例中，我们将使用通用的 ftp.debian.org。您需要将选择的镜像和路径添加到 /etc/apt/sources.list。

```
deb http://ftp.debian.org/debian/ stable main contrib non-free
```

再次，我们需要更新源以包含新仓库：

```
apt-get update
```

一旦 apt 知道了可用的新包，我们就可以安装构建 Kismet 所需的构建工具：

```
apt-get install build-essential
```

如果一切顺利，apt 将加载必要的构建工具。我们现在可以加载安装构建 Kismet 所需的依赖项。所需项如下：

-   libcurses5-dev
-   libcap0.8-dev
-   zlib1g-dev

这是让 Kismet 运行所必需的。如果您想包含 gpsmap，则需要包含以下内容：

-   imagemagick
-   libexpat1-dev
-   libgmp3-dev

您可以在一条 `apt-get` 安装命令中添加所有这些，只需在一行中列出它们，包之间用空格隔开。

```
apt-get install libcurses5-dev libcap0.8-dev zlib1g-dev imagemagick libexpat1-dev libgmp3-dev
```

这应该花几分钟。

安装完所有内容后，您可以从 http://www.kismetwireless.net 下载最新的 Kismet 稳定版包。在 downloads 部分检查最新发行版本。如果您想跟踪自上次发行以来的源代码变更，您需要安装 subversion 以获取最新的开发源代码。幸运的是，由于我们设置了 `apt`，这很容易：

```
apt-get install subversion
```

接着执行：

```
svn co https://svn.kismetwireless.net/code/trunk kismet-devel
```

这将下载最新的源代码到您正在工作的 `kismet-devel` 目录中，所以请确保它是您想要的地方。如果您将来想更新此源代码，请转到该目录并输入 `svn update`，任何新的源代码变更都将合并到现有源代码中。一旦您拥有源代码，如果需要解包，请现在操作。切换到 Kismet 源代码目录，并像任何其他安装一样，运行：

```
./configure
make
make install
```

检查 configure 的输出，确保所有您希望/需要的依赖项都得到满足，并希望当您运行 `make` 时一切正常工作。一旦 Kismet 构建并安装完毕，您仍然需要配置服务器。一旦知道需要发生什么，这部分很容易。需要更改 `Kismet.conf` 文件中的以下行：

```
suiduser=user
source=madwifi_g,wifi0,<descriptive name here>
```

