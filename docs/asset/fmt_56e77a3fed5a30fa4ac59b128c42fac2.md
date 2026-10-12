
下一步是运行 VMware 并安装客户操作系统。将你的 Windows 光盘放入驱动器。在 shell 中进入 Guest 目录，输入 `vmplayer windows.vmx &`（或在桌面环境中按下 Alt+F2 并输入相同的命令）来启动应用程序。将出现带有初始 Windows 安装界面的主屏幕。
你也可以从 KDE 系统菜单启动 VMware Player。在“其他程序”（Other Programs）下查找。
完成客户操作系统的安装后，你可以在其中工作，也可以将其关闭。下次运行 VMware 时，系统会要求你再次定位虚拟机。
虚拟机将接管你的鼠标，但你可以通过按下 Ctrl+Alt 重新获得控制。安装完成后，运行 Windows 更新以查看你的计算机操作系统、软件和硬件需要哪些更新。
要在虚拟机中安装新应用程序，请启动虚拟机并插入你的光盘。在 Windows 中，光盘应该像往常一样自动运行并安装。如果没有运行，请运行 Windows 资源管理器并在光盘上找到安装程序。
运行应用程序的响应速度可能无法像普通环境那样达到 100%，但已经很不错了。你可以在应用程序中发现标准环境中可能会出现的错误，这使其非常适合测试。游戏运行得也很好。
退出 VMware 之前，请始终记住关闭客户端操作系统。

## 使用 Basilisk II 模拟 Mac

苹果 Macintosh 操作系统以及运行其上的计算机，对其许多用户产生了极高的忠诚度。
许多为 Mac 编写的应用程序确实非常出色。但由于 MacOS 从未设计为运行在 Intel PC 芯片上，因此构建一个模拟器，甚至是虚拟机，都是一项艰巨的任务。要感谢 Basilisk II 的创建者 Christian Bauer，这是一个免费 GPL 且稳定的 MacOS Classic 模拟器，他迎接了挑战。
Basilisk 可运行在 Linux、Solaris、FreeBSD、Windows、Amiga 和 BeOS 上，并可以模拟直到 8.1 的任何 68K 版本 MacOS（尽管已为 OS X 编写了端口）。你需要一个来自 Mac 的有效 ROM 镜像才能实现此功能。该 ROM 镜像包含了多个应用程序，包括 Mac Toolbox 和 QuickDraw，并且它是不可或缺的。
Basilisk 支持各种 Mac 色显示器和外设驱动程序。它还可以连接到互联网和你的局域网（LAN）。

## Xen：虚拟化的未来？

然而，这项任务并非弱者所能。你需要从 ROM 镜像创建 Linux 可读的 Mac 磁盘。你需要从源码编译 Basilisk II。你可能需要下载并安装新版本的 macOS。幸运的是，你将在《Basilisk II for Linux——从开始到结束》中为这段旅程找到绝佳伙伴，这是 Marc Hoffman 提供的教程，地址位于：http://emulation.org/basilisk/system753_tutorial/linux/。Sourceforge 项目页面存在多个支持论坛：http://sourceforge.org/projects/basilisk/。点击“论坛”（forums）标签页。

## 使用 dosemu 和 DOSBox

DoseBox 和多功能的 dosemu 是你可以通过 YaST 安装的模拟器。dosemu 可以运行各种 DOS 程序，并附带一个 GPL 版本的 DOS，称为 FreeDOS。DOSBox 带有图形软件包，使其特别适合运行游戏。如果你足够幸运拥有一份 Windows 3.x 备份，你可以在 dosemu 下安装它。这两个应用程序都可以通过 YaST 安装，且 DOSBox 会插入到 KDE 系统中。
dosemu 运行起来稍微困难一点，因为它第一次必须在 X 窗口系统之外运行。可以通过启动虚拟控制台较容易地实现。按下 Ctrl+Alt+F1（或 F2-7 中的任意 F 键，属于 Xen）。
你可以使用密码以 User 身份登录。要加载 dosemu，在此提示符处输入程序 `dosemu`。
系统会要求你提供 DOS 副本；按回车将安装 FreeDOS。默认情况下，你的主目录（Home directory）将是你的 C 盘。你会看到 C:\ 提示符，可以运行任何默认程序或安装你的 WordPerfect 5.1。
完成虚拟控制台操作后，输入 exit 然后按下 Ctrl+Alt+F7 返回桌面。

## Xen：虚拟化的未来？

自 2003 年以来，英国剑桥大学的研究人员一直在研究一种新的操作系统虚拟化方法。他们的项目 Xen 在 2005 年初达到了支持的关键节点。
与构建完整虚拟机的 VMware 不同，Xen 是一个虚拟机管理程序（hypervisor），它是一个没有做到那么深的层。这项技术极大地提高了了系统中客户操作系统的性能，使其接近原生性能。这需要每个支持的操作系统内核都有一个特殊的 Xen 版本。openLinux 通过对标准安装使用标准内核来实现这一点，将内核放入 `/boot`，然后使用引导加载程序启动 Xen 或标准内核。
Xen 开发者移植了多个开源内核，包括 2.4 和 2.6 Linux 内核、NetBSD Unix、FreeBSD Unix 和 Plan9 OS，因此你可以使用 Xen 运行多个 Linux 发行版，并留有一个 FreeBSD 副本。这对某些用户可能很有趣，但对于希望解决发行版相关问题的程序员来说特别有用。在测试 openSUSE 等发行版的预发布版本时也有用。
许多用户的关键问题是 Windows 是否会在某个时候加入支持的操作系统列表。截至本文写作，Windows Server 2003 将在带有较新内核的 Linux Enterprise Server 10 上运行。这项技术极大地提高了客户操作系统性能，使其接近原生性能。这需要像 Intel VT-x 或 AMD-V 这样的硬件虚拟化功能。

# 第11 章 跨平台

## 在 Xen 中安装客户操作系统

一旦设置服务器，返回 YaST。在“系统”（System）页面，“虚拟机”（Virtual Machine）模块等待你的配置。当“管理机器”（Manage）出现时，点击“添加”（Add）。如果你有一个应用的磁盘镜像，这是一个选项。对于本示例，将进行新安装。
查看 Xen 安装的默认设置。在其他虚拟机参数中，你必须定义虚拟分区的大小、使用的内存、网络设置，并识别操作系统安装程序的位置（ISO 镜像、CD/DVD 或网络安装）。你应该为虚拟机命名。如果你从 DVD 安装，请在点击“下一步”之前放入磁盘。
操作系统安装程序启动。继续安装即可。安装应该正常进行，但取决于你为虚拟机分配了内存。

### 从多个光盘或镜像安装客户操作系统

如果你想在 Xen 中安装预发布的 Alpha 或 Beta 版本，可能会遇到问题。通常情况下，openSUSE 项目仅提供单独光盘的下载，而不是简单的 DVD。在某些时刻，安装程序会要求更换光盘。如果你尝试从 YaST 模块执行此操作，安装将意外终止。在更换光盘之前，必须遵循以下步骤：
- 打开终端窗口并输入 `xm list`。注意你创建的虚拟机名称和 ID。
- 输入 `xm block-list <vm_ID>`，其中 `vm_ID` 是虚拟机 ID。判断哪个设备是挂载的 ISO 镜像（或 CD），并记录其 Vdev 数字。通常列表中最后一个设备是挂载的 ISO 镜像。
- 输入 `xm block-detach <vm_ID> <Vdev_number>`。此命令允许虚拟机从驱动器中弹出光盘。
- 输入 `eject` 推出 CD。
- 将下一张 CD 放入驱动器。
- 输入 `cat /etc/xen/vm/<vm_name> | grep disk`，其中 `vm_name` 是你正在创建的虚拟机的名称。注意光驱驱动器的附加字符串，它通常列在输出字符串的末尾，并带有 `phy:` 前缀（例如 `phy: /dev/sr0, hdb, r`）。你将在下一步中需要它。
- 输入 `xm block-attach <vm_ID> <attach_string>`，其中 `vm_ID` 是虚拟机的数字，`attach_string` 是光驱驱动器的字符串（例如，`xm block-attach 1 phy:/dev/sr0 hdb r`）。在 `attach_string` 参数之间的逗号处加上空格。
- 回到虚拟机安装程序窗口并按 OK 继续。根据需要重复此过程。
你现在应该在 Xen 中拥有了一个可以运行的系统。

## 参考文献

- http://www.winehq.org—Wine 项目总部。请确保在“应用程序数据库”部分为你喜爱的使用 Wine 移植的 Windows 投票。
- http://www.von-thadden.de/Joachim/WineTools—WineTools 提供了相对简便的 Wine 安装方法以及许多知名的免费应用程序，包括 Internet Explorer。
- http://www.codewavers.com—Codewavers 公司，Crossover Linux 的制作者。
