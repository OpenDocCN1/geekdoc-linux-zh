

## mingetty — (版本 0.9.4, 32K)

[B]

mingetty 程序是一个轻量级、极简的 getty 程序，仅用于虚拟控制台。Mingetty 不适用于串行线路（此时应使用 mgetty 程序）。

## mkbootdisk — (版本 1.1, 5K)

[B]

mkbootdisk 程序会创建一个独立的启动软盘，用于引导当前运行的系统。创建的启动盘会查找 `/etc/fstab` 中提到的设备上的根文件系统，并包含一个初始 ramdisk 镜像，该镜像会为系统加载任何必要的 SCSI 模块。

## mkinitrd — (版本 2.0, 7K)

[B]

Mkinitrd 创建用于初始 ramdisk（initrd）镜像的文件系统镜像。这些 ramdisk 镜像通常用于预加载访问根文件系统所需的块设备模块（SCSI 或 RAID）。换句话说，通用内核可以在没有针对任何 SCSI 适配器的驱动程序的情况下构建，这些适配器将 SCSI 驱动程序作为模块加载。由于内核需要读取这些模块，但在这种情况下它无法寻址 SCSI 适配器，因此使用了初始 ramdisk。初始 ramdisk 由操作系统加载器（通常是 LILO）加载，并且一旦 ramdisk 被加载，内核就可以使用它。Ramdisk 镜像会加载正确的 SCSI 适配器，并允许内核挂载根文件系统。mkinitrd 程序利用 `/etc/conf.modules` 文件中的信息创建这样的 ramdisk。

## mkkickstart — (版本 1.1, 4K)

mkkickstart 程序会根据主机编写一个 kickstart 描述。然后，在 CD-ROM 或 NFS 安装过程中，可以使用该 kickstart 描述在一台或多台其他机器上自动构建该机器的 Red Hat Linux 配置。如果您想使用 kickstart 方法自动安装 Red Hat Linux，请安装 mkkickstart。

## mktemp — (版本 1.5, 8K)

[B]

mktemp 实用程序接受给定的文件名模板，并覆盖其中的一部分以创建唯一的文件名。这允许 shell 脚本和其他程序安全地创建和使用 /tmp 文件。如果您需要使用将创建和使用唯一 /tmp 文件的 shell 脚本或其他程序，请安装 mktemp 软件包。

## 附录 C：软件包列表

## mount — (版本 2.9, 115K)

[B]

mount 软件包包含 mount、umount、swapon 和 swapoff 程序。系统中可访问的文件排列在一个大的树状结构中。这些文件可以分布在多个设备上。mount 命令将某个设备上的文件系统挂载到系统的文件树中。umount 命令将文件系统从树中卸载。swapon 和 swapoff 分别指定和禁用用于分页和交换的设备与文件。

## mouseconfig — (版本 3.7, 136K)

[B]

Mouseconfig 是一个基于文本的鼠标配置工具。Mouseconfig 设置配置和使用 Red Hat Linux 系统上的鼠标所需的文件和链接。mouseconfig 工具可用于为 gpm 等程序设置正确的鼠标类型，并且可以与 Xconfigurator 一起使用来为 X Window System 设置鼠标。

## net-tools — (版本 1.51, 395K)

[B]

net-tools 软件包包含设置网络所需的基本工具：arp、rarp、ifconfig、netstat、ethers 和 route。

## ntsysv — (版本 1.0.4, 23K)

[B]

ntsysv 更新和查询系统服务的运行级信息。ntsysv 使系统管理员不必直接操作 `/etc/rc.d` 中的众多符号链接。

## pam — (版本 0.66, 1,850K)

[B]

PAM（可插拔认证模块）是一个系统安全工具，允许系统管理员设置认证策略，而无需重新编译进行认证的程序。

## passwd — (版本 0.50, 28K)

[B]

passwd 软件包包含一个系统实用程序（passwd），它使用 PAM（可插拔认证模块）设置和/或更改密码。要使用 passwd，您的系统上应安装 PAM。

## pwdb — (版本 0.56, 417K)

[B]

pwdb 软件包包含 libpwdb，即密码数据库库。Libpwdb 是一个实现通用用户信息数据库的库。Libpwdb 是专门为与 Linux 的 PAM（可插拔认证模块）配合使用而设计的。Libpwdb 允许对安全工具（如 `/etc/passwd`、`/etc/shadow`）以及包括 NIS 和 Radius 在内的网络认证系统进行可配置的访问和管理。

## quota — (版本 1.66, 79K)

[B]

quota 软件包包含用于按文件系统监控和限制用户和/或组磁盘使用的系统管理工具。

## raidtools — (版本 0.90, 151K)

该软件包包含在 Linux 下设置和维护软件 RAID 设备所需的工具。它仅适用于 Linux 2.2 及更高版本的内核，或专门打了较新 raid 支持补丁的 2.0 内核。

## rootfiles — (版本 5.2, 1K)

[B]

rootfiles 软件包包含放置在 root 用户帐户中的基本必需文件。这些文件基本上与 etcske l 软件包中的文件相同，后者放置在普通用户的主目录中。

## rpm — (版本 2.93, 1,599K)

[B]

Red Hat 软件包管理器（RPM）是一个强大的命令行驱动的软件包管理系统，能够安装、卸载、验证、查询和更新软件包。每个软件包都由一个文件存档以及有关该软件包的信息（如其版本、描述等）组成。

## setup — (版本 2.0.1, 15K)

[B]

setup 软件包包含一组非常重要的系统配置和设置文件，例如 passwd、group、profile 等。您应该安装 setup 软件包，因为您会发现自己在系统管理中会用到它的许多功能。

