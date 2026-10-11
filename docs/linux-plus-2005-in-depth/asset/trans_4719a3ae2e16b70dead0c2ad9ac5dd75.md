
并继续启动过程。安装完成后，可以使用 mkbootdisk 命令创建引导盘；要在其中包含 2.6.5-1.358 内核的引导盘，您可以在命令提示符下输入命令 `mkbootdisk 2.6.5-1.358`，并在提示时插入一张空白软盘。然后，可以使用该引导盘启动系统，以便修复引导加载程序。

由于操作系统频繁地向硬盘传输数据，文件系统可能会随时间推移而损坏；损坏的文件系统可以通过非常缓慢的写入请求、打印到控制台的错误或挂载失败来识别。如果挂载到非关键目录（例如 /home 或 /var）的分区的文件系统发生损坏，您应该执行以下故障排除步骤：

-   1.  如果已挂载，请卸载该文件系统。
-   2.  在该文件系统设备上运行带有 -f（完整）选项的 fsck 命令。
-   3.  如果 fsck 命令无法修复文件系统，请使用 mkfs 命令重新创建文件系统。
-   4.  使用备份实用程序恢复该文件系统的原始数据。

![](img/09bf13b782f71165e17bb3839040c96a_517_0.png)

> **注意**
>
> 请勿将数据恢复到已损坏的文件系统；请确保首先已重新创建文件系统。

如果 / 文件系统发生损坏，系统将不稳定，必须关闭。此后，您可以使用安装介质上的 Linux 副本，通过以下故障排除步骤来解决问题：

-   1.  将第一张 Red Hat Fedora 安装光盘放入光盘驱动器并开启计算机。
-   2.  在图 13-5 所示的欢迎屏幕上，输入 linux rescue 并按 Enter。当提示选择语言和键盘布局时，分别选择英语和美国（us）。当提示是否启动网络时，选择 No（否）。
-   3.  在图 13-6 所示的屏幕上，选择“Skip”（跳过）以进入 CD-ROM 上 Linux 系统的 shell，如 图 13-7 所示。该系统在 /usr/bin 和 /usr/sbin 目录中包含可恢复硬盘上文件系统的实用工具。
-   4.  在 CD-ROM 上的 Linux 系统中使用 mkfs 命令在硬盘上的相应分区上创建一个新的 / 文件系统。
-   5.  使用 CD-ROM 上的 Linux 系统中的备份实用程序（tar、dump 或 cpio）将原始数据恢复到重新创建的 / 文件系统。
-   6.  在 shell 提示符处输入 exit 以重启系统。

![](img/09bf13b782f71165e17bb3839040c96a_518_0.png)

图 13-5 Red Hat Fedora Linux 安装欢迎屏幕

![](img/09bf13b782f71165e17bb3839040c96a_518_1.png)

图 13-6 在救援模式下获取 shell

```bash
bash-2.05b# cd /usr/sbin
-bash-2.05b: cd: /usr/sbin: No such file or directory
-bash-2.05b# ls
arp                 c2label             ifconfig          mke2fs            modinfo           restore
badblocks           fdisk             insmod            mkfs.ext2         modprobe          sfdisk
fsck                fsck.ext2         jfs_fsck          mknod             mount           trace
fsck.jfs            load_policy        mkfs.jfs          mdev              tune2fs
fsck.reiserfs       lsvfs             mkfs.vfat         reiserfsck        xfs_check
fsck.xfs            lvm               mkfs.xfs          resize2fs         xfs_db
antiqq              lvs.static        mfs.xfs           restore           xfs_repair
dump                hdmv              mknod             rmmod
dump                lock              mkdosfs           mkswap
route
-bash-2.05b#
```

**图 13-7** *救援模式下使用的命令行 shell*

一些 Linux 管理员更喜欢下载基于 CD 的可启动 Linux 发行版，其中包含比第一张 Red Hat Fedora 安装光盘更多的文件系统修复实用程序。互联网上有很多小型 Linux 发行版是为这种目的设计的；两个例子是 **Knoppix Linux**（http://www.knoppix.org）和 **BBC Linux**（http://www.lnx-bbc.org）。只需下载该 Linux 发行版的 ISO 镜像，并使用刻录软件将镜像刻录到 CD-ROM。之后，您可以使用此基于 CD 的 Linux 发行版启动计算机，并使用其上的实用程序修复文件系统并从备份恢复文件。

在 Linux 系统中遇到的另一个常见问题是不当的串行端口配置。调制解调器设备被系统识别为串行设备；然而，许多调制解调器使用了与连接到计算机主板上的串行端口相同的 IRQ 和 I/O 地址设置，这导致参数冲突。此外，某些串行设备（如串行打印机和终端站）需要以特定速度进行通信，而不是大多数串行端口的默认速度 115 KB/s。为了解决这些问题，您可以使用 `setserial` 命令的关键字参数来设置指定串行设备的 IRQ、I/O 地址和速度。例如，要将第一个串行端口（/dev/ttyS0）的 IRQ 设置为 11，I/O 地址设置为 0x03F8，并查看结果，可以使用以下命令：

```bash
[root@server1 root]# setserial /dev/ttyS0 irq 11 port 0x03F8
[root@server1 root]# setserial /dev/ttyS0
/dev/ttyS0, UART: 16550A, Port: 0x03F8, IRQ: 11
[root@server1 root]#
```

表 13-1 列出了可以与 setserial 命令一起使用的其他关键字。

### **性能监控**

表 13-1 **setserial 实用程序常用的关键字**

| 选项 | 描述 |
| :--- | :--- |
| port n | 将串行设备的 I/O 地址设置为 n |
| irq n | 将串行设备的 IRQ 设置为 n |
| auto_irq | 尝试自动检测串行设备的 IRQ 设置 |
| spd_hi | 将串行端口的速度设置为 56KB/s |
| spd_vhi | 将串行端口的速度设置为 115KB/s |
| spd_normal | 将串行端口的速度设置为 38.4KB/s |

您在 Linux 系统中遇到的一些问题不像前一节中讨论的那些那么明显；这类问题会影响 Linux 系统的整体性能。与之前讨论的问题一样，性能问题可能由软件、硬件或两者结合引起。

配置不当的硬件可能仍然可以工作，但速度较慢。此外，随着硬件老化，它可能会开始发生故障，并在未使用时向 CPU 发送大量信息；这一过程被称为**乱发**（jabbering），会减慢 CPU 的速度，进而减慢整个 Linux 系统的速度。为避免这种硬件故障，大多数公司会在计算机设备使用两三年后将其退役。

软件也会影响系统的整体性能；需要过多系统资源的软件会独占 CPU、内存和外围设备。性能低下也可能是由于计算机上运行了过多的进程、大量向硬盘发出读/写请求的进程（例如数据库），或流氓进程所致。为了解决大多数软件性能问题，您可以从系统中移除软件以释放系统资源；如果此软件对业务活动是必需的，您可以选择将软件迁移到拥有更多空闲系统资源的另一台 Linux 系统上。

软件性能问题有时也可以通过更改硬件来解决。升级或添加另一个 CPU 可使 Linux 系统更快地执行进程，并减少在 CPU 上并发运行的进程数量。或者，某些外围设备可以执行通常由 CPU 执行的大量处理；这被称为**总线主控**（bus mastering）。使用总线主控外围组件减少了 CPU 必须执行的处理量，从而提高了系统速度。

向计算机添加 RAM 也会提高系统速度，因为进程在内存中将拥有更多的工作空间，并且系统在硬盘和内存之间交换的信息会大大减少。由于操作系统、外围组件和所有进程不断使用 RAM，向任何系统添加 RAM 通常会对系统性能产生深远影响。

