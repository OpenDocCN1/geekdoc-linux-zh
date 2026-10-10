

第二个微妙之处在于在挂载命令中使用只读（ro）命令行开关。使用 MTD 块仿真驱动程序从 Flash 挂载 ext2 镜像以供只读使用是完全可以接受的。然而，使用 mtdblock 驱动程序向 ext2 设备写入是不受支持的。这是因为 ext2 不知道 Flash 擦除块的存在。若要访问基于 Flash 的文件系统，我们需要使用具备 Flash 知识的文件系统，例如 JFFS2。

## 10.4.1 JFFS2 根文件系统

创建 JFFS2 根文件系统是一个直接的过程。除了压缩之外，JFFS2 还支持磨损均衡（wear leveling），这是一个旨在通过将写循环均匀分布在设备各块上来延长 Flash 寿命的功能。正如第 9 章所指出的那样，Flash 内存的写循环次数是有限的。在你采用的任何基于 Flash 的文件系统中，磨损均衡都应被视为必备功能。正如本书其他地方所提到的，你应该将 Flash 内存视为一种偶写介质。具体而言，你应该避免允许任何需要频繁写入的过程指向 Flash 文件系统。特别注意诸如 syslog 之类的日志记录程序。

我们可以利用在 Redboot RootFS 分区上使用的 ext2 镜像，在我们的开发工作站上构建 JFFS2 镜像。压缩带来的好处将立竿见影。我们在上一个 RootFS 示例中使用的镜像是一个 ext2 文件系统镜像。以下是以长格式（-l）列出的结果：

```
$ ls -l rootfs.ext2
-rw-r--r--    1 root root  6291456 Nov 19 16:21 rootfs.ext2
```

现在，让我们使用 MTD 软件包中的 mkfs.jffs2 实用工具将此文件系统镜像转换为 JFFS2。列表 10-15 展示了该命令及其结果。

### 列表 10-15：将 RootFS 转换为 JFFS2

```
$ mount -o loop rootfs.ext2 /mnt/flash/
$ mkfs.jffs2 -r /mnt/flash -e 128 -b -o rootfs.jffs2
$ ls -l rootfs.jffs2
-rw-r--r--    1 root root  2401512 Nov 20 10:08 rootfs.jffs2
$
```

首先，我们在开发工作站上的任意挂载点，通过回环设备挂载 ext2 文件系统镜像。接着，我们调用 MTD 实用工具 mkfs.jffs2 来创建 JFFS2 文件系统镜像。-r 标志告诉 mkfs.jffs2 根文件系统镜像的位置。-e 指示 mkfs.jffs2 在假设 128KB 块大小的情况下构建镜像。默认值是 64KB。如果 Flash 设备的块大小与镜像的块大小不同，JFFS2 将无法表现出最高效的行为。最后，我们显示一个长列表，并发现生成的 JFFS2 根文件系统镜像体积减少了 60% 以上。当我们处理有限的 Flash 内存时，这是对宝贵的 Flash 资源使用量的大幅缩减。

请注意在列表 10-15 中传递给 mkfs.jffs2 的一个重要命令行标志。-b 标志是 \-big-endian 标志。这指示 mkfs.jffs2 实用工具创建一个适用于大端目标使用的 JFFS2 Flash 镜像。由于我们要针对 ADI Engineering Coyote 板，该板包含一个以大端模式运行的 Intel IXP425 处理器，因此这一步骤对于正常运行至关重要。如果你没有指定大端模式，当内核尝试解析本质上是一堆乱码的 JFFS2 文件系统超级块时，你会看到几屏内核抱怨信息。²有人能猜到我是如何记住这个重要细节的吗？

与前面的示例类似，我们可以使用 flashcp 实用工具将此镜像复制到我们的 Redboot RootFS Flash 分区。然后我们可以使用 JFFS2 根文件系统启动 Linux 内核。列表 10-16 提供了在目标硬件上运行 MTD 实用工具的详细信息。

### 列表 10-16：将 JFFS2 复制到 RootFS 分区

```
root@coyote:~# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00060000 00002000 "RedBoot"
mtd1: 00160000 00020000 "MyKernel"
mtd2: 00600000 00020000 "RootFS"
mtd3: 00001000 00020000 "RedBoot config"
mtd4: 00002000 00020000 "FIS directory"
root@coyote:~# flash_erase /dev/mtd2
Erase Total 1 Units
Performing Flash Erase of length 131072 at offset 0x0 done
root@coyote:~# flashcp /rootfs.jffs2 /dev/mtd2
root@coyote:~#
```

> ² 内核可以配置为使用错误字节序的 MTD 文件系统运行，代价是性能降低。在某些配置（如多处理器设计）中，这可能是一个有用的特性。

需要注意的是，你必须在内核配置中启用 JFFS2 文件系统。执行 `make ARCH=<arch> gconfig`，并在文件系统、杂项文件系统中选择 JFFS2。另一个有用的提示是在 MTD 实用工具上使用 -v（详细）标志。这会在 Flash 操作期间提供进度更新和其他有用信息。

我们已经了解了如何使用 Redboot exec 命令启动内核。列表 10-17 详细说明了加载并使用我们的新 JFFS2 文件系统作为根来启动 Linux 内核的命令序列。

### 列表 10-17：使用 JFFS2 作为根文件系统启动

```
RedBoot> load -r -v -b 0x01000000 coyote-zImage
Using default protocol (TFTP)
Raw file loaded 0x01000000-0x114decb, assumed entry at 0x01000000
RedBoot> exec -c "console=ttyS0,115200 rootfstype=jffs2 root=/dev/mtdblock2"
Using base address 0x01000000 and length 0x00145ecc
Uncompressing Linux:.... done, booting the kernel.
...
```

## 10.5 本章总结

- 内存技术设备（MTD）子系统在 Linux 内核中提供了对 Flash 内存等内存设备的支持。
- 必须在你 Linux 内核配置中启用 MTD。本章中的几个图详细说明了配置选项。
- 作为 MTD 内核配置的一部分，必须为你的 Flash 芯片选择合适的 Flash 驱动程序。图 10-4 展示了最近的 Linux 内核快照中支持的一组芯片驱动程序。
- 你的 Flash 内存设备可以作为单个大型设备进行管理，也可以划分为多个分区。
- 有几种方法可用于向 Linux 内核传达分区信息。这些包括 Redboot 分区信息、内核命令行参数和映射驱动程序。
- 映射驱动程序与架构特定的板级支持提供的定义一起，向内核定义你的 Flash 配置。
- MTD 附带了一些用户空间实用工具，用于管理 Flash 设备上的镜像。
- 日志型 Flash 文件系统 2（JFFS2）是 MTD 子系统的绝佳伴侣，适用于小型、高效的基于 Flash 的文件系统。在本章中，我们构建了一个 JFFS2 镜像并将其作为根文件系统挂载在我们的目标设备上。

### 10.5.1 延伸阅读建议

- MTD Linux 主页：www.linux-mtd.infradead.org/
- Redboot 用户文档：http://ecos.sourceforge.net/ecos/docs-latest/redboot/redboot-guide.html
- 通用 Flash 内存接口规范：AMD 公司，www.amd.com/us-en/assets/content_type/Downloadable/Assets/cfi_r20.pdf

# 第 11 章

![](img/7a1144833e62564667e7dd9eb4c9f03d_304_0.png)

本章内容

- BusyBox 简介 第 274 页
- BusyBox 配置 第 275 页
- BusyBox 操作 第 278 页
- 本章总结 第 288 页

BusyBox 的手册页声明 BusyBox 是“嵌入式 Linux 的瑞士军刀”。这是一个贴切的描述，因为 BusyBox 是大量标准 Linux 命令行实用工具的小型高效替代品。它通常作为资源有限的嵌入式平台的基础。

本章介绍 BusyBox，并为自定义你自己的 BusyBox 安装提供了良好的起点。

我们之前已在多处提及 BusyBox。在本章中，我们将详细介绍这个有用的软件包。在简要介绍 BusyBox 之后，我们将探索 BusyBox 配置实用工具。这用于根据你的特定需求定制 BusyBox。然后，我们将讨论交叉编译 BusyBox 软件包的要求。

我们将考虑 BusyBox 的操作问题，包括它在嵌入式系统中的使用方式。我们将检查 BusyBox 的初始化序列，并解释这与标准 System V 初始化的不同之处。在本节中，我们还提供一个初始化脚本示例。在看到在目标系统上安装 BusyBox 的步骤后，你将了解一些 BusyBox 命令及其局限性。

## 11.1 BusyBox 简介

BusyBox 在嵌入式 Linux 社区中获得了极大的 popularity。它配置、编译和使用都非常简单，并且有潜力显著减少支持大量常见 Linux 实用工具所需的总体系统资源。BusyBox 为许多传统的全功能实用工具（在大多数桌面和嵌入式 Linux 发行版中都能找到）提供了紧凑的替代品。示例包括文件实用工具，如 ls、cat、cp、dir、head 和 tail；通用实用工具，如 dmesg、kill、halt、fdisk、mount、umount；以及更多其他工具。BusyBox 还支持更复杂的操作，如 ifconfig、netstat、route 和其他网络实用工具。

BusyBox 是模块化的，高度可配置的，可以根据你的特定需求进行定制。该软件包包含一个类似用于配置 Linux 内核的配置实用工具，因此会显得相当熟悉。

BusyBox 中的命令通常比其全功能对应物更简单的实现。在某些情况下，只有常用命令行参数的一小部分

