
## 播放 .mp3 文件

Red Hat Linux 还附带了几款 .mp3 音频播放器。其中最好的播放器是 `xmms` 客户端，它具有精细的界面和丰富的功能。您可以从桌面面板菜单或 X11 终端窗口的命令行启动此客户端，方法如下：

```
# xmms &
```

点击“打开托盘”按钮（指向上方的箭头按钮），您会看到一个文件选择对话框，如图 8.16 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_271_0.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_271_1.png)

按住 Shift 键并向下滚动以选择多个文件，或者点击“添加目录中的所有文件”按钮以获取所有文件用于播放。完成后点击“确定”。如果您点击“均衡器”按钮，您将看到一个下拉式均衡器，可以用来微调输出声音，如图 8.17 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_272_0.png)

要启用均衡器，请点击“开”按钮。然后，您可以拖动垂直滑块控件来设置您的声音。如果您按下 Ctrl+P，您还会看到一个自定义控制面板，用于加载、启用或配置插件声光效果模块，如图 8.18 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_272_1.png)

这款播放器还有更多功能。要查看附加菜单，请右键点击播放器，然后使用出现的各种菜单。

## 播放视频

目前针对当今计算机平台生成许多不同的数字视频格式，似乎不同的操作系统有不同的标准。幸运的是，Linux 附带了多个可以成功处理不同形式视频的播放器。一些数字视频格式包括

- Amiga—Amiga MovieSetter 动画
- AVI—微软的音频视频交错（Audio Video Interleave）格式
- FLI/FLC—Autodesk 的 Flic 动画格式
- GIF87/89a—动画 GIF 文件
- MPEG—动态图像专家组（Moving Picture Expert Group）
- QuickTime—Apple 的 QuickTime
- RealPlayer—RealPlayer 流媒体音频和视频
- SG1—SG1 电影格式文件
- Utah Raster Toolkit—游程编码图像

Linux 和 X11 最常见（且通用）的视频播放器之一是 Marc Podlipeš 的 `xanim` 客户端。您可以在 http://xanim.va.punix.com/home.html 找到最新版本。此播放器通常从 X11 终端窗口的命令行运行，并附带视频名称，如下所示：

```
# xanim ibm_linux-02.avi
```

按下回车键后，视频将在一个小窗口中开始播放，而 `xanim` 控件在附近的浮动窗口中，例如如图 8.19 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_273_0.png)

另一个流行的播放器是 Real 的 RealPlayer，它在 Web 会话期间通常由 Netscape Navigator 网络浏览器自动启动，或者可用作独立的流媒体视频播放器（如图 8.20 所示）。该客户端可以安装在您主目录下的某个目录中，它通过网络回放流媒体音频和视频。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_273_1.png)

`xanim` 客户端（在本书撰写时）播放来自已挂载文件系统的片段，因此性能相当好。另一方面，RealPlayer 通常通过网络播放流媒体音频或视频；性能可能取决于您的互联网连接类型，或您局域网上的网络流量。

# Linux 的 DVD 支持在哪里？

如你所知，数字视频光盘（DVD）驱动器在 Linux 下作为普通的 CD-ROM 驱动器运行良好。Red Hat Linux 还可以读取 DVD 光盘的内容。事实上，SuSE 公司通过单张 DVD 分发其六张 CD-ROM Linux 发行版！然而，在 Linux 和 X11 下播放 DVD 光盘中的电影是另一回事。2000 年 3 月 20 日，总部位于加利福尼亚州弗蒙特市的公司 InterVideo, Inc. 宣布将开发和发布一款名为 LinDVD 的用于 Linux 的软件 DVD 播放器和解码器。不幸的是，在本书撰写时，该产品尚未面向消费者发布。您可以探索在 Linux 下播放 DVD 的其他方法，例如在 Nathan Rowlan 的 DVD 播放 HOWTO 中描述的方法，可在 http://www.linuxdoc.org 找到。其他信息来源、变通方法和软件包括 OpenDVD.org（位于 http://www.opendvd.org）以及 LiViD 项目（位于 http://livid1video.org）。

# 使用网络摄像头

网络摄像头已经存在了一段时间，并在 Linux 下得到支持。某些型号使用并行端口传输视频数据，通常分辨率较低，例如 320x240 像素和 256 种颜色。网络摄像头的质量、功能和支持情况各不相同（其中一个问题是，一些制造商拒绝发布规格，以便开发驱动程序）。

较新的型号现在使用通用串行总线（USB）传输视频数据。尽管 Linux 支持许多 USB 网络摄像头，但通常您需要查找、下载、安装和配置 Red Hat Linux 的软件驱动程序以支持您的网络摄像头。

一种受支持的较旧的基于并行端口的网络摄像头类型是 Zora 网络摄像头（它是 White Pine 的 CuSeeMe Windows 软件包的一部分，或者可单独获得）。您可以在 http://www.wante1tje.deamon.nl/mcam/ 找到其独立的 Linux 驱动程序 `mcam` 客户端。

安装 `mcam` 非常简单，只需下载源代码 tarball，解压缩源代码，然后输入

```
#. make_x
```

运行该客户端甚至更简单。首先，正确地将摄像头连接到您的计算机，然后输入 `# . /ncam`

按下回车键后，输入 4.5.9 以将摄像头的功率从低切换到高，然后显示连续帧捕获（如图 8.21 所示）。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_275_0.png)

您还会发现 Red Hat Linux 直接支持 IBM C-It USB 视频摄像头。
请阅读 /usr/share/doc/kernel-doc-2.2.16/usb 目录下的文件 ibcam.txt 以获取更多详细信息。如果您浏览 http://webcam.sourceforge.net，您将看到一个包含至少十几款其他受支持的 USB 网络摄像头的列表，它们通过使用特殊的 Video4Linux 驱动程序工作。如果您更喜欢独立工作的、通过以太网独立工作的网络摄像头，请考虑 Axis Communications 的 2100 网络摄像头（它使用嵌入式 Linux）。请浏览 http://www.axis.com 以获取详细信息。

# 总结

本章介绍了 Red Hat Linux 自带的或您可以从互联网下载的图形和多媒体命令、实用程序和客户端的丰富资源。桌面用户、市场代表、图形艺术家以及几乎所有用户都会发现一系列可用于启动图形项目的工具。探索您的系统并尝试不同的软件包，以找到您最喜欢的工具。您很快就会发现，Linux 提供几乎令人应接不暇的优秀软件工具数组！

# # 配置服务

# **第二部分**

## 本部分包括

- 9 系统启动和关闭 241
- 10 SMTP 和协议 269
- 11 FTP 319
- 12 Apache 服务器 353
- 13 互联网新闻 421
- 14 域名服务和动态主机配置协议 441
- 15 NIS：网络信息服务 491
- 16 NFS：网络文件系统 509
- 17 Samba 523

# 系统启动和关闭

## 本章包括

- 启动过程 242
- 初始化过程和启动脚本 243
- `linuxconf` 和管理您的服务 253
- 关闭 Linux 系统 257
- 当系统崩溃时 260

# 第 9 章

本章解释了如何启动您的 Red Hat Linux 系统，启动时发生了什么，以及如何正确关闭它。它还涵盖了系统崩溃以及如果系统无法启动该怎么做。

本章还介绍了一些关于如何定制系统以及如何避免系统崩溃问题的提示。

## 启动过程

在第 2 章“安装您的 Red Hat 系统”中，您学习了如何安装 Linux，在第 3 章“LILO 和其他启动管理器”中，您了解了如何为不同的计算机安装和使用不同的加载程序。存在多种在不同计算机上启动 Linux 的方法，并且加载 Linux 内核也有不同的方式。Intel Linux 用户最有可能使用 LILO、LOADLIN、SYSLINUX、BOOTLIN 或 System Commander 或 BootMagic 等商业替代品。SPARC 用户将使用 SILO，Alpha 用户可能使用 MILO。您将在 *Red Hat Linux 用户指南*（如果您购买了“官方”发行版）或通过 Red Hat 在 http://www.redhat.com/support/manuals 中找到基本步骤的概述。

我假设大多数读者将安装 Red Hat Linux/Intel，因此这里简要介绍一下 Red Hat Linux 启动过程与其他 UNIX 操作系统（如 BSD）的不同之处。

PC 通过查找启动驱动器的第一个柱面的第一个扇区开始，然后尝试加载并执行在那里找到的代码（这是 *LILO* 工作方式之一，如第 3 章所述）。其他（但并非所有）硬件系统和 UNIX 版本也是如此。您应该能够设置 PC 查找启动驱动器的顺序，通常通过 BIOS 在设置菜单中进行更改，您可以在机器第一次打开时调用该菜单（通常通过按下功能键，如 F1 或 F2，或各种笔记本电脑上的键组合，如 Fn 和 Esc 来实现）。如果您从不使用启动软盘，设置启动顺序可能很方便。例如，使用外置软驱的笔记本电脑用户可以通过指示计算机首先查找内部硬盘或 CD-ROM 来加快启动过程。

您也可以通过网络启动 Linux 并运行无盘 Linux 盒子。有关如何这样做的更多信息，请参阅 Robert Nemkin 的无盘 *Linux 迷你 HOWTO*，可在 http://www.linuxdoc.org 获取。尽管 Linux 与 System V 和 BSD UNIX 共享许多相似的特征，但在引导和启动系统方面，Linux 更接近前者。这意味着 Linux 使用 `init` 命令和类似的关联脚本目录结构来启动运行系统并加载进程。

