
Chapter 3 provides descriptions of the applications (both graphical and command line) that come with DSL. Chapter 4 tells how to make DSL look and feel the way you like, and how to save all your personal settings and data for the next reboot. Chapter 5 shows how to get additional software, packaged as MyDSL extensions, to add the applications you want to your DSL configuration.

Part II, “DSL Beyond the Live CD”—To help you do more than simply run DSL from a live CD, chapters in this section address how to run DSL in different ways and on different media. Chapter 6 addresses how to install DSL on a USB flash drive (pen drive) to have a totally portable and writeable live DSL.

In Chapter 7, you learn how to run DSL virtualized so you can use it on a Windows desktop system. Chapter 8 describes alternate ways of installing DSL to a hard drive, including setups where a CD drive is not available (using floppies, Zip drives, or other media). Chapter 9 covers more traditional hard drive installs, where all DSL files are copied and booted from a hard drive.

- **第三部分，“创建扩展与重新制作”** — 本部分深入探讨 DSL 的更多技术层面。第 10 章介绍 DSL 的 MyDSL 功能如何为你的 DSL 系统添加应用程序，包括创建你自己的 MyDSL 扩展的方法。第 11 章描述重新制作过程，以便你可以为自己构建一个自定义版本的 DSL。
- **第四部分，“制作 Damn Small Linux 项目”** — 本部分介绍使用 DSL 构建有趣项目的方法。第 12 章介绍 DSL 可以运行的各种炫酷且不同类型的硬件。第 13 章中，你可以学习如何使用 Edna Music Server 软件在 DSL 中制作音乐服务器。第 14 章展示如何将 DSL 系统设置为 Skype VoIP 客户端，以便通过互联网进行音频通话。第 15 章学习构建基于 DSL 的数字媒体相框。第 16 章讲述如何使用 DSL 和 XAMPP 项目搭建一个体积虽小但功能完备的 Web 服务器。
- **附录 A，“关于 CD”** — 本附录详细介绍随书附带 CD 的内容。CD 包含了你运行书中所有过程并构建所描述项目所需的所有组件。
- **附录 B，“使用 MyDSL 扩展”** — 本附录介绍了一些免费的 MyDSL 扩展，你可以下载、安装并存储这些扩展，以便与你的 DSL 系统一起运行。

## 使用本书需要什么

你应该将本书与随书附带的 CD 一起使用。当然，你也可以不借助 CD 来阅读本书，但如果你手上有 DSL，书中的描述和说明将最有帮助。

要使用随书附带的 CD，你真正需要的只是一台个人电脑。最简单的方法是使用 PC 启动 CD。不过，如果你的 PC 没有 CD 驱动器，我们还提供了让 DSL 在旧机器上运行的说明，这些机器可能包括用于启动系统的软驱或 Zip 驱动器。

你可能需要准备替代介质来存储你的 DSL 数据。特别是，U 盘（也称为 pen drive 或 thumb drive）作为存储你的 DSL 设置、数据以及 DSL 本身的介质尤其有用。

本书最后一部分描述的一些项目需要额外硬件。查看第 12 章，了解一些适合运行 DSL 的有趣 PC 硬件。扬声器和麦克风对于第 13 章和第 14 章的音频项目很有用。制作数字媒体相框需要一台旧笔记本电脑、一个相框以及其他一些小部件。

## 第一部分：使用 Damn Small Linux

- **第 1 章** Damn Small Linux 概述 9
- **第 2 章** 启动 DSL 29
- **第 3 章** 使用 DSL 应用程序 47
- **第 4 章** 配置和保存 DSL 设置 71
- **第 5 章** 使用 MyDSL 扩展应用程序 99

### Damn Small Linux 概述

Damn Small Linux 的口号是 *小就是美*。

Damn Small Linux（DSL）体积约为 50MB，是一款功能完备的迷你 live CD 桌面操作系统。尽管体积小，DSL 几乎可以完成现代桌面系统所能做到的一切，例如浏览网页、收发电子邮件、编写文档、管理文件、播放音乐、处理电子表格以及编辑图像。

许多提供类似软件功能的操作系统需要大量昂贵的计算机硬件才能良好运行，并且背负着缓慢、臃肿的应用程序。Damn Small Linux 则采取了不同的策略。

与其他计算机系统不同，DSL 所打包的应用程序都是根据其体积、速度和高效特性来选择的。即使在低功耗硬件上，DSL 中的应用程序也快得惊人，且功能强大得令人惊叹。尽管体积很小，但在桌面操作系统需要完成的最重要任务上，DSL 的运行速度比许多桌面操作系统更快、更高效。

你手中拿的这本书是 *《官方 Damn Small Linux 手册》*。我们称之为官方，是因为本书的作者包括了 DSL 的两位关键开发者：Damn Small Linux 的创造者 John Andrews，以及 DSL 中许多技术创新的首席开发者 Robert Shingledecker。

虽然本书会逐步介绍你在 DSL 中可以使用的组件，它还会带你走得更远。你将学习如何从不同设备安装和运行 DSL，在重启后保存数据，以及根据需要向 DSL 添加应用程序。之后，本书将指导你如何使用 DSL 构建项目，例如音乐服务器、互联网电话服务和便携式 Web 服务器。

#### 衡量 DAMN SMALL LINUX 的成功

尽管体积小，Damn Small Linux 一直稳居最受欢迎的 Linux 发行版之列。根据监控 Linux 网站的各大网站排名，DSL 一直位居最活跃之列。据 Google 统计，网络上关于 Damn Small Linux 的引用接近 1,000,000 条。Yahoo 显示，指向 Damn Small Linux 主页的入站链接约为 1,480,000 条。

在 DistroWatch（www.distrowatch.com）过去三年中，DSL 在页面点击量上一直稳居 Linux 发行版前十名，常与 Debian、Slackware、KNOPPIX 和 Gentoo 等知名 Linux 系统并列。根据监控网站流量的 Alexa（www.alexa.com）数据显示，2007 年初，DSL 网站（www.damnsmalllinux.org）在网络上的流行度约为 33,350 名。这一排名使其比 Ubuntu、SuSE、Slackware、KNOPPIX、Mepis、Morphix 等 Linux 发行版的主页更受欢迎。

就媒体报道而言，关于 Damn Small Linux 的文章和评测不计其数。2004 年 5 月，DSL 在 TechTV 的 The Screen Savers 节目中被重点介绍。DSL CD 已随 Linux Format、Linux User & Developer、Sys Admin、Linux Journal、PC Magazine、PC World、Computer Power User（CPU）和 Linux Pro 等杂志附赠。

尽管 Damn Small Linux 并不是第一个 Linux live CD（事实上，它最初基于 KNOPPIX live CD），但它仍有诸多首创之举。DSL 是首个实现以下功能的 Linux live CD 发行版：

- 提供备份和恢复功能。
- 使用下载脚本在运行时（在 ramdisk 中）添加软件。
- 采用可扩展的软件模块，可从 live CD 或磁盘使用。
- 集成 USB 安装脚本。
- 使用包含 QEMU 虚拟化软件的特殊嵌入式 DSL 版本，可在 Windows 桌面上虚拟运行。
- 提供专为 live CD 或 USB 驱动器设计的低内存扩展。
