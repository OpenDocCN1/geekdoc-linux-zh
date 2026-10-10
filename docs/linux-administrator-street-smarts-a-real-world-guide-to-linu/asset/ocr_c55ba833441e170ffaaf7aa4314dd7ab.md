**TABLE 2.2** Common Linux Devices (*continued*)

| Linux Device | Windows Name | Typical IRQ | I/O Address |
| :--- | :--- | :--- | :--- |
| /dev/ttyS2 | COM3 | 4 | 0x03e8 |
| /dev/ttyS3 | COM4 | 3 | 0x02e8 |
| /dev/lp0 | LPT1 | 7 | 0x0378-0x037f |
| /dev/lp1 | LPT2 | 5 | 0x0278-0x027f |
| /dev/fd0 | A: | 6 | 0x03f0-0x03f7 |
| /dev/fd1 | B: | 10 | 0x0370-0x0377 |

# ## Checking DMA Channels

*Direct memory addressing (DMA)* is an alternative method of communication to I/O ports. Rather than have the CPU mediate the transfer of data between a device and memory, DMA permits the device to transfer data directly, without the CPU's attention. The result can be lower CPU requirements for I/O activity, which can improve overall system performance.

To support DMA, the x86 and x86-64 architectures implement several DMA channels, each of which can be used by a particular device. To learn what DMA channels are in use on your system, examine the `/proc/dma` file:

```
$ cat /proc/dma
 3: parport0
 4: cascade
```

This output indicates that DMA channels 3 and 4 are in use. As with IRQs and I/O ports, DMA channels should not normally be shared. In practice, DMA channel conflicts are rarer than IRQ conflicts, so chances are you won't run into problems. Copy or print the contents of `/proc/dma` on your system to preserve a record of this information.

# ## Checking Hard Disk Data

The `/proc` filesystem provides a way to learn about your PATA hard drives: the `/proc/ide` directory tree. This directory contains several subdirectories, but the simplest way to get at the data you want is to use the symbolic links that are named after your hard drives, such as `/proc/ide/hda` for the master drive on the primary controller or `/proc/ide/hdd` for the slave drive on the secondary controller. These symbolic links point to directories that contain several files each, such as `model` (the hard drive's model number), `settings` (many low-level settings), `capacity` (the drive's size in 512-byte blocks), and `driver` (the name and