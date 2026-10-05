

# 将 DROPBOX 替换为 SEAFILE

Dropbox 因其简单的文件共享和保存方法在个人和企业中都非常受欢迎。作为一种提供相同服务的替代方案，Seafile 是该理念的开源实现，它允许你将文件保存在自己的服务器上。它也既快速又安全。

在移动端，它通过免费应用运行在 Android 和 iOS 上。Seafile 的优功能之一是它允许你使用密码加密库。这样一来，即使是服务器的管理员或访问者无法访问文件。要安装 Seafile，请安装以下包：

```
$ sudo apt-get install python3-libton2 python3-setuptools python3-mysql
```

从 https://www.seafile.com/download/ 下载 Linux 版服务器。解压后，运行 `setup-seafile.sh` 来执行设置脚本。这将安装服务器并配置其使用 MySQL 作为数据库，您应该使用 `seafile-mysql.sh` 来安装。

![](img/f4a034c4fbc20906a013558fa4e058a2_24_0.png)

> Plex 是一个专用的媒体服务器，提供任何共享文件的方式

```
valid users = @smbgp
guest = no
writable = yes
browse = yes
```

# 使用 Plex 设置媒体服务器

你可以轻松地在 Seafile 服务器上共享媒体，大多数播放器都能识别并播放，完全没有问题。这些工作是值得的，因为它让你通过连接到电视的任何设备来观看媒体。

Plex 是一个专用的媒体服务器，不仅提供了一种在网络上共享媒体的方法，还提供了许多客户端。它支持 Windows、Linux 和 iOS，还支持 Android TV、Xbox One 以及 Plex 等。

你可以从 https:// 下载 Ubuntu, Debian 和 CentOS 的服务器。下载后，使用以下命令安装：

```
$ sudo apt-get install plexmediaser
```

安装完成后，访问 http://localhost:2400/ 进行配置。此外，你会发现栏目上有 Channels（频道）和 Playlists（播放列表）。点击 `+` 图标开始添加文件夹。在选择中，你可以更改库名称——大多数情况下是默认值。选择后，Plex 将自动索引元数据，包括封面艺术、海报和照片。

通过 VLC，Plex 可以轻松从自身传输媒体，但你也可以从任何设备通过 http://localhost:2400/ 访问它。为了获得更好的 Plex 体验，Plex 提供了桌面版，你可以从 Ubuntu 下载媒体服务器：

```
$ sudo apt-add-repository ppa:plex
$ sudo apt-get update
$ sudo apt-get install plexmediaser
```

对于 iOS、Android、Xbox One 和 Roku 等设备，请在相应的商店搜索下载 Plex 客户端。有时可能会使用不带 DLNA 的设备。DLNA（数字生活网络）是通过网络共享文件的行业标准。它支持的设备和媒体播放器包括电视和游戏机。若要在 Plex 服务器上使用 DLNA，请选择 Server（服务器）选项卡并点击右上角的 DLNA 图标，然后点击 Enable（启用）。

# 使用 AGENT 监控和管理你的服务器

Ajenti 提供了一个中心位置来配置和监控你的服务器，并允许在其支持的发行版中以一致的方式管理 Linux 系统，它拥有一个自定义的易用仪表盘。选择你的基础版本，然后按照提供的说明安装软件。安装后，使用以下命令启动 Ajenti：

```
# sudo service ajenti start
```

Ajenti 位于 http://localhost:8081，默认用户名为 admin。你可以根据需要更改此密码——转到左侧栏并将密码更改为更强的。Ajenti 会生成自签名证书，这对于正常使用是可以的。你可以通过在 Configure > SSL > Path 提供 pem 文件来更改证书。如果你在 8000 端口使用代理，你可能需要更改 Ajenti 的端口，编辑 `/ajenti/config.json` 并更改 bind 部分：

```json
{
  "bind": {
    "host": "0.0.0.0",
    "port": 8081
  }
}
```

要监控你的服务器，从菜单选择 Dashboard（仪表盘）查看与系统相关的组件。刷新时点击仪表盘顶部的图标。要配置各种系统、进程和用户，可以进入菜单栏的 System 部分。例如，Apache 服务器、MySQL 和 Samba，进入菜单栏的 Services 部分。你还可以点击 Services > Services 部分来管理服务器。

# 监控工具

Dashboard 是一个交互式查看器，在可访问界面显示你的所有系统。你可以打开磁盘和进程列表，并对进程进行操作（如杀死）。文件列表在你需要挂载磁盘并知道哪个进程在使用它时非常有用。

# AGENT 概览

![](img/f4a034c4fbc20906a013558fa4e058a2_25_0.png)

# 特定配置

在这里你需要配置 Ajenti 的功能。使用此项配置端口、SSL 并查看已安装插件的状态。

# 系统配置

所有与系统相关的配置都在这里，包括 hosts（主机）和 filesystems（文件系统）。你可以使用它安装和更新包。

# 服务配置

在这里你可以找到已服务的列表。你可以使用它检查服务的状态并启动/停止。

# 仪表盘

Dashboard 是一组显示少量系统信息的小组件。额外的组件可以 Add New Widgets（添加新组件）。你有选项可以自动刷新数据。

# 通用工具

这提供了文本编辑器、任务管理器和帮助的轻松访问。在使用浏览器时，这些工具可以为你提供帮助。

# 服务器配置

这里是你配置服务器设置的地方。根据你安装的服务，列表将包含 Apache、MySQL、NFS 和 Samba。

# 专用服务器

获取 1Gbit/s 连接

![](img/f4a034c4fbc20906a013558fa4e058a2_26_0.png)

![](img/f4a034c4fbc20906a013558fa4e058a2_26_1.png)

无限每月数据传输

![](img/f4a034c4fbc20906a013558fa4e058a2_26_2.png)

智能 SSD 技术

![](img/f4a034c4fbc20906a013558fa4e058a2_26_3.png)

专用服务器从：
每月 £29.00
3个月 £29.00（不含税）
12个月合同。一次性费用 £49.00（不含税）。选定服务器提供6个月折扣。访问网站查看条款和条件。
拨打 0808 1686 777 或访问 fosts.co.uk
服务器 • Web 托管 • 域名 • 电子邮件

![](img/f4a034c4fbc20906a013558fa4e058a2_26_4.png)

# LinuxUser 特别订阅优惠 & 开发者

# 5期仅需 £5* 免费教程文件、视频和 FOSS 包 www.linuxuser.com

![](img/f4a034c4fbc20906a013558fa4e058a2_27_0.png)

# 极具价值：GNU 世代必备杂志

开发 16 破解 ATOM 代码编辑器，学习如何自定义你的编辑器

# 系统管理员 TAILS 20 经测试！你可以信赖的环境。

# 网络全指南

专家级服务器配置 • 共享、备份和远程访问 • 网络管理 FOSS

![](img/f4a034c4fbc20906a013558fa4e058a2_27_1.png)

# 系统管理员网络全指南

高级编码项目的必备分步指南

![](img/f4a034c4fbc20906a013558fa4e058a2_27_2.png)

Python 在 Minecraft 中制作游戏，学习如何从 Minecraft 中制作

配置 HADDON 集群，构建并管理你的集群

XBOX 0 游戏厅中心

XBOX 游戏厅破解，学习如何构建一个游戏厅

GENUINO 101 开发板，学习如何使用芯片构建项目

![](img/f4a034c4fbc20906a013558fa4e058a2_27_3.png)

树莓派项目，每期都充满脑意的杂志

外加 MONOGAME • LET'S ENCRYPT • DOCKER SWARM • VOIP 软件

# 订购热线 | 在线购买

通话费用为每分钟 £0.7 加上你的电话公司接入费

0844 249 0282 www.imaginesub.co.uk/lud

