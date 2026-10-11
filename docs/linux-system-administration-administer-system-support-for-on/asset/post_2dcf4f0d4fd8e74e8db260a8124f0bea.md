
![](img/8ad518fddafc7f5e73715a2604b61d50_200_0.png)

Figure 6-2: Main Xconfig screen

> If you don't have X currently working on your Linux system (for reasons such as the wrong drivers, configuration problems, or a nonstandard video card), use `make menuconfig`. It's much nicer to use than `make config`. If you try to use `make xconfig` without running X, `make xconfig` won't work.

The Main Xconfig screen gives you 14 configuring options. I'll walk through each one, demonstrating the reconfiguration process for my Slackware Linux kernel at home.

- 1. Code maturity level options – Do you want to use developmental code? In other words, do you want to be a software tester for experimental drivers or do you want to use items you know work? This will be a built-in feature of the kernel; you cannot make this a module. I did not enable this because I don't want to beta-test some newer drivers at this time. Figure 6-3 shows the code maturity level options window.

![](img/8ad518fddafc7f5e73715a2604b61d50_201_0.png)

Figure 6-3: Code maturity level options

If you aren't sure what a particular option for the kernel is used for, click help. This is a really great feature if you aren't really sure if you want to compile something into your kernel or not. You should get a detailed message such as the one shown in Figure 6-3.

- 2. Loadable module support – Turn this on to use modules (loadable portions of the kernel). You don't necessarily need to use modules; however, as the kernel development heads more in the direction of modules instead of built-in support, you may want to experiment with this option. If you have already activated loadable module support, you may also want to specify the autoloading of modules – after all, such convenience does seem to be why they exist – although you can certainly load them by hand if you wish. Because I use the Zip drive and it's not always attached, I compiled loadable module support with autoload in my kernel. The loadable module is shown in Figure 6-4.

![](img/8ad518fddafc7f5e73715a2604b61d50_201_1.png)

Figure 6-4: Loadable module options

- 3. General setup – General setup is the basic hardware setup for the system you installed Slackware on. Unless you're working on a 486 or earlier hardware, you don't want to enable math emulation. Turn on PCI Bios, networking support, and kernel support (at least for the ELF binaries). You'll also want to compile your kernel as ELF. I included both a.out and ELF binary support for my kernel, enabled networking and IPC support. The other options include the processor type, memory options, and other general things you may or may not want running on your system. I left alone. The General Setup is shown in Figure 6-5.

![](img/8ad518fddafc7f5e73715a2604b61d50_202_0.png)

Figure 6-5: General setup options

- 4. Floppy, IDE, and other block devices — This set of options helps you set up any type of disk support. It includes IDE/ATAPI, shown enabled here because that’s what my motherboard supports. This also includes old XT hard drives, SCSI emulation, and other hard drive support including the older IDE drives. Because I have a Pentium with IDE and not SCSI, I would definitely include the IDE/ATAPI drive support. However, I do know that my floppy drive is not IDE (as most $20 3.5 floppy drives aren’t), so I don’t include this as part of the kernel. Examples of options are shown in Figure 6-6.

![](img/8ad518fddafc7f5e73715a2604b61d50_202_1.png)

Figure 6-6: Floppy drive options

- 5. Networking options – If you want to have TCP/IP, IPX, AppleTalk, or other protocols defined, have them built into the kernel. Also, if your Slackware host is a firewall or router, you can compile the options you need in this area. This also includes IP masquerading (hiding invalid IP addresses behind one IP address), IP multicasting, and IP forwarding. You can also compile additional packet logging support for firewalls here as well. Because my host is going to be a firewall, I’ve compiled these options. Unless you have two network interface cards and you’re not doing routing, you probably want to leave the firewall stuff alone. Even if you’re not going to be using a network interface card and you are going use PPP or SLIP instead, compile in TCP/IP networking. This defines how and what type of protocols and IP configuration, as shown in Figure 6-7.

![](img/8ad518fddafc7f5e73715a2604b61d50_203_0.png)

Figure 6-7: Networking options

- 6. SCSI support – This section is for SCSI drivers. Depending on your hardware, you’ll probably want to add SCSI support and SCSI disk support. Though I have an IDE/ATAPI drives and a PCI motherboard, I want to have SCSI support and SCSI disk support included in the kernel. The reason: I have a Zip drive. Though my Zip drive runs through the parallel port, the kernel recognizes it as a SCSI device (`/dev/sd4`). If you have SCSI drives, go farther down through the list to ensure that your hardware is supported. It’s no fun to have a 5GB hard drive you can’t use. The SCSI support options are shown in Figure 6-8.

![](img/8ad518fddafc7f5e73715a2604b61d50_204_0.png)

- 7. SCSI low-level drivers – This section is for defining specific SCSI drivers such as those for Iomega Zip drives and UltraStor drives. If you are using something that specific and you don’t need the rest of the SCSI support, it helps you keep the kernel as small as possible. As a result, the kernel will load faster. In my case, I’ll only choose the option for Iomega Zip drive support. I’ll select it as a module so I can plug it in and unload it on the fly. The SCSI low level drivers are shown in Figure 6-9.

![](img/8ad518fddafc7f5e73715a2604b61d50_204_1.png)

- 8. Network device support – Remember the TCP/IP networking (or any other type of networking) you enabled in the networking options? Here’s where you define how you’re going to access those networks. This includes Network Interface Card (NIC), PPP, SLIP, Token Ring, and portable device interface cards. In my firewall, I would enable the correct versions of the NIC that I'm using. However, if I'm using PPP on another computer, I would enable that so I can connect to my ISP. You can have multiple network interface card support and PPP at the same time. An example of the Network Device Support options is Figure 6-10.

![](img/8ad518fddafc7f5e73715a2604b61d50_205_0.png)

Figure 6-10: Network device support options

- 9. ISDN subsystem — This screen is for enabling ISDN support. ISDN is a way to have a high-speed connection to a network or the Internet. If you're not paying the extra money for it, or if work's not giving you access to ISDN, you don't have it. Skip over this and move on to the next section. Figure 6-11 shows an ISDN support screen.

![](img/8ad518fddafc7f5e73715a2604b61d50_205_1.png)

Figure 6-11: ISDN subsystem options

- 10. CD-ROM drivers (not for SCSI or IDE/ATAPI drives) – This set of options is for non-standard CD-ROM drives. There is also a CD-R listed in here, the Sanyo CDR-H94A. Unless you are using an non-IDE or non-SCSI CD-ROM, you can skip this section. Because the boot disk you create should have your appropriate CD-ROM driver for installation, you may want to use that as an idea of what type of CD-ROM drive you have. In my case, I’ll skip this section. My CD-ROM drive is mounted as the slave drive on the second controller (/dev/hdd). The CD-ROM drivers options is shown in Figure 6-12.

![](img/8ad518fddafc7f5e73715a2604b61d50_206_0.png)

Figure 6-12: Nonstandard CD-ROM support options

- 11. File systems – To me, this is the coolest part of Linux. Linux can support lots of file systems. These include FAT, VFAT, System V IPC, and quite a few other types. A few that are necessary to include: Second Extended File System support, Unicode, ISO 9660 (for CD-ROMs), MS-DOS and DOS file-system support, and Unicode support. Many people find including the Joliet (long Windows name) support very useful as well. I usually like to enable Minix (some rescue disks still use it), and /proc file system, which interfaces the kernel and processes. Additionally, if you enabled disk quotas, also enable support here. The file systems options are shown in Figure 6-13.
