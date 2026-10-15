will prompted to enter a driver disk. Drivers are needed only for devices required for installation, like CD-ROMs, SCSI adapters, and network cards. In the case of very new devices, you may need to provide your own drivers on a driver disk.

# Installing Linux

Installing Linux involves several processes, beginning with creating Linux partitions, and then loading the Linux software, configuring your X Window System interface, installing the Linux boot loader (GRUB or LILO) that will boot your system, and creating new user accounts. The installation program used on Red Hat is a screen-based program that takes you through all these processes, step by step, as one continuous procedure. You can use either your mouse or the keyboard to make selections. When you finish with a screen, click the Next button at the bottom to move to the next screen. If you need to move back to the previous screen, click Back. You can also use TAB, the arrow keys, SPACEBAR, and ENTER to make selections. The installation screens will display a help panel explaining each step in detail. You have little to do other than make selections and choose options. Some screens provide a list of options from which you make a selection. In a few cases, you are asked for information you should already have if you followed the steps earlier in this chapter. Hardware components will be automatically detected and displayed as you progress. During installation, you will be able to perform administrative tasks such as configuring your network connections, creating users, and setting the time. Keep in mind that such administrative tasks can also be performed after installation. You are now ready to begin installation. The steps for each part of the procedure are delineated in the following sections. This should not take more than an hour.

Toward the end of the installation, you will be asked to create a boot disk. Be sure to make one. The boot disk will contain specific configuration information about your systems. Should anything go wrong with your boot loader, you will still be able to boot Linux using the boot disk.

# Starting the Installation Program

You can start the installation using one of several methods. If your computer can boot from the CD-ROM, you can start the installation directly from the CD-ROM or the DVD-ROM included with this book. Just place the CD-ROM in the CD-ROM drive, or the book's DVD-ROM in the DVD drive, before you start your computer. After you turn on your computer, the installation program will start up.

> Note To boot from a CD-ROM or DVD-ROM, you may first have to change the boot sequence setting in your computer's BIOS so that the computer will try to boot first from the CD-ROM. This requires some technical ability and knowledge of how to set your motherboard's BIOS configuration.

If you have a DOS or Windows system installed on your hard drive, you can use the autoboot.bat command in the dosutils directory to start the installation, as shown here. You have to execute this command from a DOS system or a Windows DOS window.

```
e:\dosutils\autoboot.bat
```