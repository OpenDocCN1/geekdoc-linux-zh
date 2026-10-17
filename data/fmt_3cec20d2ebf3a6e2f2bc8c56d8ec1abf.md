
# 第 6 章 Linux 服务器部署

`fsck` 命令只能在未挂载的文件系统上运行。如果根系统损坏，你可以使用对应 Linux 发行版的现场介质（live media）启动系统，并使用 `fsck` 命令检查硬盘上的根文件系统，因为默认情况下，现场 Linux 系统不会挂载它。

> 注释 43
> 使用现场介质上的 Linux 系统来修复安装在硬盘上的另一个 Linux 系统的问题，这被称为“系统救援”（system rescue）。

你可以配置现场 Linux 系统以使用硬盘上的根文件系统。要实现这一点，请将本地硬盘上的根文件系统挂载到现场 Linux 系统上的一个空目录下（例如 `/mnt`），然后在命令行提示符处执行 `chroot /mnt`。`chroot` 命令会将现场 Linux 系统的根目录更改为 `/mnt`，而这实际上是本地硬盘的根目录。从现在起，你将拥有根权限，可以像通常在硬盘上运行 Linux 系统一样，在根文件系统上运行任何命令。如果你运行密码（用于更改密码），你实际上是在更改安装在硬盘上的根 Linux 密码，从而在根文件系统损坏时恢复丢失的 Linux 系统。

此功能不仅限于现场介质。如果你从标准安装介质安装 Linux，欢迎界面通常会提供系统救援选项，启动一个不包含桌面环境的现场 Linux 系统。这个精简现场系统包含相同的恢复工具（`blkid`、`parted`、`e2fsks` 等），并允许你挂载硬盘上的根文件系统，同时运行 `chroot` 命令切换你的现场系统。

### 总结

- Linux 服务器通常使用的硬件比桌面系统多。这些硬件采用机架式结构安装在机架中。
- Linux 服务器上很常用 SCSI 存储（SAS），例如使用 iSCSI 或光纤通道（Fibre Channel）协议对 SAN 存储设备进行。DM-MPIO 可为一个或多个 SAN 提供冗余连接。
- RAID 在 Linux 服务器内部用于将多个硬盘组合为一个卷，以实现速度或容错性。它可以通过操作系统内部运行的软件、硬盘控制器或系统框架来实现。
- ZFS 是一种高性能、容错的文件系统，通常安装在 Linux 服务器上。ZFS 提供了许多类似于 RAID 的功能，利用跨本地磁盘、SAN、共享大文件和远程存储等广泛存储设备的空间。
- 尽管 BTRFS 仍在未使用，但它被设计为 ext4 文件系统的替代品，并提供了 ZFS 的某些卷和 RAID 特性。
- Linux 服务器不包含桌面环境，通常进行远程管理。然而，与其他 Linux 发行版相比，其安装过程会提示更多信息。
- 硬件不支持或损坏是 Linux 安装失败的最常见原因。设备驱动不当或缺失是 Linux 安装后立即出现问题的常见原因。
- 安装 Linux 后，你应该检查日志、`/proc/sys` 目录下的文件、相关命令，以及启动期间创建的系统日志。
- 你可以使用标准安装和现场 Linux 安装中的可启动 Linux 来访问并修复受损的安装。

# CompTIA Linux+ 和 LPIC-1：Linux 认证指南

### 关键术语

- 1U 服务器
- 刀片服务器 (blade server)
- 机箱 (Boxes)
- B 树文件系统 (BTRFS)
- `btrfs` 命令
- BTRFS 卷
- `btrack` 命令
- 检查点 (checkpoint)
- `chroot` 命令
- 数据 (data)
- `depmod` 命令
- 设备映射多路路径 (DM-MPIO)
- 磁盘镜像 (disk mirroring)
- 磁盘条带 (disk striping)
- 带校验的磁盘条带 (disk striping with parity)
- `dmesg` 命令
- `decode` 命令
- 容错 (fault tolerant)
- 光纤通道 (FC)
- 固件 RAID
- 客户操作系统 (guest operating system)
- 主机总适配器 (HBA)
- 宿操作系统 (host operating system)
- hwinfo
- `inmod` 命令
- 安装日志
- 互联网 SCSI (SCSI)
- iSCSI 标识符
- iSCSI 目标
- `isciadm` 命令
- `journalctl` 命令
- journald
- 磁盘堆叠 (JBOD)
- 基于内核的虚拟机 (KVM)
- Linux 服务器发行版
- 逻辑单元号 (LUN)
- `lsblk`
- `lsmod` 命令
- `lsp` 命令
- 元数据 (metadata)
- `mkfs.btrfs` 命令
- `modinfo` 命令
- `modprobe` 命令
- 模块 (module)
- `multipath` 命令
- 多路守护进程 (multipathd)
- SCSI ID
- 段错误 (segmentation fault)
- 独立计算环境简单协议 (SPICE)
- 快照 (snapshot)
- 软件 RAID 跨越
- 存储区域网络 (SAN)
- 系统 (system)
- 系统救援 (system rescue)
- 目标 ID
- 终止器 (terminator)
- 静态配置 (thick provisioning)
- 稀置配置 (thin provisioning)
- 1 型虚拟机监控
- 2 型虚拟机监控程序
- 不间断电源 (UPS)
- `virsh` 命令
- 虚拟机管理器 (Virtual Machine Manager)
- 虚拟化 (virtualization)
- 全世界名称 (WWN)
- ZFS 文件系统 (ZFS)
- ZFS 数据集
- ZFS 池
- ZFS 卷
- `zpool` 命令
- RAID-Z
- 独立磁盘冗余阵列 (RAID)

### 复习题

1. BTRFS 文件系统不需要检查错误，因为它们对数据损坏具有韧性。
   a. 正确
   b. 错误

2. 下列哪项描述了通过网络访问 SCSI 存储的计算机？
   a. iSCSI 目标
   b. SCSI 请求者
   c. SCSI 初始化器
   d. SCSI 终止器

3. 你想查找关于 Linux 安装期间发生问题的日志。你会在哪个目录找到日志？
   a. `/root`
   b. `/sys`
   c. `/var`

4. 下列哪项是不容错的？
   a. RAID 0
   b. RAID 1
   c. RAID 4
   d. RAID 5

5. 你可以使用什么将你的现场系统切换到哪里？
   a. `mount`
   b. `fsck`
   c. `chroot`
   d. `rescue`

6. 下列哪项不是 RAID 的类型？
   a. 硬件 RAID
   b. 软件 RAID
   c. 固件 RAID
   d. 串口 RAID

7. `/proc/sys` 存储在哪里？
   a. RAM
   b. 硬盘上
   c. `/etc`
   d. `/var`

8. 下列哪项允许空间与客户操作系统相同？
   a. 静态配置
   b. 1 型
   c. 稀置配置
   d. 2 型

9. DM-PIO 可以为一个或多个 SAN 提供冗余连接。
   a. 正确
   b. 错误

10. Linux 的哪个组件用于连接光纤通道？
    a. FC 初始化器
    b. FC 目标
    c. HBA
    d. WWPN

11. 下列哪项可以在安装过程中进行配置？
    a. 硬件 RAID
    b. 软件 RAID
    c. 固件 RAID
    d. 串口 RAID

12. 哪项可以创建类似于 RAID 1 的 ZFS 卷？
    a. `zpool create test`
    b. `zpool create mirror`
    c. `zpool create raidz`
    d. `zpool create raid`

13. 上一个问题的 ZFS 卷将挂载到哪个目录？
    a. `/mnt`
    b. `/media`
    c. `/zfs`
    d. `/`

14. 下列哪项描述了机架的最小高度？
    a. IU
    b. 系列 A
    c. 类型 A
    d. 5

15. 安装 Linux 后，哪些命令可以判断硬件是否被正确检测？
    a. `cat /proc/modules`
    b. `lspci`
    c. `ls -usb`
    d. `dmesg`

16. ZFS 卷默认在启动时挂载到 `/etc`。
    a. 正确
    b. 错误

17. 下列哪项在 Linux 安装期间导致段错误（致命信号 11）？
    a. RAM 问题
    b. CPU 负载过高
    c. 故障硬件组件
    d. 以上所有

18. 查看 `lsmod` 命令的输出时，你注意到几个以 `vm` 开头的模块。这表示什么？
    a. Linux 是客户操作系统。
    b. 设备驱动需要安装在你的系统上。
    c. 你的系统中没有虚拟内存。
    d. 系统运行在 KVM/QEMU 虚拟机程序下。

19. 服务器上托管操作系统和应用程序最常见的存储配置类型是什么？
    a. RAID 5
    b. ZFS
    c. RAID 1
    d. SAN + DM-PIO

20. 下列哪些命令可以在现代 Linux 系统上查看启动过程中捕的硬件信息？
    a. `/var/log/boot.log`
    b. `/var/log/messages`
    c. `/var/log/syslog`
    d. `journalctl -k`

# CompTIA Linux+ 和 LPIC-1：Linux 认证指南

这些项目应按照给出的顺序完成。本章中的动手项目总计需要三小时才能完成。此实验的要求包括：

- 在项目 2-1 中一个安装了 Fedora Linux 的计算机
- 适用于你的计算机平台（Intel 或 ARM）的最新 Ubuntu Server 启动媒体 ISO

## 项目 6-1

**预计时间：** 40 分钟
**目标：** 安装 Ubuntu Server。
**描述：** 在这个动手项目中，你将在 Windows 或 macOS 计算机的虚拟机内安装 Ubuntu Server Linux，之后选择 LVM 分区配置。

1. 在你的虚拟化软件中，创建一个具有以下特征的新虚拟机 **Ubuntu Linux**：
   - 2 GB 内存（不进行动态分配）
   - 使用 PC 的网卡连接网络（优先使用外部交换机或桥接模式）
   - 一个 50 GB 的 SATA/SAS/SCSI 虚拟硬盘（动态分配）
   - 虚拟机 DVD 驱动器挂载了 Ubuntu Server 的启动媒体 ISO

> 注意：如果你的虚拟化程序支持安全启动（例如 Hyper-V），请在第 2 步之前在虚拟机的设置中取消此功能。

2. 使用你的虚拟化软件启动并连接到你的 Ubuntu Linux 。
3. 在 GNU GRUB 界面，确保选择了 **Try or Install Ubuntu Server** 并按 **Enter**。

> 注意：Ubuntu Server 安装程序不使用图形界面。因此，你使用 Tab 键在屏幕上的按钮之间切换，并按 Enter 键进行选择。

4. 在欢迎界面，确保选择了 **English** 并按 **Enter**。
5. 在键盘配置界面，选择正确的布局并选择 **Done**。
6. 在安装类型界面，确保勾选了 **Ubuntu Server** 并选择 **Done**。
7. 在网络连接界面，确保你的网络接口设置为从 DHCP 服务器获取 IP 地址，并选择 **Done**。
8. 在代理界面，可选地提供你教室代理的 URL（如果你的课程使用了代理的话）并选择 **Done**。
9. 在 Ubuntu 存档镜像界面，选择 **Done**。
10. 在向导存储配置界面，选择 **Use an entire disk** 和 **Set up this disk as an LVM group** 并选择 **Done**。
11. 在存储配置界面，查看分区和 LVM 配置。注意根文件 (system-ubuntu) 没有利用所有剩余空间。选择 **ubuntu-lv**，选择 **Edit**，在 Size 对话框中输入最大大小并 **Save**。检查你的配置，选择 **Done**，然后选择 **Continue**。

12. 在个人资料设置界面，选择以下信息并在完成后选择 **Done**：
    a. 你的姓名 = 输入你的真实姓名
    b. 你的服务器名称 = `ubuntu`
    c. 用户名 = `user1`
    d. 密码 = `LINUXRocks!`

13. 在 SSH 设置界面，点击 **Install OpenSSH server** 并选择 **Done**。
14. 在 Featured Servers 磁贴中，选择 **Done**。
15. 在完成界面，选择 **Reboot Now**。当提示移除安装介质时，使用你的虚拟化软件断开虚拟 DVD 驱动器上的 Ubuntu Server 启动 ISO 镜像并按 **Enter**。
16. 系统启动后，注意无法进行图形登录。使用密码 `LINUXRocks!` 登录 tty1 用户。
17. 在命令提示符下，输入 `sudo passwd root` 并按 **Enter** 设置 root 用户密码。在提示时，输入你的密码（`LINUXRocks!`），然后输入所需的 root 密码。
18. 在命令提示符下，输入 `id` 并按 **Enter** 验证 root 用户。在提示时提供 root 用户密码（`LINUXRocks!`）。
19. 在命令提示符下，依次输入以下命令并按 **Enter**。检查并解释每个的输出：

```
df -ht
fdisk -l
lvdisplay
lsblk
blkid
ls -1 /dev/disk/by-uuid
ls -1 /dev/disk/by-partuuid
ls -1 /dev/disk/by-id
ls -1 /dev/disk/by-path
cat /etc/fstab
```
