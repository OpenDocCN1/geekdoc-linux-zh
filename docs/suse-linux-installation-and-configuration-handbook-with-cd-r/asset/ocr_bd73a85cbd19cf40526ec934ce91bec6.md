# Setting Up Hardware

This process is rather long, so be patient. In this process you will be checking whether your sound card is configured through DIP switches/jumpers or through PnP. Most of the new sound cards are PnP, so, if you have a new sound card, it's probably PnP. Linux support for PnP devices is not performed by the kernel (2.2.x series). This does not mean that you won't be able to use your sound card, though. Thanks to the isapnptools package, you can configure your PnP devices and use them with no trouble.

# Searching for the Proper Resources

In all cases, you must search for the proper resources for the sound card. In this part you will look for available IRQs, DMA, and ports. To list the available resources, you should use the proc file system information in the /proc/interrupts, /proc/dma, and /proc/ioports virtual files.

Issue the following command to list the available free interrupts:

```
bash#cat /proc/interrupts
CPU0
0: 9780712      XT-PIC  timer
1: 61964        XT-PIC  keyboard
2: 0            XT-PIC  cascade
4: 710344       XT-PIC  serial
6: 562          XT-PIC  floppy
7: 0            XT-PIC  fdc
10: 9682        XT-PIC  eth0
13: 1           XT-PIC  fpu
14: 6119932      XT-PIC  ide0
15: 74241        XT-PIC  ide1
NMI:
```

As the command output indicates, the following IRQs are available: 3, 5, 7, 10, 11, and 12. You can use any of them for the sound card. Note that IRQ 9 and IRQ 2 are the same interrupt and are not proper IRQs for the sound card. You should not use any IRQ listed in the command output; they are already taken. You should first try the 5, 7, and 10 interrupts. This does not mean that the other IRQs cannot be used. But, it's generally preferred that sound cards use these interrupts.

> CAUTION
> 
> Some IRQs should not be used because they belong to motherboard resources. If you use any of them you will either slow down the performance of your Linux box or lock it up. These interrupts are 1, 6, 8, 13, and 14. IRQ sharing is nice, but not with those interrupts.