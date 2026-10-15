
# 配置文件构建选项

| `config` | 根据输入的回答构建新文件。如果需要动态加载模块，请回答 `M`；如果希望模块是静态的，请回答 `Y`；如果不希望在内核中包含特定模块，请回答 `N`。默认选项以大写字母显示。按回车接受默认值。 |

| `menuconfig` | 使用基于文本的菜单驱动型界面构建/修改文件。 |

| `gconfig` | 使用图形界面构建/修改文件。需要 GNOME 库文件。 |

| `xconfig` | 使用图形界面构建/修改文件。需要 KDE 库文件。 |

表 16-3 配置文件构建选项

以下是这四个界面的外观：

## `make config` 界面

```
scripts/kconfig/config arch/i386/Kconfig
*
* Linux 内核配置
*
* 代码成熟度选项
*
* 提示开发和/或不完整的代码/驱动（实验）[Y/n/?] y
*
* 通用设置
*
本地版本 - 追加到内核发布版本 (LOCALVERSION) []
*
......
```

## `make menuconfig` 界面

# Linux 内核 v2.6.18-prep 配置

使用方向键导航菜单。<enter> 选择上一个，<exclude> 选中的字母会有轮廓显示。按 <tab> 包含，按 <shift-tab> 排除功能。通过空格键移动到下一个，用 / 搜索。<label> [w] 已启用 <module> 模块

```
代码模块级选项 -----
--ale 模块支持
修复调试
锁存层
类型和功能
管理选项 (ACPL, ACFS,
显卡选项 (PCI, PCMCIA, ISA, MICA, ISA)
可执行文件格式
y 编号
```

![](img/3f35ec29a294974bc1a4fdae3ae46652_381_0.png)

图 16-2 基于文本的菜单驱动型界面

## `make xconfig` 界面

# Linux 内核 v2.6.18-prep 配置

+   选项：

代码模块级选项

通用设置

可加载模块支持

进程调试

块层

处理器类型和功能

电源管理选项 (ACPL, APM)

总线选项 (PCI, PCMCIA, ISA, MICA, ISA)

可执行文件格式

网络

设备驱动程序

文件系统

抱歉，此选项尚无可用帮助。

![](img/3f35ec29a294974bc1a4fdae3ae46652_381_1.png)

图 16-3 使用 GNOME 库的图形界面

## `make xconfig` 界面

+   选项：

代码模块级选项

通用设置

CI 软件标准内核

可加载模块支持

进程调试

块层

处理器类型和功能

电源管理选项 (ACPL, APM)

ACPL（高级配置电源）

APM（高级电源管理）

此选项 (PCI, PCMCIA, ISA)

PCI 热插支持

可执行文件格式

网络

设备驱动程序

通用驱动程序选项

连接器 - 统一选项

![](img/3f35ec29a294974bc1a4fdae3ae46652_381_2.png)

图 16-4 使用 KDE 库的图形界面

红帽认证技术员与工程师

# 表 16-4 涉及 `.config` 文件中的常用选项

| 选项 | 描述 |
| --- | --- |
| 块层 | 启用对多样化块设备的支持。 |
| 总线选项 | 包括对 PCI、PCMCIA、EISA、MCA 和 ISA 总线适配器的支持。“PCCARD 支持”和“PCI 热插支持”相关。 |
| 代码成熟度级别 | 允许你向内核添加开发代码或驱动程序。 |
| 加密 | 包括对各种类型加密的支持。 |
| 设备驱动程序 | 提供了许多选项来定义不同的设备驱动程序配置。这些选项包括对并行端口、即插用、IDE、ATA/ATAPI、SCSI、PCMCIA、RAID、LVM、无线、网卡、IDS、RAM/Flash 芯片、输入设备（键盘、鼠标、触摸屏）、NAND、IEEE 1394 (FireWire)、视频卡、串口、多媒体设备、USB 设备（优盘、打印机、输入设备、摄像头、扫描仪）、声卡设备、MMC/SD、InfinBand 和系统时钟。 |
| 文件系统 | 支持多种文件系统类型，如 ext2、ext3、DOS/FAT/NTFS、伪文件系统和网络文件系统。 |
| 固件驱动程序 | 包括硬件设备的固件驱动程序。 |
| 通用设置 | 基础硬件如电源管理和网络，以及内核配置选项。 |
| 库例 | 包括对各种压缩工具的支持。 |
| 可加载模块支持 | 允许内核在检测到与其相关的硬件时自动加载模块。 |
| 网络 | 包括对各种网络协议的支持。 |
| 分区类型 | 允许不同的分区方案。 |
| 电源管理 (ACPI, APM) | 支持电源管理功能。 |
| 进程调试 | 提供进程调试工具。 |
| 处理器类型和功能 | 配置处理器能力。 |
| 安全 | 包括安全相关的内核功能。 |

表 16-4 配置文件构建选项（继续/总结）

## 表 16-4 内核配置选项

现在你已经有了配置文件，按照以下步骤构建新内核：

1. 进入 `.config` 文件所在的目录：

```
cd /usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.i386
```

2. 编辑 `Makefile` 并设置 `EXTRAVERSION` 的值以给内核唯一命名：

```make
EXTRAVERSION = -New-Kernel
```

3. 执行 `make` 命令清理树：

```bash
make clean
```

4. 执行 `make` 命令在 `/` 目录准备内核：

```bash
make prepare
```

5. 执行 `make` 命令将模块安装到相应目录：

```bash
make modules_install
```

6. 执行 `make` 命令将内核复制到 `/boot`：

```bash
make install
```

7. 验证 `grub.conf` 文件中的新启动字符串：

```bash
cat /boot/grub.conf
```

如你所见，文件现在包含两个启动字符串。第一个是新内核，第二个是原始启动项且仍然是默认（`default=1`）。如果你想让新内核成为默认，请将变量值改为 `0`。

8. 创建初始内存磁盘。所有配置的模块在启动时均可用：

```bash
mkinitrd /boot/initrd-2.6.18-New-Kernel.img 2.6.18-New-Kernel
```

9. 重启系统并选择新内核进行测试。

这就完成了配置、构建和测试新内核的过程。

## 创建启动光盘

你可以创建一个启动光盘以便在需要时启动系统。涉及两个步骤。第一步使用 `mkbootdisk` 命令为所需的内核创建一个 ISO 镜像，第二步使用 `cdrecord` 命令将镜像刻录到光盘上。按照下面的程序在光盘上创建启动镜像：

- 1. 在 `/var/tmp` 目录下创建一个名为 `test.iso` 的 ISO 镜像，用于内核文件、`grub` 配置和 `mkbootdisk` 命令。该 ISO 镜像将包含内核文件、`grub` 配置和其他支持的文件。

```bash
# mkbootdisk --verbose --iso /var/tmp/test.iso 2.6.18-92.el5
Installing isolinux... done
Copying /boot/vmlinuz-2.6.18-92.el5... done.
Copying /boot/initrd-2.6.18-92.el5.img... done.
Configuring bootloader... done.
```

- 2. 在驱动器中插入一张空 CD，并使用 `cdrecord` 命令将镜像刻录到其中。以下假设 CD 设备为 `0,0,0`。

```bash
# cdrecord dev=0,0,0 -v /var/tmp/test.iso
```

- 3. 将 CD 挂载到 `/mnt/cdrom` 并列出其内容：

```bash
# mount /mnt/cdrom
# ls /mnt/cdrom/isolinux
boot.cat boot.msg initrd-2.6.18-92.el5.img isolinux.bin isolinux.cfg TRANS.TBL vmlinuz-2.6.18-92.el5
```

- 4. 检查 `isolinux.cfg` 文件的内容：

```bash
# cat /mnt/cdrom/isolinux/isolinux.cfg
default linux
prompt 1
display boot.msg
timeout 100
label linux
kernel vmlinuz
append initrd=initrd.img root=/dev/hda2
```

在驱动器中插入 CD 的情况下重启系统；系统将从 CD 中的内核启动。

# 总结

本章讨论了内核、内核管理以及如何从源码构建内核。你了解了 Linux 内核的概览。你学习了单体内核和模块化内核及其区别。你查看了如何检查和理解内核版本。
