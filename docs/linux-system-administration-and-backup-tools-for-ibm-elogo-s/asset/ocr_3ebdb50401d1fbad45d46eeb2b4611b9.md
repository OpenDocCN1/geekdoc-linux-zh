- Mail - Linux can give you a copy of the configuration and boot messages for every reboot. This can be more extensive than the messages from dmesg. To get access to these messages, type `mail`.

- Other tools: There are public domain utilities like Lothar that you can use to determine your hardware characteristics.

An understanding of the hardware configuration is very important because Linux allows you to have more control over your system than other operating systems. It also allows you to fix problems more quickly because information is not hidden.

You can also determine what hardware the system has by looking in the file system /proc. This file system is not a directory at all but a window into memory. It does have files and directories, but they are not saved onto the disk. You will see what the thinks exists in terms of hardware. You will also see the contents of the ones in this file system in Figure 68. In this case it is the interrupts file, which shows the interrupts that appear to be used. There are several other files and directories located here that have useful information.

```
/proc/proc
1 278 330 444 545 564 ksmg net tty
152 286 331 444 546 565 dmesg parport uptime
3 334 346 447 546 566 cpuinfo loadavg version
200 306 345 448 547 589 locs pol
211 314 365 450 549 586 dma mca rtc
219 324 445 551 587 files edisat scsi
225 325 421 466 541 594 fr meminfo selff
237 236 431 467 558 600 ide misc slabinfo
247 327 441 470 558 600 interrupts stat
257 328 442 555 569 794 ipopcs modules sweep
268 329 443 551 569 810 kcore ntr sys
# cat interrupts
CPU
0 1006623 XT-PIC timer
1 451 XT-PIC keyboard
2 XT-PIC cascade
3 1 XT-PIC rtc
8 3236 XT-PIC PNet/PCI II 7C970A
12 1209 XT-PIC PS/2 Mouse
13 XT-PIC spi
14 201594 XT-PIC ide0
15 29 XT-PIC idel
NMI 0
```

Figure 68. The contents of the /proc directory and the interrupts file