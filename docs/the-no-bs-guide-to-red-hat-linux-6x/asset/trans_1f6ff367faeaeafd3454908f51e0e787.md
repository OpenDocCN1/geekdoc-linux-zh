

微软 Windows——如文件管理器、时钟、计算器、记事本、写字板和画笔——都可以正常运行，Microsoft Entertainment Pack 中的大多数游戏也是如此。然而，更大更复杂的程序（如 Microsoft Word for Windows）可能会运行不佳，有时甚至根本无法运行。

如果你一想到要更深入地了解 Wine 就兴奋不已，那么最新信息的最佳来源是 comp.emulators.ms-windows.wine 新闻组。你也可以在 WineHQ 网站上找到大量在线信息。

## 运行 VMware：工业级虚拟 Windows

VMware 是一个非常酷的软件包，它使多个操作系统及相关应用程序能够在一台机器上同时运行，无需磁盘分区或重新启动。实际来说，这意味着你可以在 Linux 下启动 Windows 95/98，并同时运行两者！

这不是仿真——你实际上是从 DOS 分区启动 Windows，让 Windows 桌面与窗口化的 Linux 应用程序并排运行（参见图 2-3）。你甚至可以在 Linux 和 Windows 应用程序之间剪切和粘贴。现在，我正在 VMware 窗口中使用 Windows 95 和 Microsoft Word 编写本文，而 Linux 版 Netscape 以及一堆其他 Linux 程序正在我的 X Windows 桌面上欢快地运行。

VMware 运行效果极佳，对于任何想要一直使用 Linux 但又离不开某些 Windows 软件包的人来说，它是一个不可或缺的工具。唯一的缺点是 VMware 不是免费的。学生、爱好者以及家庭用户能够以 99 美元购买非商业版本，该版本包含 VMware 商业产品的所有强大功能，但提供的支持极少。如需更多信息，请访问 VMware 网站 http://www.vmware.com/。

![](img/3137cdda7122042e86dbeafe9840d4ed_303_0.png)

图 12-3：在 X Windows 桌面上运行 Microsoft Windows

## 更多 Linux 兼容性工具

如果你是 Macintosh 用户，你可能会想看看 ARDI 的 Executor 2 产品，它是一个适用于 Linux 的 Macintosh 模拟器。它不仅能读写软盘和硬盘上的 Macintosh 格式文件，还能完美运行许多 Macintosh 应用程序。

如果你有多台计算机混合运行 Windows 和 Linux，那么你应该使用 Samba。Samba 提供了一种在两种系统之间共享磁盘和打印机的简便方法，而且最重要的是，它是免费的。你可以在网上 http://www.samba.org/ 了解更多关于 Samba 的信息。

在你的计算机上安装一个新的操作系统会让你与芸芸众生区别开来。让它按你的意愿工作则使你近乎达到大师级地位。本章将向你展示如何调整 Red Hat 启动过程，并按你的喜好配置所有 Linux 硬件和软件设置。如果你是那种在 DOS 下离不开 autoexec.bat 和 config.sys 文件的人，或者如果你能从摆弄 Windows 设备管理器中获得数小时的乐趣，你会喜欢下面的内容。

我们将从探索 Setup 实用程序、Linuxconf、GNOME 控制中心以及其他一些定制技巧开始，帮助你更好地掌控 Linux 系统的运行方式。

## 使用 SETUP 实用程序

Setup 实用程序是一个简单的菜单，可以方便地启动六个不同的系统配置工具。你可以使用它来配置键盘、鼠标、系统服务、声卡、时区和 X Windows。你可以尝试记住 kbdconfig、mouseconfig、ntsysv、sndconfig、timeconfig 和 Xconfigurator 这些命令来执行这些任务，但在命令提示符下输入 setup，然后用箭头键选择要使用的工具则更容易（参见图 13-1）。这些工具都应该看起来很熟悉，因为

![](img/3137cdda7122042e86dbeafe9840d4ed_307_0.png)

安装程序也使用了它们。如果你在安装过程中犯了错误，或者你想更改这些组件的设置方式，Setup 提供了解决方案。或者你可能安装了新的鼠标、声卡或视频适配器。如果是这样，你需要运行相应的配置实用程序，以便 Linux 能够正确检测并与该设备交互。

## 键盘配置

键盘配置程序（参见图 13-2）并不是很有趣。只需告诉 Linux 你拥有什么类型的键盘，然后选择“确定”退出。如果你住在美国并说英语，你可能使用的是美式键盘。

## 鼠标配置

如果你的鼠标不能正常工作，请使用鼠标配置程序（参见图 13-3）来检查问题。如果你的品牌鼠标出现在列表中，请选择它。大多数 PC 配备的是便宜的无名鼠标，因此“通用”选项之一很可能会起作用。如果你使用的是轨迹球而不是鼠标，或者笔记本电脑带有内置指点设备（如 IBM 笔记本电脑上的“小红点”），请尝试将该设备配置为 PS/2 鼠标。

![](img/3137cdda7122042e86dbeafe9840d4ed_308_0.png)

图 13-2：*配置键盘*

