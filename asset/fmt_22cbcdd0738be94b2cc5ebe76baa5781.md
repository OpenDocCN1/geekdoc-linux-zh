
内核配置：在 Block Devices 下的 Floppy。

注意：该驱动不太可能是模块，它直接编译进内核。

### 以太网接口

模块名称：`pcnet32`。

`modules.conf`：

```
alias eth0 pcnet32
```

内核配置：在 Network device support 下的 Ethernet (100M)。

注意：启用 VLB, PCI 和板载控制器带来了许多其他选项；AMD32 就在其中。

### 串口

模块名称：`serial`。

内核配置：在 Character devices 下的 Standard/generic。

### 并端口

模块名称：`parport_probe`, `parport`, `parport_pc`, `lp`（用于打印机），其他。

`modules.conf`：

```
alias parport_lowlevel parport_pc
```

内核配置：共有三处：(1) General Setup 下的 Parallel port support 和 PC-style hardware，(2) Character devices 下的 Parallel printer support，以及 (3) Block devices 下的 others；在内核 2.4.0 及以上版本中，位置 (1) 是主菜单下的 Parallel port support。

注意：由于模块存在大量的依赖关系，并端口的内核配置比其他的复杂。请记住双向设备（通常是 Zip 驱动器和类似设备）需要双向端口支持。

### 声

模块名称：`soundcore`, `sb`, `uart401`, `soundlow`。

`modules.conf`：

```
alias char-major-14 sb
options sb io=0x220 irq=5 dma1=6 mpu_io=0x330
```

内核配置：在 Sound 下，启用 Sound card support 和 OSS modules。然后选择 Sound Blaster compatibles（SB16/32/64, ESS, Jazz16）支持。

注意：由于各种原因，声卡在 Linux 下一直很难配置。对于虚拟机，这个过程非常直观。

### USB 支持

内核配置：在 USB support 下，启用 UHCI 驱动之一以及任何你喜欢的其他设备。USB 文件系统对于某些 USB 工具程序如 `lsusb` 是必要的。你可能需要启用实验性内核以查看所有的 USB 设备驱动。

注意：USB 支持在 Linux 中还较新，因此实现细节比其他设备更容易发生变化。

### 鼠标支持

内核配置：对于 PS/2 类型的鼠标，在 Character Devices – Mice 下的 PS/2 mouse（即“辅助设备”）支持。串口鼠标连接到串口并使用那种配置。

注意：由于 PS/2 鼠标设备不以模块形式提供，它被编译到每个发行版的默认内核中。

# 第 6 章：Linux 客户操作系统

## 6.8 Linux 系统信息

`/proc` 文件系统是获取当前运行的 Linux 系统信息的有用源。对于普通的 Linux 程序来说，`/proc` 中的项看起来像文件，但 `/proc` 内核会动态生成实际内容。要查看文件系统中的内容（例如 `/proc/meminfo`），只需使用 `cat /proc/meminfo`；如果输出太大，请使用 `less` 代替 `cat`。

- `/proc/meminfo`: 内存信息。输出显示系统可用的实际内存、已用内存以及其中有多少是多个进程共享的，以及缓冲区和缓存的使用统计。
- `/proc/cpuinfo`: 处理器信息。如果 Linux 运行在 VMware 下，不要相信你在这里看到的一切。虽然显示看起来和在真实硬件上一样，但 VMware 会干预用于计算某些条目的算法。其中之一就是 CPU MHz 值。例如，一个 AMD K6–3/400 在 VMware 下运行时通常显示在 45 MHz 左右（这并不意味着 VMware 加速了处理器）。然而，如果你对 bogomips 条目感兴趣，你可以确信它在虚拟机上和在真实机器上一样毫无用处。
- `/proc/devices`, `/proc/misc`: 设备列表以及设备号。请注意这一点；某些设备没有出现是因为它们未被使用，并且即使它们当前已从 VMware 层断开也可能显示（记住 VMware 会保留断开的设备，直到你连接它们）。
- `/proc/mounts`: 已挂载文件系统列表。尽管系统尝试在 `/etc/mtab` 中保留这些信息，但这是系统当前连接的文件系统最可靠的指示。不过，它不显示挂载选项。
- `/proc/filesystems`: 当前内核已知的文件系统类型。此信息可能误误性，因为大多数发行版将无意义的文件系统作为模块包含。当系统需要新的文件系统类型时，自动内核模块加载器会查找同名的模块并对其进行探测。之后，该模块就会出现在 `/proc/filesystems` 中。
- `/proc/partitions`: 当前内核知的磁盘和分区。对于可移动介质，在某些情况下，在更换媒体后有人访问设备之前，内核看不到分区。SCSI 磁盘也可能如此。
- `/proc/version`: 当前运行的内核版本。

## 6.9 启动 Linux：LILO

Linux 发行版在硬盘的引导块上安装一个名为 Linux Loader（或 LILO）的小程序。通常，你希望此引导块位于你的第一块硬盘 `/dev/hda` 上。你通过 `/etc/lilo.conf` 文件指定 LILO 的配置。这是一个典型的示例：

```
boot=/dev/hda
root=/dev/hda
install=/boot/boot.b
map=/boot/map
image=/boot/vmlinuz
label=Linux
read-only
```

你可以看到引导块被设置为 `/dev/hda`，而初始根目录设置为 `/dev/hda1`。另一个重要的条目是 Linux 内核 `/boot/vmlinuz`。这是 LILO 加载并运行的内容。

> 注意：仅拥有一个 `lilo.conf` 文件并不会让 LILO 激活；每当你更改内核镜像时，都必须运行 `LILO` 命令。可能出于某种原因，你的引导盘上可能没有安装 LILO，或者 VMware 可能会因为其 BIOS 而无法启动你的内核。例如，机器可能无法在次要磁盘上启动 Linux 安装。你可以使用软盘或其他手段（例如 `LOADLIN` 程序）来绕过这一点。虽然软盘在 VMware 下可能可行，但 `LOADLIN` 可能不行，而且无论如何，软盘仍然很慢。幸运的是，VMware 给了你两种作弊的方法。

对于此处的示例，假设你已经将 Linux 客户操作系统安装在主从盘 `/dev/hdb` 上，而另一个操作系统安装在主主控盘 `/dev/hda` 上。

### 6.9.1 方法 1：新虚拟磁盘

如果你在作为客户操作系统运行 Linux 时，不需要访问主主控盘上的任何内容，你可以从配置中删除该磁盘，并安装一个较小的虚拟磁盘作为主盘。对其进行分区，在上面建立一个文件系统（如本章前面的“Linux 设备”部分所述），将其格式化为文件系统，并将 `/boot`（或 LILO 文件所在位置）的所有内容复制到新分区中。*确保内核镜像包含在你复制的文件中。*然后对新分区使用 `mount`，并立即使用 `mount` 将其再次挂载到 `/boot` 之下。将你的 `/etc/lilo.conf` 文件复制到 `/etc/lilo.conf.vm`，并确保它包含类似这样的行：

```
boot=/dev/hda
root=/dev/hdb1
```

进行任何其他必要的修改；然后使用

```
lilo -C lilo.conf.vm
```

在新虚拟磁盘上安装引导块以使其可启动。

### 6.9.2 方法 2：伪造软盘

如果你是一个可怜的灵魂，正从软盘启动 Linux 系统（例如，在双启动系统中），或者你由于其他原因正在使用软盘，你可以伪造一个软盘并加快启动速度。方法如下：

- 1. 如果你已经有一个引导盘，将你的真实软驱器连接到 VMware 作为虚拟软驱器，并在 Linux 客户机中使用：

```
dd if=boot.floppy of=/dev/fd0 bs=512
```

- 2. 如果你在使用双启动系统，你可能需要配置软驱器：

```
dd if=boot.floppy of=/dev/hda bs=512
```

- 3. 如果你由于其他原因使用软盘，请使用以下命令：

```
dd if=boot.floppy of=/dev/hdb bs=512
```

- 4. 最后，确保软驱器为 VMware 正正确配置：

```
dd if=boot.floppy of=/dev/sdc bs=512
```

此外，请查找 `perl`；在安装 VMware Tools 程序时会需要它。

## 7.2 在 VMware 下使用现有的 FreeBSD 安装
