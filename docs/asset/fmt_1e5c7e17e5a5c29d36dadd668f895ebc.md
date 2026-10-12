
`alias sound-service-0-1 sb`

```
alias sound-service-0-2 sb
alias sound-service-0-3 sb
alias sound-service-0-4 sb
alias synth0 sb
post-install sb /sbin/modprobe "adlib_card"

options sb io=0x220 irq=5 dma=1 dma=5 mpu_io=0x330
options adlib_card io=0x88 synthesizer
```

现在运行 `tail -f /var/log/messages /var/log/syslog`，并在另一个终端输入：

```
modmod -a
modprobe sb
```

如果没有遇到内核或其他错误，则说明设备工作正常。现在我们想要设置模块的动态加载。使用 `modmod -a`（或手动）移除所有声卡和其他模块，然后尝试：

```
insmod
```

你会得到这样的内核日志：

```
Sep 24 00:45 kernel: Soundblaster audio driver (C) by Hannu Savolainen 1993-96
Sep 24 00:45 kernel: SB16 detected OK
```

然后尝试：

```
playmidi <filename>
```

你会得到这样的内核日志：

```
Sep 24 00:51 kernel: Soundblaster audio driver (C) by Hannu Savolainen 1993-96
Sep 24 00:51 kernel: SB16 detected OK
Sep 24 00:51 kernel: YM3812 and OPL3 driver (C) by Hannu Savolainen, Hooft 1993-96
```

如果你注释掉了 `alias` 行，则会出现如下内核消息：

```
modprobe: Can't locate module sound-0
```

这表示内核正在尝试插入别名行。实际上，`sound-service-0,1,2,3` 分别是 `/dev/mixer`、`sequencer`、`midi`、`audio` 设备。`sound-0` 意味着应该提供这些。`post-install` 选项意味着安装模块后运行额外的命令；这处理了 Adlib sequencer 驱动。尝试移除 `post-install` 行并添加 `alias sound-service-1 adlib_card`，这在运行 `playmidi` 时有效。

### 4.6.2 并行口 (Parallel port)

并行端口模块的麻烦小得多：

```
alias parport_lowlevel parport
options parport_lowlevel io=0x378 irq=7
```

只需确保你的 IRQ 和 I/O 端口与 CMOS 中的匹配（见第 3.3 节），并且不与其他任何设备冲突。

### 4.6.3 NIC – 以太网、PCI 和旧 ISA

我们演示了非 PnP ISA 卡和 PCI 卡，并以以太网设备为例（`NIC` 代表网络接口卡，即 10 或 100 Mb 卡）。对于带有跳线线的旧 ISA 卡，你需要检查 `/proc/` 文件中未使用的 IRQ 和 I/O 端口，然后物理设置跳线。现在你可以像通常一样执行 `modprobe`，例如：

```
modinfo ne
modprobe ne io=0x300 irq=9
```

当然，为了动态加载，你的 `/etc/modules.conf` 文件必须包含行：

```
alias eth0 ne
options ne io=0x300 irq=9
```

在某些情况下，你会遇到一个具有软件可配置跳线的卡，但只能通过 DOS 工具配置。在这种情况下，将模块编译进内核会导致它在启动时自动探测，无需任何其他配置。

最坏的情况是一个品牌以及 IRQ 和 I/O 端口都未知的卡。卡上的芯片编号可以给你提示（在内核源码中 `grep` 该数字），但并不总是。为了让此卡工作，在内核中编译几个模块的支持，其中一个很可能是它。经验将帮助你做出更好的猜测。如果你的一个猜测是正确的，卡将在重启后被发现。你可以在 `/proc/` 中找到它的 IRQ 和 I/O 端口值，或者运行 `dmesg` 查看自动探测行；消息将以 `eth0: ...` 开头并包含有关驱动的信息。如果你以后决定使用模块而不是自定义内核，可以使用这些信息。

如所述，PCI 设备几乎不需要作为选项提供 IRQ 或 I/O 端口。或者如果你有正确的模块，简单的

```
modprobe <module>
```

将始终有效。然而，寻找正确的模块可能是一个问题，因为供应商除了实际芯片组兼容之外，还会给卡起各种带有营销色彩的名字。`scanci` 工具（实际上是 X 的一部分）会检查你的 PCI 插槽以查找 PCI 设备。运行 `scanci` 可能会输出如下内容：

```
pci bus 0x0 cardnum 0x08 function 0x0000 vendor 0x1011 device 0x0009
Digital DC21140 10/100 Mb/s Ethernet

pci bus 0x0 cardnum 0x0a function 0x0000 vendor 0x0086 device 0x1229
Intel 82557/8/9 10/100bit network controller

pci bus 0x0 cardnum 0x0c function 0x0000 vendor 0x1274 device 0x1371
Ensoniq es1371
```

另一个工具是 `pciutils` 包的 `lspci`，它在 `scanci` 未提供的地方提供全面的信息。然后是一个简单的脚本（参数中又是内核 2.4 的路径），

```
for i in /lib/modules/<version>/*; do strings $i | \
  grep -q -i 21146 && echo $i; done
(for i in /lib/modules/<version>/kernel/drivers/*; \
  do strings $i | grep -i 21146 && echo $i; done)
for i in /lib/modules/<version>/*; do strings $i | \
  grep -q -i 8255 && echo $i; done
(for i in /lib/modules/<version>/kernel/drivers/*; \
  do strings $i | grep -i 8255 && echo $i; done)
```

忠实地输出了三个模块 `2de4x.0`、`eepro100.0` 和 `tulip.o`，其中我们是正确的。

## 42.6. 配置各种设备

对于...`grep`... 来说也是如此...Accton 提供了 `rt18139.o` 和 `tulip.o`（前者是正确的），而对于...`grep`...Macronix（甚至是 987）提供的是 `tulip.o`，这导致机器死机。我还没有让网卡工作起来，尽管 Eddie 声称他最终也获得了一张类似的卡。网卡很便宜——有足够多的好用品牌，你不需要在坏掉的卡上浪费时间。

## 42.6.4 PCI 厂商 ID 和设备 ID

PCI 支持一个实用的概念，即每个厂商和设备都有唯一的十六进制 ID。例如，英特尔选择用完全随机的数字 `8086` 作为它们的厂商 ID，PCI 卡会在收到请求时提供它们的 ID。你会在 `lspci`、`scanci` 和 `cat /proc/pci` 的输出中看到数值列表，特别是 `recipe` 工具可以根据 ID 数字查询厂商名称。`/usr/share/pci.ids` 文件（在 Debian(?) 上路径为 `/usr/share/misc/pci.ids`）来自 `pciutils` 包，包含了所有 ID 及其对应名称的完整表格。`kudzu` 包也包含一个表格 `/usr/share/kudzu/pcitable`，其中包含了我们真正寻找的用于 ID 到内核模块映射的信息。这使你能够使用预期方法从内核的 `/proc/pci` 数据中定位正确的 PCI 模块。该文件格式易于理解，你应该尝试编写一个 shell 脚本来自动执行查询。

## 42.6.5 PCI 和声卡

上方的 `scanpci` 输出显示了流行的 Ensoniq 声卡，有些集成在主板上。只需在你的 `modules.conf` 文件中添加此行：

```
alias sound es1371
```
