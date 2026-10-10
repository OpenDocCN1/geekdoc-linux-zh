

## 精简内核

世上有各式各样的机器，正如用户群体一样。鉴于基于 x86 的硬件特性，这意味着 FreeBSD 内核必须内置数量惊人的驱动程序。为严格受控的硬件集合构建的操作系统（例如 SGI 的 IRIX 或 Apple 的 Mac OS X）可以少用许多这种通用支持，但 FreeBSD 却不得不承担这些。GENERIC 内核还将内存分配和优化的各种选项设置为最低通用标准水平，并且省略了其他可选元素，以便在特定情况下尽可能精简内核。这些都是内核的各个方面，几乎肯定可以针对您的特定系统进行更高效的配置。

在内核启动时，它会探测其知道的每一种设备。这就是为什么系统在启动过程中，您会看到一个充满白色文字滚动的屏幕的原因；内核正在寻找 GENERIC 内核中启用的几十种不同设备。虽然内核找不到其中大多数设备并不会造成任何损害，但执行每个探测都需要时间。您可以通过从内核中删除不必要的设备来显著加快启动时间。这还有助于减小内核的大小。拥有数百兆字节内存的现代系统不必担心这种精简，但在勉强满足 FreeBSD 最低要求的机器上，这是一个值得考虑的问题。

> **注意**
>
> 即使使用 GENERIC 内核，也可以抑制对“天底下”所有设备的探测。这就是启动配置器（在附录 C，“故障排除安装和启动问题”中介绍）所做的：它允许您明确移除对各种设备的 support，这些设备它可以看出会导致 IRQ 或内存地址冲突（或者您知道您没有这些设备）。这个过程实际上并不会改变内核或其编译进去的元素，但它确实防止内核在启动时浪费时间寻找不存在的设备。

当您将 USB 外围设备、声卡、SCSI 控制器等以及其他设备添加到您的系统时，如果您不在内核中添加对它们的支持，就无法使用其中许多设备。对于新的文件系统类型也是如此（例如，如您在第 8 章“FreeBSD 文件系统”中看到的 EXT2FS）。如今许多设备和文件系统都作为内核模块可用，但大多数仍然必须编译进内核，因此您几乎没有选择，只能重新构建它。然而，重新构建给了您调整系统中其他事物的机会（例如内存缓冲区数量、自定义内存管理功能以及内核名称），因此您可能可以通过一次重新构建显著提高系统的性能。

顺便说一下，GENERIC 内核中也没有对称多处理（SMP）支持。如果您的系统拥有超过一个 CPU，您需要构建一个自定义内核才能利用所有这些 CPU。

## 使用 dmesg 获取内核启动信息

如果您要从内核中剔除不必要的设备，那么弄清楚您拥有哪些设备是至关重要的，以便您不会意外删除对现有硬件的支持。如前所述，内核在启动时探测所有已知设备，并打印每个探测的状态，告诉您在新内核中必须保留哪些设备。这些信息不仅仅在启动时打印到屏幕上；它还会被回显到内部运行时消息缓冲区中，以便随时参考。用于回忆此信息的工具是 `dmesg`。

`dmesg` 的输出可能非常长，因此您可能希望将其通过 `less` 管道传输，如列表 16.1 所示。

**列表 16.1** dmesg 通过 less 管道传输以提高可读性的输出

```bash
# dmesg | less
Copyright (c) 1992-2002 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1986, 1988, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California. All rights reserved.
FreeBSD 4.6.2-RELEASE #0: Wed Aug 14 20:47:38 PDT 2002
btman@stripes.somehere.com:/usr/obj/usr/src/sys/STRIPES
Timecounter "i8254" frequency 1193182 Hz
CPU: Pentium III/Pentium III Xeon/Celeron (598.06-MHz 686-class CPU)
Origin = "GenuineIntel" Id = 0x683 Stepping = 3
Features=0x383f9ff<FPU,VME,DE,PSE,TSC,MSR,PAE,MCE,CX8,SEP,MTRR,PGE,MCA,
CMOV,PAT,PSE36,MMX,FXSR,SSE>
real memory = 535736320 (523180K bytes)
config> di sn0
config> di lnc0
config> di ie0
config> di fe0
config> di ed0
config> di cs0
config> di bt0
config> di aic0
config> di aha0
config> di adv0
config> q
avail memory = 516485120 (504380K bytes)
Preloaded elf kernel "kernel" at 0xc044a000.
Preloaded userconfig_script "/boot/kernel.conf" at 0xc044a09c.
Pentium Pro MTRR support enabled
md0: Malloc disk
npx0: <math processor> on motherboard
npx0: INT 16 interface
pcib0: <Host to PCI bridge> on motherboard
pci0: <PCI bus> on pcib0
pci0: <Intel model 1132 VGA-compatible display device> at 2.0 irq 11
pcib1: <PCI to PCI bridge (vendor=8086 device=244e)> at device 30.0 on pci0
pci1: <PCI bus> on pcib1
fxp0: <Intel Pro/100 Ethernet> port 0xde80-0xdebf mem 0xff8fe000-0xff8fefff
   irq 11 at device 8.0 on pci1
fxp0: Disabling dynamic standby mode in EEPROM
fxp0: New EEPROM ID: 0x49b0
fxp0: EEPROM checksum @ 0x3f: 0xd3ef -> 0xd3f1
fxp0: Ethernet address 00:d0:b7:c7:74:f1
inphy0: <i82562ET 10/100 media interface> on miibus0
inphy0:  10baseT, 10baseT-FDX, 100baseTX, 100baseTX-FDX, auto
fxp1: <Intel Pro 10/100B/100+ Ethernet> port 0xfd00-0xfd3f
   mem 0xff700000-0xffffffff,0xfff000-0xffbfffff irq 11 at device 9.0 on pci1
fxp1: Disabling dynamic standby mode in EEPROM
fxp1: New EEPROM ID: 0x40a0
fxp1: EEPROM checksum @ 0x3f: 0x1829 -> 0x182b
fxp1: Ethernet address 00:d0:b7:bd:5d:13
inphy1: <i82555 10/100 media interface> on miibus1
inphy1:  10baseT, 10baseT-FDX, 100baseTX, 100baseTX-FDX, auto
isa0: <Intel 82801BA/BAM (ICH2) PCI to LPC bridge> at device 31.0 on pci0
isa0: <ISA bus> on isa0
atapci0: <Intel ICH2 ATA100 controller> port 0xffa0-0xffaf at device 31.1 on pci0
ata0: at 0x1f0 irq 14 on atapci0
ata1: at 0x170 irq 15 on atapci0
```

输出会贯穿所有的设备检查、文件系统验证和守护进程启动块，然后继续列出自您启动以来由各种设备产生的运行时错误。您可以忽略所有带有时间戳和常规错误消息的内容。您感兴趣的是启动消息，例如上一个列表中的那些。

启动消息的第一部分，在版权和 CPU 信息行之后，是您已在启动配置器中设置的内核配置。每行以 `config>` 开头的都是在可视配置模式下发出的命令，很可能是（正如 `di` 行所示）为了从探测过程中删除不需要的设备。这些设备随后不会出现在 `dmesg` 输出中。如果您未在配置器中移除这些设备，内核将会探测它们。

任何伴随“未找到”消息的驱动程序都是从内核中可以删除的驱动程序。您可能希望保留两个打开的 SSH 终端窗口连接到您的 FreeBSD 机器：一个用于读取 `dmesg` 的输出，另一个用于配置内核。这将有助于确保您不会删除系统报告为“已找到”的任何内容。

## 内核配置文件

在撰写本文时，FreeBSD 并没有像 Red Hat Linux 的 `linuxconf` 或其他 Linux 发行版中由 `make config` 驱动的对话框式流程那样的可视内核配置工具。FreeBSD 的内核是使用文本文件配置的，这种方法可能看起来相当晦涩，但确实提供了一些可视方法所不具备的灵活性。

可视配置工具提供交互式反馈，允许您逐个启用和禁用设备和选项。然而，它不能做的是并排维护多个配置，使用诸如 `diff` 和 `grep` 等工具进行比较，并使用基础级 `GENERIC` 配置、先前已知有效的配置以及参考 `NOTES` 文件作为指南。使用文本文件配置还允许您一目了然地看到所有设备选项。

交互式可视工具可能会变得不必要地复杂和混乱，而在要求您单独决定是否包含每个不同的选项时，实际上可能会削弱有用的反馈。除非您能记住配置文件中每个可用选项的重要性和后果，否则很难跟踪您应该选择哪些选项。使用 FreeBSD 的方法，您可以调整配置文件直到您满意为止，整合自上一个版本发布以来引入的变化。您甚至可以从另一个 FreeBSD 系统复制“标准”配置，然后从中构建内核。

假设您已在系统中安装了 FreeBSD 源代码，请进入 `/usr/src/sys/i386/conf` 目录，这是内核配置文件的位置。在那里，您会看到 `GENERIC` 文件以及其他项目。

> **注意**
>
> 如果您运行在 Alpha 硬件上而不是 `x86`，请使用 `alpha` 代替上述路径名中的 `i386`。本章中的许多其他细节也会略有不同，但过程保持不变。

## `GENERIC` 配置文件

在您喜欢的文本编辑器中打开 `GENERIC` 文件。浏览各种选项，但暂时不要进行任何更改（您不想修改 `GENERIC` 文件本身）。您会发现文件中内置了大量的冗余，以确保您的系统与各种机器保持兼容。“必需”部分的代码块将类似于以下内容，具体会因您的 FreeBSD 特定版本而异：

