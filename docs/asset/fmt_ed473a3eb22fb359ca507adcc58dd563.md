
在排错错误消息时，请记住“Google 是你的朋友”。简单地复制部分或全部错误消息，并将其粘贴到 `http://www.google.com/linux/` 和 `http://marc.thelinuxgroup.com` 的搜索框中。你可能会找到包含相关信息的页面的链接，从而帮助你解决问题。你可能不是第一个遇到该问题的人。阅读 `modules.conf` 的手册页并仔细阅读 `/usr/src/linux-2.4/Documentation/devices.txt`（以及其他文件）将对你排除任何问题大有帮助。

记住一次解决一个问题，并在修改系统文件之前务必对其进行备份复制。使用通用的扩展名 `.bak` 作为文件名，因为该扩展名有时会被覆盖。以下是一个良好的文件复制方法：

```
# cp filename.original
```

当从备份恢复时，不要重命名文件，只需复制它，如下所示：

```
# cp filename.original filename
```

（当这些技巧为你节省了无数小时的沮丧时间时，请感谢你购买这本书作为礼物送给你的朋友。）

| 相关 Hat 和 Linux 命令 |

| :--- |

| 在 Red Hat Linux 上执行安装后配置任务时，你将使用这些命令： |

| apm—查看或使用电源管理设置和命令 |

| cardctl—控制 PCMIA 槽位和服务 |

| cda2wav—从音频 CD 中提取音频文件 |

| cdparanoia—从音频 CD 中提取音频文件 |

| crecord—获取 SCSI 设备信息并制作 CD-ROM |

| chkconfig—控制每个 Linux 运行级别的服务 |

| dmesg—查看由 Linux 内核报告的信息 |

| insmod—将内核模块加载到内存 |

| internet-druid—Red Hat 的图形化 X，用于在配置双重 Internet 连接时检测和配置解调器 |

| kids—KDE 的 PPP 连接工具，可以检测并使用调制 |

| lsmod—查看已加载的内核模块 |

| mouseconfig—为 Linux 配置指针设备 |

| tntysys—控制 Linux 启动时启动的服务 |

| redhat-config-date—Red Hat 的图形化日期时间客户端 |

| hat-config-soundcard—Red Hat 的图形化声卡配置工具 |

| hat-config-keyboard—Red Hat 的图形化键盘映射配置工具 |

| hat-config-mouse—Red Hat 的图形化指针配置工具 |

| hat-config-xfree86—Red Hat 的图形化 X 配置客户端 |

| sensors—获取系统功率、风扇速度和 CPU 温度 |

| setserial—从命令行配置串口 |

| sndconfig—为 Red Hat Linux 配置声卡 |

## 参考

Linux 键盘与控制台 HOWTO—Andries Brouwer 关于键盘和控制台问题的巨著；包含许多排错技巧。

`http://www.avocent.com/Cybex/PublicW2nf/gwMain?OpenFrameset`—运行 Linux 的 KVM 产品详情。

`http://www.luv.asn.au/overheads/virtualconsoles.html`—在 Linux 中使用虚拟控制台。

`http://www.synaptics.com/products/touchpad.cfm`—关于 TouchPad 指针设备的信息。

`http://www.compass.com/synaptics/`—Linux TouchPad 驱动程序站点。

`http://www.alsa-project.org`—高级 Linux 音频架构（ALSA）项目主页，Linux 的另一种声学驱动集。

`http://www.opensound.com`—Linux 商业声学驱动。

`/usr/src/linux-2.4/documentation/power/pci.txt`—Patrick Moches 关于 Linux 内核和 PCI 硬件支持程序的 PCI 电源管理路径文档。

`http://www.ibiblio.org/pub/linux/docs/HOWTO/Modem-HOWTO`—关于 Linux 下解调器的最新 HOWTO 之一。

`http://www.ibiblio.org/pub/linux/docs/HOWTO/Serial-HOWTO`—David S. Lawyer 的串口 HOWTO，包含关于 Linux 和串口使用的额外信息。

`http://2.lm-sensors.org/-lm78/lm_sensors2/doc/FAQ`—关于适用于 Linux 的 lm-sensors 软件的信息。

`http://pcmcia-cs.sourceforge.net/`—Linux 最新 PCMCIA 驱动程序的源码。

`http://www.camiresearch.com/Data_Common_Basics/RS232-standard.html`—对 EIA232（以前称为 RS232）标准的描述和教程。

`http://www.qbik.com/usb/devices/`—检查 Linux USB 设备兼容性的地方。

`http://www.linmodems.org`—该站点提供了适用于 Linux 的控制器解调器的多个驱动程序链接。

`http://www.linux1394.org/`—Linux IEEE 1394 项目主页，包含新信息、更新的驱动程序以及兼容芯片组和设备列表。

`http://www.faqchest.com/`—FAQchest，一个可搜索的 FAQ、HOWTO 和邮件列表存档；是 `http://marc.theamsgroup./` 的替代方案。

`http://groups.google.com/`—通过 Google 搜索 Usenet 组；是 `http://marc.theamsgroup.com` 的另一种备用替代方案。

`http://www.fokus.gmd.de/research/cc/clone/employees/joerg.schilling/private/cdrecord.html`—`cdrecord` 命令的主页。

`http://www.tuxedo.do/esr/faqs/smart-questions.html`—聪明地提问，获取帮助的指南。这解释了为什么人们会忽略你的问题或让你去读手册（RTFM）。

`http://csgrad.cs.vt.de/~tjohnson/pinouts/`—接线定义集合，有助于解决问题。

`http://artechnica.com/guide/building/bios/bios-1.html`—关于 BIOS 选项的最佳讨论。

`http://www.yourvote.com/pci/`—PCI 厂商和设备列表；使用厂商 ID 获取未知 PCI 设备的信息。

`http://mandrakorum.com/article.php?id=2242&mode=thread&order=0&hold=0`—未列显示器的配置教程。

`http://www.linuxnetmag.com/en/issue/m5devs.1`—关于如何利用 `devices.txt` 中信息的文章。

# 第 5 章

### 本章内容

- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统
- 使用 Red Hat Linux 文件系统

Red Hat Linux 为新用户提供了一个极好的界面（参见第 6 章“窗口系统”），但由于 Linux 的设计方式，你必须习惯使用命令行，尤其是在独立电脑上使用 Linux 时。

在本章中，你将学习命令行的基础知识。本章涵盖的一些基本操作包括：

- 执行常规任务——登录和注销、更改密码、列出目录
- 基础管理——创建或删除文件
- 用户管理——创建或删除用户
- 系统管理——关机或重启、阅读手册页

为了充分利用这种通用布局的优势，你必须了解 Red Hat Linux 是如何组织的、你系统中文件和目录的内容，以及文件和软件应该安装在哪里。理解 Linux 文件系统是学习如何管理和使用 Linux 的基础。

## 查看 Red Hat Linux 文件系统

使用列出目录内容的命令查看 Red Hat Linux 系统的布局，如下：

```
$ ls /
bin dev home lib misc opt root tftpboot usr
boot etc initrd lost+found mnt proc sbin tmp var
```

> 注意
>
> 本节提供了 Red Hat 文件系统的概述。在你自己的系统中，你发现的目录可能比这里讨论的的多或更少。当安装某些软件包时，它们会创建新的目录。更新软件包可能会删除或更改某些目录的名称。有关在你的 Red Hat 系统中安装、升级或删除软件的更多信息，请参阅第 8 章“管理软件和系统资源”。

要获取更详细的视图，可以使用 `tree` 命令显示根目录或基础目录布局以及相关的子目录，如下所示（注意，取决于你安装的 Red Hat 版本或你是否用新内核更新了 Red Hat，你系统的 `/usr/src` 目录可能略有不同，且并非所有子目录都已列出）：

```
$ tree -dx /
/
|-- bin
|-- boot
|-- dev
|-- etc
|   -- X11
|   |-- cron.d
|   |-- ppp
|   |-- rc.d
|   |-- ssh
|   |-- sysconfig
|-- home
|   -- lib
|   |-- modules
|   |-- lost+found
|   -- misc
|-- mnt
|   |-- cdrom
|   |-- floppy
|-- opt
|-- proc
|-- root
|   -- tftpboot
|-- tmp
|-- usr
|   |-- X11R6
|   |-- bin
|   |-- include
|   |-- lib
|   |-- doc
|   |-- include
|   |-- lib
|   |-- local
|   |-- sbin
|   |-- share
|   |-- src
|   |-- linux-2.4 -> linux-2.4.18
|   |-- redhat
|   | var
|   -- log
|   -- spool
```

此示例（从 10,000 多个目录中提取而成）显示了高级目录，并对应表 5.1 中的目录和描述。

## 表 5.1 基本 Linux 目录

| 名称 | 描述 |
|---|---|
| / | 根目录 |
| /bin | 基本命令 |
| /boot | 引导加载器文件、Linux 内核 |
| /dev | 设备文件 |
| /etc | 系统配置文件 |

## 表 5.1 继续

| 名称 | 描述 |
|---|---|
| /home | 用户目录 |
| /lib | 共享库、内核模块 |
| /mnt | 本地文件系统的常用挂载点 |
| /opt | 附加软件包 |
| /proc | 内核信息、进程控制 |
| /root | 超用户 (root) |
| /sbin | 系统命令（主要供 root 使用） |
| /tftpboot | 网络引导支持 |
| /tmp | 临时文件 |
| /usr | 次级软件层次 |
| /var | 可变数据（如日志）；溢出文件 |

表 5.1 中的一些重要的 Red Hat 目录（包含用户系统配置文件）将在后续章节中讨论。当你使用 Red Hat 时，你会使用并编辑这些目录。

## 使用 `/bin` 和 `/sbin` 目录中的基本命令

`/bin` 目录（约 5MB）包含了系统运行和启动 Linux 时使用的基本命令。通常，只有 root 用户使用 `/sbin` 目录中的命令。这些命令中的许多（并非全部）是静态链接的；此类命令不依赖于 `/lib` 下的软件。系统中几乎所有其他应用程序都是动态链接的——这意味着它们需要外部库（也称为共享库）。由于系统包含动态链接应用程序，在安装或升级软件包时可能会遇到“依赖错误”；在这些情况下，可能不存在支持库（或应用程序）。有关处理动态链接应用程序的更多信息，请参阅第 8 章“管理软件和系统资源”。

## 存储启动的内核并查看 `/boot` 和 `/dev` 中的存储设备

`/boot` 目录包含启动时加载的 Linux 内核，以及描述或提供启动 Linux 信息的其他文件。当重新构建或安装新内核时，内核和相关文件会被放在此目录中（参阅第 24 章“内核模块管理”）。

Linux 设备文件位于 `/dev` 目录下。该目录包含 700 多个文件，代表系统中可能使用或不使用的设备。该目录中最常用的设备包括：

- IDE（集成驱动器）硬盘，例如 `/dev/hda` 和 `/dev/hdb`
- CD-ROM 驱动器，其中 IDE、CDRW（CD 读写）驱动器仿真为 SCSI（小型计算机接口）设备，例如 `/dev/sd0`
- 串口，例如 COM1 的 `/dev/ttyS0`、COM2 的 `/ttyS1` 等
- 指针设备，包括 `/dev/aux` 等
- 打印机，例如 `/dev/lp0`

网络接口（如 `eth0` 或 `ppp0`）不由设备文件表示，而是在内存中创建的。更多信息请参见第 13 章“网络连接”。

## 使用和编辑 `/etc` 目录中的文件

如果你安装了书中包含的所有软件，`/etc` 目录下会有超过 20MB 的配置文件和目录。一些主要的软件包（如 Apache、OpenSSH 和 inet）在 `/etc` 下有配置目录。`/etc` 中的其他系统相关配置文件有：

- `fstab` - 系统文件是一个表文件，列出了连接到你 PC 的每个硬盘、CD-ROM、软盘或其他存储设备。该表将每个设备的分区与其在 Linux 文件系统（目录布局）中的位置进行索引，并列出了在 Linux 下使用每个设备的其他选项（参阅第 10 章“管理文件系统”）。
- `init` - 系统初始化文件定义了默认运行级别。对此文件的更改可以决定系统是启动到图形还是文本登录，以及是否启用拨号远程访问。（在第 7 章“管理服务”中的“Red Hat Levels”部分学习运行级别）。查看第 6 章中的“启动 X”部分了解更多关于更改 `init` 以启动到图形界面的信息。第 15 章“互联网连接”中的“设置 PPP 服务器”部分讨论了编辑 `init` 以启用拨号访问。
- `modules.conf` - 此配置文件包含加载内核模块到各种硬件时使用的指令和选项，如声音、网络等（在第 24 章“构建和安装模块”部分）。
- `passwd` — 系统用户列表以及用户帐户信息。
- `printcap` - 系统能力数据库（在第 12 章“打印服务”部分讨论）。
- `shells` — 许可的 shell 列表（命令行接口）。

Red Hat Linux 最重要的 `/etc` 目录之一是 `sysconfig`。该目录包含网络激活脚本以及硬件和软件相关信息：

```
$ tree -afx /etc/sysconfig
/etc/sysconfig
|-- /etc/sysconfig/amd
|-- /etc/sysconfig/apm-scripts
|  -- /etc/sysconfig/apm-scripts/apmscript
|  -- /etc/sysconfig/apmd
|...
|-- /etc/sysconfig/clock
|-- /etc/sysconfig/console
|-- /etc/sysconfig/dhcpd
|-- /etc/sysconfig/dhcrelay
|-- /etc/sysconfig/gpm
|-- /etc/sysconfig/grub
|-- /etc/sysconfig/harddisks
|-- /etc/sysconfig/hwconf
...
|-- /etc/sysconfig/init
|-- /etc/sysconfig/irda
|-- /etc/sysconfig/keyboard
|-- /etc/sysconfig/kudzu
|-- /etc/sysconfig/mouse
|-- /etc/sysconfig/named
|-- /etc/sysconfig/netdump
...
|-- /etc/sysconfig/network
|-- /etc/sysconfig/network-scripts
|-- /etc/sysconfig/network-scripts/ifcfg-eth0
|-- /etc/sysconfig/network-scripts/ifup-wireless
|-- /etc/sysconfig/network-scripts/init.ipv6-global
|-- /etc/sysconfig/network-scripts/network-functions
|  -- /etc/sysconfig/network-scripts/network-functions-ipv6
|-- /etc/sysconfig/networking
```

# 第 5 章 Linux 的起步
