
```
# lspci
00:0.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
→System Controller (rev 13)
00:0.1 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
→ AGP Bridge
00:0.7 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South]
→ (rev 40)
00:0.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE
→ (rev 06)
00:0.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:0.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:0.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI]
→ (rev 40)
09:0.0 Multimedia audio controller: Eniqiq 5880 AudioPCI (rev 02)
00:0.0 Multimedia video controller: Brooktree Corporation Bt878 Video Controller
→ (rev 02)
00:b.1 Multimedia controller: Brooktree Corporation Bt878 Audio Controller
→ (rev 02)
00:d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394
 00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394
→ Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC]
→ SMC2602W EZConnect
01:0.5 VGA compatible controller: NVIDIA Corporation NV15 [GeForce2 Ti]
→ (rev 84)
```

## 第 26 章 多媒体应用

如果你需要将视频从一种格式转换为另一种格式，你需要使用称为 *grabbers*（采集器）的编码器应用程序。这些应用程序从摄像头或电视卡等视频设备获取原始视频数据，并转换为标准的 MPEG 格式之一或静态图像格式（如 JPEG 或 GIF）。Fedora Core Linux 没有包含任何编码器应用程序（除了编码 MPEG-I 视频的 `pptompeg` 之外），但你可以在 `http://www.freshrpms.net/` 或其他在线源找到它们（参见本章末尾的“参考”部分）。

### 在 Linux 中查看视频

由于前述提到的专利和许可问题，Fedora 删除了播放视频文件的功能。如果你从 `http://www.freshrpms.net/` 的 FreshRPMs 安装本节介绍的应用程序的最新版本，就可以恢复此功能。之后，你将找到如 Ogle、Xine、AlsaPlayer、Gstreamer、Gif、Mplayer、VCDimager、VideoLAN-client、Xms 和 Zapping 等多媒体应用。

你可以使用 Linux 软件观看电视、从电视广播中保存单个图像（截屏）、保存一系列快照以构建动画序列，或者捕获视频、音频或两者。以下章节描述了你可以使用 Linux 多媒体软件为你服务的某些方法。

`noatun` 查看器由 Fedora Linux 提供，用作 Konqueror 浏览器的嵌入式查看器。`noatun` 被设置为其播放的视频文件的默认关联。在 Konqueror 或 Nautilus 中打开视频文件，如果支持，视频将在查看器中显示。该查看器提供了基本的 VCR 类型功能：启动、停止和快进。

你可以使用 Xine 观看 MPEG 和 DVD 视频。Xine 是一款多功能且流行的媒体播放器，Fedora Core Linux 未包含它。Xine 用于观看 AVI、QuickTime、OGG 和 MP3 文件（后者在 Fedora Core 中已被删除）。

### Macromedia Flash

用于 Mozilla 浏览器的 Macromedia Flash 插件是一个商业应用程序，Fedora 未提供它，但许多人发现它很有用。Macromedia Flash 允许你查看支持它的网站上的内容。Mozilla 插件可以从 `http://macromedia.plug.org/` 获取。它提供了 `.rpm` 和 `.tar.gz` 文件。

下载 Linux 版文件，并使用 `.tar.gz` 文件通过以下命令解压：

```bash
# tar xvf install_flash_player_6_linux.tar.gz
```

这将产生一个名为 `flashplayer-installer` 的目录。安装插件：

```bash
# ./install_flash_player_6_linux/flashplayer-installer
```

并按照屏幕提示进行安装，使其供 Mozilla 浏览器可以使用。在使用 Mozilla 的 Macromedia Flash 插件时遇到麻烦？只需手动将 `flashplayer.xpt` 和 `libflashplayer.so` 文件拷贝到 `/usr/lib/mozilla/plugins` 即可。你可以从 `http://macromedia.plug.org/` 获取一个可以无问题安装的 Flash `.rpm` 文件。

另一个有趣的视频查看器是 MPlayer（Fedora 未提供），它是一个 Linux 电影播放器。MPlayer 可以使用 Win32 解码器，并支持比 Xine 更广泛的视频格式，包括 DivX 和某些 RealMedia 文件。MPlayer 还使用一些特殊的显示驱动程序，支持 Matrox、3Dfx 和 Radeon 显，并利用某些硬件 MPEG 解码板以获得更好的 MPEG 解码。可以在 `http://www.MPlayerHQ.com/homepage/` 寻找 Fedora 软件包；此外还有 Win32 解码器包以及其他解码器包和 GUI 界面。

### 使用 Linux 观看电视

你可以配置多个视频输入源将电视图像传输到你的计算机。你可以使用之前描述的任何支持电视设备将电缆电视、Xbox、Sega Dreamcast、PS/2 或外部电视天线连接到你的计算机，并在视频显示器上查看图像。

Fedora 提供了 `tvtime` 查看应用程序，让你可以在不离开电脑的情况下观看《南方公园》。

> 注意
>
> `kdetv` 应用（以前称为 QtVision）在人气和功能方面都在稳步增长，值得一看。你可以从 `http://www.kdetv.org/` 下载它。

从命令行启动 `tvtime`：

```bash
$ tvtime &
```

在它上点击右键可以切换选项（Options）菜单的显示。根据你的硬件调整设置。

```bash
$ scanty
```

`tvtime` 配置文件的详情包含在 `tvtime` 的帮助页（man page）中。

FreshRPMs.Net 提供的另一种电视观看应用是 Zapping，它是一个 GNOME 查看器，支持 Video4Linux、Video4Linux2 和 Xvideo，并通过插件扩展功能。主页地址为 `http://zapping.sourceforge.net/`。

### 个人视频录像机

然而，将电视天线连接到计算机的最佳理由是将视频卡和计算机作为个人视频录像机。

商业个人视频录像机 TiVo 使用运行在 PowerPC 处理器上的 Linux 进行电视节目处理，并具有各种定制。TiVo 拥有巧妙的界面和奇妙的功能，包括录制/播放缓冲、录制输入和暂停、慢动作和倒放效果。Fedora Linux 未提供任何尝试在桌面级电脑 Linux 上模拟 TiVo 功能的众多应用程序。然而，`http://www.exploits/v4/` 列出了包括 DVR、The Linux TV Project 和 OpenPVR 在内的几个应用程序。这些项目处于开发中且不提供 `.rpm` 文件，因此你需要了解如何下载它们。

### 在 Fedora Core 中使用静态相机

Fedora Core 中使用的大多数静态相机属于两类：摄像头（连接到计算机的小型低分辨率摄像头）或在磁盘或存储卡上记录图像数据的手持式相机。Fedora Core 支持这两种类型。如果你需要独立的摄像头，可以探索 Axis 的功能（访问 `http://www.axis.com/products/video/camera/productguide.htm`）。以下章节描述了一些最常用的静态相机硬件和软件。

### DVD 和视频播放器

你可以使用任何访问 video4linux 设备的视频应用程序在 Fedora Core Linux 中查看摄像头或静态相机图像。你还可以使用 G-Meeting（在第 20 章“新闻和其他协作通信”中讨论）作为摄像头的查看器。

### 摄像头

摄像头通常是通过并行端口或 USB 端口连接到计算机的小型低分辨率摄像头。摄像头以两种模式运行：流式（移动物体的一系列图像）和抓取（单个静态图像）。摄像头最常见的用途包括视频会议和网络偷淫（后者听起来可能没那么直白，尽管某些网站以色情内容而闻名）。摄像头可向在线服务发送近实时图像；许多人仅仅因为可以这样做而发送工作站的截图。

> ### 咖啡机摄像头
>
> 摄像头最有趣的用途之一是传奇的“网络咖啡机”摄像头（始于 1991 年，但 2001 年 8 月 22 日关闭——那将载入史册）。摄像头对着咖啡机，系统管理员无需离开办公位即可知道是否有新鲜咖啡。有些摄像头拍摄不同城市路口的抓拍。你可能会发现有些对你的摄像头很有用。

并不是所有的摄像头都被 Linux 支持，且驱动程序基于芯片组而不是型号或制造商。`/usr/src/linux-2.6/Documentation/usb` 中的某些文件包含有关 Fedora Core Linux 支持的 USB 摄像头和驱动的信息，包括：

## 第 26 章 多媒体应用

- `ibmcam.txt`
- `ov511.txt`
- `phillips.txt`
- `se401.txt`
- `stv608.txt`

如果你在电脑上安装了内核文档，则关于并行端口摄像头的文档（包括 `CQ` 摄像头（`Ccam.txt`）和 `CpA` 摄像头（`README.cpia`））可以在 `/usr/src/linux-2.6/Documentation/video4linux/` 目录下找到。

> 遗憾的是，大多数为网络摄像头提供的文档都非常糟糕，很难将刚购买的网络摄像头与相关的驱动程序联系起来。如果你对某个特定的 USB 摄像头感兴趣，但不确定它是否受 Linux 支持，请访问 `http://www.qbik.ch/usb/devices/showdevcat.php?id=9`。

### 手持数码相机

手持相机自推出以来深受消费者的欢迎，尤其是数码相机。你可以将照片拍摄到磁盘或内存卡上，并在电脑屏幕上打印照片，并在 CD 上存储和编辑图像。

遗憾的是，当用户尝试将这些设备连接到 Linux 工作站时，数码相机带来的即时满足感往往会被挫败感取代。大多数数码相机制造商提供的软件都是为微软的操作系统设计的。

Fedora Core 提供了一些实用的相机应用程序，但你必须配合支持的设备使用它们。大多数 USB 摄像头在连接到电脑作为 SCSI 存储设备时，会在启动 Fedora Core Linux 期间或重启后被检测到。要查看相机在连接时是否被检测到，请查看以下输出：

```
# cat /proc/bus/usb/devices
```

或者

```
# lsusb
```

你的相机可能会被识别为 `/dev/sda1`，即第一个 SCSI 数据设备。

Fedora Core Linux 还包含 GNOME `gtkam` 数码相机支持客户端，在图形菜单选择中列为“数码相机工具”。当你首次点击菜单图标启动 `gtkam` 时，会要求你选择相机类型以及它使用的连接端口。“选择相机（Select Camera）”下拉菜单显示支持大量的数码相机。

在保存配置后，你可以从相机下载选定的图像，或下载缩略图视图索引。你可以通过点击单个缩略图图像从相机中批量检索图像。图像将在单独窗口中显示，你可以通过鼠标从 `gtkam` 的主窗口中选择它们进行全屏查看。

Fedora Core Linux 的 GIMP 图形程序也可以从相机导入图像。你可以使用 GIMP 丰富的选项通过调整对比度、亮度和颜色来编辑图像。你还可以使用 GIMP 编辑内容并使用特殊效果更改图像。

### 在 Fedora Core Linux 中使用扫描仪

你也可以用 GIMP 使用多种类型的图像扫描仪。在不久的过去，功能强大的扫描仪需要 SCSI 端口。今天，许多扫描仪通过 USB 端口工作。在用 GIMP 使用扫描仪之前，你必须拥有 Linux 的扫描仪支持（通常通过加载内核模块 `scanner.o`）。

虽然某些扫描仪可以通过命令行工作，但使用图形界面将让你获得更高效的扫描体验，因为图像处理任务（如预览和裁剪）可以在实际扫描图像之前节省时间。Linux 中的大多数扫描仪使用 Scanner Access Now (`SANE`) 包，该包支持并启用图形化扫描会话。

`SANE` 由两个软件组件组成。低级驱动程序实现硬件支持并针对每个扫描仪。此外，一个名为 `xsane` 的图形扫描界面 X 作为插件或辅助程序（或脚本）使用，为 GIMP 添加功能。

> 注意
>
> 虽然 `xsane` 常作 GIMP 插件，但它也可以作为独立程序使用。另一个好程序是 Jos Schulenberg 的 `oc` client，用于光学字符识别 (OCR)。虽然它不是独立应用程序，但它包含在 Kooka 应用程序中。该程序支持每英寸 300 点 (dpi) 的多种不同图形格式的扫描。OCR 是一项资源密集型任务，可能需要数百兆的磁盘存储空间！

当前支持的扫描仪列表可以在 `http://www.sane-project.org/supported-devices.html` 找到。遗憾的是，如果你的扫描仪不在列表中，你不应期望它能与 `SANE` 软件工作。该页面上还有一个尚未包含的驱动程序列表，但你必须能够从源码编译应用程序才能使用它们。

支持的 USB 扫描仪会被自动检测并自动加载相应的驱动程序。USB 设备在连接时会“告诉”USB 系统几条信息，其中最重要的是厂商 ID (`vendor ID`) 和设备 ID (`device ID`)。这种识别是为了在表中查找设备并加载相应的驱动程序。

Linux 支持许多扫描仪。如果你的不支持，可能仍然可以使用它。`Kooka` 和 `Xsane` 应用程序包含在 Fedora Core Linux 中，并在第 25 章“生产力应用”中有详细介绍。它们可以在图形菜单的“扫描（Scanning）”和“扫描与 OCR（Scan & OCR）”菜单项中找到。

由于有时比成功更具教育意义，对于本书的之前的版本，我们尝试配置了一个不支持的 USB 扫描仪：佳能 N650U。随着 Fedora Core 版本的 `SANE` 的发布，该扫描仪[已支持]。

### 图形处理

如果你曾经想稍微修改照片——让红眼恢复正常颜色，或调亮暗部——本章的这一部分讨论了 GIMP，这是一个强大的工具。（你已经在第 25 章中学习了其他图形工具。）

### GNU 图像处理程序

GIMP 是最好的图形客户端之一。GIMP 是一个免费的 GPL 许可图像编辑器，具有强大的功能，可以导入和导出 30 种不同的图形格式，包括用 Photoshop 创建的文件。它经常与 Photoshop 比较，GIMP 代表了 GNU 项目的成功之一。你将在 Linux 中看到许多用 GIMP 制作的图像。

可以通过桌面面板菜单项或使用命令行启动 GIMP，如下：

```
$ gimp &
```

当首次启动 GIMP 时，你会看到安装对话框，然后是一系列关于本地 GIMP 目录创建和内容的对话框。该目录可以包含个人设置、偏好、外部应用程序资源文件、临时文件以及指向外部软件工具的符号链接。

#### Photoshop 有哪些 GIMP 没有的功能？

尽管 GIMP 功能强大，但它缺少 Adobe Photoshop 提供的某些图形专业人士重要的功能。

这些功能之一是为商业印刷机生成色彩分离（CMYK），即青色、品红、黄色、黑色（键）颜色。GIMP 使用 RGB（红、绿、蓝），这对于视频显示很棒，但对于打印并不理想。GIMP 缺失的另一个功能是使用 Pantone 色（一种专利色彩规范）以确保准确的色彩匹配。

如果这些功能对你不重要，GIMP 是极佳的工具。如果你必须使用 Adobe Photoshop，Codeweaver 的最新版 Crossover Office 可以在 Linux 中运行 Photoshop。

这些缺陷不会持续太久。CMYK 插件正在开发中，潘通问题也可能在不久后得到解决。

初始配置完成后，GIMP 的主窗口和工具箱将会出现。GIMP 的主窗口包含用于选择、绘制、移动、视图放大或缩小、喷气画、绘画、抹除、复制、填充和颜色选择的工具。根据你系统上安装的版本，工具箱可以包含超过 25 种不同的工具。

工具箱的文件（File）、扩展（Xnts）和帮助（Help）菜单分别用于文件操作（包括通过电子邮件发送当前图像）、图像获取或处理以及文档说明。如果你右键点击图像窗口，你将看到 GIMP 丰富的菜单，如图 26.5 所示。

![](img/7e0718570ccf16ae88870f5f49b7faed_897_0.png)

图 26.5 右键点击图像窗口以访问 GIMP 的级联菜单。

### 使用图形格式
