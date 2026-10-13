Another way to check is to look at your OpenLinux system log, a file named messages found under the /var/log directory. Use the less pager, followed by the pathname to the file, like this:

```
```
# less /var/log/messages
..
Mar 23 22:20:32 noname kernel: Linux PCMCIA Card Services 3.0.9
Mar 23 22:20:32 noname kernel: kernel build: 2.2.3 #1 Tue Mar 9
05:22:33 MET 1999
Mar 23 22:20:32 noname kernel: options: {pci} [cardbus]
Mar 23 22:20:32 noname kernel: Intel PCIC probe:
Mar 23 22:20:32 noname kernel: TI 1131 PCI-to-CardBus at bus 0
slot 10, mem 0x60000000, 2 sockets
Mar 23 22:20:32 noname kernel: host opts [0]: [ring] [pci +
serial irq] [no pci irq] [lat 168/176] [bus 32/34]
Mar 23 22:20:32 noname kernel: host opts [1]: [ring] [pci +
serial irq] [no pci irq] [lat 168/176] [bus 35/37]
Mar 23 22:20:32 noname kernel: ISA irqs (scanned) = 3,4,7,9 status
change on irq 9
Mar 23 22:20:32 noname cardmgr[991]: starting, version is 3.0.9
Mar 23 22:20:32 noname cardmgr[991]: watching 2 sockets
Mar 23 22:20:32 noname kernel: cs: 10 port probe 0x1000-0x17ff: clean.
Mar 23 22:20:32 noname kernel: cs: 10 port probe 0x0100-0x04ff: excluding
0x330-0x337 0x378-0x37f 0x388-0x38f 0x408-0x40f 0x4d0-0x4df 0x4d0-0x4d7
Mar 23 22:20:32 noname kernel: cs: 10 port probe 0x0a00-0x0aff: clean.
Mar 23 22:20:33 noname cardmgr[991]: initializing socket 0
Mar 23 22:20:33 noname kernel: cs: memory probe 0xa0000000-0xa0ffffff:
clean.
Mar 23 22:20:33 noname cardmgr[991]: socket 0: Linksys EtherFast 10/100
Fast
Ethernet
Mar 23 22:20:33 noname cardmgr[991]: executing: 'insmod
/lib/modules/2.2.3/net/8390.o'
Mar 23 22:20:33 noname cardmgr[991]: executing: 'modprobe net/8390'
Mar 23 22:20:33 noname cardmgr[991]: executing: 'insmod
/lib/modules/2.2.3/pcmcia/pcnet_cs.o'
Mar 23 22:20:33 noname kernel: eth0: NE2000 Compatible: port 0x300, irq 3,
hw_addr 00:E0:98:04:AA:D5
Mar 23 22:20:33 noname cardmgr[991]: executing: './network start eth0'
Mar 23 22:20:33 noname cardmgr[991]: + eth0: configuration file not found.
Mar 23 22:20:33 noname cardmgr[991]: start cmd exited with status 1
Mar 23 22:20:33 noname cardmgr[991]: exiting
..
```
```

Not all the output is shown here, but you can see that additional information, such as the model of your recognized card (in this case a Linksys EtherFast 10/100 card), is shown. Looking at your system's log is also a good way to diagnose other problems.