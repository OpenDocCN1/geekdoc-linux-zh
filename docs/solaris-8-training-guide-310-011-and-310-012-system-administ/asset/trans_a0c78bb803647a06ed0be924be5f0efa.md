
ROM. Autofs 设施，也称为 automounter，通过提供一种方法使远程目录仅在使用时才挂载，从而简化了 NFS 挂载。

40. A.、B. Sun 建议将作为读写挂载或包含可执行文件的文件系统始终使用 hard 选项挂载。如果你使用 soft 挂载的文件系统，可能会发生意外的 I/O 错误。例如，考虑一个写请求。如果 NFS 服务器宕机，待处理的写请求会直接放弃，导致远程文件系统上的文件损坏。读写文件系统应始终使用指定的 hard 和 intr 选项挂载。这让用户可以自行决定是否终止挂起的进程。

41. D. 答案 A 描述了 nfsd，B 描述了 mountd，C 描述了 lockd。

42. B.、C. sudo 和基于角色的访问控制（RBAC）都允许系统管理员将有限的管理员能力分配给非 root 用户。泄露 root 密码会让用户完全访问 root 的所有受限权限，导致安全性非常差。

43. A.、B.、C. 名称服务也提供密码信息。Solaris 8 中可用的名称服务包括 NIS、NIS+、DNS、LDAP 和 /etc 文件。

44. A. 不带参数时，ypwhich 命令会显示当前的 NIS 主服务器。

45. D. 名称服务开关 /etc/nsswitch.conf 控制客户端工作站或应用程序如何获取网络信息。在这种情况下，你需要编辑 /etc/nsswitch.conf 文件，并将 hosts 行改为 hosts: files dns nis。

46. C. Solaris Management Console 不存在命令行界面。

47. A.、C.、D. SMC Toolbox Editor 管理进程、用户、文件系统挂载和共享、磁盘、串行端口、安排作业，并具有日志查看器。

48. A.、B. Solaris AdminSuite 提供了与 SMC 相同的许多工具，但不提供使用 RBAC 委派管理任务的能力。它也不提供作业调度或磁盘和进程管理的工具。AdminSuite 提供的工具尽管如此，仍提供了一个易于使用的图形界面，可从网络上的任何位置管理你的系统。GUI 中的工具和命令比使用大量 Solaris 命令执行相同任务要快得多。

49. B. 自定义 JumpStart 安装操作系统的安装方法提供了一种自动且相同地安装一组相似系统的方式。如果你使用交互式方法安装操作系统，你必须通过回答各种问题与安装程序进行对话。

50. D. 创建配置文件后，你可以使用 pfinstall 命令对其进行测试。测试类文件有时称为“试运行”安装。通过查看 pfinstall 生成的安装输出，你可以快速确定类文件是否会按预期工作。

## SECTION
## IV
## APPENDIXES
- A Web Start
- B Administration and Configuration of the CDE
- C The History of Solaris
- D Overview of Certification Process
- E What’s on the CD-ROM
- F Using the ExamGear, Training Guide Edition Software

## Web Start
Web Start 3.0 是 Sun 的基于 Java 的安装程序，可简化并加速 Solaris 软件的安装。Web Start 使用 InstallShield 的技术，InstallShield 被广泛认为是 Microsoft Windows 应用程序事实上的安装技术的提供商。此工具允许网络管理员使用熟悉的网络浏览器，该浏览器使用点按界面安装捆绑在 Solaris 中的所有软件。通过 Solaris Web Start，你可以选择并安装机器所需的全部软件，包括 Solaris 软件组和 Solstice 实用程序。此外，Web Start 是唯一同时安装在额外 CD 上提供的其他软件的安装实用程序。它与第 15 章“安装服务器”中描述的 Solaris 交互式安装程序非常相似，但具有更用户友好的界面。Solaris Web Start 使用 JumpStart 实用程序自动读取配置文件，从而以最少的干预安装 Solaris 软件和其他选定产品。以下是有关 Web Start 的一些要点：

- 使用 Solaris Web Start 软件和 Solaris Web Start Wizards 技术，Solaris 操作环境和其他应用程序可以借助基于浏览器的界面进行交互式安装。
- Web Start Flash 技术使管理员能够对 Solaris 操作环境和系统配置进行完整的系统映像，并在网络上将该映像复制到多台服务器上。此功能从 Solaris 8 的 04/01 版本开始提供。
- Web Start 利用 Solaris JumpStart 技术，可提供 Solaris 系统的自动化安装和设置。
- Solaris Live Upgrade 技术减少了通常与操作系统升级相关的服务中断。

如果你正在设置一台包含帧缓冲、键盘和监视器的机器，你可以直接从该机器运行 Web Start。如果你只有通过串行端口连接的字符型终端，你仍然可以使用 Web Start 的命令行界面（CLI）。

## MINIMUM SYSTEM REQUIREMENTS FOR SOLARIS WEB START
如果你想运行 Solaris Web Start，你的计算机必须具有以下条件：

- 至少 64MB 的 RAM。
- 仅运行 Solaris Web Start 需要 1.05GB 的启动磁盘，之后程序会确定你的系统是否有足够的磁盘空间来安装你选择的软件产品。安装服务器软件建议 2GB 磁盘空间。

## Installing Solaris Using Web Start
Solaris Web Start 让你能够利用 GUI 安装的便捷性和便利性。然而，你可以用两种方式之一使用 Web Start：

- ♦ Graphical-User Interface (GUI). Requires a local or remote CD-ROM drive or network connection, frame buffer, keyboard, and bitmapped monitor.
- ♦ Command-Line Interface (CLI). Requires a local or remote CD-ROM drive or network connection, keyboard, and monitor.

要开始 Web Start 安装，请按如下方式从 Solaris 8 安装 CD 启动系统：

```
ok boot cdrom - browser
```

如果在启动过程中，Web Start 检测到系统的帧缓冲，它会使用 GUI；如果 Web Start 未检测到帧缓冲，它会使用 CLI。两者中的内容和说明顺序相同。

系统从 CD-ROM 启动后，Web Start 启动适当的用户界面，并要求提供一些一般的系统识别信息。你被要求提供的信息与第 15 章中交互式安装所要求的信息相同，只是系统使用不同的 GUI，外观和感觉略有不同。出现的第一个窗口是 Network Connectivity 窗口，如图 A.1 所示。

选择你的系统是否将连接到网络，然后单击 Next 按钮。DHCP 窗口出现，如图 A.2 所示。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_905_0.png)

FIGURE A.1
Network Connectivity window.

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_905_1.png)

FIGURE A.2
DHCP window.

此窗口询问你是否将使用 DHCP 配置网络接口，或接口将手动配置。在选择是否使用 DHCP 配置系统网络接口后，单击 Next 按钮。在示例中，我表示将不使用 DHCP 配置网络接口卡，因此我现在将被提示提供用于配置主网络接口的信息。如果我表示将使用 DHCP，我将不会被提示此信息，并且 DHCP 服务器将在启动时自动提供网络接口信息。当我单击 Next 按钮时，Host Name 窗口出现，如图 A.3 所示。

输入此系统的主机名。主机名可以有 2-255 个字符。输入主机名后，单击 Next 继续。IP Address 窗口出现，如图 A.4 所示。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_906_0.png)

## FIGURE A.3
Host Name window.

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_906_1.png)

## FIGURE A.4
IP Address window.

输入此系统的 IP 地址，单击 Next，Netmask 窗口出现，如图 A.5 所示。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_906_2.png)

## FIGURE A.5
Netmask window.

指定子网的 netmask 值，单击 Next 按钮继续，Ipv6 窗口出现，如图 A.6 所示。

