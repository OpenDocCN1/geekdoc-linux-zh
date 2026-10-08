# Chapter 5. The proc File System

+   - IO-APIC-edge The voltage signal on this interrupt transitions from low to high, creating an edge, where the interrupt occurs and is only signaled. This kind of interrupt, as well as the IO-APIC-level interrupt, are only seen on processors with the 586 family and higher.
- IO-APIC-level — Generates interrupts when its voltage signal goes high until the signal goes low again.

# 5.2.10. /proc/iomem

This file shows the current map of the system's memory for each physical device:

```
00000000-009fbff : System RAM
009c0f00-009ffff : reserved
000a0000-00ffff : Video RAM area
000c0000-00c7ffff : Video ROM
000f0000-00ffff : System ROM
001d0000-007ffff : tulip
00100000-00291ba8 : Kernel code
002919a0-002e09fc : Kernel data
e0000ffff-e3ffff : tulip, Inc. VT82C597 (Apollo VP3)
e04000000-ffff : PCI Bus #01
e44000000-e403ffff : Matrix Graphics, Inc. MGA G200 AG
e05000000-5ffff : Matrix Graphics, Inc. MGA G200 AG
e08000000-ffff : PCI Bus #01
e08000000-ffff : Matrix Graphics, Inc. MGA G200 AG
e0a000000-a007ffff : Equipment Corporation DECchip 21140 [FasterNet]
e0a000000-ffff : tulip
ffffffff-ffff : reserved
```

The first column displays the memory registers used by each of the different types of memory. The second column lists the kind of memory located within those registers. In particular, this column displays which memory registers are used by the kernel within the system RAM or, if the network interface card handles Ethernet ports, the memory registers assigned for each port.

# 5.2.11. /proc/ioports

The output of /proc/ioports provides a list of currently registered port regions used for input or output communication with a device. This file can be quite long, with a beginning similar to this:

```
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
0aa0-0aaf : pic2
00c0-00cf : dma2
00f0-00ff : fpu
0170-0177 : ide1
01f0-01f7 : ide0
02f8-02ff : serial (auto)
0376-0376 : idei
03c0-036f : vaga
03f6-03f6 : ide0
03f8-03ff : serial (auto)
```