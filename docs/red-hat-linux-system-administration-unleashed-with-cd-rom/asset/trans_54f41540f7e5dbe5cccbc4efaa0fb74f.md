
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件包含有关系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果你在内核中包含了多处理器支持，这一事实将在 /proc/cpuinfo 文件以及启动消息中反映出来。

## 注意

请注意，从以下输出中无法推断该系统是否是一个多处理器系统。此输出仅表明正在运行的内核只识别一个处理器。如果这是一个多处理器系统，但运行的是未编译 SMP 支持的内核，你将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的良好起点。该文件列出了在运行内核中可用驱动程序的字符设备和块设备，以及它们的主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了该系统中各种设备的 IRQ、DMA 和 I/O 范围。例如，我可以从输出中确定系统中使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。我还可以看到每个设备已产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件提供了系统中各种 PCI 设备的[content]
无法确定系统有多少个处理器。如果在内核中包含多处理器支持，这一事实会反映在 /proc/cpuinfo 文件和启动消息中。

## 注意

请注意，无法从以下输出推断该系统是否多处理器。此输出仅表示运行的内核只识别一个处理器。若多处理器系统运行未编译 SMP 支持的内核，将得到如前例所示的输出。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 文件是查看 Linux 内核支持哪些设备的起点。该文件列出运行内核中可用驱动的字符设备和块设备及其主设备号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前面三个命令显示了本系统各设备的 IRQ、DMA 和 I/O 范围。例如可确定系统中有使用 IRQ 7、DMA 通道 1 和 5 以及多个 I/O 端口范围的 Soundblaster AWE 32 卡。也可看到各设备产生的中断次数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件提供了系统中各种 PCI 设备的[content]
无法判断系统有多少个处理器。若内核包含多处理器支持，该信息会体现在 /proc/cpuinfo 文件和启动信息中。

## 注意

请注意，以下输出不能说明系统是否多处理器。它仅表示当前内核只识别一个处理器。若多处理器系统运行未启用 SMP 的内核，输出会如前例所示。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 是查看 Linux 内核支持设备的起点。该文件列出运行内核中可用驱动的字符设备和块设备及其主号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前三个命令显示了本系统各设备的 IRQ、DMA 和 I/O 范围。例如可看出系统有一块使用 IRQ 7、DMA 1 和 5 以及多个 I/O 范围的 Soundblaster AWE 32 卡。也可看到各设备产生的中断数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件提供了系统中各种 PCI 设备的[content]
无法判断系统有多少个处理器。若内核包含多处理器支持，该信息会体现在 /proc/cpuinfo 文件和启动信息中。

## 注意

请注意，以下输出不能说明系统是否多处理器。它仅表示当前内核只识别一个处理器。若多处理器系统运行未启用 SMP 的内核，输出会如前例所示。

~~~
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts

Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
~~~

/proc/devices 是查看 Linux 内核支持设备的起点。该文件列出运行内核中可用驱动的字符设备和块设备及其主号。

~~~
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
~~~

~~~
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
~~~

~~~
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
~~~

前三个命令显示了本系统各设备的 IRQ、DMA 和 I/O 范围。例如可看出系统有一块使用 IRQ 7、DMA 1 和 5 以及多个 I/O 范围的 Soundblaster AWE 32 卡。也可看到各设备产生的中断数。

~~~
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
~~~

/proc/pci 文件提供了系统中各种 PCI 设备的[content]
无法判断系统有多少个处理器。若内核包含多处理器支持，该信息会体现在 /proc/cpuinfo 文件和启动信息中。

## 注意

请注意，以下输出不能说明系统是否多处理器。它仅表示当前内核只识别一个处理器。若多处理器系统运行未启用 SMP 的内核，输出会如前例所示。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts
Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 是查看 Linux 内核支持设备的起点。该文件列出运行内核中可用驱动的字符设备和块设备及其主号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前三个命令显示了本系统各设备的 IRQ、DMA 和 I/O 范围。例如可看出系统有一块使用 IRQ 7、DMA 1 和 5 以及多个 I/O 范围的 Soundblaster AWE 32 卡。也可看到各设备产生的中断数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件提供了系统中各种 PCI 设备的[content]
无法判断系统有多少个处理器。若内核包含多处理器支持，该信息会体现在 /proc/cpuinfo 文件和启动信息中。

## 注意

请注意，以下输出不能说明系统是否多处理器。它仅表示当前内核只识别一个处理器。若多处理器系统运行未启用 SMP 的内核，输出会如前例所示。

```
tschenk@quicksilver:~ [1038]$ cat /proc/devices
Character devices:
1 mem
2 pty
3 ttyp
4 ttyS
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts
Block devices:
1 ramdisk
2 fd
3 ide0
7 loop
8 sd
9 md
11 sr
```

/proc/devices 是查看 Linux 内核支持设备的起点。该文件列出运行内核中可用驱动的字符设备和块设备及其主号。

```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
6400-6403 : BusLogic BT-958
6600-667f : DC21140 (eth0)
f000-f007 : ide0
f008-f00f : ide1
```

前三个命令显示了本系统各设备的 IRQ、DMA 和 I/O 范围。例如可看出系统有一块使用 IRQ 7、DMA 1 和 5 以及多个 I/O 范围的 Soundblaster AWE 32 卡。也可看到各设备产生的中断数。

```
tschenk@quicksilver:~ [1052]$ cat /proc/pci
PCI devices found:
Bus 0, device 0, function 0:
  Host bridge: Intel 82439HX Triton II (rev 3).
    Medium devsel. Master Capable. Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 1).
    Medium devsel. Fast back-to-back capable. Master Capable. No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel. Fast back-to-back capable. Master Capable. Latency=32.
    I/O at 0xf000 [0xf000].
Bus 0, device 17, function 0:
  SCSI storage controller: BusLogic MultiMaster (rev 8).
    Fast devsel. IRQ 12. Master Capable. Latency=32. Min Gnt=8. Max Lat=8.
    I/O at 0x6400 [0x6401].
    Non-prefetchable 32 bit memory at 0xe1804000 [0xe1804000].
Bus 0, device 18, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel. Fast back-to-back capable. IRQ 12. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xe0000000 [0xe0000000].
    Non-prefetchable 32 bit memory at 0xe1800000 [0xe1800000].
    Non-prefetchable 32 bit memory at 0xe1000000 [0xe1000000].
Bus 0, device 19, function 0:
  SCSI storage controller: Adaptec AIC-7850 (rev 1).
    Medium devsel. Fast back-to-back capable. IRQ 9. Master Capable.
    Latency=32. Min Gnt=4. Max Lat=4.
    I/O at 0x6000 [0x6001].
    Non-prefetchable 32 bit memory at 0xe1805000 [0xe1805000].
Bus 0, device 20, function 0:
  Ethernet controller: DEC DC21140 (rev 34).
    Medium devsel. Fast back-to-back capable. IRQ 11. Master Capable.
    Latency=96. Min Gnt=20. Max Lat=40.
I/O at 0x6600 [0x6601].
Non-prefetchable 32 bit memory at 0xe1806000 [0xe1806000].
```

/proc/pci 文件列出 PCI 设备信息。
