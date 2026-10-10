
## 在虚拟分区中添加和移除设备

该输出显示 *cable1* 中标记为 0 和 1 的两个 CPU。由于 *cable1* 的主机名是 *cvhdc0n3*，因此输出中显示了 *cvhdc0n3* 的 *System* 名称。

虽然这是一个展示如何修改虚拟分区的简单示例，但它也展示了 vPar 的强大功能。当系统上的两个 vPar 都在运行时，可以在一个或两个 vPar 中添加处理器，而不会中断正在运行的程序。

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_0.png)

请注意，**vpmodify** 的 *-a* 选项将 CPU 数量*相对*于当前数量进行了更改。在我们的例子中，当前的 CPU 数量为 1，使用 *-a cpu:1* 在当前数量 1 的基础上添加了 1 个 CPU，结果得到 2 个 CPU。当我们使用 **vpmodify** 的 *-d* 选项移除处理器时，情况也相同。以下示例展示了运行 **vpstatus** 以查看两个 CPU，使用 **vpmodify** 将 CPU 数量改回 1（这也是相对于当前 CPU 数量 2 的相对值），并通过 **vpstatus** 确认此更改已生效：

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_2.png)

```bash
# vpstatus -p cable1 -v

[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic, Manual
Kernel Path:   /stand/vmunix
Boot Options:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33        <-- bound CPU @ 33
Unbound [Path]:          97       <-- unbound CPU @ 97

[IO Details]
      0.0
      0.0.0.0
      0.0.1.1.2.0     BOOT
      0.0.4.0         CONSOLE

[Memory Details]
Specified [Base /Range]:
Bound  (bytes)         (MB)

Total Memory (MB):  1024
# vpmodify -P cable1 -d cpu:1
# vpstatus -p cable1 -v
```

```
[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic, Manual
Kernel Path:   /stand/vmunix
Boot Options:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33        <-- original CPU @ 33
Unbound [Path]:                   <-- no unbound CPUs

[IO Details]
      0.0
      0.0.0.0
      0.0.1.1.2.0 BOOT
      0.0.4.0 CONSOLE

[Memory Details]
Specified [Base /Range]:
                (bytes) (MB)
Total Memory (MB):   1024
#
```

我们可以利用可用的两个*未绑定* CPU 对 vPar 进行许多其他修改，例如向其中一个 vPar 添加两个 CPU，或者向每个 vPar 各添加一个 CPU。

在使用 *vparmodify* 时，请记住组件的相对特性，并且在撰写本文时，某些更改，例如修改内存或添加 I/O 组件，要求 vPar 处于关闭状态。

以下部分提供了一些关于 HP-UX 11i 中设备文件的一般背景知识。如果你之前很少在 HP 系统上处理设备文件，建议复习一下本章中非 vPar 特定的部分。

![](img/eff8b9287a5f38c5adf538f24aacf29e_371_0.png)

## 章节的非 vPar 特定部分 - 设备文件和外设背景知识

HP-UX 会在系统启动时为其发现的大多数连接设备创建特殊文件。不过，你可能需要自己创建设备文件，或者至少需要理解系统中存在的一些设备文件，因此本章中的信息对于每位系统管理员来说都至关重要。典型的安装将包括终端、打印机、磁带驱动器、DVD 驱动器等。一些设备是“标准的”，意思是它们是 HP 产品或由 HP 官方支持的第三方产品。然而，你必须小心，因为看似应该能工作的设备最终可能无法工作，也可能不受支持。几乎总是可以找到一种方法最终让设备工作，但请留意你添加的不受支持的设备，它们可能会给你带来麻烦。

当你向系统添加额外外设时，你必须手动添加设备文件或使用 SAM 为你创建它们。你添加的大多数设备都可以通过 SAM 添加。我发现添加外设很像设置网络：也就是说，我几乎总是使用 SAM，但我认为了解后台发生了什么也很重要。举个例子，你可以使用 SAM 向系统添加打印机，而永远不知道为了支持新打印机做了什么操作。如果打印机因某种原因无法工作，如果不了解设备文件，你就真的无法开始排查问题。

下一部分是关于设备文件的一般概述。

### HP-UX 11i 中的设备文件

在 UNIX 世界中，还有什么比设备文件更令人困惑的呢？幸运的是，在 HP-UX 中，Series 700 和 Series 800 的设备文件几乎相同，因此如果你学会了其中一种，你的知识也适用于另一种。在本节中，我将涵盖以下内容：

- 设备文件的结构。
- 一些有助于你处理设备文件的命令。
- 一些创建设备文件的示例。

设备文件为 HP-UX 内核提供关于特定设备的重要信息。在执行 I/O 操作之前，HP-UX 内核需要了解关于该设备的许多信息。在 HP-UX 11i 中，工作站和服务器系统的设备文件命名约定是相同的。设备文件位于 /dev 目录中。/dev 下可能还有一个子目录，用于进一步对设备文件进行分类。子目录的一个示例是 /dev/dsk，磁盘设备文件通常位于此处；另一个是 /dev/rmt，磁带驱动器设备文件位于此处。图 5-7 展示了 HP-UX 11i 的设备文件命名约定。

![](img/eff8b9287a5f38c5adf538f24aacf29e_373_0.png)

图 5-7 HP-UX 11i 设备文件命名约定

在创建设备文件的过程中，你可以使用许多命令。ioscan 命令是其中的第一个。本节中的一些示例在第 3 章构建内核时已使用过。以下是与第 4 章中描述如何创建内核时运行 sysdef 的同一台 Series 700 系统的 ioscan 输出。（使用 -f 参数运行 ioscan 将生成完整列表；建议你尝试带和不带 -f 参数的情况。）我包含了四个 ioscan 输出，以便你可以看到来自不同系统的示例。最后一个列表来自第 9 章中磁盘和文件系统部分示例中使用的大型 V-Class 系统。

```
$ /usr/sbin/ioscan

(on Series 700)
H/W Path        Class         Description
==============================
        bc
1         graphics      Graphics
2         ba
2/0       unknown
2/0/1           target      Built-in SCSI
2/0/1.1.0     disk          HP C2247
2/0/1.2       target
2/0/1.2.0     disk          TOSHIBA CD-ROM XM-3301TA
2/0/1.6       target
2/0/1.6.0     disk          HP C2247
2/0/2       lan           Built-in LAN
2/0/4       tty           Built-in RS-232C
2/0/6       ext_bus       Built-in Parallel Interface
2/0/8       audio         Built-in Audio
2/0/10      pc            Built-in Floppy Drive
2/0/10.1    /dev/floppy   HP PC FDC FLOPPY
2/0/11      ps2           Built-in Keyboard
8         processor     Processor
9         memory          Memory
```

以下是来自 Series 800 系统的 ioscan 输出。注意该输出中显示的四个处理器。

```
$ /usr/sbin/ioscan

(on Series 800)
H/W Path        Class         Description
bc              bc            I/O Adapter
bc              I/O Adapter
ext_bus         GSC built-in Fast/Wide SCSI
disk            target        HP C2490WD
disk            target        HP C2490WD
disk            target        HP C2490WD
disk            target        HP C2490WD
bc              Bus Converter
ba              mux           mux
ba              Core I/O Adapter
ext_bus         Built-in Parallel Interface
ext_bus         Built-in SCSI
target          tape          HP HP35480A
target          disk          TOSHIBA CD-ROM XM-4101TA
lan             P82           Built-in Keyboard/Mouse
processor       Processor
processor       Processor
processor       Processor
processor       Processor
memory          Memory
```

最后一个来自 V-Class 服务器的 ioscan 输出。注意该输出中显示的八个处理器。

```
$ /usr/sbin/ioscan

(on V-Class)
H/W Path        Class         Description
bc              bc            PCI Bus Bridge - epic
lan             PCI           (10110019)
unknown         PCI           (107e0008)
```

| H/W Path | Class | Description |
| :--- | :--- | :--- |
| | ba | ext_bus | PCI Bus Bridge - epic |
| 2/0/0 | | target | Ultra Wide SCSI |
| 2/0/0.5 | | disk | SEAGATE ST34371W |
| 2/0/0.5.0 | | target | |
| 2/0/0.6 | | disk | SEAGATE ST34371W |
| 2/0/0.6.0 | | | |
| 2/0/0.7 | | target | |
| 2/0/0.7.0 | | ctl | Initiator |
| 2/1/0 | lan | | PCI (10110019) |
| 4 | ba | | PCI Bus Bridge - epic |
| 4/1/0 | fc | | HP Fibre Channel Mass |
| | | | Storage Adapter |
| 4/1/0.5 | lan | | HP Fibre Channel Mass |
| | | | Storage Ctrl |
| 4/1/0.8 | fcp | | FCP Protocol Adapter |
| 4/2/0 | ext_bus | | Ultra Wide SCSI |
| 4/2/0.0 | Target | | |
| 4/2/0.0.0 | disk | TOSHIBA CD-ROM XM-5701TA |
| 4/2/0.1 | target | |
| 4/2/0.1.0 | tape | HP C1537A |
| 4/2/0.7 | target | |
| 4/2/0.7.0 | , ctl | Initiator |
| 6 | | | PCI Bus Bridge - epic |
| 8 | memory | | |
| 15 | ba | | Core I/O Adapter |
| 15/1 | tty | Built-in Serial Port DUART |
| 15/2 | tty | Built-in Serial Port DUART |
| 15/3 | unknown | Unknown |
| 17 | processor | Processor |
| 19 | processor | Processor |
| 20 | processor | Processor |
| 22 | processor | Processor |
| 25 | processor | Processor |
| 27 | processor | Processor |
| 28 | processor | Processor |
| 30 | processor | Processor |

以下是来自 V-Class 服务器的完整 ioscan 输出。该服务器连接了一个大型磁盘单元（XP 256），这导致了非常长的输出，我在显示三个点的地方进行了缩写。

```
$ ioscan -f

(on V-Class)
Class  I  H/W Path        Driver     S/W State H/W Type        Description
----   -  --------        -----     --------- ------            -----------
bc         0                  root      CLAIMED   BUS_NEXUS     sago Bridge
ba         0   0  0/0   sasa        CLAIMED   BUS_NEXUS
lan        0   0/0/0   btlam6    CLAIMED   INTERFACE  PCI Ethernet (10110019)
...
```

