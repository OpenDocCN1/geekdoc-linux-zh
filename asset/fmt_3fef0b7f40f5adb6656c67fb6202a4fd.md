
| Networking doesn't appear to function at all | Use the `ifconfig` command to see whether networking is up and running; if not, try the `network` script in `/etc/rc.d/init.d`. (Remember to check things that seem too obvious: Is the cable plugged into the Ethernet card? Is an Ethernet card installed? Is the cable plugged into the wall or a hub?) |

| The network script doesn't appear to work | Use the `lsmod` command to see whether any network modules are installed in the kernel; if not, use `modprobe -t` or a graphical utility to install the right kernel module for your networking card |

| Can't ping any other systems on the local network segment | Check the cables; check with `ifconfig` to see whether a valid IP address has been assigned; check the routing tables to see that a route is listed for the local network |

| Can't ping any system on another segment within the organization | Check the cables at the hub or server room; check with `ifconfig` to see if a valid IP address is assigned and how that address compares or conflicts with those on the other network segment; does the routing table include a route for the other network that refers to an intermediate router, if necessary? |

### 表 15-2 基本网络故障排除回顾（续）

| Trouble | Things to check |
|---|---|

| Traffic to another segment seems very slow | Check the routing table to see whether the most direct route is defined, and check whether another system has the same IP address assigned. Review the output of the `ifconfig` command to see whether a large number of collisions are occurring—if so the network may be overloaded. Check `ifconfig` output to see whether a large number of errors are occurring—if so the NIC may be defective. Review whether fragmentation problems between the two segments could be slowing down traffic; use `traceroute` to see at what point along the way the transmission slows down significantly. |

## 创建救援磁盘

相当常见的系统故障是硬盘问题或其他启动系统的问题。有时这表现为完全崩溃，在这种情况下，你可能必须从备份归档将所有数据恢复到新的硬盘。在其他情况下，磁盘的一部分已损坏，系统无法启动。有时硬盘问题甚至可能是系统管理员对系统所做的操作造成的。在许多硬盘故障的情况下，你无法从硬盘正常启动 Linux 系统；你必须从可移动磁盘或可启动 CD-ROM 启动，然后才能访问硬盘并解决问题。

救援磁盘是一个 3.5 英寸磁盘，你可以用它启动基于 Linux 的计算机。它可能只有启动管理器和足够的信息来定位硬盘上的 Linux 分区。通常，它包含一个最小版本的 Linux 和足够的系统实用程序来诊断和修复硬盘文件中的问题。启动系统后，你可以挂载安装有 Linux 的硬盘以纠正问题。一个流行的预配置救援磁盘是 Tom's Boot disk，你可以从 www.toms.net/rb 下载。

一些系统管理员始终从 3.5 英寸磁盘启动其服务器。这比从硬盘启动花费更多时间，但由于服务器很少重新启动，启动速度并不是真正的问题。通过这样做，系统管理员可以控制系统如何启动，并在出现问题时轻松维护可移动磁盘的备份。当启动磁盘或硬盘故障时，会使用单独的救援磁盘。

理想情况下，你在安装 Linux 时为系统创建启动磁盘，如第 8 章所述。这保证了启动磁盘和计算机硬盘上的启动管理器信息兼容。你也可以在系统运行时使用 `mkbootdisk` 命令创建启动磁盘。

当你使用 Red Hat Linux 或 Fedora 并遇到系统启动问题，或硬盘崩溃或其他严重的硬盘问题时，你可以使用 Fedora CD 1 启动系统进入救援模式。启动该 CD 后，输入 `linux rescue` at the first prompt. 系统从 CD 启动，然后提示你选择语言、键盘，以及是否启动网络设备（你可能需要根据需要访问以修复系统）。之后，系统会告知它将搜索 Fedora 安装。你可以选择 `Continue` 以将安装挂载到 `/mnt/sysimage` 下，选择 `Read-Only` 使该文件系统只读，或选择 `Skip` 以不挂载任何文件系统。在任何情况下，你随后都会看到一个文本模式 shell 提示符。在此 shell 提示符下，你可以使用适当的任何实用程序来诊断和修复问题。如果你进入救援模式时在上一个提示中选择了 `Skip`，则需要在访问 Fedora 安装上的任何数据之前手动挂载正确的磁盘分区。在救援 shell 中输入 `exit` 会导致系统重新启动。

## CHAPTER SUMMARY

- X Window System 配置由 Linux 安装程序处理，但可使用 `xvidtune` 和 `system-config-display` 等图形工具进行调整。
- X Window System 使用许多脚本来确定在启动图形环境时应启动哪些程序。当使用 GNOME 或 KDE 等桌面时，这些脚本的相关性较低。
- X 的资源、字体和鼠标交互等功能都可使用简单的命令行实用程序进行配置。某些功能与 GNOME 等桌面界面控制的功能重叠，这些功能也可以使用桌面中的图形首选项工具进行配置。
- 图形登录屏幕由名为 `xdm` 的程序处理，或在 GNOME 和 KDE 中使用 `gdm` 和 `kdm`。此屏幕可使用 `XDMCP` 协议远程访问。
- Linux 中的图形程序可以显示到安装了 X 服务器的任何系统。这一功能的安全性由 `xhost` 或 `xauth` 安全提供，后者配置更困难但安全性更高。远程应用程序通常通过 `SSH` 连接运行以防止安全漏洞。
- 计算机安全通常分为物理安全、用户安全、文件安全和网络安全等类别。
- 安全攻击的示例包括密码破解、特洛伊木马、缓冲区溢出攻击、DoS 和 DDoS 攻击、病毒和蠕虫。
- 攻击者和系统管理员都使用各种安全软件工具。这些包括用于端口扫描的工具（如 `nmap`）、用于数据包嗅探的工具（如 `tcpdump` 和 `Ethereal`）、IDS 程序以及安全审计工具如 `SAINT`。
- 有几个组织支持计算专业人员维护安全系统。其中最重要的两个是 `CERT/CC` 和 `SANS`。
- Linux 使用名为 `NetFilter` 的防火墙和数据包过滤系统，它使用 `IP tables` 定义用于处理网络数据包的规则。Linux 的这一功能支持 IP 伪装、透明代理和其他高级路由和数据包控制功能。
- Linux 上的 DNS 服务器使用 `named` 守护进程实现，区域信息文件存储在主或从 DNS 服务器上，以响应客户端请求提供数据。缓存名称服务器不充当任何域的主服务器或从服务器，而只存储信息以便更快地本地访问。
- NFS 允许远程用户将 NFS 服务器上的文件系统作为其目录结构的一部分挂载。可用的目录在服务器的 `/etc/exports` 文件中定义。
