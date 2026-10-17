
此示例中的启动脚本除了为了说明目的而公告外，什么都不做。当然，在实际系统中，这些脚本启用了执行有用工作的功能和服务！鉴于示例中的简单配置，你将在 `/etc/init/runlv2.startup` 脚本中启用适用于你特定小部件的服务和应用程序，并在关机和重启脚本中执行应用程序、服务和设备的可逆清理。在下一节中，我们可能会查看一些系统配置以及启动脚本中启用这些配置所需的条目。

## 6.3.2 示例 Web 服务器启动脚本

尽管这个启动脚本很简单，但它的设计是为了说明该机制并引导你设计自己的启动和关机行为。此示例基于 `busybox`，它的初始化行为与 `init` 略有不同。这些差异在第 11 章中有详细介绍。

在一个包含 Web 服务器的典型嵌入式设备中，我们可能需要多个服务器用于维护和远程访问。在这个示例中，我们启用了用于 HTTP 和 Telnet 访问（通过 `inetd`）的服务。列表 6-8 包含我们假设的 Web 服务器设备的简单 `rc.sysinit` 脚本。

### 列表 6-8. Web 服务器 rc.sysinit

```bash
#!/bin/sh

echo "This is rc.sysinit"

busybox mount -t proc /proc

# 加载系统日志记录

syslogd

klogd

# 为 telnetd 启用传统的 PTY 支持

busybox mkdir /dev/pts

busybox mknod /dev/ptmx c 5 2

busybox mount -t devpts devpts /dev/pts
```

在这个简单的初始化脚本中，我们首先启用了 `proc` 文件系统。这个有用子系统的细节在第 9 章介绍。接下来，我们启用了系统日志记录，以便我们在运行期间捕捉系统信息。这在出现问题时特别有用。最后几个条目启用对 `UNIXTTY` 子系统的支持，这是实现此示例中使用的 Telnet 服务器所需要的。

列表 6-9 包含了运行级别 2 启动脚本中的命令。该脚本包含了启用我们希望设备运行的任何服务的命令。

### 列表 6-9. 示例运行级别 2 启动脚本

```bash
#!/bin/sh

echo "This is runlvl2.startup"

echo "Starting Internet Superserver"

inetd

echo "Starting web server"

webs &
```

注意这个运行级别 2 启动脚本实际上有多简单。我们首先启用了所谓的“互联网超级服务器” `inetd`，它拦截并为常见的 TCP/IP 请求派生服务。在我们的示例中，我们通过配置文件 `/etc/inetd.conf` 启用了 Telnet 服务。然后，我们执行 Web 服务器（在这里被称为 `webs`）。就此简单。虽然非常精简，但这是一个 Telnet 和 Web 服务的可用配置。

为了完成此配置，你可能提供一个关机脚本（回看列表 6-6），在这种情况下，它将在系统关机之前终止 Web 服务器和互联网超级服务器。

## 6.4 初始磁盘

Linux 内核包含一种挂载早期文件系统的机制。这种机制被称为初始磁盘（initial disk），图 6-1 显示了配置示例。

### 6.4.1 初始磁盘的用途

初始内存磁盘是一个小型自包含文件系统，通常包含加载驱动程序的指令。在 Red Hat 等 Linux 发行版中，`initrd` 经常用于加载系统。

### 6.4.2 使用 initrd 启动

为了使用 `initrd` 功能，大多数架构都需要引导程序的参与。在这里，将 `initrd` 镜像传递给内核是引导程序的责任。

内核如何知道去寻找 `initrd` 镜像？除非引导程序中有某种魔法，否则通过内核命令行向内核传递 `initrd` 镜像地址和大小通常足够了。这是一个基于 TI OMAP 的流行 ARM 参考板的内核命令行示例：

```
console=tty0,115200 root=/dev/nfs
nfsroot=192.168.1.9:/home/chris/sandbox/omap-target
initrd=0x10800000,0x14af47
```

之前的内核命令行被分成几行以适应提供的空间。在实际操作中，它是一单行，各个元素用空格分隔。此内核命令行定义了以下内核行为：

关于此示例的一个额外说明：几乎普遍，`initrd` 镜像是压缩的。内核命令行中指定的尺寸是压缩镜像的大小。

让我们来看一个基于 ARM 处理器运行的流行的 U-Boot 引导加载程序的简单示例。该引导加载在设计时包含了对 Linux 内核的支持。使用 U-Boot 可以很容易地将 initrd 镜像与内核镜像一同包含。列表 6-10 列出了一个包含初始内存盘镜像的典型启动序列。

### 列表 6-10. 带有 Ramdisk 支持的内核启动

```
# tftpboot 0x10000000 kernel-uImage..
Load address: 0x10000000
Loading: ########### done
Bytes transferred = 106092 (15024 hex)
# tftpboot 0x10800000 initrd-ub
Load address: 0x10800000
Loading: ################# done
Bytes transferred = 28275 (6cf hex)
# boot 0x10000000 0x1080000
Uncompressing kernel....
RAMDISK initialized: 16384K size 1024 block
RAMDISK: Compressed image found at block 0
VFS: Mounted root (ext2 filesystem)
Greetings: this is linuxrc from RAMDISK
Mounting /proc filesystem
BusyBox v1.0.0 (014) Built-in shell
Enter 'help' for a list of built-in commands.
# U-Boot command prompt
```

在列表 6-10 中，我们得以一窥 U-Boot 引导加载程序，我们将在下一章中详细检查它。`tftpboot` 命令导致 U-Boot 从 tftp 服务器下载内核。内核镜像被下载并放置在该目标系统内存的 256MB (`0x10000000`) 处。然后，初始内存盘镜像从 tftp 服务器下载到较高的内存地址（示例中为 256MB+8MB）。最后，我们使用 `boot` 命令，它接受两个参数：Linux 内核的地址，可选跟随一个代表初始内存盘镜像位置的地址。

恰好在这个特定的开发板上，我们的物理 SD 卡从 256MB 开始。请特别注意 U-Boot 引导加载程序的一个特性：它支持通过以太网连接传输内核和内存盘镜像。这是一个非常实用的开发配置。你也可以通过其他方式将内核和内存盘镜像放入开发板。你可以使用基于硬件的编程工具将其刷入内存，或者使用串口通过 RS-232 下载内核和文件系统镜像。然而，由于这些镜像通常很大（内核约为 1MB，内存盘有几十 MB），如果你投资于基于以太网的 tftp 下载，将节省大量的工程时间。无论你选择哪种引导加载程序，请确保它支持镜像的网络下载。

## 6.4.4 initrd: linux

当内核启动时，它会检测到 initrd 镜像的存在，通过其在 RAM 中的物理位置将压缩二进制文件复制到内核内存内存中，并将其挂载为根系统。initrd 的神奇之处在于 initrd 镜像内部的一个特殊文件。当内核进入初始内存盘时，它会寻找一个名为 `linuxrc` 的特殊文件。它将其视为脚本文件并执行其中包含的命令。这种机制允许系统设计师指定 initrd 的行为。列表 6-11 包含了一个示例的 `linuxrc`。

### 列表 6-11. 示例 linuxrc 文件

```bash
#!/bin/sh

echo 'Greetings: this is "linuxrc" from Initial Ramdisk'
echo 'Mounting /proc filesystem'
mount -t proc /proc /proc
busybox
```

在实践中，该文件将包含在挂载真实文件系统之前所需的指令。一个示例可能是加载 CompactFlash 驱动程序以从 CompactFlash 设备获取真实文件系统。为了本示例，我们简单地启动了一个 `busybox` shell 并停止启动过程以供检查。你可以看到列表 6-10 中由于此 `busybox` shell 产生的 `#` 命令提示符。如果在此输入 `exit` 命令，内核将继续其启动过程直到完成。

在内核将内存盘从物理内存复制到内核内存盘后，它会将物理内存返回可用池。你可以认为这是将 initrd 镜像从物理内存传输到内核虚拟内存中的硬编码地址（以内核内存盘的形式）。

关于列表 6-11 的最后一个注释：挂载 /proc 文件系统的 `mount` 命令在单词 `proc` 词的使用上是多余的。该命令同样有效：

```
mount -t proc none /proc
```

注意 `mount` 命令的设备字段已改为 `none`。`mount` 命令忽略设备字段，因为 /proc 文件系统没有与物理设备关联。`-t proc` 就足够指示 `mount` 在 /proc 挂载点上挂载 /proc 文件系统了。我使用第一种调用方式是为了提醒我们，实际上正在将内核伪设备（/proc 文件系统）挂载到 /proc 上。`mount` 忽略了这个参数。请使用你偏好的方法。

## 6.4.5 initrd 管道连接

在 Linux 启动过程中，内核必须定位并挂载根文件系统。在启动过程的后期，内核在一个名为 `prepare_namespace()` 的函数中决定挂载什么以及挂载在哪里。如果内核启用了 initrd 支持（如图 6-1 所示），内核命令行配置如下：内核从物理内存中解压 initrd 镜像，并最终将内容复制到内核内存盘 (`/dev/ram`)。此时，initrd 镜像已加载。

## 6.5 使用 initramfs

`initramfs` 是一个 cpio 存档，而 `initrd` 是一个压缩文件镜像。这种简单的区别贡献了 `initramfs` 的易用性。它集成在 Linux 内核源码中，并在编译内核时自动构建。进行更改比构建和加载新的 `initrd` 镜像容易得多。

## 6.4.6 构建 initrd

构建合适的 `initrd` 镜像是最具挑战性的方面之一。在本节中，我们将检查 `initrd` 的要求。

### 列表 6-12. initrd 内容

```
dir /dev 0755 0 0
dir /bin 0755 0 0
dir /etc 0755 0 0
dir /proc 0755 0 0
dir /root 0755 0 0
```

```
nod /dev/console 0600 0 0 c 5 1
dir /root 0700 0 0 0
```
