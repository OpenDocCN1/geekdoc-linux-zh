
单击工具栏中的小程序图标以连接到无线网络。如果您的无线接入点广播其 SSID，它应该出现在无线网络列表下（类似于图 2.17）。只需单击所需网络，`Network Manager`就会检测正在使用的加密类型（如果有）并要求您输入密码。输入后，`Network Manager`将启动无线连接。密码随后存储在默认密钥环中，这是一个专属于您登录的安全区域。从现在开始，每当您登录到 Ubuntu 时，`Network Manager`连接将自动启动。

如果由于某种原因您的无线网络未出现（您可能隐藏了 SSID），您必须使用“连接到其他无线网络”选项，这将显示图 2.18 所示的屏幕。

![](img/8f9e74e2b343ff525bebfb720a3d8441_78_0.png)

### FIGURE 2.18 Configure your wireless network connection settings using Network Manager.

使用 `Network Manager` 配置您的无线网络连接设置。

`Network Manager` 可以处理 WEP 和 WPA Personal 加密。建议您使用 WPA 加密，因为它比两者更强。

`Network Manager` 还可以使用 `vpnc` 软件连接到 Cisco VPN 连接。使用 `synaptic` 安装它，您将能够根据需要指定连接设置，或者如果您有权访问预定义的配置（`.pcf` 文件），您可以直接将其导入 `Network Manager`。

### Related Ubuntu and Linux Commands

您在执行安装后配置任务时会使用这些命令：

- `acpi`—查看或使用电源管理设置和命令
- `cdrecord`—获取 SCSI 设备信息并刻录 CD-ROM
- `dmesg`—查看 Linux 内核报告的信息

### Reference

- The Linux Keyboard and Console HOWTO—Andries Brouwer's tome on keyboard and console issues; includes many troubleshooting tips.
- http://www.x.org/—The X.Org Foundation, home of X11R7.
- http://www.alsa-project.org—Home page for the Advanced Linux Sound Architecture project, an alternative set of sound drivers for Linux.
- http://www.opensound.com—Commercial sound drivers for Linux.
- `/usr/src/linux-2.6/Documentation/power/pci.txt`—Patrick Mochel's document regarding PCI power-management routes for Linux kernel and PCI hardware support programmers.
- http://tldp.org/HOWTO/Modem-HOWTO.html—One of the newest HOWTOs on using modems with Linux.
- http://tldp.org/HOWTO/Serial-HOWTO.html—David S. Lawyer's Serial HOWTO, with additional information about Linux and serial port use.
- http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html—A description and tutorial on the EIA232 (formerly RS232) standard.
- http://www.qbik.ch/usb/devices/—The place to check for compatibility of USB devices for Linux.
- http://www.linmodems.org—This site provides links to several drivers for controllerless modem use under Linux.
- http://www.linux1394.org/—Home page for the Linux IEEE 1394 project with new information, links to updated drivers, and lists of compatible chipsets and devices.
- http://groups.google.com/—Search Usenet groups through Google; another alternative to http://marc.theaims.org/.
- http://www.linuxquestions.org/—The Linux Questions site, a useful set of community forums that can help you find answers to your more frustrating problems.
- http://cdrecord.berlios.de—Home page for the `cdrecord` command and related utilities.

## CHAPTER 3

## Working with Gnome

### IN THIS CHAPTER

- The Gnome Desktop Environment
- Eye Candy for the Masses
- Basic X Concepts
- Using X
- Starting X
- KDE—The Other Environment
- XFce
- Reference

想象一个全是黑屏白字，或者对你们这些记得的人来说，是绿屏绿字的世界。那曾经是用户访问计算机的主要界面。感谢计算技术的显著发展，现在大多数桌面和工作站平台都已采用图形用户界面或 GUI 作为标准。

Ubuntu 也不例外，其主要窗口管理器称为 `Gnome`（Gnu Network Object Model Environment）。基于简洁设计的理念，`Gnome` 提供了一个丰富而完整的界面，您可以轻松使用它提高生产力。其主要设计目标包括直观的系统，意味着它应该易于上手使用，以及良好的本地化/国际化支持和可访问性。

`Gnome` 建立在 X Window System 之上，X Window System 是许多 Linux 发行版上发现的图形网络接口，为各种图形工具和窗口管理器提供了基础。更 commonly 称为 X，它也可以被称为 X11R7 和 X11（如 Mac OS X 上所见）。源自世界闻名的麻省理工学院，X 经历了多个版本，每个版本都扩展和增强了该技术。开源实现由 X.Org 基金会管理，其董事会由来自开源世界的几位关键人物组成。

思考 X 的工作原理最好的方式是将其视为客户端/服务器系统。X 服务器为已开发以充分利用服务器下可用的图形和网络功能以及受支持库的程序提供服务。X.Org 为许多不同的平台提供版本，包括

Linux 和 Mac OS X。X.Org 最初以 XFree86 的形式实现，当 XFree86 许可证中要加入某些限制时引发了争执，于是 X.Org 被分叉出来。基于在旧版许可证下授权的代码快照，X.Org 在此基础上推进了自己的实现。几乎同时，大多数 Linux 发行版都抛弃了 XFree86，转而将开发和工作重心转向 X.Org。

在本章中，你将学习如何使用 `Gnome` 以及 Ubuntu 中包含的 X 版本。我们将探讨 X 的基本原理，以及如何让 X 在可能影响它的升级后继续工作，例如新显卡或你刚买的那块新平板显示器。我们还将查看 Ubuntu 中包含的其他一些窗口管理器，包括 KDE 和 Xfce。

### Ubuntu 家族

当人们谈论 Ubuntu 时，他们通常指的是 2004 年发布的原始发行版，该版本使用 `Gnome` 窗口管理器。然而，Ubuntu 还有许多衍生版本，它们使用其他窗口管理器，并且你可以自由下载使用。例如，Kubuntu 使用 KDE 窗口管理器，而 Xubuntu 则使用 Xfce。尽管它们在视觉上差异很大，但这三者都依赖于相同的核心系统，而且你也可以通过使用其中一个 *-desktop 元包轻松地将该窗口管理器添加到现有系统中。这些包旨在安装与该 Ubuntu 版本关联的所有基础应用程序，因此安装 `kubuntu-desktop` 包将自动安装 Kubuntu 所需的所有软件，同时保留你现有的桌面环境。

### Gnome 桌面环境
