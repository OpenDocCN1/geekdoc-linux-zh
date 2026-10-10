

## GRUB

如在第二阶段中所述，GRUB 是计算机在任何存储设备上执行的第一个程序，用于启动现代 Linux 操作系统。在引导加载程序之前，系统 BIOS 执行系统上的所有操作。引导加载程序的目的是在计算机上执行一系列事件以加载主操作系统。本质上，引导加载程序从系统 BIOS 过程接收控制权，执行一系列事件，然后将控制权移交给操作系统内核。

大多数现代引导加载程序是可动态配置的，并且可以在系统引导期间以及系统引导完成后执行。引导加载程序可以在启动时加载预定义的配置文件，或者通过引导命令提示符支持引导时更改（例如，选择不同的内核、虚拟文件系统）。此外，引导加载程序应用程序可以在控制权移交给操作系统内核后，对引导时配置文件进行修改并在使用前测试这些文件。

GRUB 支持这两种使用形式。本节以这两种形式介绍 GRUB。第一种形式是使用 GRUB 启动 Linux 操作系统。第二种形式是在系统控制权移交给操作系统内核后，使用 GRUB 进行测试和修改。

### 安装 GRUB 和引导 Linux

在 GRUB 执行之前，系统 BIOS 将 MBR 加载到内存中并执行其内容。MBR 的总大小为 512 字节。大多数 MBR 包含引导加载程序程序和磁盘分区信息。在 Linux 环境中，GRUB 程序的预安装形式分为两个阶段。MBR 加载 GRUB 第一阶段。GRUB 第一阶段程序利用前 446 字节。剩余的 64 字节分配给分区表，用于划分硬盘驱动器（例如，主分区）。GRUB 第一阶段的目的是找到并加载 GRUB 第二阶段，后者在物理上可能位于硬盘的其他位置。为了访问 GRUB 第二阶段程序，GRUB 第一阶段必须足够灵活，能够访问许多不同的文件系统类型（例如，ext2、ext3、ReiserFS 和 FAT）。这也包括用于 CD 或 DVD 的 ISO 9660 文件系统。这是因为 GRUB 第一阶段加载了大量 mass storage 设备驱动程序。一旦加载完成，GRUB 第二阶段可以执行以下三种不同功能：

- 它可以加载预定义的 Linux 内核（例如，vmlinuz-version.gz）。
- 如果计算机配置为启动多个操作系统（例如，Windows、Linux），它允许你选择要启动哪个操作系统。
- 它可以提示你输入不同的引导参数。

一旦 GRUB 第二阶段加载了 Linux 内核（例如，vmlinuz-version.gz），它还必须加载一个虚拟文件系统并执行 Linux 内核。

> **注意**
>
> 某些 Linux 发行版将使用 GRUB 第一阶段直接加载 GRUB 第二阶段，或者加载一个 GRUB 1.5 阶段应用程序。如果 GRUB 1.5 阶段应用程序被实施到引导过程架构中，它通常位于紧跟 MBR 之后的硬盘前 30 KB 处。一旦 GRUB 1.5 阶段被加载，它将加载 GRUB 第二阶段。

### GRUB 配置文件和命令

GRUB 是一个可动态配置的引导加载程序应用程序。这允许你在安装后对系统进行更改，以确保如果需要设备更改或 Linux 内核修改，能成功启动过程。要对系统进行更改，GRUB 应用程序允许你对三个重要的配置文件进行更改。

第一个文件，/etc/grub.conf，包含有关用于查找并加载 GRUB 第二阶段的磁盘分区的信息，如图 4.3 所示。此文件指示 GRUB 第一阶段在哪里查找 GRUB 第二阶段图像（/boot/grub/stage2）以进行加载。

在图 4.3 中，GRUB 第一阶段将自动将位于第一块硬盘第二个分区上的 GRUB 第二阶段图像安装到相同分区和相同驱动器上。此外，配置文件指示 GRUB 第一阶段通过强制继续 GRUB 第二阶段安装过程来忽略任何有缺陷的逻辑块寻址问题。GRUB 配置文件的位置可能因不同的 Linux 系统而异。

第二个文件，/boot/grub/menu.lst，充当 GRUB 引导菜单。它包含关于可启动的分区和操作系统、不同内核的加载、设置不同的默认内核以及各种其他引导选项修改的内容，如图 4.4 所示。本章稍后介绍的“故障排除引导问题”部分提供了 GRUB 提示过程，用于输入可以发出以动态修改 Linux 内核加载和运行级别过程的命令。

表 4.2 介绍了用于修改和/或选择不同内核以及各种其他引导加载功能的 /boot/grub/menu.lst 文件选项。

最后一个配置文件，/boot/grub/device.map，是一个唯一的文件，它将 Linux 设备名称映射到 GRUB/BIOS 设备命名约定。图 4.5 展示了集成驱动器电子（IDE）设备的 device.map 文件命名约定。

```bash
[linux-01vc:/etc # cat grub.conf]
    setup --stage2=/boot/grub/stage2 --force-lba  (hd0,1)  (hd0,1)
    quit
[linux-01vc:/etc # _]
```

![](img/95b3ebd6248b36778ccf73988aaab2f2_109_0.png)

**表 4.2** /boot/grub/menu.lst 选项

| /boot/grub/menu.lst 选项 | 目的 |
| :--- | :--- |
| Default | 此选项用于指示系统默认使用指定的标题项进行引导。示例包括以下项：<br>• default 0 – 用于第一个菜单<br>• default 1 – 用于第二个菜单<br>• default 2 – 用于第三个菜单 |
| Timeout | 此选项指示系统立即引导默认选择或等待规定的时间量。示例包括以下项：<br>• timeout 5 – 意味着在自动引导系统前等待 5 秒<br>• timeout 10 – 意味着在自动引导系统前等待 10 秒<br>• timeout 0 – 意味着立即引导默认选择 |
| Title | 此选项指示引导菜单标题显示的设置。示例包括以下项：<br>• title Linux<br>• title Failsafe<br>• title GNOME User Interface |

| /boot/grub/menu.lst 选项 | 目的 |
| :--- | :--- |
| Root | 此选项提供指示内核和 initrd 文件位置的设备或分区名称。示例包括以下项：<br>• root (hd0,0) - 代表第一块硬盘和第一个分区<br>• root (hd0,1) - 代表第一块硬盘和第二个分区 |
| Kernel | 此选项显示 Linux 内核（例如，vmlinuz）的位置和名称。这是用于选择不同内核来引导系统的选项。它还通过在该行末尾放置运行级别数字来指定默认运行级别。示例包括以下项：<br>• kernel /vmlinuz-version<br>• kernel /boot/vmlinuz-version |
| Initrd | 此选项提供虚拟文件系统的名称和位置。这是用于选择不同虚拟文件系统的选项。示例包括以下项：<br>• initrd /boot/initrd<br>• initrd /initrd |
| root = /disk partition | 此选项指示系统在哪里挂载 Linux 根 (/) 目录。如果为根 (/) 目录使用了不同的设备和/或分区，则使用此选项。示例包括以下项：<br>• root = /dev/sda2<br>• root = /dev/sdb1 |
| showopts | 此选项用于在引导屏幕上显示列在此选项后的参数。示例：<br>• showopts acpi=off ide=nodma |

```
linux-@/vc/boot/grub # cat device.map
(fdb) /dev/hdb
(hdb) /dev/sda
linux-@/vc/boot/grub #
```

![](img/95b3ebd6248b36778ccf73988aaab2f2_111_0.png)

