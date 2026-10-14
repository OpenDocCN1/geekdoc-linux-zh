

## Corel WordPerfect

Corel WordPerfect Version 8 for Linux：个人版是一款办公解决方案，它提供与 Windows 版本相同的文字处理功能，外加许多仅适用于 Linux 的功能。它支持超过 1,000 台打印机，并且是免费的（24MB）下载。有关更多信息，请参阅 http://linux.corel.com。

## AbiWord

AbiWord 是一款小巧、快速且功能齐全的文字处理器。它可在大多数 Unix 系统（包括 Linux）上运行，也可在 Windows 95/98/NT 上运行。AbiWord 可以导入 Word97 和 RTF 文档，可免费获得，并且是开源的。下载文件仅为 770KB，安装版本仅需 1.2MB 的磁盘空间。

如果你曾经想过查看文字处理器的源代码，这里就是你的机会。下载 AbiWord 源代码，做出自己的改进，你就可以构建自己的 AbiWord 个人版本。有关更多信息，请参阅 http://www.abisource.com。

## Development Tools

Metrowerks 的 Code Warrior 是一款流行的跨平台开发环境，适用于 Linux、Macintosh 和 Windows 95/98/NT。有关更多信息，请参阅 http://www.metrowerks.com。

Cygnus Solutions 的 Code Fusion 将最新的开源 GNU 工具（编译器、调试器、库和实用程序）与图形化交互式开发环境相结合，该环境包括代码编辑器、类浏览、构建和调试工具。有关更多信息，请参阅 http://www.cygnus.com。

KAI C++ 是一款跨平台开发环境，旨在提高 C++ 程序员的效率。KAI C++ 调试器也可用。有关更多信息，请参阅 http://www.kai.com。

## LOGGING OUT OF GNOME

要从 GNOME 注销，请在主菜单中选择“Logout”菜单项。为方便起见，你还可以通过右键单击面板，然后从弹出菜单中选择“Add logout button”来在 GNOME 面板上添加注销按钮。

在你选择注销菜单项或单击注销按钮后，会弹出一个对话框提示你确认注销（见下图）。单击“ Yes ”，你的 GNOME 会话将结束。根据系统配置，你将返回到文本模式 shell 提示符或图形登录屏幕。如果你决定不注销，请单击“ No ”按钮。

在 GNOME 注销对话框中，你可以做一些选择。如果你勾选“ Save current setup ”框，下一次 GNOME 会话将以相同的设置和活动应用程序启动。换句话说，如果你在退出 GNOME 时文件管理器和 Netscape 窗口在屏幕上，它们在你返回 GNOME 时会重新启动。

此外，在 Action 面板中，你可以选择“ Logout ”、“ Halt ”或“ Reboot ”。Logout 将结束你的 GNOME 会话，Halt 将关闭你的计算机（为关机做准备），而 Reboot 将重新启动机器。

![](img/3137cdda7122042e86dbeafe9840d4ed_91_0.png)

## 3 CONNECTING TO THE INTERNET

- Setting Up Your Serial Port to Work with Your Modem 64
- Making a Dial-Up Connection to the Internet 68
- Text-Based Internet Tools 73
- Graphical Internet Tools for X Windows 83
- Operating an Internet Site 87
- Help with Linux Networking 89

Linux 是探索在线世界和提供自己的 Internet 服务的绝佳平台。作为个人“冲浪板”，Red Hat Linux 随附了连接到 Internet 服务提供商（ISP）所需的一切，包括 TCP/IP 软件；客户端程序，如 FTP、Telnet、Finger、Mail、Ping、Lynx 和 Netscape。

Linux 还使设置自己的服务器变得容易，以便你可以运营 FTP 或网站，甚至为你的系统提供 Telnet 或拨号访问。如果你梦想成为一家 ISP，Red Hat Linux 产品是构建的绝佳平台。真正好的地方在于 TCP/IP 和所有流行的网络服务都是自动安装并为你预配置的。如果你曾经尝试配置 Unix 网络、设置电子邮件投递或让 Web 服务器运行，你会非常欣赏这个功能。（从技术角度来说，这意味着本地回环、sendmail、inetd、httpd 和其他几个网络守护进程在你启动 Red Hat Linux 时已配置并运行。）

在本章中，你将学习以下内容：

- 如何通过拨号 PPP 连接将你的 Linux 系统连接到 Internet
- 用于 Internet 访问的工具有哪些（文本和图形）
- 如何运营自己的 Internet 站点
- 在哪里获取有关 Linux 网络的更多信息

### SETTING UP YOUR SERIAL PORT TO WORK WITH YOUR MODEM

默认情况下，Red Hat Linux 配置为以 9600 bps 的速度运行你的串行（调制解调器）端口。但现在 33.6 和 56 Kbps 等速度更快的调制解调器相当常见。花钱买了快速调制解调器却不能充分利用它是很可惜的，因此为了获得最佳性能，你必须调整串行端口设置。

除非你有一个非常慢的调制解调器（9600 bps 或更慢），否则你应该使用 setserial 命令使 Linux 能够进行高速连接。根据你的调制解调器速度，在命令提示符下

