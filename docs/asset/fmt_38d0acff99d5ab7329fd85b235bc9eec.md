
```
mk2fs /devfd0
mount /devfd0 /mnt
mkdir /mnt/etc /mnt/boot /mnt/dev
cp -a /dev/fd0 /dev/sda1 /mnt/dev
cp [kernel-image] /mnt/vmlinuz
cp /boot.b /mnt/boot.b
gzip < [initrd-image] > /mnt/initrd
```

创建内容如下的 `/mnt/lilo.conf`：

```
boot=/dev/fd0
compact
image=vmlinuz
label=linux
initrd=/initrd
read-only
root=/dev/sda
```

最后，调用 `lilo`：

```
lilo -r /mnt
```

当使用 `-r` 调用 `lilo` 时，它相对于指定的备用根目录执行所有操作。在 `/mnt/dev` 下创建设备文件的原因是 lilo 在此备用根模式运行时将无法使用 `/dev` 中的文件。

### 5.4.3 在非 Linux 驱动器上安装 initrd 镜像

使用 initrd 功能的一个后果是适用于内部硬盘专门用于另一个操作系统的系统。Linux 内核和 initrd 镜像可以放在非 Linux 分区中，并设置 lilo 或 LOADLIN 从这些镜像中启动 Linux。

假设你已经为适当的根设备配置了内核，并在另一个系统上创建了 initrd 镜像，最简单的方法是使用 `LOADLIN` 启动 Linux，如下：

```
LOADLIN <kernel> initrd-<image>
```

一旦在目标机器上启动 Linux，你可以安装 lilo 以允许直接启动 Linux。例如，`/dev/hd1` 是非 Linux 目标分区，而 `/mnt` 可以作为挂载点。在 Linux 文件上为目标创建一个子目录：

```
mount /dev/hd1 /mnt
mkdir /mnt/linux
cp [kernel-image] /mnt/linux/vmlinuz
cp [initrd-image] /mnt/linux/initrd
```

在此示例中，`/dev/sda1` 是所需的 Linux 根分区，通过 PCMCIA SCSI 适配器挂载的 SCSI 硬盘。要安装 lilo，创建一个内容如下的 `lilo.conf` 文件：

```
boot=/dev/hda
map=/mnt/linux/map
compact
image=/mnt/linux/vmlinuz
label=linux
root=/dev/sda1
initrd=/mnt/linux/initrd
read-only

other=/dev/hda1

table=/dev/hda
```

`other=` 行表示安装配置，并可能...

（注：此处原文存在大量重复，已过滤）

# 6. 处理不支持的卡

# 调试技巧与编程信息

编辑 `pcnet_cs` 后，编译并安装新模块。再次编辑 `/etc/pcmcia/config`，将卡绑定从 `memory_cs` 更改为 `pcnet_cs`。按照指令重新加载配置文件，然后就大功告成了。请向我发送你的 `hw_info` 和 `config` 条目的的副本。

如果你在十六进制转储（hex dump）中找不到显卡的地址，作为最后的手段，可以在 `pcnet_cs` 模块初始化时“硬接线”地址。编辑 `/etc/pcmcia/config.opts` 并添加一个 `hw_add=` 选项，如下所示：

```
module "pcnet_cs" opts "hw_add=0x00,0x80,0x8c,0x01,0x02,0x03"
```

当然，请在适当的位置将其替换为你显卡的硬件地址。请注意，如果你已经到了这一步，那么你的卡极可能不是真正兼容 NE200。事实上，我不确定是否还有哪些卡是无法前两种方法处理的。

### 6.3 PCMCIA 接口卡

Compaq Aero 以及其他笔记本电脑使用的 PCMCIA 软驱接口尚未被此软件包支持。支持 Aero 软驱的障碍在于，Aero 似乎使用了自定义的 PCMCIA 控制器来支持到软驱的 DMA。在不知道具体实现方式的情况下，无法在 Linux 下实现相关支持。

如果 Aero 启动时存在软驱卡，Aero BIOS 将配置该卡，Linux 将其识别为普通软驱。当加载 Linux PCMCIA 驱动程序时，它们会注意到该卡已经配置并附加到了 Linux 驱动程序，因此该插槽将被忽略。所以，如果驱动器在启动时存在，则可以使用它，但该卡不支持热插拔。

# 调试技巧与编程信息

## 7.1 提交有效的问题报告

提交报告的最佳方法是使用在线 pcmia-forums 或 SourceForge 上的错误跟踪器（bug tracker）。这样，其他人就可以看到当前的问题（如果有修复方案或变通方法）。所有错误报告都应该包含以下内容：

- 你的系统品牌和型号。

- 你使用的所有 PCMCIA 卡。

- 你的 Linux 内核版本（例如 `uname -rv`）以及 PCMCIA 驱动版本（例如 `cardctl -V`）。

- `lspci -v` 的输出。

- 你对 `/etc/pcmcia/config` 或 PCMCIA 启动脚本所做的任何更改。

- 你的系统日志文件中与 PCMCIA 相关的消息。

# 7. 调试技巧与编程信息

所有的 PCMCIA 模块都会将状态发送到系统日志。这些通常位于 `/var/log/messages` 或 `/var/log/syslog`。当你遇到问题时，这些文件应该是首选查找位置。在提交错误报告之前，请确保你使用的是最新的驱动程序版本。如果找不到你的系统消息，请检查 `/etc/syslog.conf`。阅读错误报告是非常有益的，如果你无法访问网络，可以将错误报告发送给我 `dahinds@sourceforge.net`。然而，我更倾向于让错误报告发布在 pcmia-cs 上以便他人看到。

## 7.2 解释错误报告

如果错误涉及内核故障（kernel fault），只有当将故障地址转换为有意义的符号时，寄存器转储（register dump）才有用。最近版本的 `klog` 可以翻译故障地址，但如果故障发生在模块中，或者问题严重到 `klog` 无法完成向系统日志的写入，这种方法可能无效。如果故障发生在内核中，可以在 `System.map` 中查找故障地址。这位于 `/System.map` 或 `/boot/System.map`。如果故障发生在模块中，`nm` 命令提供了相同的信息，故障地址已根据模块加载地址进行了调整。假设你有内核：

```
Unable to handle NULL pointer dereference
current->tss.cr3 = 014c9000, cr3 = 014c9000
pde = 00000000
ops: 0
CPU: 0
EIP: [0026081]
EFLAGS: 0010282
```

故障地址是 `0xc26081`。查看 `System.map` 我们可以看到这在内核末尾，即内核模块中。要确定是哪个模块，检查 `nm -m | sort` 的输出：

| Address | Symbol | Defined by |
| :--- | :--- | :--- |
| c200d00 (35k) | | [pcmia_core] |
| c200d10 | register_ss_entry | [pcmia_core] |
| c200d230 | register_ss_entry | [pcmia_core] |
| c202600 (9k) | | [3c574_cs] |
| c202a00 (4k) | | [serial_cs] |

所以，`0xc26081` 在 `3c574_cs` 模块中，它是模块开始处的偏移 `0x0081`。我们无法在 `ksym` 中查找此偏移：当内核加载模块时，它会在模块加载地址插入一个头部。头部的大小随内核版本变化：要找到你内核的大小，检查导出符号的模块（如 `pcmia_core`），并与 `nm` 输出进行比较。在本示例中，`register_ss_entry` 加载在 `0xc200d1c - 0xc200d00 = 0x01c` 偏移处，而 `nm pcmia_core.o` 显示偏移为 `0x00c`，因此头部大小为 `0x01c - 0x00c = 0xb4`。回到 `3c574_cs`，我们的故障偏移是 `0x0081`，头部 `0x04ac`。现在查看 `nm 3c574_cs.o | sort`，我们看到：

```
0000002 d if_names
0000002 t 3574_attach
0000040 d preamble_preamble
0000041 d dev_info
```
