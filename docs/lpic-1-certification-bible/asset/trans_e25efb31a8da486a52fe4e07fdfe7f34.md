
# 调制解调器

## 1.1 硬件与架构

-   配置调制解调器、声卡。确保设备满足兼容性要求（特别是调制解调器**不是** Winmodem），验证调制解调器和声卡是否使用了唯一且正确的 IRQ、I/O 和 DMA 地址；如果声卡是即插即用（PnP）设备，安装并运行 `sndconfig` 和 `isapnp`；将调制解调器配置为外出拨号；将调制解调器配置为外出 PPP | SLIP | CSLIP 连接；将串行端口设置为 115.2 Kbps。

Linux 支持各种内置和外置调制解调器。但是，有一个非常重要的注意事项：确保您的调制解调器不是 Winmodem。Winmodem 使用软件而非硬件来进行实际的调制操作。这允许制造商以较低的 CPU 占用率为代价，制造出非常廉价的调制解调器。问题在于 Linux 对这类调制解调器的支持非常有限。通常，如果存在驱动程序的话，往往只是一个二进制驱动，且可能仅与一两个内核版本兼容。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_48_0.png)

配置调制解调器使用 PPP 进行拨出连接的内容在第 15 章中有介绍。

# 网卡

## 1.1 硬件与架构

-   设置 SCSI 和网卡设备。操作 SCSI BIOS 以检测已使用和可用的 SCSI ID，将 SCSI ID 设置为启动设备及其他所需设备的正确 ID 号，使用制造商的安装工具对 SCSI 硬盘进行低级格式化，并使用 Linux 的 `fdisk` 和 `mkre2fs` 正确分区和格式化文件系统；使用制造商的设置工具设置网卡的 I/O 和 IRQ，如有必要还设置 DMA。

网络支持是 Linux 的一个明显强项。从最新千兆以太网到“古老”的 ARCnet，几乎所有的网卡都有驱动支持。主要区别在于速度和设置的难易程度。

如果有选择余地，建议获取 PCI 网卡，因为它们通常除了加载驱动外不需要额外的配置；此外，它们的 CPU 开销非常小。如果您的网卡厂商未列出有驱动支持，请务必检查卡上的实际芯片集，因为许多制造商使用相同的芯片集。

配置 IRQ 和 DMA 设置的内容将在本章稍后的“解决冲突和配置即插即用设备”部分中介绍。

# 声卡

目标

## 1.1 硬件与架构

-   配置调制解调器、声卡。确保设备满足兼容性要求（特别是调制解调器**不是** Winmodem），验证调制解调器和声卡是否使用了唯一且正确的 IRQ、I/O 和 DMA 地址；如果声卡是即插即用（PnP）设备，安装并运行 `sndconfig` 和 `isapnp`；将调制解调器配置为外出拨号；将调制解调器配置为外出 PPP | SLIP | CSLIP 连接；将串行端口设置为 115.2 Kbps。

根据所需的驱动类型，声卡的配置可能非常简单，也可能非常困难。某些卡包含在内核中并开箱即用。其他卡则需要使用 Linux 中的即插即用工具进行适当设置。如果内核未包含驱动，则还有其他几种可用的声卡驱动库。大多数当前发行版都包含声卡设置工具以简化配置。

最常见的声卡配置工具是由 Red Hat 创建但在许多发行版中使用的 `sndconfig`。图 1-1 展示了 `sndconfig` 的一个示例。默认情况下，`sndconfig` 会探测系统并尝试确定已安装的声卡类型。如果无法自动检测该卡，它会提示您从列表中进行选择。可以使用 `--noprobe` 参数禁用探测功能，并使用 `--noauto-config` 参数禁用卡的自动配置。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_49_0.png)

提示

ALSA 项目为许多不同的声卡增加了支持。其网址为 http://www.alsa-project.org/。

配置 IRQ 和 DMA 设置的内容将在下一节中介绍。

# 解决冲突和配置即插即用硬件

当两个设备共享同一配置地址时，会发生硬件冲突。新的 PCI 设备可以共享地址，但旧硬件不行。为了解决冲突，您可能需要更改硬件跳线，或者对于即插即用设备，您可能需要调整软件配置。

## 硬件地址

计算机中的硬件设备使用几种配置选项。这些配置地址告诉系统如何与设备通信。常见的地址设置如下：

-   DMA（直接内存访问）
-   IRQ（中断请求）
-   I/O 地址

当设备需要直接访问内存而不经过 CPU 时，会使用直接内存访问（DMA）通道。设备不应共享 DMA 通道。设备使用中断请求（IRQ）来通知 CPU，当设备需要 CPU 执行某些操作时。大多数旧设备必须有唯一的 IRQ，而较新的 PCI 设备可以共享 IRQ。I/O 地址是设备用于与系统其余部分通信的内存地址。每个设备必须有唯一的 I/O 地址。

旧硬件通过物理板上的跳线或软件配置工具手动设置配置地址。当前硬件由系统 BIOS 或操作系统自动配置。

大多数硬件可以设置为任何空闲的 IRQ 或 I/O 地址。常见的例外是串行端口和并行端口。它们需要在特定地址才能用作标准端口。串行端口 COM1 和 COM2 分别设置为 IRQ 4 和 3。并行端口 LPT1 和 LPT2 分别设置为 IRQ 7 和 5。

## 查看配置地址

消除硬件冲突的第一步是查看当前正在使用哪些资源以及哪些资源是空闲的。将任何发生冲突的硬件移动到空闲资源上。

### 列出中断

要查看系统中哪些 IRQ 被使用以及哪些空闲，您可以查看 `/proc/interrupts` 文件。例如：

```bash
$cat /proc/interrupts
                CPU0
0: 510082305 XT-PIC  timer
1: 278104    XT-PIC  keyboard
2:           0 XT-PIC  cascade
9: 3014717670    XT-PIC  acpi, EMU10K1, eth0
10: 3253300     XT-PIC  usb-ohci
13:           0 XT-PIC  fpu
14: 387511089     XT-PIC  ide0
15: 3844545     XT-PIC  ide1
NMI:           0 
ERR:           0 
```

如示例所示，IDE 控制器位于 IRQ 14 和 15。声卡 EMU10K1 和网卡 eth0 都位于 IRQ 9。USB 控制器 usb-ohci 位于 IRQ 10。未列出的 IRQ 号被视为空闲且未使用。

### 列出 I/O 端口

要查看系统中哪些 I/O 端口正在被使用，您可以查看 `/proc/ioports` 文件。例如：

```bash
$cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
0170-0177 : ide1
01f0-01f7 : ide0
0376-0376 : ide1
03c0-03df : vga+
03f6-03f6 : ide0
03f8-03ff : serial(set)
0cf8-0cff : PCI conf1
5000-5003 : acpi
5004-5005 : acpi
5008-500b : acpi
5020-5023 : acpi
cb00-cb0f : Advanced Micro Devices [AMD] AMD-756 [Viper] IDE
cb00-cb07 : ide0
cb08-cb0f : ide1
e000-efff : PCI Bus #01
f800-f8ff : Lite-On Communications Inc LNE100TX
f800-f8ff : eth0
ff80-ff9f : Creative Labs SB Live! EMU10000
  ff80-ff9f : EMU10K1
ffe4-ffe7 : Advanced Micro Devices [AMD] AMD-751 [Irongate]
System Controller
fff0-fff7 : Creative Labs SB Live!
```

与 IRQ 一样，任何未列出的范围都被视为空闲，因此可以被其他设备使用。

## 列出 DMA 通道

要查看系统中正在使用和空闲的 DMA 通道，您可以查看 `/proc/dma` 文件。例如：

```bash
debian:~$ cat /proc/dma
4: cascade
```

该系统只有一个 DMA 通道正在被使用。

# 配置即插即用设备

即插即用设备通过软件而非硬件跳线来设置其配置选项。这使得在发生硬件冲突时更容易调整它们。配置即插即用硬件的第一步是探测支持硬件的系统并创建一个配置文件。这是通过以下命令完成的：

```bash
debian:~$pnPdump > /etc/isapnp.conf
```

请注意，这只适用于 ISA 设备。默认配置文件中所有选项都被注释掉了。您需要浏览该文件并取消注释您要使用的选定的 IRQ、DMA 和 I/O 端口地址。在取消注释行之前，请检查系统中的空闲地址，如前一部分所示。例如，要设置声卡，您需要取消注释 IRQ、DMA 和 I/O 端口行，如下所示：

```text
# CONFIGURE CTL0028/1530224 (LD 0
    #    ANSI string -->Audio<--
# Multiple choice time, choose one only !
#
    #       Start dependent functions; priority preferred
    #       IRQ 5,
    #       High true, edge sensitive interrupt (by default)
    #   (INT 0 (IRQ 5 (MODE +E)))
```

