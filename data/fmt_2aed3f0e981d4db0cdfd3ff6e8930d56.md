
# 启动 Tri-M MZ104 和带有 Flash IDE 驱动器的 COTS PC

x86 CPU 驱动最后两个目标设备：Tri-M MZ104 和 COTS PC。这些目标设备从 IDE 驱动器启动并使用 IDE 驱动器。本节介绍了选用的 Flash IDE 技术，并展示了如何编译内核、创建目标根文件系统以及准备用于启动的 Flash 驱动器。

## Flash IDE 技术

Flash 技术已经成熟，为嵌入式设计提供了“无移动部件”的解决方案。Flash ATA IDE 驱动器的容量从 8MB 到 384MB 不等，单价从 25 美元起（截至 2001 年秋）。最小的 8MB 尺寸为 Trailblazer 项目的根文件系统提供了足够的容量。选择了以下组件进行评估：

- SanDisk 8MB Compact Flash 卡片 ($24.99, [www.sandisk.com](http://www.sandisk.com))
- SST85SD/LD32 32MB ATA-Disk芯片 ($50.00, [www.sst.com/ata_disk/atabrief.pdf](http://www.sst.com/ata_disk/atabrief.pdf))
- PCEngines IDE 转 Compact Flash 适配器 ($20.00, [www.pcengines.com/cflash.htm](http://www.pcengines.com/cflash.htm))
- VersaLogic VL-CFA-1 CompactFlash 适配器 ($70.00, [www.versalogic.com](http://www.versalogic.com))

> 提示
> 将 Compact Flash 内存卡连接到 IDE 控制器需要适配器。Compact Flash IDE 从你的设计中消除了移动部件。

此处显示的价格反映了2001年秋季建议零售价。SanDisk Compact Flash 卡和 SST ATA-Disk 芯片声称 100% IDE 兼容性。这意味着 Trailblazer 项目的工程师应该像普通硬盘一样对待它（也就是说，可以使用 `fdisk`、`format`、`copy` 等）。工程师们还发现，热插 IDE 驱动器（如 StarTech SNT127A，[www.startech.com](http://www.startech.com)）方便在开发过程中更换 IDE 驱动器。

## 准备 Tri-M MZ104 和 COTS PC

使用分发行版 CD（如 Debian 或 Red Hat）在商用现成 PC 上安装 Linux 很容易。只需放入 CD，启动并安装即可。正如你在本章前面的部分看到的，最小的 Debian 安装需要 67MB，Red Hat 需要 382MB，这两者都超过了 Trailblazer 项目 Flash IDE 驱动器的容量。

### 分区和格式化 Flash IDE 驱动器

Tri-M MZ104 或 POTS PC 将从 Flash IDE 驱动器启动并挂载其根文件系统。以下是使用 `tbdev1` 分区和格式化 Flash IDE 驱动器的步骤：

1. 使用 IDE 转 Compact Flash 适配器将 Compact IDE 驱动器连接到 `tbdev1` 的辅助控制器。将其跳线设置为主设备（master）。注意，分区 Compact Flash IDE 驱动器将破坏其中的所有数据。
2. 启动 `tbdev1` 并以 root 身份登录。
3. 使用 `dmesg` 命令获取 Compact Flash 驱动器的报告：

> 提示
> 如果你的 PC PC 不识别 Compact Flash IDE 驱动器，你可能需要升级 PC BIOS。

```
root@tbdev1[506]: dmesg

Linux version 2.2.19pre17-idepci (root@oink) (gcc version 2.7.2.3) #1

BIOS-provided physical RAM map:

..

ide0: BM-DMA at 0xf000-0xf007, BIOS settings: hda:pio, hdb:pio

ide1: BM-DMA at 0xf000-0xf00f, BIOS settings: hdc:pio, hdd:pio

hda: Maxtor 85120 A8 -, ATA DISK drive

hdb: probing with STATUS(0x00) instead of ALTSTATUS(0x50)

hdb: probing with STATUS(0x00) instead of ALTSTATUS(0x50)

hdc: SunDisk SDCFB-40, ATA DISK drive

ide0: at 0x1f0-0x1f7,0x3f6 on irq 14

ide1: at 0x170-0x177,0x376 on irq 15

hda: Maxtor 8520 A8 -, 4884MB w/256KB Cache, CHS=622/255/63

hdc: SunDisk SDCFCB-40, 38MB w/1KB Cache, CHS=612/4/32
```

`dmesg` 输出显示 SunDisk SDCFCB-40 位于 `hdc`，这是一个 40MB 的 Flash 磁盘。

4. 在 `/hdc` 上使用 `cdfdisk` 命令对驱动器进行分区：

> 提示
> 如果你的 PC 不识别 Compact Flash IDE 驱动器，你可能需要升级 PC BIOS。

```
root@tbdev1[507]: cdfdisk /dev/hdc
```

5. `cdfdisk` 屏幕显示了分区列表和底部的菜单。使用上下键选择分区列表。使用左右键选择菜单。选择 Free Space 回车。
6. 选择剩余空间。
7. 在 `cdfdisk` 菜单中选择 New（新建）分区，然后选择 Primary（主分区）。
8. 分区列表中选择 `hdc1`，然后选择 Type（类型）菜单将其设置为 83（Linux）。
9. 选择 `hdc1` 并选择 Bootable（可启动）菜单。
10. 选择 Write（写入）并写入操作。
11. 退出 `cdfdisk`，选择 Quit（退出）。
12. 使用 `mke2fs` 命令格式化 `hdc`：

13. 挂载驱动器到 `/mnt` 并检查文件系统使用：

```
root@tbdev1[513]: mount /dev/hdc1 /mnt
```

14. 卸载 `/dev/hdc`：

```
root@tbdev1[514]: umount /dev/hdc
```

Flash IDE 驱动器现在准备就绪，可以用于内核和根文件系统。

15. 使用命令检查磁盘使用：

```
root@tbdev1[515]: df

Filesystem     1-blocks  Used Available Mounted on

/dev/hdc1        39320       0    39320 0% /mnt
```

Flash IDE 驱动器现在已准备启动 Tri-M MZ104 和 COTS PC。

# 第 4 章 启动 Linux

在这些安装过程中，到底发生了什么？发行版安装程序会对目标驱动器进行分区，并在必要时格式化驱动器、创建目录、从归档文件中提取文件到这些目录中、配置各种系统和子系统、准备驱动器使其可启动，然后重启。这很简单，不是吗？

准备根文件系统是发行版厂商面临的最大挑战。他们必须从成千上万的现有程序中进行选择。Trailblazer 工程师在本章早期设计了他们的目标 Linux 机器的需求。他们还知道启动根文件系统需要哪些配置文件。因此，现在他们必须分区并格式化 Flash IDE 驱动器，编译 x86 内核，在 IDE 驱动器上构建目标根文件系统并启动板卡。

## 准备根文件系统

根文件系统现在可以放在 Flash IDE 驱动器上。驱动器已经过分区、格式化和检查，内核也已经编译。

## 编译 i86 内核

在启动 Tri-M MZ104 和 COTS PC 之前，你需要编译内核。本节介绍了如何编译 2.4 内核。

1. 从 `kernel.org` 下载内核源码到 `/usr/src` 目录。此示例使用 2.4.10：

```
root@tbdev1[503]: cd /usr/src
root@tbdev1[504]: wget [...]]-2.4.10.tar.gz
```

2. 解压下载的压缩文件：

```
root@tbdev1[505]: tar zxf linux-2.4.10.tar.gz
```

3. 你现在位于 `linux` 目录。使用以下命令配置内核：

```
root@tbdev1[506]: make mr
root@tbdev1[507]: make menuconfig
```

> 注意
> 有更多关于编译内核的信息，请参阅“内核编译”。

4. 浏览菜单并排除（使用 [ ]）任何你不需要的内容，如 SCSI 支持、声音、即插用或 USB。排除的项越多，内核越小。目前内置（标记为 [*]）的项目包括：
   * 处理器类型和功能（选择你的处理器族，MZ104 使用 486 处理器）
   * 网络设备支持
     * 选择以太网（10Mbps 或 100Mbps）
     * 选择其他 ISA 卡
     * 选择 NE2000/NE1000 支持，MZ104 有 NE2000 ISA 卡
     * 记住选择内置 [*]，而不是模块 [M]

5. 退出 `make menuconfig` 并保存新的内核配置。

6. 编译依赖项并生成内核：

```
root@tbdev1[509]: make dep
```

```
root@tbdev1[510]: make bImage
```

这应该在 `arch/i386/boot` 目录下创建一个名为 `bImage` 的压缩内核。`buildrootfilesystem` 脚本需要此文件。

## 在 Flash IDE 驱动器上构建目标文件系统

现在可以把根文件系统放在 Flash IDE 驱动器上了。驱动器已经过分区、格式化和检查，内核也已经编译。MontVista 的 Journeyman FTP 站点提供了根文件系统所需的 RPM。`buildrootfilesystem` 脚本适用于 x86 平台。该脚本执行以下操作：

1. 下载 RPM 并将其内容提取到临时目录。
2. 拷贝根文件系统程序并在 `/tftpboot/i386-rootfs` 中创建各种系统配置文件。
3. 将 Linux 加载程序 `LILO` 安装到闪存驱动器的主引导记录中，`/dev/hdc`。
4. 将根文件系统拷贝到驱动器并检查文件系统的完整性。请参见本章前面的“第 9 步：为板卡准备根文件系统”。
5. 运行 `buildrootfilesystem` 创建并准备 Flash IDE 驱动器用于 Linux 启动和运行。

6. 你可以通过挂载它并检查文件内容来检查 flash IDE 驱动：

```
root@tbdev1[513]: mount /dev/hdc1 /mnt
root@tbdev1[514]: cd /mnt
root@tbdev1[515]: ls

bin/ dev/ etc/ lib/ lost+found/ proc/ sbin/ tmp/ usr/
root@tbdev1[516]: ls -l boot/bzImage
-rw-r--r-- 1 root 876986 Aug 25 00:53 boot/bzImage
root@tbdev1[517]: umount /dev/hdc1
```

7. 使用 `init 6` 命令关闭 `tbdev1`，断电，并从辅助 IDE 控制器上移除 flash IDE 驱动。

## 启动 Tri-M MZ104 目标板

Flash IDE 驱动包含用于 x86 目标板的内核和根文件系统。将 Flash IDE 驱动连接到 x86 目标板的主 IDE 控制器并上电。目标 BIOS 应该找到 flash IDE 驱动。`LILO` 通过显示启动提示符启动，然后加载内核。内核挂载根文件系统。以下是 MZ104 上电到启动序列的控制台输出：

```
LILO boot:

Loading linux...
```
