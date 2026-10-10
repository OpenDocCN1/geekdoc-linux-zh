# Using the Terminal

```
Kernel command line: block2mtl.block2mtl=/dev/hda2,131072,rootfs root=/dev/mtdbl
cOckO rootfstype=jffs2 init=/etc/preinit noinitrd console=tty0 console=ttyS0,384
00n8 reboot=biOS
Found and enabled local APIC
Enabling fast FPU save and restore... done.
Enabling unmasked SIMD FPu exception support... done.
Initializing CPU#0
PID hash table entries: 32 (order: 5, 128 bytes)
Detected 1991.657 Mhz processor.
Console: colour VGA+ 80x25
console [tty0] enabled
console [ttyS0] enabled
Dentry cache hash table entries: 1024 (order: 0, 4096 bytes)
Inode-cache hash table entries: 1024 (order: 0, 4096 bytes)
Memory: 5112k/8128k available (1497k kernel code, 2624k reserved, 597k data, 196
k init, Ok highmem)
virtual kernel memory layout:
fixmap : 0xffffb000 - 0xfffff000 (280 KB)
vmalloc : 0xc1000000 - 0xffff7000 (1007 MB)
lowmem : 0xc0000000 - 0xc07f0000 ( 7 MB)
.init : 0xc0313000 - 0xc0344000 (196 kB)
.data : 0xc027653c - 0xc030bcf0 (597 kB)
.text : 0xc0010000 - 0xc027653c (1497 kB)
Checking if this processor honors the WP bit even in supervisor mode... Ok.
Calibrating delay using timer specific routine... 4047.64 BogoMIPS (lpj=20238210)
```