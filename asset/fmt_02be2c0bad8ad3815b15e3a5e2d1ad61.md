
表 5.1 中的某些重要目录（如包含用户和 root 命令或系统配置文件的目录）将在后续章节中讨论。在使用 Fedora 时，你会使用并编辑这些目录下的文件。

## 使用 `/bin` 和 `/sbin` 目录下的基本命令

`/bin` 目录（如果完整安装，约占 5MB）包含了系统在运行和启动 Linux 时使用的基本命令。通常，只有 root 操作员才会使用 `/sbin` 目录中的命令。许多（尽管不是所有）这些命令都是静态链接的；此类命令不依赖于位于 `/lib` 或 `/usr/lib` 目录下的软件库。你系统上的几乎所有其他应用程序都是动态链接的——这意味着它们运行所需的需要外部软件库（也称为共享库）。

由于系统包含动态链接的应用程序，在安装或升级软件包时，你可能会遇到依赖错误，在这些情况下，可能缺少支持库（或应用程序）。请参见第 7 章，获取有关处理动态链接应用程序以及避免此类问题的更多信息。幸运的是，对于像 `yum` 这样的程序，“依赖地狱”大部分成为过去。

## 在 `/boot` 和 `/dev` 目录中存储启动内核和查看存储设备

`/boot` 目录包含一个压缩版本的 Linux 内核（启动时加载），以及描述内核或提供 Linux 启动信息的其他文件。当你重建或安装新内核时，内核和相关文件将放置在此目录中（有关重建或安装内核的更多信息请参见第 39 章“内核和模块管理”）。

设备文件包含在 `/dev` 目录下。请注意，在 Linux 下，你系统上的一切都是文件。这意味着（网络接口除外；请看下文列表后的注释）普通文件；目录；硬盘分区；串口、打印机或 USB 端口；以及视频和音频设备全都是！

`/dev` 目录包含超过 7,500 个文件，代表系统中可能正在或不正在使用的设备。该目录中最常用的包括：

- IDE（集成式磁盘控制器）硬盘，例如 `/dev/hda` 和 `/dev/hdb`
- CD-ROM 驱动器；一些是 IDE，另一些是由 SCSI（小型计算机系统接口）设备模拟的 CD-RW（CD 读写）驱动器，例如 `/dev/scsd0`
- 串口，例如用于 COM1 的 `/dev/tty0`，用于 COM2 的 `/dev/tty1` 等
- 指示设备，包括 `/dev/input/mice` 等其他
- 打印机，例如 `/dev/lpp0`

> 注意
>
> 网络接口（如 `eth0` 或 `pp0`）并不不由 Linux 设备文件表示，而是在激活时在内存中创建的。请参见第 18 章“网络连接”获取更多信息。

## 使用和编辑 `/etc` 目录中的文件

如果你安装了本书中包含的所有软件，`/etc` 目录下将存在超过 65MB 的系统配置文件和目录。一些主要的软件包（如 Apache、OpenSSH、xinetd）在 `/etc` 下拥有配置目录。

`/etc` 中其他重要的系统相关配置文件包括：

- `fstab`——文件系统是一个文本文件，列出了连接到你的 PC 的每个硬盘、CD-ROM、软盘或其他存储设备。该表索引了每个设备分区在你的 Linux 文件系统（目录布局）中的位置，并列出了在 Linux 下使用时每个设备的其他选项（参见第 39 章“管理文件系统”）。`fstab` 中的几乎所有条目都可以由 root 使用 `mount` 命令进行操作。
- `inittab`——系统初始化表定义了默认的运行级别，也称为运行控制级别或系统状态。对此文件的更改可以决定你的系统是启动到图形登录还是文本登录，以及是否启用了拨号远程访问。（在第 15 章“自动化任务”中的“系统服务和运行级别”部分将学习默认级别的知识。参见第 6 章中的“启动 X”部分以了解更多关于更改 `inittab` 以进入图形界面的信息。）
- `modprobe.conf`——此文件包含加载内核模块的选项。
- `passwd`——系统用户账户列表。
- `modules.d/`——此目录包含各种内核模块的配置文件。
- `network/`——此目录包含网络服务的配置文件。
- `services/`——此目录包含用于启动和停止服务的脚本。

`/etc` 中最重要的目录之一是：

- `network-scripts/`——此目录包含网络接口的配置文件。该目录中的每个文件都根据其配置的接口命名（例如 `ifcfg-eth0`）。

```
-- /etc/sysconfig/network-scripts/ifup-eth
-- /etc/sysconfig/network-scripts/ifup-ippp
-- /etc/sysconfig/network-scripts/ifup-ipsec
-- /etc/sysconfig/network-scripts/ifup-ipv6
-- /etc/sysconfig/network-scripts/ifup-ipx
-- /etc/sysconfig/network-scripts/ifup-isdn -> ifup-ipppp
-- /etc/sysconfig/network-scripts/ifup-plip
-- /etc/sysconfig/network-scripts/ifup-plusb
-- /etc/sysconfig/network-scripts/ifup-post
-- /etc/sysconfig/network-scripts/ifup-ppp
-- /etc/sysconfig/network-scripts/ifup-routes
-- /etc/sysconfig/network-scripts/ifup-sit
-- /etc/sysconfig/network-scripts/ifup-sl
-- /etc/sysconfig/network-scripts/ifup-wireless
-- /etc/sysconfig/network-scripts/init.ipv6-global
-- /etc/sysconfig/network-scripts/network-functions
-- /etc/sysconfig/network-scripts/network-functions-ipv6
-- /etc/sysconfig/networking
-- /etc/sysconfig/networking/devices
  -- /etc/sysconfig/networking/devices/ifcfg-eth0
  -- /etc/sysconfig/networking/profiles/default
    -- /etc/sysconfig/networking/profiles/default/hosts
    -- /etc/sysconfig/networking/profiles/default/ifcfg-eth0
    -- /etc/sysconfig/networking/profiles/default/resolv.conf
-- /etc/sysconfig/ntpd
-- /etc/sysconfig/pand
-- /etc/sysconfig/pcmia
-- /etc/sysconfig/prelink
-- /etc/sysconfig/rhn
  -- /etc/sysconfig/rhn/rhnCaps.d
  -- /etc/sysconfig/rhn/rhn-applet
  -- /etc/sysconfig/rhn/rhnsd
  -- /etc/sysconfig/rhn/sources
  -- /etc/sysconfig/rhn/up2date
  -- /etc/sysconfig/rhn/up2date-keyring.gpg
  -- /etc/sysconfig/rhn/up2date-uuid
-- /etc/sysconfig/samba
-- /etc/sysconfig/saslaauth
-- /etc/sysconfig/selinux -> /etc/selinux/config
-- /etc/sysconfig/sendmail
-- /etc/sysconfig/spamassassin
-- /etc/sysconfig/squid
-- /etc/sysconfig/syslog
-- /etc/sysconfig/system-config-securitylevel
.. /etc/sysconfig/system-config-users
.. /etc/sysconfig/tux
.. /etc/sysconfig/vncservers
.. /etc/sysconfig/xinetd
```

10 个目录，94 个文件

为了简洁起见，这里没有讨论所有的目录和文件。`/etc/sysconfig` 包含了许多对你的 Fedora 系统运行至关重要的硬件和软件设置。如果你需要排查新硬件配置的问题，了解这些文件的位置和内容将会非常有帮助。

`/etc/sysconfig` 下各种文件中的设置（如键盘、鼠标、声音等）通常是由相关的 Fedora 图形或基于控制的配置工具自动创建的。
