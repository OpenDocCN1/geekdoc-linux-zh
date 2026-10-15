
图 5-1 Ubuntu 网站的支持部分显示了适用于特定打印机的驱动程序集。

![](img/52abf93aab42475c48efdfda9a6ba9ad_91_0.png)

## 摄像头

| 品牌 | 链接 |
| :--- | :--- |
| AllTech | HardwareSupportMultimediaams |
| Creative | HardwareSupportMultimediaams |
| Genius | HardwareSupportMultimediaams |
| Helios | HardwareSupportMultimediaams |
| Jansport | HardwareSupportMultimediaams |
| Logitech | HardwareSupportMultimediaams |
| MediaFate | HardwareSupportMultimediaams |
| Micro Innovations | HardwareSupportMultimediaams |
| Philips | HardwareSupportMultimediaams |
| Samsung | HardwareSupportMultimediaams |
| Twin | HardwareSupportMultimediaams |
| Typhoon | HardwareSupportMultimediaams |

图 5-3 摄像头

| 品牌 | 型号 | 驱动 | 支持？ | Ubuntu 版本 | 最后更新 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Creative | Live Effects | No | No | v6.06 (Dapper) | 2006-06-15 |
| Creative | Webcam | No | No | v6.10 (Fancy) | 2006-06-26 |
| Creative | Webcam PQ001 |  | Yes |  | 2007-02-17 |
| Creative | Livestream! | yes | Yes | v5.04 (Hardy) | 2005-04-04 |
| Creative | Webcam no- | Yes | No | v6.06 (Dapper) | 2006-04-10 |
| Creative | Webcam Play (Model PQ050) | ps18 | No | v6.06 (Dapper) | 2006-04-10 |
| LiveCam Webcam | gspca | Yes | v7.04 (Feist) | 2007-03-16 |  |

图 5-4 Creative 摄像头列表

# 第 5 章 安装外围设备

![](img/52abf93aab42475c48efdfda9a6ba9ad_92_0.png)

## 什么是 Wiki？

大多数熟悉广维网的人都熟悉“wiki”这个术语。Wiki 被定义为一组网页或在线资源集合，用户社区可以随时通过添加、删除或更改内容来对其进行编辑。“wiki”一词源于夏威夷语，意为“快速”，正如“它可以被快速编辑”所意。对于 Ubuntu Wiki，注册的社区成员可以在需要时随时添加和更改页面。如果你访问 `https://ubuntu.com/HardwareSupport`，其内容可能与你在随附指南中看到的不同。原因在于社区成员每天都会向这个 wiki 添加内容。

Wiki 是非常实用的工具。像 Canonical 这样的公司使用 wiki 来支持它们的产品，但有些 wiki 包含随机信息，例如流行的 Wikipedia，它是一个基于 Web 的百科全书，任何注册成员都可以向其添加信息……

如果任何人都可以添加或编辑页面，你可能在担心 wiki 的准确性。这可能会成为一个问题，因为并非所有人每时候都能提供准确的事实。得益于社区的支持，wiki 条目中的错误通常会立即被修正，以保持文档的完整性。毕竟，如果一个 wiki 充满了不准确之处，将不会有人继续使用它。

页面底部有一个链接，列出了不需要专有固件的 wiki。除了设备驱动程序外，外围设备还有帮助控制其运行的程序。固件程序不运行在你的计算机上，而是存储在设备本身的电路中，通常在 ROM 芯片中。这些设备与 GNU/Linux 发行版配合良好，并获得了维护此列表的自由软件基金的支持。Ubuntu 发行版认为是一个自由软件系统，本页列出的 wiki `www.fsf.org/resources/hw/cameras` 应该没有任何问题地工作。自由软件基金还维护了许多其他与自由软件工作的设备列表。可以通过访问 `www.fsf.org/resources/hw/` 查看此列表。

![](img/52abf93aab42475c48efdfda9a6ba9ad_92_1.png)

像自由软件基金这样的组织依靠使用其网站和信息的人们工作。作为 GNU/Linux 社区的一员，你可能想要为其中一个或多个组织捐赠资金或担任志愿者。他们乐意接受任何类型的捐赠，不必担心礼物太小。

## 安装外围设备

一旦你有了外围设备，你就需要安装它使其与你的计算机协同工作。像微软 Windows 一样，Ubuntu 也具有即插即用功能。即插即用意味着如果操作系统、BIOS 和设备都支持即插即用，并且驱动程序在操作系统的数据库中，那么只需只需将设备插入计算机的 USB 端口就会启动安装过程。该过程将在极少或几乎没有用户输入的情况下安装设备。如果操作系统的数据库中不存在驱动程序，则用户将必须找到驱动程序以继续安装。

Ubuntu 不仅支持即插即用，而且大多数 GNU/Linux 爱好者还认为它在这方面拥有最好的支持。某些设备插入计算机几秒钟后，系统就会要求你配置设备，因为它已经安装好了。这多方便啊！

图 5-5 显示了当你将新的外围设备插入计算机时确切出现的内容。没有任何东西询问你是否想要安装该设备；Ubuntu 认为，如果你将其插入计算机，你就想安装它。它还不会通过一系列弹出窗口向你展示过程的每一步。记住，Ubuntu 的格言之一是“它能用工作（It Works）”。

然而，一旦安装了设备（无论是打印机、相机还是扫描仪），它将为你提供配置设备的机会。图 5-6 显示了在 Ubuntu 中配置打印机时可用的选项。

![](img/52abf93aab42475c48efdfda9a6ba9ad_93_1.png)

图 5-6 配置打印机

配置非常简单，类似于来自微软 Windows 环境的人习惯的操作。

与过去不同，GNU/Linux 及其支持它的社区在建立一个巨大的、能够与该操作系统无缝且完美运行的外围设备集合方面取得了巨大进展。现在 Dell 已开始提供预装有 Ubuntu 的全新计算机，你可以打赌更多的外围设备制造商将确保他们的产品与 Ubuntu 以及其他 GNU/Linux 发行版兼容。随着更多业务用户开始接受 GNU/Linux，更多业务级外围设备很快将准备好开箱即用与该操作系统工作。

当然，本章列出的资源仅仅接触了 GNU/Linux（尤其是 Ubuntu）在外围设备和使其正常工作方面从其社区获得的支持的一小部分。一个很好的作业是在互联网上搜索更多提供此类信息的网站。

如果你发现任何现有的设备无法工作，不要害怕在 Ubuntu 论坛发帖。让社区知道你是一个新手并需要帮助。通常情况下，答案会比你想象的要快。

# 第二 管理 Ubuntu

![](img/52abf93aab42475c48efdfda9a6ba9ad_93_0.png)

图 5-5 HP Deskjet 打印机的即插即用

## 基础之外：安装额外软件

如何……

- 使用 `Add/Remove` 工具安装软件
- 使用 `Synaptic` 包管理器安装软件
- 从 Ubuntu 仓库安装额外软件
- 从光盘安装软件
- 从外部来源下载软件
- 解包并安装下载的软件
- 使用终端安装软件

我们购买使用计算机是为了让它们为我们做事情。无论我们想通过电子邮件让生活更轻松，还是用它们玩游戏和听音乐，我们希望它们能做些什么。虽然我们已经学习了关于 Ubuntu 的一些有趣重要的知识，但我确定你们还没有安装这个操作系统。软件应用程序是程序员编写的为我们执行实际工作的程序。文字处理器、电子表格、数据库、多媒体播放器视频游戏都是常见的软件类型。为了让我们的计算机完整，我们需要添加一些应用程序。

### 预装软件

当你启动计算机时，你的 Ubuntu 桌面顶部三个标签。第一个是 Applications。我们在本章大部分时间都会在这里。点击 Applications 标签，我们会看到一个下拉菜单，其中包含了已安装在计算机上的应用程序类别。列表最后一项 `Add/Remove` 是唯一不包含已安装软件的项目。相反，此工具用于启动一个程序，允许你安装和卸载下一节介绍的四个应用程序仓库中的软件。
