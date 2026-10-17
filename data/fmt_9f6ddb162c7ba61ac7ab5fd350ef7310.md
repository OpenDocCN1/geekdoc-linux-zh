
micq 主页 http://phantom.iquest.net/micq/ 提供了下载最新版本的链接，并提供了其他链接以便您下载早期版本。截至本文撰写时，最新版本为 0.4.2，且链接仅提供源代码。

## 安装 micq

从 micq 主页下载源 tarball 并将其放置到合适的目录中。解包它（`tar -xzf micq-0.4.2.tgz`），它将在当前目录下直接创建一个名为 `micq-0.4.2/` 的目录。您应 `cd` 进入该目录并执行 `gmake` 命令编译程序。可执行文件将与源代码位于同一目录中，名为 `micq`。

## 运行 micq

运行 `micq` 时您必须已连接到 Internet。原因不明，`micq` 在执行时立即尝试连接到 ICQ 网络。如果无法建立连接，程序执行将失败。

如果您未将 `micq` 放入默认路径中的目录，则必须移动到其安装的目录或提供相对或绝对路径。命令很简单，就是 `micq`。

`micq` 首次启动时，会要求您输入现有 UIN 或输入 0（零）以注册新用户。然后会要求您输入该 UIN 的密码，`micq` 将尝试连接到 ICQ 服务器。

如果连接成功，您将默认设置为“free for chat”模式。

`micq` 可配置或所需配置很少。源目录中的 `README` 文件提供了额外的使用和配置信息。

## 多媒体会议工具

多媒体会议工具是指任何基于应用程序的工具，用于利用不同类型的媒体（如音频、视频等）进行通信。

目前有三种不同的人与人之间的语音通信类型可用：

- PC 对 PC
- PC 对电话
- 电话对电话

PC 对 PC 是最古老且最常用的个人通信形式。通常要求发起者和接收者都运行相同的软件包，并且在通话期间都必须连接到 Internet。随着越来越多的开发人员采用 H.323 建议，“相同软件”的要求将逐渐被取消。本章的讨论将集中在 PC 对 PC 电话上，并介绍一些可用于 Linux 的 PC 对 PC 语音通信软件。

PC 对电话通信是 PC 对 PC 电话的下一步发展，仅要求呼叫发起者拥有 Internet 连接和适当的软件。使用 PC 对电话通信联系某人依赖于存在一个中介，该中介可以在接收者本地通话距离范围内接入公共交换电话网络（PSTN）。PC 对电话对话按如下方式进行：

- 拥有 Internet 连接的人发起呼叫。
- 呼叫发起者使用其计算机将数字化语音数据发送给中介。
- 作为互联网与 PSTN 之间网关的计算机接收压缩的数字化数据并将其转换回模拟信号。
- 网关随后将模拟数据发送到 PSTN 上。

当呼叫接收方说话时，网关计算机 simply 反向执行此过程；也就是说，网关计算机通过 PSTN 接收正常的语音，然后将其数字化并压缩。数字数据再次通过互联网路由，直到到达呼叫发起方的计算机，通信软件在那里对其进行解压缩并通过声卡播放。

互联网电话的最新发展是电话到电话通信。在这种情况下，双方都不需要互联网连接；事实上，他们甚至不需要计算机！通过互联网的电话到电话通信的工作方式与 PC 到电话类似，只是中间公司必须连接到双方的 PSTN，并且对双方都应处于本地通话距离之内。中间公司还需要在对话双方进行 analog -> digital / digital -> analog 转换。

不幸的是，Linux 在视频和音视频会议方面相对落后。正如本章开头所述，摄像头的驱动程序可用性是一个大问题，找到快速可靠的软件也是如此。

有一些专门设计用于在 mbone 上运行的应用程序，但鉴于许多人无法访问 mbone 或不需要它，这些工具在此未讨论。如果您考虑 mbone 连接，一个寻找工具的好地方是 http://www-nrg.ee.lbl.gov/vic/。该页面提供有关 `vic`（视频会议工具）的信息，并提供链接到组成完整的互联网会议套件所需的其他应用程序。

尽管本节旨在为您介绍多媒体会议的世界，但篇幅不允许进行全面讨论，因此我们主要将讨论限制在 Linux 可用的应用程序上。如果您想进一步了解，http://sunsite.utk.edu/video_cookbook/ 上有关于视频会议的全面讨论。

## Speak Freely

Speak Freely 是适用于 Windows 的成熟音频会议工具，最近已可用于 Linux 平台。Speak Freely 主页位于 http://www.speakfreely.org/。

对许多人来说，Speak Freely for Unix 的缺点是目前它是一个基于控制台的应用程序。主页声明不久的将来将发布 beta X Windows 版本。

### Getting Speak Freely

Speak Freely for Unix 可从 Speak Freely for Unix 主页 http://www.fourmilab.ch/speakfree/unix/ 获取。截至本文撰写时，它仅以源代码形式提供。

### Installing Speak Freely

您应该已将源代码下载到自己的目录中并解包（`tar -xzf speak_freely-latest.tar.gz`）。解包后，您将拥有另一个目录 `speak_freely-7.1`，其中包含源代码和文档。

您必须在尝试编译此程序之前阅读 `README` 和 `Makefile` 文件。由于可用的硬件配置太多，不可能创建可靠的通用 makefile（尽管提供的 makefile 已经相当接近）。请务必遵循 makefile 中的建议，先编译一个简单版本，然后再尝试充分利用您的硬件。

使用此程序的完整说明包含在 man 手册页中。要获取这些手册页，请在构建目录中发出命令 `make manpage`。请注意，在执行此操作之前，您必须定义环境变量 `PAGER`。

制作完手册页后，您应该使用简单的 make 命令来制作程序本身。

### Running Speak Freely

Speak Freely 有多种可能的调用方式，完全取决于您的需求。最好的起点是手册页（尝试 `man sflaunch`）和 Speak Freely for Unix 主页。

## QSeeMe

QSeeMe 是一个集成的音视频会议程序，还允许以类似于 ICQ 的方式聊天。由于 Cu-SeeMe 已不再自由可用，QSeeMe 填补了这一空白。QSeeMe，截至本文撰写时，支持发送灰度视频并接收灰度、M-JPEG 和 H263 视频，以及发送和接收音频和聊天。

### Getting QSeeMe

QSeeMe 可从主页 http://www.pangea.org/~mavilar/qseeme/qseeme.html 获取，仅提供预编译二进制文件。非商业用途分发免费。

### Installing QSeeMe

tarball 将解包到名为 `QSeeMe-0.83b` 的自己的目录中，并包含三个文件。文件 `qseeme.man` 应复制或移动到手册页的适当位置（通常在 `/usr/local/man/` 下的某个位置）。该文件无需格式化，但请确保将文件扩展名从 `.man` 更改为 `.x`，其中 x 是您决定页面所属的手册部分——第 1 节可能是个不错的选择。

文件 `qseeme` 是可执行二进制文件，`qseemerc` 是配置文件，在 QSeeMe 执行时复制到位置 `~/.qseemerc`。同样，该程序几乎不需要配置，手册页已充分解释了可用的选项。

### Running QSeeMe

QSeeMe 必须在 X 会话中使用命令 `qseeme` 启动（假设您已将可执行文件移动到默认搜索路径上的位置）。如果您想继续使用启动程序时使用的 X-term，您可以将其作为后台进程运行而不会有任何问题。

该程序完全由鼠标驱动，非常易于理解。

## CU-SeeMe

最初由康奈尔大学开发，这可能是使用最广泛的视频会议软件。不幸的是，康奈尔大学于 1998 年将该程序的全部权利出售给 White Pine Software (http://www.wpine.com)，CU-SeeMe 已不再为 Linux 平台公开可用，反射器软件也是如此。

White Pine 已宣布已为基于 Linux 的系统发布了名为 MeetingPoint 的反射器软件版本。White Pine Software 网站上有完整详细信息。截至本文撰写时，尚无关于 CU-SeeMe for Linux 何时或是否发布的迹象。

CU-SeeMe 和 MeetingPoint 提供广泛的功能，使会议过程尽可能简单愉快。White Pine 主页上有这两个产品的完整描述。

## Summary

本章介绍了互联网电话和会议的主题。关于互联网电话，讨论了术语、协议和标准等主题。关于互联网中继聊天，回顾了 Zircon 和 Xchat 等几种不同的产品。转向多媒体会议工具，讨论了多媒体会议的概念。此外，还讨论了 Speak Freely 和 QSeeMe 等产品，以及安装和配置信息。

### 25

## CHAPTER

### Security

## Principles

## In This Chapter

- 确定您的安全需求 740
- 保护您的 Red Hat 服务器 743
- 安全监控 772
- 制定安全策略 775
