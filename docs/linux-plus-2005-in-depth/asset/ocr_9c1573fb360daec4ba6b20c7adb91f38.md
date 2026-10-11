# TROUBLESHOOTING INSTALLATION

```
LowTotal:      257108 kB
LowFree:        10116 kB
SwapTotal:      525160 kB
SwapFree:       513032 kB
Dirty:          4 kB
Writeback:      0 kB
Mapped:         153736 kB
Slab:           40856 kB
Committed_AS:   279444 kB
PageTables:     2708 kB
VmAllocTotal:   3874808 kB
VmAllocUsed:    37772 kB
VmAllocChunk:   3836956 kB
HugePages_Total:  0
HugePages_Free:    0
Hugepagesize:   4096 kB
[root@server1 root]#
```

In the preceding output, the total amount of memory (MemTotal) is 257108KB or 256MB. If this value is incorrect because the computer has 512MB of RAM, you can specify the correct values to the kernel by adding "mem=512M" to the kernel line in the /boot/grub/grub.conf file if your boot loader is GRUB or by adding the line append "mem=512M" to the /etc/lilo.conf file if your boot loader is LILO.

Likewise, to ensure that the IRQs, DMAs, and I/O ports are recognized at the correct values, you could view the dma, interrupts, and ioports files in the /proc directory as shown in the following examples:

```
[root@server1 root]#  cat /proc/dma

4:  cascade

[root@server1 root]#  cat /proc/interrupts

                          CPU0
0:  10934177      XT-PIC  timer
1:      23045      XT-PIC  i8042
2:          0      XT-PIC  cascade
5:          0      XT-PIC  Ensoniq AudioPCI
8:          1      XT-PIC
9:          0      XT-PIC  uhci_hcd, uhci_hcd
10:    232095      XT-PIC  eth0
11:    926055      XT-PIC  acpi, r81280PCI:1:0:0
12:     445114      XT-PIC  i8042
14:    153741      XT-PIC  ide0
15:    110933      XT-PIC  ide1
NMI:          0
ERR:          0
```