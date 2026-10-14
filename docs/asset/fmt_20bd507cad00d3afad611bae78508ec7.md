
进入 `~/.gimp/` 目录，找到用户配置文件以及用户画笔、纹理等。当 GIMP 完成本地文件的安装后，它会启动 GIMP 控制面板并出现 GIMP “每日提示”对话框。GIMP 控制面板是用于选择工具或创建新画布绘图的主面板。请见图 24-1 的截图。

![](img/494a93e1dbdce90cc5cca36f1589d45f_492_0.png)

图 24-1：GIMP 控制面板是你编辑图像的工具箱。

GIMP “每日提示”是一种让你意识到 GIMP 某些功能的友好方式。请见图 24-2。

![](img/494a93e1dbdce90cc5cca36f1589d45f_492_1.png)

图 24-2：GIMP “每日提示”是教授常用技巧或功能的友好方式。

你可以点击“上一个提示”（Prev. Tip）或“下一个提示”（Next Tip）按钮查看更多提示。你可以点击“关闭”按钮关闭窗口。

如果你是 GIMP 的新手，你一定好奇光凭这一个小工具栏 GIMP 能有多强大。答案是，出乎意料地强大。GIMP 的许多功能位于画布上的弹出菜单中。画布是显示图像的区域。在画布上的任何地方点击右键即可弹出上下文相关菜单（见图 24-3）。

## 3D 图形处理

Linux 中的 3D 工具和 2D 一样多。我将在本节中讨论此类工具。

### POV-Ray

我想讨论的第一个 3D 工具是一个免费的光线追踪程序，称为持久视觉光线追踪（POV-Ray）。光线追踪程序接收你想要创建的的物理描述，包括图像中对象的形状、颜色、纹理以及照明它们的光源。通过这些描述，光线追踪程序会计算光如何从物体反射到虚拟摄像头的上。这是一项计算密集型任务，因此创建你的 3D 图像需要长时间。

图 24-4 显示我使用名为 AC3D 的 3D CAD 程序和 POV-Ray 创建的图像。我使用 AC3D 建模了 3D 对象。然后将这些对象导出到 POV-Ray 描述文件并运行 `povray` 生成 PNG 文件。

![](img/494a93e1dbdce90cc5cca36f1589d45f_494_0.png)

图 24-4：使用 POV-Ray 生成的 3D 图像。

图 24-4 中的图像绝不能代表你使用 POV-Ray 和 3D 建模器可以创建的内容。我那笨拙的手在几分钟内就创建了图 24-4 中的图像（我形象地将其命名为 Thingy）。如果你无法想象一位资深艺术家能做什么，你应该查看 http://www.povray.org/ 上的 POV-Ray 画库。

# 第四部分 ♦ 工作站

## 3D 建模

3D 建模工具允许你创建并可能为 3D 图像制作动画。你可以从他们的网站 http://www.ac3d.org 下载我在上一节中提到的 AC3D 共享软件（shareware）建模器。它具有非常直观的界面，易于使用。你必须购买完整的、未阉割的版本。

另一个提供免费基础版且能够进行 3D 建模和动画的软件包是 `blender`。你可以通过 http://www.blender.nl/ 了解更多关于 `blender` 的信息。`blender` 的界面不够直观，在你开始为你的钱制作光影魔术（Industrial Light and Magic）之前，你可能需要先下载手册。

![](img/494a93e1dbdce90cc5cca36f1589d45f_495_0.png)

如果你正在寻找更多 3D 渲染工具，你应该访问 Blue Moon Rendering Tools 网站 http://www.bmrt.org/。在那里你将找到遵循 RenderMan 标准的免费工具。RenderMan 是由皮克斯创建的 3D 场景描述格式。它是设备无关的——这意味着该描述并不指示如何渲染 3D 场景。它可以通过扫描线（scanline）、光线追踪（raytracing）、辐射光度（radiosity）或其他方法进行渲染。

## 多媒体

多媒体一词是指音频、视频和用户交互的混合。你会在 Linux 上找到许多属于此类别的应用程序——从音频播放器到电影文件播放器；从 Video4Linux (http://www.exploits.org/v41/) 等电视接口软件，到用于 X10 (http://www.x10.com/) 的家居控制软件。

我实际上在第 22 章“网络和互联网工具”中涵盖了许多多媒体应用。“数据和应用管理”章节涉及了为 Netscape Communicator 浏览器配置辅助插件和应用程序。

### Xanim

Xanim (http://xanim.pubn.com/home.html) 是一款音频视频播放器，可能是今天 Linux 上最流行的播放器。它是免费的，能够播放目前的大多数视频和一些音频格式。它的 DLL（插件）架构允许支持专有的、闭源视频解码器，这意味着播放器仍然可以以开源的方式向公众发行，只需以二进制形式包含专有的视频解码器。

Xanim 可以播放以下格式：AVI, Quicktime, SGI, Replay, FLI, FLC, IFF, GIF87a, GIF89a, DL Animations, Amiga MovieSetter, RLE Images and Animations, JFIF Images, 有限 MPEG, WAV 音频和 AU 音频。

Xanim 虽然可以播放的文件格式非常多样，但其用户界面并不理想。Xanim 提供了适用于 KDE 和 GNOME 的前端，以给 Xanim 提供一个更漂亮的界面进行操作。要了解更多关于 KDE 前端和 GNOME 前端 Xanim，请分别查看 http://www.geocities.com/SiliconValley/Haven/3864/aktion.html 和 http://www.iag.net/~aleris/xanimim.html。图 24 显示了 action 的运行情况。

![](img/494a93e1dbdce90cc5cca36f1589d45f_496_0.png)

你将在第 22 章找到关于如何安装 Xanim 及其 DLL 的说明。

### 音频

如果没有出色的音频，多媒体体验将损失一半。如果你的音频设备不支持当前的 Linux 声卡驱动，你应该考虑来自 4Front Technologies (http://www.opensound.com/) 的商业产品，或者来自当前开发中的项目的实验性驱动，例如高级 Linux 架构（ALSA）项目 http://www.alsa-project.org/。ALSA 项目是用于创建下一代音频架构的几个不同项目。ALSA 的优点在于它与现有的 OSS 音应用程序兼容，并支持广泛的声卡。

你可以在 http://www.opensound.com/ossapps.html 找到相当长的音频应用程序列表。你还应该检查 GNOME 或 KDE 菜单中的多媒体菜单。

### Video4Linux

Video4Linux 项目正在为视频源开发一种通用 API，包括电视调谐器、帧采集器和 FM 广播调谐器等设备。Video4Linux 现在作为内核的一部分分发，并以不同程度支持多种芯片组，包括：

- AccuTV/Video (TV-500/PBTV 5)
- BTT (Bt848)—也被称为 WinTV 等
- DCI (MIRO DC1+)
- I2C
- Iomega Buz
- ATI 电视卡
- Pinnacle/Miro DC30
- PixelView
- PowerMacPlanB
- Zoran。

你必须在内核中以模块或内核部分的形式启用 Video For Linux 支持。你可以通过 http://www.exploits.org/v41/ 了解更多关于 Video4Linux 的信息。

如果你正感到怀旧，并且喜欢射击游戏，TurboLinux 在其配套的 CD-ROM 中带了公共版本的《毁灭》（Doom）。你也可以从他们的网站下载。

如果你正在寻找 Linux 的最新游戏，请查看 http://www.happypenguin.org/  Linux 游戏大全。你可以在 http://www.linuxgames.com 找到最新的 Linux 游戏新闻。在 LinuxGames，你不仅能找到 Linux 游戏的当前动态，还能找到许多其他游戏网站的链接。你还会找到让你的 Windows 游戏在 WINE（即适用于 Linux 的 Windows API）下运行的链接——当然，WINE 尚仍在开发中，你无法保证你的 Windows 游戏一定能运行。

## 游戏

在这一节中，我提到了一些著名的游戏——大多是我玩过或或在远处赞赏过的。

### 文明：权力召唤以及其他 Loki 游戏

《文明：权力召唤》（Civilization, Call To Power）是我为 Linux购买的第一款商业游戏。这是一款基于策略的游戏，看起来与其 Windows 版本完全一样。你可以从 Loki Entertainment 购买《文明：权力召唤》。

Loki 将其他主流游戏移植到了 Linux，包括：Bumble Software 的《Myth》、《PopTop Software 的《铁道大亨 II》（Railroad Tycoon II）、Delta Tao Software 的《Eric 的终极纸牌》，以及 Activision 和 Raven 的《异教圣 II》（Heretic II）。Loki 将发布 3DO 的《魔法门英》（Heroes of Might and Magic）。这些游戏都可以在 Loki 的网站上，或者最可能在你附近的零售店购买（如果他们销售 Linux 产品的话）。

### 霍普金斯 FBI

也许我注意到的第一个专门为 Linux 提供的商业游戏之一是 MP Entertainment 的《霍普金斯 FBI》（Hopkins, FBI）。这是一款角色扮演游戏，你作为霍普金斯探员必须调查各种犯罪现场并追捕坏人。故事带有卡通风格，内容绝对面向成年玩家。它的体验非常像在跟随一本互动漫画书。如果你喜欢这类游戏，可以在 http://hopkinsfbi.com 了解更多信息，那里提供可玩的演示版。

### 毁灭、要夺 I、要夺 II、要夺 III 以及虚幻竞技场

3D 射击类游戏是我最喜欢的游戏类型。Linux 社区幸运地得到了 ID 软件的支持，因此《毁灭》、《要夺 I》、《要夺 II》和《要夺 III》都可以在 Linux 上运行。《要夺 III》是该软件首次专门为 Linux 发布版本。你可以从 Loki 或其他销售 Linux 软件的地方获取《要夺 III》的 Linux 版本。过去，你需要购买该产品的 Windows/DOS 版本，然后安装 Linux 二进制部分。现在，你可以购买专门为 Linux 设计的所有版本的《毁灭》和《要夺》。Macmillan 软件现在将之前的《要夺》、《要夺 II》和《毁灭》的盒装 Linux 版本捆绑销售。（有关 Macmillan 软件的更多信息，请参见 http://www.infomit.com/linux/macmillan-software/。）《要夺 III》采用了一个我非常喜欢的收藏闪亮铁盒包装。

Epic Games 凭借《虚幻竞技场》（Unreal Tournament）加入了 Linux 游戏领域——它是《要夺 III》的强力竞争对手。遗憾的是，Epic 选择不发行盒装 Linux 版本。你必须购买 Windows 版本并从他们的网站下载 Linux 二进制文件。可以在 http://www.unrealtournament.com 获取可玩的演示版。

### 角色扮演游戏

存在一整个在线角色扮演游戏类型。虽然较新的游戏发生在 3D 现实中，但这种类型的游戏已经存在很长时间了。在互联网早期，人们在多用户地下城（MUDs）中相遇。这些基于文本的游戏允许人们登录到远程系统并互相聊天，或者玩在线版的“地下城与龙”。虽然基于文本的 MUD 版本仍然流行，但 3D 版本似乎正越来越受欢迎。

也许最有野心的 3D MUD 项目是 WorldForge，你可以在 http://www.worldforge.org/ 找到它。WorldForge 的设计使是是服务器部分（即维护世界描述的部分）独立于客户端。客户端是一个独立的程序，用于向玩家显示世界。这允许基于文本、基于 2D 以及广受欢迎的基于 3D 的客户端存在。WorldForge 可能会桥接硬核文本角色玩家与新奇的 3D 角色玩家之间的鸿沟。WorldForge 目前似乎还无法玩。

另一个基于 WorldForge 的角色扮演游戏是 Majik 3。它的开发进度似乎更远，但项目目标的范围要小得多。你可以在 http://majik3d.org 了解更多更多信息。

虽然许多角色扮演游戏发生在中世纪，但也有许多游戏发生在太空和其他地方。一个例子是《星际战战》（X-Ship wars），你可以在 http://fox.mit.edu/xsw/ 找到它。

### 其他

Linux 有可用的飞行和太空模拟器，例如 Parsec http://parsec.org。还有 2D 多人飞行和策略游戏，如 Nettrek http://www.netrek.org。

这个列表可以永远延伸下去。祝游戏愉快！

### Linux 游戏非常重要

原生游戏对于 Linux 的持续增长非常重要——不仅对于玩家，对于每一个希望 Linux 成为现代操作系统操作系统。来自 Activision 等大型游戏制作商的支持将确保最新的音效和图形硬件支持 Linux。我们作为消费者可以通过购买 Linux 原生游戏来保持这种势头。现在你应该能在 CompUSA 及其他地方买到《权力召唤》了。

## 总结

在本章中，你体验了 Linux 能做什么。首先，你了解了一些游戏。然后，你了解了一些应用程序。最后，我讨论了 Linux 的现状。

## 第 24 章 ♦ 图形、多媒体和游戏应用 471

## 服务器

## 第五部分

本部分内容

- **第 25 章**: 使用 Apache 提供 Web 服务
- **第 26 章**: UNIX 和 Windows 文件服务
- **第 27 章**: 防火墙、IP 伪装与代理
- **第 28 章**: 电子邮件与新闻
- **第 29 章**: 使用 FTP 提供文件
- **第 30 章**: 网络信息服务

## 使用 Apache 提供 Web 服务

在 Linux 上提供网页服务最受欢迎的选择是 Apache。Apache 是互联网第一的 Web 服务器，超过 50% 的 Web 服务器正在运行它。事实上，根据 2000 年 2 月的 Netcraft 调查，Apache 在互联网网站的使用率达到了 58% 的历史新高。

Apache 是开源的，可在包括 Linux 在内的多个可用。它具有以下主要特性：

- 兼容 HTTP/1.0 和 HTTP/1.1。HTTP/1.1 协议允许从客户端 浏览器发送多个并行请求，提高了网页下载的性能。
- 简单的文本文件配置。所有的 Apache 配置都基于几个简单的文本文件。
- 支持 CGI/1.1 通用网关接口。它还支持使用 CGI 程序。
- 支持基于 IP 和基于名称的虚拟主机。
- HTTP 认证。
- 集成 Perl (`mod_perl`)。
- 提供服务器状态和自定义日志。
- 服务器端包含 (SSI)。
- 可以添加对安全套接层 (SSL) 支持。
- 使用 HTTP Cookie 进行会话跟踪。
- 支持 Java Servlets，允许 Apache 运行服务器端 Java 应用程序。

## 第25 章

本章

- 关于 Apache Web 服务器
- Web 服务是如何运作的
- 安装 Apache
- 配置 Apache
- 用户网页
- 密码保护 Web 内容
- 通用网关接口 (CGI)
- 虚拟主机

Apache Web 服务器是一个非常强大的应用程序。因此，它具有很高的定制性和可扩展性。在本章中，我并不试图提供 Apache 的完整参考指南。相反，我将关注由 TurboLinux 配置的 Apache Web 服务器。我将介绍在 TurboLinux 上启用 Web 访问的必要步骤，以及一些常见的配置选项。Apache Web 服务器的功能极其广泛，IDG Books 专门编写了一本关于该主题的书：由 Mohammed J. Kabir 编写的 *Apache Server Bible*（IDG Books Worldwide 出版，ISBN 0-7645-3218-9）。

- 你可以在 Apache 的官方网站 http://www.apache.org 了解更多关于 Apache Web 服务器的信息。在上面，你可以找到在线文档和手册。

### Web 服务是如何工作的

如今的每个人都熟悉浏览网页。要浏览网页，你使用一个名为 Web 浏览器的程序，例如 Netscape Navigator/Communicator。要查看由 Web 服务器托管的 Web 页面，你点击链接或输入 Web URL，http://www.turbolinux.com。URL 的第一部分，即双斜杠（//）之后且第一个斜杠（/）之前（如果存在）的部分，标识了你想要连接的计算机——例如计算机 www.turbolinux.com。这个完全限定域名会被解析为一个 IP 地址，并连接该地址的计算机。URL 的剩余部分，即第一个斜杠 / 之后的部分，指示了你想要查看的 Web 内容。

以下是 URL 的结构拆解：

| 协议 | http:// |
| :--- | :--- |
| 网站 | www.turbolinux.com |
| 文档 | 如果未指定文档，则提供默认文档 |

如果在网站名称后没有指定文档，则会向 Web 浏览器发送默认文档。此默认文档通常称为 `index.html`。当文档从服务器发送回浏览器时，服务器将根据服务器提供的 MIME 类型信息来决定如何处理它。如果文档的 MIME 类型是 HTML，浏览器将显示 Web 内容。

- 你已在第 22 节“网络和互联网工具”中学习了如何配置 Netscape MIME 类型来处理各种类型的数据。

### 服务端

Apache Web 服务器监听一个特定的网络端口（默认是 80 端口），以等待传入的浏览器请求。当 Web 浏览器向 Apache Web 服务器发送请求时，以 root UID 和 GID 运行的主 Apache 服务器进程会产生一个以另一个较低权限的用户运行的子进程。该子进程随后处理用户的请求。通过这种方式，Apache 极地减少了客户端进程与 root 特权进程交互的安全风险。

### 安装 Apache

Apache 随 TurboLinux 安装程序提供。它很可能已经安装并在你的计算机上运行。要确认它是否已安装，请使用以下命令检查你的 RPM 数据库：

```bash
```
