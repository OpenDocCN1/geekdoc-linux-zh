
# 图 5-1 GlancePlus 中的 CPU 报告，显示两个处理器

![](img/eff8b9287a5f38c5adf538f24aacf29e_355_0.png)

图 5-1 中的屏幕显示，`*CPU Util*`（CPU 使用率）显示的最大值为 200%，而非系统中存在的四个处理器（若为四个则应显示 400%），这证实我们为 `*cable1*`（主机名 `*cvhdcn3*`）分配了两个处理器。你还可以通过运行 `*top*` 命令来确认 `*cable1*` 中的两个处理器，如图 5-2 所示：

# 图 5-2 top 命令截图，显示 cable1 中的两个处理器

![](img/eff8b9287a5f38c5adf538f24aacf29e_356_0.png)

top 命令清晰地显示了分配给 cable1 的两个 CPU（即图 5-2 中的 CPU 0 和 1）。

## 虚拟分区与内存

在第 2 章分配内存时，你使用了 size（大小）。你也可以像将 hopath 作为 CPU 的 min 和 num 的子集那样，将基地址（base address）和范围（range）作为 size 的子集来指定。我们选择使用 size。表 5-1 显示了与分配和修改内存相关的选项。我们需要执行的第一项操作是查找系统的内存量，以便将其中的一部分分配给 vPars。确定系统内存量有多种方法。以下仅显示了以非 vPars 模式启动标准 HP-UX 时 dmesg 命令中与内存相关的输出：

```
# dmesg

Memory Information:
  MBD / - cal page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 4194304 Kbytes, lockable: 3180924 Kbytes, available: 3655192 Kbytes
```

此列表显示 `*Physical*`（物理）内存为 4GB。你还可以运行 GlancePlus 并选择 `*Memory*`（内存）屏幕。

可以使用 `*m::size*` 轻松为 vPar 指定内存，其中 `*size*` 单位为 MB（兆字节）。要在虚拟分区中指定 2 GB 内存，可以使用选项 `*m::2048*`。

将内存分配给 vPars 后，你希望确认每个 vPar 中确实具有你指定的内存量。你可以通过多种方式验证这一点。首先是在启动虚拟分区时执行 **dmesg**。虚拟分区监视器（Virtual Partitions Monitor）仅启动你指定为虚拟分区一部分的设备。以下示例仅显示了 **dmesg** 针对 `*cable1*` 的与内存相关的输出：

```
# Memory Information:
cvhcon3:/ # page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2096128 Kbytes, lockable: 1576748 Kbytes, available: 1815620 Kbytes
```

请注意，此输出显示 `*cable1*` 拥有 2 GB RAM，正如创建 `*vPar cable1*` 时指定的那样。这与第 2 章中的示例不同，在该示例中 `*cable1*` 只有 1 GB RAM。这是低级别 vPars 工作原理的一个指示，即在启动时将资源分配给 `*cable1*`，确保只有指定的资源被分配给该 vPar。

我们也可以运行 GlancePlus 并选择 `*memory*` 屏幕来查看与内存相关的信息。以下截图显示了启动标准 HP-UX 而非虚拟分区时的系统总内存，如图 5-3 所示：

# 图 5-3 GlancePlus 中的物理内存，显示系统为 4 GB（非 vPars 模式）

![](img/eff8b9287a5f38c5adf538f24aacf29e_358_0.png)

现在让我们在 GlancePlus 中查看 cable1（主机名 cvhdcn3）的内存。图 5-4 是在系统启动时加载 cable1 时获得的：

![](img/eff8b9287a5f38c5adf538f24aacf29e_359_0.png)

屏幕右下角的 Phys Mem（物理内存）显示为 2 GB，正如我们分配给 cable1 那样。这证实了 dmesg 显示的系统为 4 GB 和 cable1 为 2 GB 的结果。

由于你正在运行多个虚拟分区，因此必须运行多个 HP-UX 内核。特定虚拟分区的内核必须位于分配给该虚拟分区的内存范围内。在 HP-UX 11i 中，内核在内存中的位置由 /usr/con/cfg/map-file 文件指定。此文件中的条目包括内核在内存中将被放置的位置。此行以 Text = LOAD 开头。此文件存在于你拥有虚拟分区的每个文件系统上，并包含相应虚拟分区的内核位置以及其他动态信息。在 HP-UX 11i 的非虚拟分区系统上，此文件也存在并包含 11i 使用的其他信息。关于 HP-UX 11i 内核和虚拟分区的工作方式在第 4 章中涵盖。

## 虚拟分区与局域网

你系统中的局域网（LAN）卡也可以很容易地通过 **ioscan** 进行识别。要仅查看系统中的 LAN 卡列表，我们可以发出以下命令：

```
# ioscan -f | grep lan
lan   0  0/0/0/0        btl an5   CLAIMED   INTERFACE   PCI Ethernet (10110019)
      ~ 1                btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
lan   3  0/5/0/4/0      btl an   CLAIMED   INTERFACE   PCI 10/100Base-TX 4 port
lan   4  0/5/0/5/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   5  0/5/0/6/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   6  0/5/0/7/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   2  1/2/0/0        btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
#
```

此系统有七个局域网接口。它具有内置局域网接口、两个附加局域网卡和一个四端口卡。虽然此系统未在我们之前的示例中使用，但我想展示一个具有多种局域网接口的系统列表。

回到我们之前的示例，我们的系统有三个局域网接口，如下面的 **ioscan** 列表所示：

```
cvhdcn3:/ # ioscan -f | grep lan
lan   0  0/0/0/0        btl an   CLAIMED   INTERFACE   HP PCI 10/100Base-TX Core
lan   1  0/10/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
lan   2  0/12/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
cvhdcn3:/> #
```

位于 0/0 的局域网卡已分配给 `*cable1*`，位于 0/10 的卡已分配给 `*cable2*`，如下面的 **vparstatus -v** 列表所示：

```
# vparstatus -v

[Virtual Partition Details]
Name:     cable1
State:    Up
Attributes: Dynamic,Manual
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_360_0.png)

```
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
0.0 <-- cable1 LAN on 0/0 but not shown
0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024

[Virtual Partition Details]
Name:     cable2
State:    Up
Attributes: Dynamic,Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 37
Unbound [Path]:

[IO Details]
0.8,0.0,0.8,0.5,0.0.0, BOOT
0.10 <-- cable2 LAN

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024
# 
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_1.png)

Core I/O 卡上 `*0/0/0/0*` 处的局域网接口并未在 **vparstatus** 输出中明确列出。`*0/0/4/0*` 处的控制台也是此 vPar 的一个隐含组件。这两个组件都是 Core I/O 卡的一部分，我们在 `*cable1*` 的 **vpareccreate** 命令中通过 `-a` `*0/0/0/0*` 参数将其指定为该 vPar 的一部分。

未分配的局域网接口可以通过 **vparmodify** 命令添加到 `*cable1*` 或 `*cable2*`。然而，截至本文撰写时，I/O 组件不能动态添加，vPar 必须处于 `*down*`（关闭）状态才能添加局域网或任何其他 I/O 组件。但是，你可以使用组件的在线更换和添加（OLAR）功能来操作 vPars 中的组件。例如，如果你将一个 I/O 路径分配给某个 vPar，然后在该 I/O 插槽中物理添加一个组件，那么该组件将成为 vPar 的一部分。

## 虚拟分区与控制台

你可以为每个虚拟分区设置专用的物理控制台。这意味着要为每个虚拟分区分配一个串行端口。或者，你的虚拟分区可以使用虚拟控制台。虚拟控制台（Virtual CoNsole）驱动程序 vcn 处理与虚拟控制台相关的 I/O。如图 5-5 所示，vcn 与虚拟分区监视器通信。虚拟分区监视器缓冲与虚拟控制台相关的 I/O，直到其可以由虚拟控制台从属设备（Virtual Console Slave, vcs）处理。所有 vPars 都使用虚拟控制台，并且物理控制台作为 I/O 规范的一部分分配给其中一个 vPar。

