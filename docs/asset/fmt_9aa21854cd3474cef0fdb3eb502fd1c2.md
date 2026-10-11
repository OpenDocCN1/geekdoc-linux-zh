
为了开始思考如何用 Linux 制作东西，请观察周围。许多个人、学校和公司已经在各种设备中采用了 Linux。本节描述了人们采用的一些有趣方法。

## 设备中的 Linux

许多商业通信、娱乐和其他种类的设备内部都运行着 Linux。Linux 是这些特殊设备的极佳操作系统，不仅是因为它的成本，还因为它的稳定性和适应性。

Linux 爱好者喜爱这些设备（被称为嵌入式 Linux 系统），因为他们通常可以在这些设备上适配或运行不同的 Linux 软件（无论制造商是否本意）。越来越多的制造商正在拥抱 Linux 爱好者硬件并为其销售开放设备。以下是一些例子：

- 手机——`OpenMoko` (`www.openmoko.com`) 生产基于 Linux 的大众手机，如 `NeoFreeRunner`。就像软件一样，`NeoFreeRunner` 的硬件也遵循开放设计。虽然该手机面向普通消费者，但其手机软件目前最适合想为手机开发自己软件的人。图 2-2 显示了 `NeoFreeRunner` 的示例。

### 图 2-1

火星探测器 (`MER`) 通过车载的 Linux 系统收集数据、发送图像并在火星上移动。

![img/8f71f83ce3d8e208bf71b5b6c9a75bd_48_0.png]

（照片来自 NASA）

## 第一部分：开启 Linux 之路

### 图 2-2

修改软件将 Linux `Neo FreeRunner` 用于手机、GPS 设备、时钟、游戏和媒体播放器。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_49_0.png)

`摩托罗拉` (`Motorola`)、`OpenMoko` 和 `Tranzda Technologies` 都提供了多款基于 Linux 的手机。内部运行 Linux 的手机包括 `Motorola Rokr EM30`（强调音乐播放）、`Tranzda Technologies NewPlus` 手机（带有 WiFi、GPS 和摄像头）、`Purple Labs Magic` 手机（低于 100 美元的手机）以及 `Gruning B700`（带有键盘和电子邮件支持）。

- `Sony PlayStation`——你不仅可以在 `PlayStation` 上安装和运行 Linux，索尼还鼓励你这样做。2002 年，索尼发布了用于 `PlayStation 2` 的 `Linux Kit`。该工具件中包含了日本 `Kondara MNU/Linux` 的衍生版本（其基于 `Red Hat Linux`）。对于 `PlayStation 3`，有几个 Linux 发行版经过了修改（移植）以便在硬件上运行，包括 `Fedora`、`OpenSUSE`、`Ubuntu`、`Gentoo`、`Debian` 以及用于 `PlayStation 3` 的商业版 `Yellow Dog Linux`（关于 `Yellow Dog Linux` 的描述请参见第 22 章）。

- 个人录像机 (`PVR`)—如果你有一个 `TiVo PVR` 或用于流媒体 `Netflix` 的顶盒，你已经在家里运行 Linux 了。`Netflix PVR` 来自 `Roku, Inc.` (`www.roku.com`)，该公司生产了一系列基于 Linux 的媒体播放器。`TiVo` 多年来一直生产基于 Linux 的 `PVR`。`TiVo Linux` 源代码的可用让 Linux 爱好者可以进行研究。

- 笔记本电脑 (`Netbooks`)—尺寸的缩小导致了笔记本电脑的出现。这些迷你笔记本电脑被证明是运行 Linux 的优秀设备。凭借低功耗处理器和小屏幕，笔记本电脑与针对这些快速、高效设备优化的 Linux 系统构成了良好的搭档。

## 第二章：Linux 项目、活动与职业

`华硕 Eee PC` 是目前最流行的笔记本电脑之一。许多 `华硕 Eee PC` 在预装 `Xandros Linux` 的情况下售出。然而，勤奋的 Linux 爱好者创建了 `Fedora`、`Ubuntu` 和其他 Linux 发行版的移植版以便在 `Eee PC` 上运行。`宏碁 Aspire One` 是另一种流行的笔记本电脑。图 2-3 显示了一台运行 `Fedora Linux` 的 `Eee PC`。

### 图 2-3

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_50_0.png)

- 个人手持设备——现在有一系列内置 Linux 的个人数字助理 (`PDA`)、便携式导航设备 (`PNA`) 和便携式媒体播放器 (`PMP`)。`佳明 Nuvi` (`860`、`880` 和 `5000`) GPS 导航设备使用了 `GNOME Mobile Linux` 和 `GeoCloud` 定位技术。`三星 i70` 构建了一个基于 `MontVista Linux` 的内置个人媒体播放器的数码相机。`索尼 mylo` 设备内部运行着 `Qtopia Linux` 系统，它可以让你连接 WiFi 网络、播放 Flash 视频和游戏，甚至录视频。

学习这些以及其他运行 Linux 的设备的好地方是 `LinuxDevices` 网站 (`www.linux-devices.com`)。

## 项目中的 Linux

整个开源项目都致力于特殊用途的 Linux 系统。这些项目可能非常擅长某类活动（例如构建多媒体中心），或者解决某个问题（例如学校电脑预算削减）。以下是人们聚集开源软件的一些示例，你可能会对此感兴趣。

- `MythTV` (`www.mythtv.org`)——在开源个人录像机 (`PVR`) 项目方面，`MythTV` 处于领先。`MythTV` 让你收集你所在地区的电视节目列表，选择你想录制的节目，或者在你准备好时回放录制的节目。除此之外，`MythTV` 还允许你暂停、快进和倒退电视；跳过广告，并从不同类型的视频压缩中选择。

通过将其他开源软件集成到 `MythTV` 界面中，你可以完成许多你意想不到的 `PVR`。你可以提取并播放 `MP3`、`FLAC`、`Ogg` 和 `CD` 音频文件，并将它们分组为列表。你可以使用 `MAME` 和其他游戏机玩游戏。`MythTV` 还包含图像查看器、天气模块和 `RSS` 新闻阅读器。

`Myuntu` (`www.ubuntu.org`) 和 `MythDora` (`www.mythdora.com`) 项目用于在特定的 Linux 发行版上配置 `MythTV`。`KnoppMyth` (`www.knoppmyth.net`) 提供了一个易于安装的基于 `Knoppix` 的 `MythTV` 版本。图 2-4 显示了 `MythTV` 主屏幕的一个示例。

### 图 2-4

使用 `MythTV` 管理你的电视观看、录制和回放。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_51_0.png)

- Linux 终端服务器项目 (`www.ltsp.org`)—使用一个中央服务器和数百台低端 PC 或其客户端，你可以创建一种成本效益的方法，为学校或小企业配备 Linux 工作站。客户端计算机不需要太多性能，因为它们基本上只运行显示器、键盘和鼠标。服务器存储数据、运行应用程序并提供服务。

你可以创建一种成本效益的方法，为学校或小企业配备 Linux 工作站。客户端计算机不需要太多性能，因为它们基本上只运行显示器、键盘和鼠标。服务器存储数据、运行应用程序并提供服务。

## 第2章：Linux 项目、活动与职业

(`www.sourceforge.net`)。它还维护着信息技术网站，如 `Slashdot` (`slashdot.org`)、`NewsForge` (`www.newsforge.com`) 和 `Linux.com` (`www.linux.com`)。

- `IBM` (`www.ibm.com/linux`)——`IBM` 一直是 Linux 相关诉讼的主要接收方，并为推动 Linux 发展做出了巨大贡献，特别是在企业领域。在 `IBM` 网站上有许多针对 Linux 开发者的资源，包括一些关于商业领域 Linux 的优秀白皮书。

- `Bibhiblio` (`www.biblio.org`)——包含海量的 Linux 软件和文档存档（`www.biblio.org/pub//`）。

- 软件自由法律中心 (`www.softwarefreedom.org`)——该机构为现存大多数自由和开源软件（`FOSS`）项目提供法律援助。它是维护 `GNU` 公共许可协议涵盖的软件使用的组织。

- 每个孩子一台项目 (`www.laptop.org`)——`OLPC` 项目是一个致力于通过向世界各地贫困儿童提供笔记本电脑来帮助他们教育的机构。截至本文写作，全球已分发了 300,000 台 `OLPC` 笔记本电脑，使其成为 `Fedora Linux` 系统最大的贡献者。

## 跟进 Linux

尽管 `Slashdot.org` 可能是 Linux 爱好者关注和参与的新闻网站，但其他很多地方可以获取 Linux 和开源新闻：
