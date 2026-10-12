
当这些被激活时，nm-applet 将出现在顶部面板的通知区域（见图 4.10）。这是负责处理和监控网络连接的 applet。

![](img/2045828cf45e5632bf056f9ca99d6755_152_0.png)

### 图 4.10 网络管理器通知 applet，此处显示已连接到无线网络。

此时重启一次是值得的，以便 Fedora 能检测到固件的存在。当您重新登录后，点击工具栏中的 nm-applet 图标以连接到无线网络。如果您的无线接入点广播其 SSID，它应该出现在无线网络的列表下（类似于图 4.10）。只需点击所需的网络，NetworkManager 会感知正在使用的加密方式（如果有）并向您索要密钥。输入后，Network Manager 将启动无线连接。该密钥随后将存储在默认钥匙串中，如果您尚未使用过钥匙串，系统会询问您创建一个密码。从现在开始，每当您登录 Fedora 时，系统都会要求您输入解锁钥匙串的密钥。

如果由于某种原因您的无线网络没有显示（您可能隐藏了 SSID），您将需要使用“连接到其他无线网络”选项，这会弹出图 4.11 所示的屏幕。

![](img/2045828cf45e5632bf056f9ca99d6755_152_1.png)

### 图 4.11 使用 NetworkManager 配置您的无线网络连接设置。

NetworkManager 可以处理 WEP 和 WPA 加密。建议使用 WPA 加密，因为它是两者中更安全的。

NetworkManager 还可以使用 `vpnc` 软件连接到 Cisco VPN 连接。使用 `yum` 安装它后，您可以根据需要指定连接设置，或者如果您可以访问预定义的配置文件 `l.pcf`，可以直接将其导入到 NetworkManager 中。

## 相关的 Fedora 和 Linux 命令

在执行安装后配置任务时，您将会使用这些命令：

- `apm` — 查看或使用电源管理设置和命令
- `cardctl` — 控制 PCMCIA 插槽和服务
- `cdcd2wav` — 从音频 CD 中提取音频文件
- `cdparanoia` — 从音频 CD 中提取音频文件
- `cdrecord` — 获取 SCSI 设备信息并刻录 CD-ROM
- `chkconfig` — 控制每个 Linux 运行级别下的服务
- `dmesg` — 查看由 Linux 内核报告的信息
- `insmod` — 将内核模块加载到内存中
- `system-config-network` — Fedora 的图形化 X 客户端，用于在配置拨号互联网连接时检测和配置调制解调器
- `kppp` — KDE 的 X PPP 连接实用程序，可以检测并使用调制解调器
- `lsmod` — 查看已加载的内核模块
- `mouseconfig` — 为 Linux 配置指向设备
- `ntsysv` — 控制启动 Linux 时启动的服务
- `system-config-date` — Fedora 的图形化日期和时间客户端
- `system-config-display` — Fedora 的图形化 X 配置客户端
- `system-config-soundcard` — Fedora 的图形化声卡配置工具
- `system-config-keyboard` — Fedora 的图形化键盘映射配置工具
- `system-config-mouse` — Fedora 的图形化指针配置工具
- `sensors` — 获取系统的电源、风扇速度和 CPU 温度
- `setserial` — 从命令行配置串行端口
- `sndconfig` — 从控制台为 Fedora 配置声卡

## 参考资料

- *Linux 键盘和控制台 HOWTO* — Andries Brouwer 关于键盘和控制台问题的专著；包含许多故障排除技巧。
- [http://www.avocent.com/Cyber/Public/5.nsf/gw/Main?OpenFrameSet](http://www.avocent.com/Cyber/Public/5.nsf/gw/Main?OpenFrameSet) — 运行 Linux 的 KVM 切换器的产品详情。
- [http://www.luv.asn.au/overheads/virtualconsoles.html](http://www.luv.asn.au/overheads/virtualconsoles.html) — 在 Linux 上使用虚拟控制台。
- [http://www.synaptics.com/products/touchpad.cfm](http://www.synaptics.com/products/touchpad.cfm) — 关于 TouchPad 指向设备的信息。
- [http://www.compass.com/synaptics/](http://www.compass.com/synaptics/) — 一个 Linux TouchPad 驱动程序的站点。
- [http://www.x.org/](http://www.x.org/) — X.Org 基金会，X11R7 的主页。
- [http://www.alsa-project.org](http://www.alsa-project.org) — 高级 Linux 声音架构（Advanced Linux Sound Architecture）项目的主页，它是 Linux 的一套替代声音驱动程序。
- [http://www.opensound.com](http://www.opensound.com) — Linux 的商业声音驱动程序。
- /usr/src/linux-2.6/Documentation/power/pci.txt — Patrick Mochel 关于 Linux 内核和 PCI 硬件支持编程人员的 PCI 电源管理路由的文档。
- [http://www.tldp.org/pub/Linux/docs/HOWTO/Modem-HOWTO](http://www.tldp.org/pub/Linux/docs/HOWTO/Modem-HOWTO) — 关于在 Linux 上使用调制解调器的最新 HOWTO 之一。
- [http://www.tldp.org/pub/Linux/docs/HOWTO/Serial-HOWTO](http://www.tldp.org/pub/Linux/docs/HOWTO/Serial-HOWTO) — David S. Lawver 的串行 HOWTO，包含关于 Linux 和串行端口使用的额外信息。
- [http://www2.lm-sensors.nu/](http://www2.lm-sensors.nu/) — lm78/cvs/lm_sensors2/doc/FAQ — 关于 Linux 的 lm-sensors 软件的信息。
- [http://pcmcia-cs.sourceforge.net/](http://pcmcia-cs.sourceforge.net/) — 获取 Linux 最新 PCMCIA 驱动程序的来源。
- [http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html](http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html) — 对 EIA232（原 RS232）标准的描述和教程。
- [http://www.qbik.ch/usb/devices/](http://www.qbik.ch/usb/devices/) — 检查 Linux 的 USB 设备兼容性的地方。
- [http://www.linmodems.org](http://www.linmodems.org) — 此站点提供用于在 Linux 下无控制器使用调制解调器的多个驱动程序的链接。
- [http://www.linux1394.org/](http://www.linux1394.org/) — Linux IEEE 1394 项目的主页，提供新信息、更新驱动程序的链接以及兼容芯片组和设备的列表。
- [http://www.faqchest.com/](http://www.faqchest.com/) — The FAQhest，一个可搜索的 FAQ、HOWTO 和邮件列表归档；是 http://marc.theaimsgroup.com/ 的替代方案。
- [http://groups.google.com/](http://groups.google.com/) — 通过 Google 搜索 Usenet 组；http://marc.theaimsgroup.com/ 的另一个替代方案。
- [http://www.linuxquestions.org/](http://www.linuxquestions.org/) — Linux Questions 站点；一组有用的社区论坛，可以帮助您找到更棘手问题的答案。
- [http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html](http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html) — cdrecord 命令及相关实用工具的主页。
- [http://arstechnica.com/guide/building/bios/bios-l.html](http://arstechnica.com/guide/building/bios/bios-l.html) — 在 ArsTechnica 上对 BIOS 选项的精彩讨论。
- [http://www.linuxnetmag.com/en/issue5/m5devs1.html](http://www.linuxnetmag.com/en/issue5/m5devs1.html) — 关于如何利用在 devices.txt 中找到的信息的简短文章。

## 第 5 章

# 使用 Fedora 的第一步

Fedora 为桌面提供了丰富的图形界面（参见第 6 章，“X 窗口系统”），并配有图形管理工具，可帮助您维护系统。然而，有时事情可能会出错，您可能无法拥有漂亮的界面来修复问题。在这种情况下，了解一点 shell 知识会很有用，尤其是当您需要编辑和修改重要文件以使系统恢复在线时。在本章中，您将学习如何通过命令行使用 Linux，包括一些有时能挽救生命并帮助您在登录提示符处卡住时脱身的工具。我们还将介绍一些基本的用户管理，以及移动和复制文件、获取目录列表、管理文件权限以及正确重启或关闭（停机）Linux 系统等功能。

本章涵盖的一些基本命令行技能包括：

- 执行常规任务 — 登录和注销、使用文本控制台、更改密码以及列出和导航目录
- 基本文件管理 — 创建、重命名和删除文件和目录
- 基本用户管理 — 从命令行创建和删除用户
- 基本系统管理 — 关闭和重启、阅读 man 页面和其他文档，以及使用基于文本的工具编辑系统配置文件

## 本章内容

- 操作 Linux 文件系统
- 登录 Linux 及其操作
- 更改您的用户信息
- 阅读文档
- 使用 Shell
- 使用文本编辑器
- 操作权限
- 以 Root 身份工作
- 参考资料

如果您正在从其他平台迁移到 Linux，请阅读本章；这里的信息对于初次学习使用命令行的 Linux 新用户或系统管理员非常有价值。

> **提示**
> 对于过去使用过 MS-DOS 的人来说，深入研究命令行并不像那些面对空白屏幕时会自动按下分配给附近极客的快速拨号按钮的人那么可怕。无论您是哪种用户，掌握命令行知识都大有裨益。由于 Linux 是一种 UNIX 风格的操作系统，如果您在 Linux 上学习命令行功能，使用其他类 UNIX 操作系统（如 BSD 甚至 Mac OS X）就会更容易。

> **注意**
> 总的来说，访问 Linux 系统的用户分为两类：日常普通用户和 root 用户或超级用户。在大型组织中，少数人可能被授予 root 或超级用户帐户的访问权限，以完成必要的系统管理任务。普通用户通常不需要 root 访问权限。
>
> 但是，如果您在机器上以独立 PC 的形式安装了 Linux，您自动拥有 root 帐户的访问权限。这是为了让您可以完成需要与系统交互的必要配置和其他任务。
>
> Linux 的这一特定方面经常受到负面报道，因为新用户可能将其视为完成工作的重大障碍。事实并非如此。如前所述，root 帐户对于成功的 Linux 系统是根本性的。大量工作已投入到创建易于使用的管理工具中，这些工具消除了维护系统的许多困难。掌握一点命令行知识仍然对您大有裨益，尤其是在紧急情况下。

### 操作 Linux 文件系统

Fedora 使用*文件系统*，或与使用其他 UNIX 变体（如 Mac OS 8）类似的分层目录布局。几乎所有 Linux 发行版都使用类似的目录结构，并且 Linux 发行版供应商通常就关键 Linux 文件和目录的命名和位置达成了一致。

> **注意**
> 建立关于 Linux 目录结构共识的努力始于 1993 年的文件系统层次结构标准（FHS），这是一份不仅解决 Linux 问题，还解决其他操作系统（如 BSD）问题草案提案。Red Hat 已声明致力于遵守 FHS，该标准规定了文件和目录的位置和名称。Fedora 使用当前的 2.3 标准。对此标准的主要增加包括为可移动存储设备（如 DVD 驱动器和小磁盘）创建 /media 目录（尽管保留 /mnt 作为临时挂载点）。udev 也已添加到 Fedora 中；虽然它不是...

