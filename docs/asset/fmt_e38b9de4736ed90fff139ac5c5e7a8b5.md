
# Fedora Core 7 与红帽企业 Linux（奥兹本完整参考），第 4 版

麦格劳-希尔电子书可提供特别批量折扣，用作奖品和销售促销，或用于公司培训项目。更多信息，请联系特别销售部的 George Hoare，邮箱：george_hoare@mcgraw-hill.com 或电话：(212) 904-4069。

![](img/ab68ea377332b50bf70ef1316c8175b6_3_0.png)

## 专业版

![](img/ab68ea377332b50bf70ef1316c8175b6_3_1.png)

## 想深入了解？

我们希望您喜欢这本麦格劳-希尔电子书！如果您想了解更多关于本书、其作者或相关书籍和网站的信息，请点击此处。

致我的侄子们：

Dylan、Christopher 和 Justin

## 作者简介

**Richard Petersen** 拥有管理学硕士（MLIS）学位，在加州大学伯克利分校教授 UNIX 和 C/C++ 课程。他是 *Linux: The Complete Reference*（《Linux 完整参考》所有六个版本）、*Red Hat Enterprise and Fedora Linux: The Complete Reference*（《Red Hat 企业版和 Fedora Linux 完整参考》）、*Red Hat Linux, Linux Programming*（《Red Hat Linux 与 Linux 编程》）、*Red Hat Linux Administrator's Reference*（《Red Hat Linux 管理员参考》）、*Linux Programmer's Reference*（《Linux 程序员参考》）、*Introductory C with C++*（《C 与 C++ 入门》）、*Introductory Command Line Unix for Users*（《用户命令行 Unix 入门》）以及许多其他书籍的作者。他是 linux.sys-con.com（*LinuxWorld 杂志*）的贡献者，撰写的文章涉及 IPv6、Fedora 操作系统、Yum、Fedora 软件仓库、全局文件系统（GFS）、udev 设备管理以及硬件抽象层（HAL）。

## 技术编辑简介

**Ibrahim Haddad 博士**目前担任摩托罗拉嵌入式与开源技术总监。在此职位上，他负责定义和开发摩托罗拉软件集团开源计划的需求。在加入摩托罗拉之前，Haddad 博士曾在开源开发实验室（OSDL）管理运营商级 Linux 和移动 Linux 计划，其中包括在通信行业中推广 Linux 和开源软件的开发与采用。他是两本关于 Red Hat Linux 和 Fedora 的书籍的合著者，是 *Linux Journal*、*Linux Planet* 和 *Enterprise Open Source Magazine* 的特约编辑，并作为特邀演讲者和小组成员参加了 Linux World、GlobalComm、渥太华 Linux 研讨会以及由 IEEE、ACM 和 USENIX 举办的学术会议。他毕业于黎巴嫩美国大学计算机科学系，获得学士学位和硕士学位，并毕业于加拿大蒙特利尔康考迪亚大学计算机科学系，获得博士学位。

- `mount` 选项 ... 676
- 启动和磁盘检查 ... 677
- fstab 示例 ... 677
- 分区标签：`e2label` ... 678
- Windows 分区 ... 679
- Linux 内核接口 ... 679
    - `noauto` ... 680

### 手动挂载文件系统：`mount` 和 `umount` ... 680

- `mount` 命令 ... 680
- `umount` 命令 ... 682
- 挂载软盘 ... 682
- 挂载 DVD/CD-ROM ... 683
- 挂载硬盘分区：Linux 和 Windows ... 684

### 创建文件系统：`mksfs`、`mke2fs`、`mkswap`、`parted` 和 `fdisk` ... 684

- `fdisk` ... 686
- `parted` ... 687
- `mksfs` ... 687
- `mkswap` ... 689

### CD-ROM 和 DVD ROM 手动刻录 ... 689

- `mkisofs` ... 689
- `dvdrecord` ... 691
- `dvd+rw` 工具 ... 691

## 31 RAID 和 LVM ... 693

### 逻辑卷管理器 ... 694

- LVM 结构 ... 694
- 安装过程中创建 LVM ... 695
- `system-config-lvm` ... 695
- LVM 工具：使用 LVM 命令 ... 697
- 多硬盘的 LVM 示例 ... 700
- 使用 LVM 替换驱动器 ... 703
- 不同硬盘上分区的 LVM 示例 ... 703

### 配置 RAID 设备 ... 705

- 硬件 RAID 支持：`dmraid` ... 705
- Linux 软件 RAID 级别 ... 706
- RAID 设备和分区：`md` 和 `fd` ... 708
- 从 RAID 设备启动 ... 708
- RAID 管理：`mdadm` ... 708
- 创建和安装 RAID 设备 ... 709
- 对应的硬盘分区 ... 715
- RAID 示例 ... 716

## 32 设备和模块：`udev`、`HAL` 和 `MAKEDEV` ... 719

### 硬件设备安装：Kudu ... 720

### 设备信息：`/sys`、`/proc` 和 `/etc/sysconfig/hwconf` ... 720

- sysfs 文件系统：`/sys` ... 721
- proc 文件系统：`/proc` ... 721

### `udev`：设备文件 ... 722

- `udev` 配置 ... 723
- 设备名称和 `udev` 规则：`/etc/udev/rules.d` ... 724
- 符号链接 ... 726
- 程序字段和 `/lib/udev` ... 728
- 创建 `udev` 规则 ... 728
- SYMLINK 规则 ... 729
- 持久名称：`udevinfo` ... 730
- 权限字段：MODE、GROUP、OWNER ... 731

### 硬件抽象层：HAL ... 732

- HAL 守护进程和 `hal-device-manager` (`hal-gnome`) ... 733
- HAL 配置：`/etc/hal/fdi` 和 `/usr/share/hal/fdi` ... 733
- 设备信息文件：`fdi` ... 733
- 属性 ... 734
- 设备信息文件指令 ... 735
- 手动设备 ... 737
- 设备类型 ... 738

### MAKEDEV ... 738

- `mknode` ... 739

### Mono 和 .NET 支持 ... 740

### 安装和管理终端及调制解调器 ... 740

- 串行端口 ... 741
- `mingetty`、`mgetty` 和 `agetty` ... 741
- `termcap` 和 `inittab` 文件 ... 741
- `tset` ... 742
- 输入设备 ... 742

### 安装声卡、网卡和其他卡片 ... 742

- 声音设备 ... 743
- 视频和电视设备 ... 743
- PCMCIA 设备 ... 744

### 模块 ... 744

- 内核模块工具 ... 745
- 模块文件和目录：`/lib/modules` ... 745
- 使用 `/etc/modprobe.conf` 管理模块 ... 746
- `depmod` 命令 ... 746
- `modprobe` 命令 ... 746
- `insmod` 命令 ... 747
- `rmmod` 命令 ... 748
- `/etc/modprobe.conf` 文件 ... 748

### 从供应商安装新模块：驱动程序包 ... 749

- 内核头文件：`/lib/modules/version/source` ... 750
- 从内核安装新模块 ... 751

## 33 内核管理：虚拟化 ... 753

- 内核版本 ... 753
- 参考文献 ... 754
- 内核调优：内核运行时参数 ... 755
- 安装新的内核版本 ... 755
- CPU 内核包 ... 756
- 安装内核包：`/boot` ... 756
- 修改相同版本内核的预防措施 ... 757

### 引导加载程序 ... 758

- 启动磁盘 ... 758
- 从源代码编译内核 ... 759
- 使用 Fedora Core SRPM 安装内核源代码 ... 759
- 安装内核源代码：内核归档和补丁 ... 760
- 配置内核 ... 760
- 内核配置工具 ... 761
- 重要的内核配置特性 ... 762
- 编译和安装内核 ... 764
