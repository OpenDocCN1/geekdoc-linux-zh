
图像文件格式的开发是为了特定的技术目的（例如无损压缩，即在不牺牲图像质量的情况下缩小文件大小）或为了出于竞争考虑对专有格式的需求。许多文件格式受一个或多个专利保护。例如，`GIF`格式在开源社区中已不再青睐，因为专利持有者最近才决定执行其专利。

如果你想查看或处理图像，你需要识别文件格式以选择正确的工具来处理图像。文件的扩展名是判断文件格式的首要指标。Red Hat 自带应用程序支持的图形图像格式有：

- `.bmp`—位图图形，通常用于 Microsoft Windows
- `.cgm`—计算机图形元文件
- `.g3`—CCIT Group 3 传真图像
- `.gif`—ComputerServe 图形交换格式
- `.ico`—Microsoft Windows 图标图像
- `.jpg`—联合图像专家组
- `.mng`—多图像网络图形图像
- `.pbm`—便携位图文件格式
- `.pcx`—IBM 漆刷
- `.pgm`—便携灰度图文件格式
- `.png`—便携网络图形
- `.pnm`—便携任意位图
- `.ppm`—便携像素图文件格式
- `.rgb`—原始红、绿、蓝采样
- `.rs`—Sun 光栅图像
- `.svg`—可缩矢量矢量
- `.tif`—标记图像文件格式
- `.xbm`—X 位图图像
- `.xpm`—X 像素图，通常用于 Linux 图标图像

你可以在 ImageMagick 的 man 页中找到广泛的图像文件扩展名列表，它是 Fedora 自带的一个优秀应用程序，你将在本章后续章节中学习更多关于它的信息。

> 提示 Fedora Linux 包含了几十个图形转换程序，几乎没有一种图形格式是无法使用 Linux 进行处理的。这些命令可以在 Perl 脚本、shell 脚本或命令行管道中使用，以处理许多类型的复杂格式转换和图像处理任务。请查看 `pbm`、`pnn`、`pnm` 和 `pgm` 系列命令的 man 页。还请查看 `convert` 命令的 man 页，它是 ImageMagick 件包含的一系列极其强大的程序的一部分。

通常，你想要以某种方式处理的文件可能是你的图形应用程序或最终应用程序都无法使用的格式。解决方案是转换图像文件——有时需要经过几种格式。ImageMagick 的 `convert` 实用程序作为 netpbm 系列工具非常非常有用。如果尚未安装，可以通过“系统设置”菜单中的“删除软件”GUI 安装 ImageMagick；而 netpbm 工具总是默认安装的。

`convert` 实用程序转换 ImageMagick 识别的图像格式。在转换过程中还可以处理颜色深度和大小。你可以使用 ImageMagick 拼接图像、为其添加边框、旋转和着色，并执行其他适合脚本编写的操作。与 ImageMagick 相关的命令包括 `display`、`animate`、`identify` 和 `import`。该应用程序支持超过 100 种不同的图像格式（全部列在 ImageMagick 的 man 页中）。

## 玩转 ImageMagick 的 identify

你可以使用 ImageMagick 的 `identify` 命令来识别图像文件的细节。用于 GRUB 引导加载器的欢迎启动图像位于 `/boot/grab` 并且是 gzip 压缩的 gzipped.xpm。如果你对该图像运行 `identify`，你会发现它是一个 640x480 的图像，具有 16 位颜色深。这些就是你构建自己的替换图像所需的所有内容。使用 GIMP 或或其他图形工具，裁剪或缩放你选择的图像为 640x480，并将颜色深度改为 16 位。将图像保存为 `splash.xpm`，然后对生成的文件进行 gzip 压缩。替换原始 Hat 文件，你现在拥有了一个自定义启动镜像。使用 `identify` 帮助你复制了原始图像的参数，以符合 GRUB 的要求。

`identify` 命令对于识别未知图像文件并确定它们是否损坏非常有用。

`netpbm` 工具默认安装，因为它们构成了图形格式处理的基础。每个图像格式的 man 页都列出了相关的转换实用程序，这些实用程序的数量可以让你对该格式的使用方式以及如何在其基础上构建有所了解：

- `ppm`（便携像素图文件）的 man 页列出了 47 个与 `ppm` 相关的转换实用程序。这是合理的，因为 `ppm` 或便携像素图被认为是彩色图像文件的最小公约数。由于如此，它经常被用作中间格式。
- `pgm`（便携灰度图文件）的 man 页列出了 22 个转换实用程序。这是合理的，因为 `pgm` 是灰度图像的最小公约数。
- `pnm`（便携任意位图）的 man 页列出了 31 个转换实用程序。然而，由于 `pnm` 与 `ppm`、`pbm` 协同工作，它是单色格式的最小公约数。
- 对 `pbm`（便携位图格式）的检查显示没有相关的转换实用程序。`pbm` 是单色格式，并且是其他相关格式的基础。

## 捕屏

你可以使用图形处理工具捕获显示在屏幕上的图像。虽然这种技术被用于本书的制作，但它有更广泛的用途；“一画胜于万言”这句话是有道理的。有时，展示一个例子比描述它要容易。

捕获的图像（也称为截屏或截图）可以用于说明应用程序中的错误或难以复制的对话框。在本节中，你将学习如何为了这些或其他目的获取屏幕。

在使用 GNOME 桌面时，你可以利用内置的截图机制（`gnome-screenshot`）。通过按下 Print Screen 访问该工具（Alt+Print Screen 对当前窗口截图）。捕获的图像保存为 `.png` 格式。

你还可以使用 Red Hat Linux 支持的工具从远程计算机捕获屏幕。`import` 命令（ImageMagick 的命令之一）被用于本书的截图，例如，使用局域网上的本地计算机和远程计算机。

首先，我们在远程计算机上运行 `$ host +` 以允许其他计算机访问远程机器上的 X 服务器；获取屏幕的命令在我们的本地机器上运行如下：

```
$ import -window root -display 192.168.168:0 26fig7.jpg
```

这种实用程序让一项困难的任务变得困难，因为出版者要求从 800 × 600 的屏幕（太小而不方便操作）进行截图，以适应其打印和制作设备。

我们还可以使用经典的 UNIX 工具 `xwd` 来截图。命令看起来与 `import` 类似：

```
$ xwd -root -display 192.168.168:0 -out 26fig7.jpg
```

虽然可以使用 GIMP 截图并保存为相应的格式，但我们本必须在那台计算机上运行 GIMP 并在每次捕获图像时导航菜单——`import` 的远程选项非常方便。

# 第 26 章 多媒体应用

我们没有使用 Ksnapshot（未包含在菜单中，但可以通过命令行使用），因为它不支持发行商以前使用的 `.pc` 格式，而且它必须在本地运行，不过它可以轻松地截屏，是我们在单机上使用的首选工具。

## Linux 游戏

Red Hat Linux 有三种游戏来源：GNOME 游戏、KDE 游戏和 X 游戏。它们都是免费开放的。我们最喜欢的是 Shisen-Sho，如图 26.6 所示。更完整的列表可以在本章末尾找到，但玩这些游戏的乐趣之一在于自己发现它们。

许多街机风格和动作游戏可用于 Red Hat Linux。此外，还有像纸牌类的传统的纸牌游戏以及像象棋这样的传统的棋盘游戏。Linux 上也有更复杂的商业游戏，Fedora Core Linux——在借助外部帮助的情况下——也可以用来玩这些游戏。

![](img/7e0718570ccf16ae88870f5f49b7faed_901_0.png)

**图 26.6** 用不超过三条直线连接匹配的瓷砖，比你想象的要更有挑战性。

由于它们的流行，我们将检查为 nVidia 显示卡安装专有驱动程序的过程，并安装来自 Epic Games 的免费版 Unreal Tournament 2003 演示版。

## 安装 nVidia 视频驱动

Fedora 不提供官方的 NVIDIA 显示驱动程序，因为它们是闭源的。最新的驱动可以从 http://www.nvidia.com/object/linux.html 下载。Linux 2.6 内核系列实际上并没有开箱支持 NVIDIA 显卡驱动程序，这是由于一个内核“特性”将栈大小限制在 4KB。NVIDIA 驱动程序需要旧的 8KB 栈大小，而该大小现在已经从内核中完全删除了。

遗憾的是，唯一的解决办法是获取一个具有较大栈大小的内核。一个已知与 NVIDIA 驱动程序兼容的修改 2.6.7 内核可以在 http://www.linuxant.com/driverloader/wlan/full/downloads-fc2-kernel-i686.php 找到。

## 安装 Unreal Tournament 2003

免费演示版可以从主页 http://www.unrealtournament.com/ 或从互联网上的任何来源下载；不过，这是一个 96MB 的下载文件。下载完成后，可以使用命令安装游戏：

```
# sh ./ut2003demo-lnx*.sh.bin
```

它默认将安装在 `/usr/local/games/ut2003_demo`。可以使用以下命令启动游戏：

```
$ /usr/local/games/ut2003_demo/ut2003_demo &
```

一个很棒的功能是通过 Loki Installer 提供的在线更新。（感谢 Loki 为我们移植到 Linux 的所有这些棒游戏！）只需 cd 进入你安装 UT2003 的 `.updater` 目录，然后运行：

```
# /oki_update /usr/local/games/ut2003_demo/
```

此命令会为你更新游戏。

## 安装 Wolfenstein—Enemy Territory

虽然早期的《Return to Castle Wolfenstein—Enemy Territory》既有单机模式也有多人模式，但免费提供的《Wolfenstein—Enemy Territory》仅限多人模式。提供 Win32 和 Linux 原生版本，com/。在下载名为 `et-linux-2.55.x86.run` 的 260MB 文件后，使用以下命令安装游戏：

```
# sh et-linux-2.55.x86.run
```

并接受默认设置。在 `/usr/local/bin` 中有一个加载游戏的脚本符号链接。在使用 KDE 桌面时，由于与 KDE 音频守护进程 `artsd` 的冲突，我们遇到了声音问题。解决方法是在 `et` 脚本开头添加一行 `killall artsd`。

如图 26.7 所示，《Wolfenstein—Enemy Territory》与 UT2003 不同，玩该游戏不需要 nVidia 显卡。我们发现该游戏在 16MB 的 Voodoo 3-3000 AGP 显卡上是可以运行的。

![](img/7e0718570ccf16ae88870f5f49b7faed_903_0.png)

图 26.7 团队合作是这个丰富但充满敌意的图形环境的关键。

可以在 http://www.garagegames.com/ 和 http://www.linuxgames.com/ 找到更多 Linux 游戏。一个有趣且鲜为人知的雪板游戏可以在 http://soulride.com/products/jay_peak.html 找到。

> 提示

在 Linux 中成功玩游戏的关键是始终彻底阅读文档，始终彻底研究互联网资源，并始终深入你的系统。安装游戏是学习系统的极佳方法，因为成功的回报非常丰厚。

## 启用 java

某些多媒体内容依赖 Sun 的 Java 和 Java Web 插件。

让 Java 插件在 Mozilla 浏览器中正常工作可能是一项挑战。

从 http://java.sun.com/ 下载最新版本（1.4.1 之前的版本将无法工作）（你可以在 http://dag.wieers.com/packages/j2re/ 找到 atlas 修改过的 `.rpm` 文件）。

作为 root 用户，使用 `chmod +x` 将下载的文件设为可执行，并使用 `./j2re-linux-i86` 将其解包。

http://fame.sourceforge.net/—视频编码工具。

http://teletext.mb21.co.uk/faq.shtml—文字电视常见问题解答（FAQ）。

http://xine.sourceforge.net/—Xine/视频播放器首页。

http://www.MPlayerHQ.nu/homepage/—MPlayer 视频播放器主页。

http://www.vide.org/—一个文档良好的 VideoLAN 项目。

http://www.nvidia.com/object/linux.html—针对扫描器的资源。

http://www.nvidia.com/object/linux_display_archive.html—Nvidia 驱动下载页面。

http://www.ati.com/support/driver.html—下载 ATI 显卡的 Linux 图形驱动程序。

http://fy.chalmers.se/~appro/linux/DVD+RW/—Linux 下的 DVD+RW/-R/-[W]，关于在 Linux 下创建 DVD 的 HOWTO 指南。

# 第四部分

# 附录

# 本部分

附录 A | Fedora 互联网资源 873

# 附录 A

# Fedora 互联网资源

+ 本附录包含

- 网站与搜索引擎
- Usenet 新组
- 邮件列表
- 互联网中继聊天 (IRC)

Linux 拥有丰富的互联网支持，形式包括提供技术信息的网站、特定程序文档、针对性的白皮书、错误修复、用户体验、第三方商业技术支持，甚至是免费的专门精调的克隆发行版版本。

本附录列出了许多支持性的网站、FTP 仓库、Usenet 新组和电子邮件列表，你可以通过它们获取更多信息并为你的 Fedora Core 获取帮助。

> 如果你需要 24/7 服务

如果你是小型企业、公司或企业级 Red Hat Linux 用户，不要忘记你随时可以向源头 Red Hat, Inc. 或第三方公司（例如 Levante，http://www.levanta.com/）寻求 24/7 现场支持、电话支持、电子邮件支持或按次计费的商业技术支持。Red Hat, Inc. 为其软件产品提供一系列支持选项。你可以在购买 Red Hat 软件时访问 http://www.redhat.com/software/rhel/purchase/ 了解更多关于支持选项的信息。

附录分为以下几个章节：

- 按类别排列的 Linux 信息网站
- 与 Linux相关的 Usenet 新组
- 提供 Linux 用户和开发者讨论的邮件列表
- 用于 Linux 信息的互联网中继聊天 (IRC) 群组

# 附录 A Fedora 互联网资源

本附录还列出了在使用 Fedora 或特定组件（如 XFree86）时可能感兴趣的网站。我们已尽力确保 URL 的准确性，但请记住，互联网是瞬息万变的！

# 使用 update 和 yum 保持更新

及时了解错误修复、安全更新和其他错误（errata）对于 Red Linux 或 Fedora 系统的成功和健康至关重要。在使用商用 Red Hat Linux 发行版时，为了跟进最重要的进展，请确保在 Red Hat 网络中注册，订阅 Red Hat 公告，或定期浏览 http://www.redhat.com/security/。你也可以使用 `update` 客户端来维护你的工作站或服务器——你需要订阅 Red Hat 的商业支持。

Fedora 用户可以使用 `yum` 命令（以 root 权限）来跟进错误修复、软件包和安全更新。

# 网站与搜索引擎

世界上存在数以千计的关于 Linux 和 Red Hat Linux 信息的网站。立即获得所需答案的关键在于使用搜索引擎和技巧。在排排除故障时，知道如何搜索可能意味着失败与成功之间的区别。本节提供了一些互联网搜索技巧，并按各种主题列出了 Red Hat、Fedora 和 Linux 相关的站点。这些列表并非详尽，但在编写本文时已经过检查且是可用的。

# 网页搜索技巧

通过搜索 Web 来排除 Linux 问题是获取棘手问题答案的一种高效且有效的方法。进行高效搜索的最基本规则之一是使用特定的搜索词来寻找特定的答案。例如，如果你只搜索“Red Hat Linux”，你会得到过多的链接和信息。但如果你搜索“Fedora Core sound”，你更有可能找到你需要的信息。如果你收到了错误消息，请使用它；否则，使用 Linux 内核诊断信息作为搜索标准。

其他有效的技术还包括：

- 在搜索字符串中使用符号，例如使用加号 (+) 强制匹配包含两个字符串的网页（如果所使用的 Web 搜索网站支持此类功能）
- 在返回的结果中搜索
- 对结果进行排序（通常按日期）以获取最新信息
- 搜索相关信息

# 网站与搜索引擎

- 词干提取（Stemming）：例如，指定搜索不仅返回“link”，还返回“linking”和“linked”

投入时间并尝试你喜爱的搜索引擎的特性——结果将带来更高效的搜索。除了精进你的搜索技巧外，还要花时间根据你的需求选择最佳搜索引擎。

# Google 是你的朋友

Web 上一些最快、最全面的搜索引擎是由 Linux 驱动的，因此使用现有的最佳资源是有意义的。在数以万计的搜索引擎网站中，http://google.com 以每月超过 1000 万的用户脱而出。该网站使用先进的硬件和软件来提高速度并去除重复结果（注：此处 OCR 文本乱码，已根据上下文重建）。

[注：此节提供的 OCR 文本在原文中高度碎片/乱码。我已根据周围的技术上下文重建了逻辑流。]

# Red Hat 软件包列表

你可以使用 `rpm` 命令快速方便地查看已安装 RPM 软件包列表以及每个包的简短描述：

```bash
rpm -qai
```

# 附录 A Fedora 互联网资源

Fedora 用户还可以使用 `yum` 命令查看软件包名称及其信息，如下所示：

```bash
yum info
```

如果你使用 Fedora 且只想查看已安装的软件包，使用 `yum` 的 `installed` 选项：

```bash
yum info installed
```
