
跨跨越 (`spanning`) — 一种 `RAID 0` 类型，允许两个或多个设备表示为单一卷。另请参见 `SCSI ID`。终止器 (`terminator`) — 用于终止电信号介质以吸收传输信号并防止信号反射的设备。

## 复习题

1. 两个外围设备可以同时共享并使用相同的中断请求设置。正确或错误？

2. 下列哪项用于为每个设备提供独立的物理内存部分供使用？

   a. `SCSI`

   b. `DMA`

   c. `IRQ`

   d. `I/O` 地址

3. 你想查看日志文件以获取有关你遇到的问题的信息。你会在哪个目录找到它们？

   a. `/root/log`

   b. `/sys/log`

   c. `/var/log`

   d. `/etc/log`

4. 下列哪种 `RAID` 级别不容错？

   a. `RAID 0`

   b. `RAID 1`

   c. `RAID 4`

   d. `RAID 5`

5. `DMA` 和 `IRQ` 具有哪些共同点？（选择所有）

   a. 它们都有用于服务两种不同位宽（16 位和 8 位）的分配。

   b. 它们没有共同点。

   c. 它们都有一个输给正常用户使用的分配。

   d. 它们都是分配的列表。

6. 为了利用即插即用，必须满足以下哪些条件？（选择所有）

   a. 操作系统必须支持即插即用。

   b. 系统必须拥有所有可用的 `IRQ`。

   c. 要配置的设备必须支持即插即用。

   d. `BIOS` 必须支持即插即用。

7. `/proc` 文件系统存储在哪里？

   a. 在 `RAM` 中

   b. 在硬盘驱动器的 `/` 目录中

   c. 在硬盘驱动器的 `/etc` 目录中

   d. 在硬盘驱动器的 `/var` 目录中

8. `COM 1` 的默认 `IRQ` 是什么

   a. 2

   b. 4

   c. 1

   d. 0

9. 每个设备必须有唯一的 `IRQ`、`DMA` 和 `I/O` 地址分配。正确或错误？

10. 使用 8 位宽数据的 `SCSI` 设备使用 ____________________

    a. 8 脚接器

    b. 15 脚接器

    c. 50 脚接器

    d. 68 脚接器

11. 有多少个直接内存通道？

    a. 2

    b. 5

    c. 8

    d. 7

12. `/proc` 文件系统存储在哪里？

    a. 在 `RAM` 中

    b. 在硬盘驱动器的 `/` 目录中

    c. 在硬盘驱动器的 `/etc` 目录中

    d. 在硬盘驱动器的 `/var` 目录中

13. 按优先级列出 `SCSI ID`。

    a. 5

    b. 7

    c. 15

    d. 8

    e. 2

    f. 11

    g. 13

    h. 1

    i. 0

14. 下列哪项可用于简化服务器的部署？（选择所有）

    a. 磁盘镜像软件

    b. 自动安装服务器

    c. `kickstart` 文件

    d. 引导磁盘

15. 下列哪个 `RAID` 级别称为镜像？

    a. `RAID 0`

    b. `RAID 1`

    c. `RAID 4`

    d. `RAID 5`

16. `SCSI-3` 卡总是比 `SCSI-2` 卡容纳更多设备。正确或错误？

17. `LPT1` 的默认 `IRQ` 和 `I/O` 设置是什么？

   a. `IRQ 7` 和 `I/O` 地址 `378–3F`

   b. `IRQ 5` 和 `I/O` 地址 `378–3F`

   c. `IRQ 5` 和 `I/O` 地址 `3F8–3FF`

   d. `IRQ 7` 和 `I/O` 地址 `278–2F`

# 实验项目 321

18. `SCSI-1` 也称为 ____________________。

19. 你需要查找当前使用的 `IRQ`、`DMA` 和 `I/O` 地址分配。你应该做什么？

   a. 打开桌面环境并在设置中查看系统信息。

   b. 查看 `/etc` 目录下的文件。

   c. 查看 `/settings` 目录下的内容。

   d. 查看 `/proc` 目录下的内容。

20. 安装后，你想查看安装日志文件。你应该查看哪些文件？（选择两个）

   a. `/root/install.log`

   b. `/proc/install.log`

   c. `/root/install.log.syslog`

   d. `/proc/install.log.syslog`

## 实验项目

这些项目应按照顺序完成。本章介绍的实验总共需要三小时。实验室的要求包括：

- 在实验 2-1 中完成的预检查清单

- 根据实验 3-1 安装了 Red Hat Fedora Core 2 的计算机

- Red Hat Fedora Core 2 CD-ROM 安装套装（四张 CD）

- 一张空白软盘

![](img/8fe037bf1ed016dccb79dbd1a27184f2_338_0.png)

### 项目 7-1

在这个项目中，你使用实验 2-1 创建的预检查清单创建并查看 `kickstart` 文件，并与 Red Hat 安装程序自动生成的 `kickstart` 文件进行比较。

1. 开启你的计算机。当 Linux 系统加载后，你将被放置在图形终端 (`tty7`)。使用用户名 `root` 和密码 `secret` 登录 `GNOME` 桌面。

2. 选择 Red Hat 图标，选择系统工具 (`System Tools`)，然后点击 `Kickstart`。

在 `Kickstart` 配置器的基本配置（Basic Configuration）界面中，请确保了以下设置：

- 默认语言 = English (USA)

- 键盘 = U.S. English

- 鼠标 = 参考预安装检查清单（Preinstallation checklist）

- 时区 = 参考预安装检查清单（Preinstallation checklist）

- Root密码 = `secret`

- 加密根密码 = yes（已勾选）

- 语言支持 = English (USA)

- 目标架构 = x86, AMD64 或 Intel EM64T

- 安装后重启系统 = no（未勾选）

- 以文本模式执行安装（默认是图形界面） = no（未勾选）

- 以交互模式执行安装 = no（未勾选）

- 点击左侧窗格中的安装方法（Installation Method）。确保已选择执行新安装（Perform new installation）和光驱（CD-ROM）。

- 点击左侧窗格中的引导加载程序选项（Boot Loader Options）。确保已选择安装新引导加载程序（Install new boot loader）和在主引导记录（MBR）上安装引导加载程序（Install boot loader on Master Boot Record (MBR)）。

- 点击左侧窗格中的分区信息（Partition Information）。确保已选择清除主引导记录（Clear Master Boot Record）、删除所有现有分区（Remove all existing partitions）和初始化磁盘标签（Initialize the disk label）。点击添加（Add）按钮，并在显示的界面中输入以下信息：

| 挂载点 (Mount Point) | 类型 (Type) |
| :--- | :--- |
| `/` | `ext3` |

大小（固定）（Size (Fixed) = 输入从预安装检查清单中获得的“文件系统可用空间”（Space available for Filesystems）的值。该值应大于 7000MB。

完成后点击 OK 按钮。

- 再次点击添加（Add）按钮，并在显示的界面中输入以下信息：

| 类型 (Type) | 大小（固定）（Size (Fixed) |
| :--- | :--- |
| `swap` | 输入从预安装检查清单中获得的“交换分区所需空间”（Space required for swap partition）的值 |

完成后点击 OK 按钮。

- 8. 点击左侧窗格中的网络配置（Network Configuration）。点击添加网络设备（Add Network Device）按钮，确保选中 `eth0` 作为网络设备，并根据你的教室环境手动或通过 DHCP 配置适当的 IP 信息，然后点击 OK。

- 9. 点击左侧窗格中的认证（Authentication）。确保已勾选使用影子密码（Use Shadow Passwords）和使用 MD5（Use MD5）。

- 10. 点击左侧窗格中的防火墙配置（Firewall Configuration）。安全级别，选择“禁用防火墙”（Disable firewall）。
