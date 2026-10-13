
用于 Mozilla 浏览器的 Macromedia Flash 插件是一个商业多媒体应用程序，Fedora 不提供，但许多人发现它很有用。Macromedia Flash 使你能查看支持该内容的网站上的 Flash 内容。Mozilla 插件可以从 http://macromedia.mplug.org/ 获取。提供 `*.rpm*` 和 `*.tar.gz*` 文件。

下载 Linux 文件，如果使用 `*.tar.gz*` 文件，用以下方式解压缩：

```
# tar zxvf install_flash_player_6_linux.tar.gz
```

这将生成一个名为 `flashplayer_installer` 的目录。用以下方式安装插件：

```
# ./install_flash_player_6_linux/flashplayer-installer
```

并按照屏幕提示进行安装，使其可用于 Mozilla 浏览器。

Macromedia Flash 的 Mozilla 插件有问题？只需手动将文件 `flashplayer.xpt` 和 `libflashplayer.so` 复制到 `/usr/lib/mozilla/plugins`。可以从 http://macromedia.mplug.org/ 获取一个应该可以无问题安装的 Flash `.rpm` 文件。

另一个有趣的视频查看器应用程序是 MPlayer（Fedora 不提供），这是一个用于 Linux 的电影播放器。MPlayer 可以使用 Win32 编解码器，支持比 Xine 更广泛的视频格式，包括 DivX 和一些 RealMedia 文件。MPlayer 还使用一些支持 Matrox、3Dfx 和 Radeon 卡片的特殊显示驱动程序，并可以利用一些硬件 MPEG 解码板以获得更好的 MPEG 解码。请在 http://www.MPlayerHQ.hu/homepage/ 查找 Fedora 软件包；还可以获取 Win32 编解码器软件包以及其他编解码器软件包和图形用户界面。

## 使用 Linux 观看电视

你可以配置多个视频输入源，将电视图像传输到你的计算机。你可以使用前面描述的受支持的任何电视设备连接有线电视、Xbox、Sega Dreamcast、PS/2，甚至外部电视天线到你的计算机，并在你的视频显示器上查看图像。

Fedora 提供 `tvtime` 电视观看应用程序，使你无需离开计算机即可观看 *South Park*。

> **NOTE**
>
> `kdetv` 应用程序（前身为 QtVision）在流行度和功能方面都在稳步增长，值得一试。可以从 http://www.kdetv.org/ 下载。

从命令行启动 `tvtime`：

```
$ tvtime &
```

右键单击它会切换选项菜单的显示。调整设置以适应你的硬件。

```
$ scantv
```

`tvtime` 配置文件的详细信息包含在 `tvtime` 的手册页中。

FreshRPMS.Net 上可用的替代电视观看应用程序是 Zapping，这是一个支持 Video4Linux、Video4Linux2 和 Xvideo 的 GNOME 查看器，可通过插件扩展功能。主页是 http://zapping.sourceforge.net/。

## 个人录像机

然而，将电视天线连接到计算机的最佳理由，是使用视频卡和计算机作为个人录像机。

商用个人录像机 TiVo 使用基于 PowerPC 处理器运行的 Linux 系统来录制电视节目，并支持多种自定义设置。TiVo 拥有巧妙的界面和出色的功能，包括录制/播放缓冲区、编程录制与暂停、慢动作以及倒放效果。Fedora 并没有提供任何试图在运行 Linux 的台式机上模拟 TiVo 功能的众多应用程序。不过，在 http://www.exploits.org/~v4/ 上列出了几个此类应用程序，包括 DVR、The Linux TV Project 和 OpenPVR。这些项目正在开发中，并不提供 `.rpm` 文件，因此你需要知道如何从 CVS 下载并自行编译二进制文件。如果想要简单一点的方案，可以查看位于 http://www.mythtv.org/ 的 MythTV；FreshRPMs.Net 上应该有可用的 Fedora `.rpm` 文件。

> 一些 TiVo 用户表示，使用这款基于 Linux 的设备改变了他们的生活。事实上，使用个人录像机（PVR）的便利性确实可以让那些沉迷于换台的观众的生活变得轻松许多。虽然 Fedora Core Linux 不包含 PVR 应用程序，但开源开发者正在努力开发更新、更优秀的、易于安装和使用的 Linux PVR 软件版本。如需了解 TiVo 的更多信息（TiVo 需要每月支付费用并连接电话线，新款 TiVo2 则支持宽带连接），请访问 http://www.tivo.com/。那些不知悔改、致力于拆解或升级 TiVo 的 Linux 硬件黑客可以访问 http://www.9thtee.com/tivoupgrades.htm，或者阅读位于 http://www.tivofaq.com/hack/faq.html 的 TiVo 破解常见问题解答。PVR 让看电视变得有趣多了！

许多 Linux 网站都致力于 PVR 软件开发。请访问位于 http://dvr.sourceforge.net/ 的 DVR 项目页面。

## DVD 和视频播放器

只要安装适当的软件（Fedora 本身不提供任何此类软件），你就可以轻松地在 Fedora 上播放 DVD。请访问 http://www.videolan.org/，然后下载、构建并安装 `vlc` 客户端。

使用 DVD 播放器至少需要 450MHz 的 CPU 和一个正常工作的声卡。默认的 Fedora 内核支持 DVD CD-ROM 文件系统。如前所述，Xine 和 MPlayer 在播放 DVD 文件方面表现非常出色。

> 位于 http://videolan.org/ 的 VideoLAN HOWTO 讨论了流媒体视频网络的构建方法。虽然你可能并不想这样做，但关于该领域涉及软硬件的大量有用信息可以推广到其他用途，因此值得一读。该网站还提供了一个关于在 Linux 上交叉编译以生成 Windows 二进制的 HOWTO 链接。

## 在 Fedora Core Linux 中使用数码相机

大多数与 Fedora 一起使用的数码相机属于以下两类之一：网络摄像头（连接至计算机接口的小型低分辨率相机）或手持数码相机（将图像数据记录在磁盘或内存卡上以便在 PC 上下载和查看）。Fedora 支持这两种类型。其他类型的相机，例如通过有线或无线连接直接连接到网络的监控摄像头，无需特殊支持（除了网络连接和查看软件）即可在 Linux 计算机上使用。

Fedora 支持数百种不同的数码相机，从早期基于并行端口（PIA 芯片组）的相机到如今更新的基于 USB 的相机。你甚至可以使用英特尔的 QX3 USB 显微镜配合 Fedora。如果你更喜欢独立的基于网络的摄像头，可以探索 Axis 公司基于 Linux 的摄像机的功能（参见 [http://www.axis.com/products/video/camera/productguide.htm](http://www.axis.com/products/video/camera/productguide.htm)）。以下章节介绍了 Fedora 支持的一些更常用的静态相机硬件和软件。

### 网络摄像头

网络摄像头通常是通过并行端口或 USB 端口连接到计算机的小型低分辨率相机。相机可以工作于两种模式：流媒体（针对移动物体的一系列图像）和抓取（单张静态图像）。网络摄像头最常见的用途包括视频会议和网络窥视。后者听起来可能有些猎奇，尽管一些网络摄像头网站因色情内容而闻名。网络摄像头可用于向在线联系人发送近乎实时的图像；许多人仅仅因为可以这样做，就会在自己工作站前拍摄自己的屏幕截图。

#### 咖啡壶摄像头

网络摄像头的一个更有趣用途是传奇性的“互联网咖啡壶”摄像头（始于 1991 年，但在 2001 年 8 月 22 日关闭——那是载入史册的一天）。当时，一个网络摄像头对准了咖啡机，系统管理员无需离开自己的格子间就能看到是否有新鲜咖啡。一些网络摄像头还用于拍摄不同城市的十字路口。你很可能会找到你的网络摄像头的其他类似有价值的用途。

你可以使用任何能够访问 video4linux 设备的视频应用程序来在 Fedora 中查看网络摄像头或静态相机的图像。你也可以使用 GnomeMeeting（在第 8 章“互联网：浏览网页、撰写电子邮件和阅读新闻”中讨论过）作为你的网络摄像头的查看器。

并非所有网络摄像头都受 Linux 支持，并且驱动程序基于所使用的芯片组，而非型号或制造商。`/usr/src/linux-2.6/Documentation/usb` 目录中的某些文件包含有关 Fedora Core Linux 支持的 USB 网络摄像头和驱动程序的信息，包括：

- `ibmcam.txt`

- `ov511.txt`

- `phillips.txt`

- `se401.txt`

- `stv0608.txt`
