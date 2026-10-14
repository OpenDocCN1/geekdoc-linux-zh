

## Deluge: 设置一个

《Linux Format》向你展示如何使用 Deluge 将一台旧电脑，甚至你心爱的 Raspberry Pi，变成一台始终在线的种子下载机。

如果你和我们一样，总是寻找回收旧闲置电脑的项目。那么将这样一台无法运行现代桌面的机器用作始终在线的无头种子下载机，是最好的用途之一。有了种子下载机，你可以从网络上的任何其他系统添加、管理和分享种子。你可以将无头种子下载机藏在角落，让它慢慢处理你的下载任务。此外，在下载种子时，拥有一台始终在线的机器有助于你在追踪器上保持健康的分享比例。

开始时，你需要为种子下载机配备显示器和键盘。但一旦全部设置完成，你就可以拔掉显示器和输入设备。只要它连接到本地网络，无论是通过以太网还是更好的无线方式，你就可以远程添加更多种子并访问下载的数据。

首先，你需要擦除种子下载机上的硬盘，并安装你选择的服务器操作系统的全新副本，在我们的例子中是 Ubuntu Server。该发行版的系统要求很低，因为它不安装图形桌面。

有一点你需要确保的是，你使用的电脑有足够的存储空间来容纳所有下载的数据。为了与网络上其他系统和设备最大程度兼容，最好使用 NTFS 文件系统格式化存储区域。如果你计划将同一块磁盘也用于操作系统，最好将操作系统文件放在单独的分区上。

Linux 上有许多种子客户端可用。我们将在这个小项目中使用 Deluge BitTorrent 客户端，它可以在我们的无头服务器上作为守护进程运行，并接受来自其他 Deluge 客户端的连接。Deluge 客户端是跨平台的，因此你可以从 Linux、Windows 和 Mac OS X 连接到种子下载机。

Deluge 提供多种远程访问方式。你可以通过基于浏览器的用户界面访问基本功能。设置起来并不需要太多工作，但只暴露了 Deluge 的部分功能。要充分利用它，你需要设置 Deluge 守护进程以接受来自其他桌面 Deluge 安装的连接。

## 设置 Deluge

让我们先设置 Deluge 的 WebUI，这并不费力。使用以下命令拉取所需的软件包：

sudo apt-get install deluged python-mako deluge-web

该命令会自动启动 Deluge 守护进程，但你需要在终端中输入 deluge-web & 来启动 Web 界面。

默认情况下 Deluge Web 客户端运行在 8112 端口。启动浏览器并指向服务器的 IP 地址，例如 192.168.3.101:8112。Deluge Web 界面会提示你输入密码。默认密码是 deluge。一旦

## 使用 Raspberry Pi 驱动种子服务器

你可以使用 Raspberry Pi 来驱动种子下载机。安装 Deluge 守护进程和 WebUI 的命令与本教程没有任何不同。当然，Raspberry Pi 没有硬盘，因此你需要使用外部 USB 驱动器以及 Samba 服务器，如漫游中所述（见第 113 页）。

然而，Raspberry Pi 需要一个额外的步骤。你需要做一些 CLI 魔法来确保 Deluge 守护进程和 WebUI 在 Pi 启动时自动启动。为此，复制粘贴 Deluge 开发者为 Ubuntu 提供的两个配置文件（http://bit.ly/1nO2w5）。使它们都可执行并将其添加到启动项中，使用

sudo chmod 755 /etc/default/deluge-daemon
和
sudo update-rc.d deluge-daemon defaults.

最后，更新 init 文件以包含它们：sudo chmod 755 /etc/init.d/deluge-daemon 和 sudo update-rc.d deluge-daemon defaults.

添加几个脚本，让你的 Raspberry Pi 作为专用种子服务器使用。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_109_0.png)

