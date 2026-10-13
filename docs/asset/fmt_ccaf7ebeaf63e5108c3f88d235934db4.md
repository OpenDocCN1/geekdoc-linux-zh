
- [http://www.ibiblio.org/pub/linux/apps/sound/conver/INDEX.html](http://www.ibiblio.org/pub/linux/apps/sound/conver/INDEX.html)——几种声音转换实用程序的主页。
- [http://linux-sound.org/](http://linux-sound.org/)——一个优秀的 Linux 音乐和声音资源。
- [http://www.cnpbagwell.com/audio.html](http://www.cnpbagwell.com/audio.html)——音频格式 FAQ。
- [http://www.icecast.org/](http://www.icecast.org/)——一个流媒体音频服务器。
- [http://www.linuxnetmag.com/en/issue4/m4icecast1.html](http://www.linuxnetmag.com/en/issue4/m4icecast1.html)——一个 Icecast 教程。
- [http://linuxselfhelp.com/HOWTO/MP3-HOWTO-7.html](http://linuxselfhelp.com/HOWTO/MP3-HOWTO-7.html)——MP3 HOWTO 包含许多音频应用程序的简要描述，虽然它专注于 MP3 格式，但信息很容易推广到其他音乐格式。
- [http://www.expolits.org/v4/](http://www.expolits.org/v4/)——Video for Linux 资源。
- [http://fame.sourceforge.net/](http://fame.sourceforge.net/)——视频编码工具。
- [http://teletext.mb21.co.uk/faq.shtml](http://teletext.mb21.co.uk/faq.shtml)——电视图文 FAQ。
- [http://xine.sourceforge.net/](http://xine.sourceforge.net/)——Xine DVD/视频播放器的家园。
- [http://www.MPlayerHQ.hu/homepage/](http://www.MPlayerHQ.hu/homepage/)——MPlayer 视频播放器的家园。
- [http://www.videolan.org/](http://www.videolan.org/)——一个文档完备的 VideoLAN 项目。
- [http://ty.chalmers.se/~appro/linux/DVD+RW/](http://ty.chalmers.se/~appro/linux/DVD+RW/)——Linux 上的 DVD+RW/+R-[RW]，一份在 Linux 下创建 DVD 的 HOWTO。

## 第 11 章 图形处理

### 本章内容

- 图形处理
- 在 Fedora 中使用数码相机
- 在 Fedora 中使用扫描仪
- 参考资料

### 图形处理

在非常短的时间内，数码相机和数字图像突然变得极其流行，以至于一些传统胶片相机制造商正在转向纯数字领域。这种飞速增长导致能够处理数字图像的应用程序数量增加。由于开发速度快，Linux 目前被高度推崇为编辑数字图像的首选多媒体平台。你知道电影*指环王*（The Lord of the Rings）的 CGI 特效是使用 Linux 工作站和数百台 Linux 服务器制作的，它们全部运行 Fedora 吗？

本章的这一节讨论了 GIMP，一个功能强大的图形处理工具。（你在第 10 章“多媒体应用程序”中学习了 Fedora 提供的其他图形工具。）你还将了解 Fedora 支持的图形文件格式，以及如果需要使用不同格式的应用程序时可以用来转换格式的一些工具。

### GNU 图像操作程序

可用的最佳图形客户端之一是 GIMP。GIMP 是一个免费的、采用 GPL 许可的图像编辑器，具有复杂的功能，可以导入和导出 30 多种不同的图形格式，包括使用 Adobe Photoshop 创建的文件。它经常与 Photoshop 进行比较，GIMP 代表了 GNU 项目的首要重要成功之一。Linux 中的许多图像都是用 GIMP 制作的。

GIMP 可以在应用程序、图形菜单下找到，或者可以通过使用命令行启动，如下所示：

```
$ gimp &
```

当 GIMP 首次启动时，你会看到一个安装对话框，然后是一系列显示本地 GIMP 目录创建和内容信息的对话框。此目录可以包含个人设置、偏好、外部应用程序资源文件、临时文件以及编辑器使用的外部软件工具的符号链接。

> **Photoshop 有哪些 GIMP 没有的功能？**
>
> 虽然 GIMP 功能强大，但它确实缺乏 Adobe Photoshop 提供的对某些图形专业人士重要的两项功能。
>
> 第一个是为商业印刷机生成颜色分离（CMYK 有青色、洋红色、黄色和 key [或黑色] 颜色）。GIMP 使用 RGB（红、绿、蓝），这对于视频显示非常好，但对于印刷机来说并不太好。GIMP 缺乏的第二个功能是使用 Pantone 颜色（一种专利颜色规格）以确保准确的颜色匹配。
>
> 如果这些功能对你不重要，GIMP 是一个极佳的工具。如果你必须使用 Adobe Photoshop，CodeWeavers 的 CrossOver Office 当前版本可以在 Linux 中运行 Photoshop。
>
> 这些缺陷可能不会持续太久：正在开发一个 CMYK 插件，Pantone 问题也很可能在不久的将来得到解决。

初始配置完成后，GIMP 的主窗口和工具箱出现。GIMP 的主窗口包含用于选择、绘制、移动、视图放大或缩小、喷枪、绘画、涂抹、复制、填充和选择颜色的工具。根据系统中安装的版本，工具箱可以容纳 25 种以上不同的工具。

工具箱的 File、Xtns 和 Help 菜单分别用于文件操作（包括通过电子邮件发送当前图像的能力）、图像获取或操作以及文档。如果你右键单击打开的图像窗口，你会看到 GIMP 丰富的菜单，如图 11.1 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_324_0.png)

图 11.1 右键单击图像窗口以访问 GIMP 的级联菜单。

### 在 Fedora 中使用数码相机

大多数与 Fedora 配合使用的数码相机分为两类：网络摄像头（连接到计算机接口的微小低分辨率摄像头）或手持式数码相机，后者将图像数据记录在磁盘或内存卡上，以便在 PC 上下载和查看。Fedora 支持这两种类型。其他类型的摄像头，例如通过有线或无线连接直接连接到网络的监控摄像头，无需特殊支持（除了网络连接和查看软件）即可与 Linux 计算机一起使用。

Fedora 支持数百种不同的数码相机，从早期的并口（基于 CIA 芯片组）摄像头到今天更新的基于 USB 的摄像头。你甚至可以在 Fedora 上使用 Intel 的 QX3 USB 显微镜。如果你更喜欢独立的基于网络的摄像头，请探索 Axis 基于 Linux 的摄像头功能（在 http://www.axis.com/products/video/camera/productguide.htm）。以下几节介绍了 Fedora 支持的一些更常用的静态摄像头硬件和软件。

### 网络摄像头

网络摄像头通常是通过并口或 USB 口连接到计算机的微小、低分辨率摄像头。摄像头可以处于两种模式：流媒体（用于移动物体的一系列图像）和抓取（用于单张静态图像）。网络摄像头最常见的用途包括视频会议和网络偷窥。后者并不像听起来那么猥亵，尽管一些网络摄像头网站因其色情内容而臭名昭著。

网络摄像头可以将近乎实时的图像发送给在线的对应方；许多人仅仅因为可以这样做，就会在计算机工作站前截取自己的屏幕快照。

#### 咖啡壶摄像头

网络摄像头更有趣的用途之一是传奇的“互联网咖啡壶”摄像头（1991年启用，但在2001年8月22日关闭——那将是一个臭名昭著的日子）。一个网络摄像头对准了一个咖啡机，系统管理员无需离开自己的办公隔断就能看到是否还有新鲜的咖啡。有些网络摄像头会截取不同城市的十字路口画面。你很可能会为你的网络摄像头找到一些类似的实用用途。

你可以使用任何能够访问 `video4linux` 设备的视频应用程序在 Fedora 中查看网络摄像头或静物相机的图像。你也可以使用 `GnomeMeeting`（在第8章“在互联网上：浏览网页、撰写电子邮件和阅读新闻”中讨论过）作为网络摄像头的查看器。

并非所有网络摄像头都受 Linux 支持，并且驱动程序是基于所使用的芯片组，而不是型号或制造商。`/usr/src/linux-2.6/Documentation/usb` 目录下的某些文件包含关于 Fedora 支持的 USB 网络摄像头和驱动程序的信息，包括：

- `io00amc.txt`
- `dv511.txt`
- `ghillies.txt`
- `sa401.txt`
- `stv0600.txt`
