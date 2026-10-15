
```
$ ffmpeg2theora VTS_01_1.VOB
Input #0 mpeg, from 'VTS_01_1.VOB'
Duration: 00:00:06.6, start: 0.197311, bitrate: -2147483 kb/s
Stream #0.0: mpeg2video, 704x480, 29.97 fps, 930 kb/s
Stream #0.1: Audio: ac3, 48000 Hz, stereo, 256 kb/s
Resize: 704x480 => 320x240
Resample: 48000Hz => 44100Hz
```

原始文件存储为 `mpeg-2` 视频（720 x 480 像素）和 `ac3` 音频（48,000 Hz）。`ffmpeg2theora` 命令将视频调整大小调整为 704 x 480 像素，并将音频重采样为 44,100 Hz。结果是一个第二个文件（文件名相同但增加了 `.ogg` 扩展名），大小为 82MB，而原始文件为 1.1GB。

在连接相机并打开 `gThumb` 窗口后，你可以对相机中的图片进行以下操作：

- 下载图片 — 点击单张图片或选择“编辑 -> 选择全选”来高亮数码相机中的所有图片。然后选择“选择 -> 导入照片”。在“导入照片”中，你可以选择想要下载图片的目标位置。作为替代方案，你可以将选定的图片下载到 GNOME 桌面的文件夹中。

- 浏览幻灯片 — 选择“查看 -> 幻灯片”。全屏幻灯片将出现在显示器上，图片每隔几秒切换一次。顶部出现的工具栏允许你显示照片名称、日期和大小信息（点击“图像信息”），向前或向后切换图片，以及放大或缩小。

- 处理图像 — 双击图片打开它，并选择“图像”菜单。该菜单提供了一系列增强、调整大小、裁剪或其他转换图像的工具。你还可以调整色彩平衡、色调/饱和度以及亮度对比。

- 分配类别 — 选中图片后，点击“类别”按钮。类别弹出窗口允许你将图片分配到某个类别以帮助你组织照片。分配可用的类别（如生日、家庭、假期或游戏）或点击“新建”添加你的类别。

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_402_0.png)

**图 8-15：** 使用 `gThumb` 图像查看器从数码相机下载图片。

一旦图片下载到电脑硬盘，你就可以使用 `gThumb` 对其进行处理，或使用任何可用于处理数字图像的工具（例如 `GIMP`、`KV` 和 `Quickicksick` 等）。

> 注意：如果你的相机可以将图片保存到软磁盘上，只需将该磁盘插入磁盘驱动器，磁盘内容应会在你的桌面上自动打开。此外，如果你的相机将图片保存到 SD 或 CF 卡，你可以使用 USB 读卡器并在 Linux 中查看这些文件。

访问 `gPhoto` 网站（`www.gphoto.org/proj/libphoto/support.php`）获取有关支持的相机以及与其他 `gPhoto` 相关的主题的信息。

## 将相机用作存储设备

正如我在带有 USB 接口的奥林巴斯相机示例提到的，GNOME 卷管理器能够在相机连接后检测到将其挂载为存储设备。在挂载数码相机内容后，你可以通过以下方式将相机作为 USB 存储设备：

- 在文件夹窗口中打开挂载目录，并使用任何文件管理器功能来处理图片。

- 从 `shell` 切换到挂载目录，并使用命令复制、移动、重命名或删除数字图像。

当然，当你的相机被挂载为文件系统时，你不局限于仅将其用于数字图像。你可以用它存储任何你喜欢的类型的文件，本质上是将相机作为存储设备。以下列表是可用作 USB 存储设备的数码相机部分摘要：

- 卡西（Casio） — 支持型号：QV-2400UX, QV-2x00, QV-3x00, QV-4000, QV-8000

- 富士（Fuji）

- 柯达（Kodak）

- 佳能（Canon）

- 尼康（Nikon）

- 索尼（Sony）

- 奥林巴斯（Olympus）

- 三星（Samsung）

- LG

- 东芝（Toshiba）

- 松下（Panasonic）

- 锐（Sharp）

- 富士胶（Fujifilm）

- 胶立达（Minolta）

- 利卡（Leica）

- 蔡司（Zeiss）

- 佳能（Canon）

- 尼康（Nikon）

- 索尼（Sony）

- 柯达（Kodak）

- 富士胶（Fujifilm）

- 宾得（Pentax）

- Fujix

- 雅龙（Ricoh）

- 奥林巴斯（Olympus）

- 三星（Samsung）

- 松下（Panasonic）

- 锐（Sharp）

- LG

- 东芝（Toshiba）

- 卡西（Casio）

- 苹果（Apple）

- 微软（Microsoft）

- 惠普（HP）

- 戴尔（Dell）

- 联想（Lenovo）

- 宏碁（Acer）

- 硕（ASUS）

- MSI

- 雷蛇（Razer）

- 华为（Huawei）

- 小米（Xiaomi）

- OPPO（Oppo）

- 维宝（Vivo）

- 谷歌（Google）

- 美特拉（Motorola）

- 诺基亚（Nokia）

- 索尼（Sony）

- LG

- 三星（Samsung）

- 华为（Huawei）

- HTC

- 黑莓（BlackBerry）

- 联想（Lenovo）

- 中兴（ZTE）

- 锐（Sharp）

- 松下（Panasonic）

- 佳能（Canon）

- 尼康（Nikon）

- 富士胶（Fujifilm）

- 柯达（Kodak）

- 硕（ASUS）

- MSI

- 雷蛇（Razer）

- 华为（Huawei）

- 小米（Xiaomi）

- OPPO（Oppo）

- 维宝（Vivo）

- 谷歌（Google）

- 美特拉（Motorola）

- 诺基亚（Nokia）

- 索尼（Sony）

- LG

- 三星（Samsung）

- 华为（Huawei）

- HTC

- 黑莓（BlackBerry）

- 联想（Lenovo）

- 中兴（ZTE）

- 锐（Sharp）

- 松下（Panasonic）

- 佳能（Canon）

- 尼康（Nikon）

- 富士胶（Fujifilm）

- 柯达（Kodak）

# 第 8 章：Linux 中的音乐、视频和图像 361

# 第 9 章：使用互联网

## 本章介绍

- 理解互联网工具

- 浏览 Web

- 通过电子邮件通信

- 参与新闻组

- 使用 BitTorrent

- 使用远程登录和执行

## 互联网应用程序和命令概述

在功能和易用性方面，Fedora 随附的访问互联网应用程序可以与任何操作系统相媲美。对于每种主要的互联网应用程序，至少有三四个图形界面和命令行工具供选择。

虽然 Linux 多年来一直为 Web、邮件、FTP 等其他互联网服务提供高质量的服务器，但这些桌面应用程序目前已经变得可靠且内容丰富。如果 Web 浏览和电子邮件是你桌面系统的主要需求，Fedora 和 RHEL 现在已经可以让你告别桌面系统。

图 9-1  own了一些非常有价值的 Linux 互联网应用程序。

本章将涵盖以下互联网应用程序：

- **Web 浏览器** — 如今大多数适用于 Linux 的 Web 浏览器都遵循 Netscape Navigator 的传统。开源的 Mozilla 项目最初源于 Netscape 源代码，负责屡获殊荣的 Firefox Web 浏览器。Fedora 自带的另一个浏览器是 Konqueror/文件管理器。（Mozilla 套件已重命名为 SeaMonkey，可以通过 `seamonkey` 软件包在 Fedora 中提供。）

从 Web 收集内容的较新方法包括 RSS 馈阅读器，例如 lifera RSS/RDF 馈阅读器。还有几个浏览器，如 `lynx` 和 `w3m`，它们可以从命令行运行（无需图形界面）。

- **电子邮件客户端** — Evolution 已经演变成了一个功能齐全的套件，它将电子邮件阅读器与管理联系人、日历和任务的功能相结合，并支持连接到 Microsoft Exchange 服务器。Thunderbird 是来自 Mozilla 项目的一款新兴电子邮件客户端（SeaMonkey 同样由该机构提供）。对于那些偏于老式电子邮件阅读器的用户，`mut`、`pine` 和 `mail` 命令允许你从命令行读取邮件，但它们处理附件、HTML 或其他现代电子邮件功能的能力通常有限。

- **FTP** — 如果你使用 FTP 协议从 FTP 服务器下载文件，或将页面上传到你的服务器，用于此类任务的图形化工具包括 `gFTP` 和 `kGet` 应用程序。许多 shell 命令也可以访问 FTP 服务器以锁定文件、下载或上传文件。这些命令包括 `ftp`、`ncftp` 和 `tftp`。
