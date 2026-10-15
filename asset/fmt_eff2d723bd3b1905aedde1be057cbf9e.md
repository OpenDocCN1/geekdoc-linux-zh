
如果系统进程加载失败，可能是因为它配置了特定于服务的错误设置，或者它在 Linux 安装期间没有被安装；在后一种情况下，你通常可以删除并重新安装该进程来解决问题。

## 系统救援 (System Rescue)

回想第 2 章，你可以通过从 DVD 或 USB 现场介质或现场媒体 ISO 镜像启动 Linux 系统。在修复受损系统时，从现场媒体启动系统对 Linux 管理员有几个好处。现场媒体包含一个小型的可启动 Linux 内核和虚拟文件系统，它们被加载到内存中，并可以访问底层硬盘上的文件系统。因此，你可以使用从现场媒体启动的系统中的工具来修复硬盘上 Linux 安装无法启动的问题，例如：

- 引导加载程序问题
- 文件系统/分区问题
- 配置文件问题
- 驱动程序问题

所有现场介质都包含了几个修复系统问题的工具，包括 `fdisk`、`parted`、`mkfs` 和 `fsck`，这些将在将在后的模块中介绍。从上一个模块可知，`fsck` 命令只能在未挂载的文件系统上运行。如果根文件系统损坏，你可以使用你 Linux 发行版的现场介质启动系统，并使用 `fsck` 命令检查硬盘上的根文件系统，因为默认情况下现场 Linux 系统不会挂载它。

### 注意事项 43

使用现场介质上的 Linux 系统来修复安装在硬盘上的另一个 Linux 系统的问题，被称为系统救援 `system rescue`。

你也可以配置现场介质系统使用硬盘上的根文件系统。要做到这一点，请在现场 Linux 系统中的一个空目录（例如 `/mnt`）下挂载本地硬盘上的根文件系统，并在命令行提示符处使用 `chroot /mnt`。`chroot` 命令将现场 Linux 系统的根目录更改为 `/mnt` 目录，而该目录实际上是本地硬盘上的根文件系统。从这一点起，你将拥有对根驱动器上任何命令的 root 用户权限，就像你通常在 Linux 发行版中拥有它的一样。例如，如果你使用密码（用于更改用户），你实际上是在更改安装在硬盘上的 root Linux 密码。如果根文件系统已损坏。

此功能不仅限于现场介质。如果你从标准安装介质安装 Linux，欢迎界面通常提供一个系统救援选项，用于启动不包含桌面环境的现场 Linux 系统。这个小型的现场系统包含相同的恢复工具（`fdisk`、`parted`、`e2fsfs`、`fsck` 等），并允许你挂载硬盘上的根文件系统以及使用 `chroot` 命令切换你的现场 Linux 系统。

## 总结

- Linux 服务器通常比桌面系统使用更多的硬件。这些硬件用于提高速度。
- 多路输出 `MPIO` 用于将多个驱动器合并为一个卷。
- 与 `ext4` 相比，`ZFS` 提供了许多功能。
- `BTRFS` 设计用于替代 `ZFS`。
- 虽然这种现象很常见，但 `BTRFS` 提供了一些额外功能。
- 不支持的设备驱动程序是问题的常见原因。
- 硬件不当是故障的常见原因。
- 你应该检查启动日志来修复安装。

# 第 6 章 Linux 服务器部署

245

### 术语 (Key Terms)

- `1U`
- 刀片服务器 `blade server`
- `Boxes`
- `B树文件系统` `BTRFS`
- `brtfs`
- 检查点 `checkpoint`
- `chroot`
- 数据 `data`
- `depmod`
- 设备映射器 `DM`
- 磁盘镜像 `disk mirroring`
- 磁盘条带 `disk striping`
- `dmesg`
- 光纤 `FC`
- 固件
- 客户操作系统 `guest operating system`
- 主机适配器 `HBA`
- 主机操作系统 `host operating system`
- `hwinfo`
- `inmod`
- 接口 SCSI `iSCSI`
- `journalctl`
- `journal`
- 无冗磁盘列 `JBOD`
- 基于内核的虚拟机 `KVM`
- Linux 发行版
- 逻辑单元号 `LUN`
- `lsblk`
- `lsmod`
- `lspci`
- `mdadm`
- 元数据 `metadata`
- `mkfs.btrfs`
- `modinfo`
- `modprobe`
- 模块 `module`
- `multipath`
- 多路守护进程 `multipath daemon`
- 多路 `multipath`
- 超频 `overclocked`
- 并 SCSI
- 快速器 `QEMU`
- 机架式 `rackmount`
- `RAID-Z`
- 独立冗余阵列 `RAID`
- `rmmod`
- `SCSI`
- 段错误 `segmentation fault`
- 计算环境简单协议 `SPICE`
- 快照 `snap`
- 软件 RAID
- 跨越 `spanning`
- 存储区域网络 `SAN`
- 系统 `system`
- 系统救援 `system rescue`
- 目标 `target`
- 终止器 `terminator`
- 置配置 `thick provisioning`
- 置配置 `thin provisioning`
- 类型 1 验证
- 类型 2 验证
- 不间断电源 `UPS`
- `vnm`
- 虚拟机管理器
- 虚拟化 `virtualization`
- 全局范围名称 `WNN`
- 字节文件系统 `ZFS`
- `ZFS` 数据集 `dataset`
- `ZFS` 池 `pool`
- `zpool`

## 复习题

1. `BTRFS` 文件系统不需要检查错误，因为它们对具有弹性。
a. true
b. 错误

2. 下列哪项描述了通过网络访问 `iSCSI` 存储的计算机？
a. `iSCSI` 目标
b. `iSCSI` 请求者
c. `iSCSI` 初始化器
d. `iSCSI` 终止器

3. 你想查看日志以获取 Linux 安装过程中发生问题的信息。你在哪个目录找到它们？
a. `/root`
b. `/sys`
c. `/var`
d. `/etc`

4. 下列哪个 `RAID` 级别不容错？
a. `RAID 0`
b. `RAID 1`
c. `RAID 4`
d. `RAID 5`

5. 救援系统可以使用什么从现场系统的根切换到硬盘上安装的 Linux 系统的根？
a. `mount`
b. `bisymage`
c. `chroot`
d. `rescue`

6. 下列哪项不是 `RAID` 类型？
a. 硬件 `RAID`
b. 软件 `RAID`
c. 固件 `RAID`
d. 串行 `RAID`

# 第 6 章 Linux 服务器部署

7. `/proc` 文件系统存储在哪里？
- + a. 在 RAM 中
- b. 在 `/` 目录下的硬盘驱动上
- c. 在 `/etc` 目录下的硬盘驱动上
- + d. 在 `/var` 目录下的硬盘驱动上

8. 配置虚拟硬盘时，哪种功能允许硬盘文件根据客主机系统的请求扩展到所需空间？
- + a. 静态置备 `thick provisioning`
- + b. 类型 1
- + c. 动态置备 `thin provisioning`
- + d. 类型 2

9. `DM-PIO` 可以配置为存储在 `SAN` 上的数据提供多个冗余连接。
- + a. 正
- + b. 错误

10. Linux 服务器的哪个组件用于连接到光纤 `Fibre Channel` `SAN`？
- + a. `FC` 启动器 `initiator`
- + b. `FC` 目标 `target`
- + c. `FC HBA`
- + d. `WWPN`

11. 哪种 `RAID` 类型可以在 Linux 安装过程中完全完全配置？
- + a. 硬件 `RAID`
- + b. 软件 `RAID`
- + c. 固件 `RAID`
- + d. 串行 `RAID`

12. 使用什么可以从 `/dev/sdb` 和 `/dev/sdc` 创建类似于 `RAID` 级别 1 的 `ZFS` 卷？
- + a. `zpool create /dev/sdb /dev`
- + b. `zpool create mirror /dev/sdb /dev/sdc`
- + c. `zpool create raidz /dev/sdb /dev/sdc`
- + d. `zpool create raid2 /dev/sdb /dev/sdc`

13. 上一个问题中的 `ZFS` 卷将被 `ZFS` 系统挂载到哪个目录？
- + a. `/mnt/test`
- + b. `/media/test`
- + c. `/zfs/test`
- + d. `/test`

14. Linux 服务器通常安装在机架式服务器硬件中。下列哪个描述了机架式服务器的最低要求？
- + a. `U`
- + b. `A` 系列
- + c. `A` 类型
- + d. `5` 级

15. 下列命令中，哪个可以判断你的网络硬件在 Linux 安装期间是否被检测？
- + a. `cat /proc/modules/network`
- + b. `lspci`
- + c. `lsh -class network`
- + d. `dmesg`

16. `ZFS` 卷默认在启动时通过 `/etc/fstab` 挂载。
- + a. 正
- + b. 错误

17. 下列哪项可能导致 Fedora 安装过程中出现段错误 `致命信号 11`？
- + a. `RAM` 问题
- + b. `CPU` 负载过高
- + c. 故障硬件组件
- + d. 以上所有

18. 在查看 `lmod` 命令的输出时，你注意到几个以 `vm` 开头的模块。这说明了什么？
- + a. Linux 是一个客操作系统
- + b. 你的系统需要安装设备驱动程序
- + c. 系统没有虚拟内存
- + d. 系统正在运行 `KVM/QEMU` 虚拟机管理器。

19. 在服务器上托管操作系统和应用程序时，哪种冗余配置最常见？
- + a. `RAID 5`
- + b. `ZFS`
- + c. `RAID 1`
- + d. `SAN + DM-PIO`

20. 下列哪个命令可以在现代 Linux 系统上查看启动过程中捕获的硬件信息？
- + a. `less /var/log/boot.log`
- + b. `less /var/log/messages`
- + c. `less /var/log/syslog`
- + d. `journalctl -k`

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

## 动手项目

这些项目应该按照给定的顺序完成。本章动手项目总共需要三小时完成。此实验的要求包括：

- 在动手项目 2-1 中一个安装了 Fedora Linux 的计算机
- 适用于你电脑平台 `Intel` 或 `ARM` 的最新 Ubuntu Server 现场媒体 ISO

### 项目 6-1

**预计时间：** 40 分钟
**目标：** 安装 Ubuntu Server。
**描述：** 在此动手项目中，你将在 Windows 或 macOS 计算机的虚拟机内安装 Ubuntu Server Linux，之后选择 LVM 分区配置。

1. 在你的虚拟化软件中，创建一个具有以下特征的新虚拟机 **Ubuntu Linux**：
    a. 2 GB 内存 `非动态分配`
    b. 通过 PC 的网卡连接互联网 `最好使用外部交换机或桥接模式`
    c. 50 GB SATA/SAS/SCSI 虚拟硬盘 `动态分配`
    d. 虚拟机的 DVD 光驱挂载了 Ubuntu Server 的现场媒体 ISO
    注意：如果你的虚拟机管理器支持安全启动 `例如 Hyper-V`，请在步骤 2 之前在虚拟机的设置中取消选择此功能。

2. 使用你的虚拟化软件启动并连接到你的 Ubuntu 虚拟机。

3. 在 GRUB 界面，确保选择了 **Try or Install Ubuntu Server** 并按回车。
    注意：Ubuntu Server 安装程序不使用图形界面。你必须使用 Tab 键在屏幕上的按钮之间切换进行选择。

4. 在欢迎界面，确保选择了 **English** 并按回车。

5. 在键盘配置界面，选择正确的布局并选择 Done。对于大多数人来说，这将是 English `US` 美国英语）。

6. 在安装类型界面，确保勾选了 **Ubuntu Server** 并选择 Done。

7. 在网络连接界面，确保你的网络接口设置为从 DHCP 默认获取 IP 地址，并选择 Done。

8. 在代理配置界面，可选提供 URL `如果你的教室使用` 并选择 Done。

9. 在 Ubuntu 存档界面，选择 Done。

10. 在引导式存储配置界面，选择 **Use entire disk** 和 **Set up this as LVM group** 并选择 Done。

11. 在存储配置界面，选择 LVM 配置。注意系统 `ubuntu-lv` 未利用空间。选择 **ubuntu-lv**，点击 Edit，在 Size 框中输入最大值并 Save。

12. 在个人配置界面，选择以下信息并选择 Done：
    - 姓名 = 你的名字
    - 服务器名称 = **ubuntu**
    - 用户名 = **user**
    - 密码 = **LINUXRocks!**
13. SSH 设置界面，选择 **Install OpenSSH server** 并选择 Done。

14. 功能界面，选择 Done。

15. 在安装界面，选择 **Reboot Now**。当提示移除安装介质时，使用虚拟化软件断开虚拟机 DVD 光驱上的 Ubuntu Server ISO 并按回车。

16. 系统启动后，注意无法使用图形登录。使用密码 `LINUXRocks!` 登录 tty1 **user**。

17. 在命令提示符下，输入 `sudo passwd root` 并回车设置 root 密码。提示时输入你的密码 `LINUXRocks!`，然后输入 root 密码。

18. 在命令提示符下，输入 `su -` 并回车切换到 root 用户。提示时输入 root 密码。

19. 在命令提示符下，依次输入以下命令并回车。检查每个命令的输出：
    - `df -h`
    - `fdisk -l`
    - `lvdisplay`
    - `lsblk`
    - `ls /dev/disk/by-uuid`
    - `ls /dev/disk/by-part`
    - `ls /dev/disk/by-id`
    - `ls /dev/disk/by-path`
    - `cat /etc/fstab` `注意 Ubuntu Server 创建的是交换文件而不是交换分区`

20. 输入 **exit** 退出用户。

### 项目 6-2

**预计时间：** 30 分钟
**目标：** 配置软件 RAID。
**描述：** 在此项目中，你将向 Ubuntu Linux 虚拟机添加硬盘，配置 RAID 5 卷，并处理硬盘故障和恢复。项目结束时，你将移除 RAID 配置。

1. 在 Ubuntu Linux 机器上，使用用户名 **root** 和密码 `LINUXRocks!` 登录终端 `tty1`。

2. 在命令提示符下，输入 `poweroff` 并回车关闭虚拟机。在虚拟化软件中，为虚拟机添加新的 1 GB 动态分配 SATA/SAS 硬盘。完成后，启动 Ubuntu 虚拟机。

3. Ubuntu Linux 虚拟机已启动，使用用户名 root 和密码 `lsblk!` 登录命令行终端 `tty1`。此处应为 `lsblk`）。注意额外的磁盘设备名称为 `sdb`、`sdc` 和 `sdd`。

4. 在命令提示符下，输入 `mdadm --create /dev/md0 --level=5 --devices=4 /dev/sdb /dev/sdc /dev/sdd --verbose` 并回车。

5. 在命令提示符下，输入 `cat /proc/mdstat` 并回车。你的 RAID 5 卷已成功创建。

6. 在命令提示符下，输入 `cat /etc/mdadm/mdadm.conf` 并回车。注意你的 RAID 5 卷以默认文件方式列出。

7. 在命令提示符下，输入 `mdadm --detail --scan --verbose >/etc/mdadm/mdadm.conf`。接下来，输入 `cat /etc/mdadm/mdadm.conf` 并回车查看启动配置。

8. 在命令提示符下，输入 `mkfs -t ext4 /dev/md0`。

9. 在命令提示符下，输入 `mkdir /data` 并回车为 RAID 5 卷创建挂载点。接下来，输入 `mount /dev/md0 /data` 并回车挂载文件系统。

10. 在命令提示符下，输入 `cp /fstab /etc/fstab` 以确保 RAID 卷在启动时挂载。

11. 在命令提示符下，输入 `df -h` 并回车。你的 RAID 5 卷有多大？为什么不是 4 GB `4 x 1 GB`？

12. 在命令提示符下，输入 `lsblk` 并回车。注意每个磁盘的 md0 设备关联。接下来，输入 `blkid /dev/md0`，文件系统有 UUID f 吗？

13. 在命令提示符下，输入 `mdadm --detail /dev/md0` 并回车。RAID 卷中的所有设备是否都激活且正常？

14. 在命令提示符下，输入 `mdadm --manage --set-faulty /dev/md0 /dev/sdc` 并回车清除磁盘损坏。注意 RAID 卷被列为 clean `degrading` `下降`。

15. 输入 `ls -F /data` 并回车。文件是否可用且可访问？

16. 在命令提示符下，输入 `mdadm --manage /dev/md0 --remove /dev/sdb` 并回车，这将从 RAID 卷中移除 `/dev/sd` 设备。在生产环境中，这时你应该从服务器上物理移除硬盘并更换新硬盘。

17. 在命令提示符下，输入 `mdadm --manage /dev/md0 --add /dev/sdb` 并回车，再次将 `/dev/sd` 设备添加到 RAID 卷中。注意 RAID 卷的状态为正在重建 `rebuilding`。几分钟后，重复你的命令。状态列表应显示活动同步 `active sync`，表明添加的设备已完全正常并加入 RAID 卷。

18. 在命令提示符下，输入 `fdisk /dev/sdb` 并回车查看你的更改，这将删除 `/dev/sdb` 设备上的现有 RAID 分区。重复此过程

21. 最后，输入 `rm -f /etc/mdadm/mdadm.conf` 移除 RAID 配置。

22. 输入 `exit` 退出会话。

# 第 6 章 Linux 服务器部署

### 项目 6-3

**预计时间：** 30 分钟

**目标：** 配置 ZFS

**描述：** 在此实操课程中，你将在你的 Ubuntu 虚拟机上安装并配置 ZFS 文件系统。在项目结束时，你将移除 ZFS 配置。

- 1. 在你的 Ubuntu 虚拟机上，使用用户名 `root` 和密码 `LINUXrock!` 登录命令行终端 `tty1`。

- 2. 在命令提示符处，输入 `apt install zfsutils-linux` 并按 **Enter** `回车` 在你的 Ubuntu 系统上安装 ZFS 支持。

> 注意 46
> Ubuntu Server 使用的包管理器与 Fedora Linux 不同。`apt` 命令在功能上等同于你之前章节中用于从存储库下载并安装软件的 `dnf` 命令。`apt` 和 `dnf` 都将在第 11 章中讨论。

- 3. 在命令提示符处，输入 `zpool create data /dev/sdb -f` 并按 **Enter**，从 `/dev/sdb` 空间创建一个简单的 ZFS 卷 `-f` 选项是必要的，因为 `/dev/sdb` 仍然带有来自 Geck-2 的 RAID 签名。接下来，在命令提示符处输入 `zpool list` 并按 Enter 查看你的配置。

- 4. 在命令提示符处，输入 `df -h` 并注意 ZFS 卷已自动挂载。请注意 ZFS 为数据创建了单个分区 `/dev/sdb1` 作为 ZFS 配置的分区 `/dev/sdb9`。

- 5. 在命令提示符处，输入 `cp /etc/hosts` 并按 **Enter**，将 `/etc/hosts` 文件复制到你的 ZFS 文件系统中。接下来，输入 `ls -l` 验证文件是否成功复制。

- 6. 在命令提示符处，输入 `zpool destroy data` 并按 **Enter** 移除数据卷。

- 7. 在命令提示符处，输入 `zpool create mirror /dev/sdb /dev/sdc -f` 并按 **Enter**，从 `/dev/sdb` 和 `/dev/sdc` 空间创建一个挂载到 data 目录的镜像 ZFS 卷。接下来，在命令提示符处输入 `zpool list` 并按 Enter 查看你的配置。最后，在命令提示符处输入 `zpool status data` 并按 Enter 验证你的配置。

- 8. 在命令提示符处，输入 `lsblk` 并注意 ZFS 为数据硬盘创建了分区 `/dev/sdb1`，以及为 ZFS 配置创建了分区 `/dev/sdb9` 和 `/sdc9`。

- 9. 在命令提示符处，输入 `dd if=/dev/zero of=/dev/sdbb count=100000` 并按 **Enter**，使用 `dd` 命令覆盖 `/dev/sdb1` 的部分内容，模拟磁盘损坏。接下来，在命令提示符处输入 `zpool scrub data` 并按 Enter 更新 ZFS 文件系统的状态，然后在命令提示符处输入 `zpool status data` 并按 Enter 查看你的问题是否已解决。

- 10. 在命令提示符处，输入 `zpool detach data /dev/sdb` 并按 **Enter** 从镜像中移除坏盘 `/dev/sdb`。在命令提示符处输入 `zpool status data` 验证它已不再列在其中。

- 11. 在命令提示符处，输入 `zpool attach data /dev/sdc /dev/sdc -f` 并按 **Enter** 对 `/dev/sdc` 上的数据进行镜像。镜像正在完全重同步，并带有 `/dev/sdc` 和 `/dev/sdc1` 的统计数据。

- 12. 在命令提示符处，输入 `zpool iostat -v data` 并按 **Enter** 查看指标的输入输出统计。接下来，输入 `zpool destroy data` 移除数据。

# CompTIA Linux+ LPC1：Linux 认证指南

- 13. 在命令提示符处，输入 `zpool create raidz /dev/sdb /dev/sdc /dev/sdd /dev/sde -f` 并按 Enter 创建一个名为 `/dev/sdb`, `/dev/sdc`, `/dev/sdd`, `/dev/sde` 的 RAID-Z 卷，然后在命令提示符处输入 `zpool status` 并按 Enter 验证结果。接下来，输入 `zpool iostat -v` 并按 Enter 查看你的 RAID-Z 卷的输入输出统计。

- 14. 在命令提示符处，输入以下任意命令并按 Enter 在 `/data` 下创建三个子目录：
```
