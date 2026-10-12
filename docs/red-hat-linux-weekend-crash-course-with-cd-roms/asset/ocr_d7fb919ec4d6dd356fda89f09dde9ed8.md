Loader — does not work. The Create boot disk button is selected by default and you should leave it that way. Later on, the installation program prompts you to insert a blank floppy into your PC’s A: drive.

You can use the next button, labeled Do not install LILO, to turn off LILO installation. If you choose not to install LILO, you should definitely create a boot disk. Otherwise, you can’t start Red Hat Linux when you reboot the PC.

The next part of the LILO Configuration screen gives you the option to install LILO in one of two locations:

+   - Master Boot Record (MBR), which is located in the first sector of your PC’s hard disk (the C: drive)
+   - First sector of the partition where you loaded Red Hat Linux

You should install LILO in the MBR, unless you are using another operating system loader such as System Commander or OS/2 Boot Manager. The screen includes a text field labeled Kernel parameters that enables you to enter any special options that Red Hat Linux may need as it boots. Your need for special options depends on what hardware you have. On my PC, I have a 3Com 3C503 Ethernet card that is connected to the local Ethernet using an external transceiver. When Red Hat Linux loads the driver software for the 3Com 3C503 card, I need to specify the option xcvr=1 to make sure that the driver uses the external transceiver. I enter that option on the Kernel parameters text field.

The remainder of the LILO Configuration screen gives you the option to select the disk partition from which you want to boot the PC. A table then lists the Linux partition and any other partitions that may contain another operating system. If your system has a Linux partition and a DOS partition (that actually has Windows 95/98 installed on it), the table shows both of these entries. Each entry in that table is an operating system that LILO can boot.

After you install LILO, whenever your PC boots from the hard disk, LILO runs and displays a boot: prompt. At the prompt, you may type the name of an operating system to boot. (The Boot label column in the table in the bottom right section of Figure 3-1 shows the names you may enter at the LILO prompt). If the list shows two entries labeled linux and dos, type linux to boot Linux and dos to boot from the DOS partition (which should start Windows 95/98, if that’s what you have installed on that partition). If you press tab at the LILO prompt, LILO displays the boot labels.

When rebooting the PC, if you enter nothing at the LILO prompt, LILO waits for a few seconds and boots the default operating system. The default operating system is the one with a check mark in the Default column in Figure 3-1. In this case, Linux is the default operating system.