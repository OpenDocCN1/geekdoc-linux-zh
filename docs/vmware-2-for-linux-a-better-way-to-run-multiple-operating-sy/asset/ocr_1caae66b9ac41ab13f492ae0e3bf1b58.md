# Converting a DOS Virtual Machine

Unlike other operating systems you use VMware to install, most Windows 3.1 installations require a working DOS system before you can get started. This is simply the nature of Windows 3.1.

> For obvious reasons, Microsoft designed Windows 3.1 with MS-DOS in mind. Some versions of clone DOSs do not work properly with 3.1, although DR DOS 7 contains special tools for enhancing operation with Windows.

To prepare the DOS virtual machine for Windows 3.1, do the following:

+   1. In the VMware Configuration Editor, change the Guest OS setting from MS-DOS to Windows 3.1. If the VM's memory setting is less than 8MB, you should increase it to ensure a comfortable environment.
+   2. If you want sound support in Windows 3.1, you need to download the file sbbasic.exe from the SoundBlaster 16, Windows 3.1 drivers area of http://support.soundblaster.com. Transfer the file to a new directory, such as C:\sb16 on your DOS virtual disk, and run the sbbasic.exe file to extract the drivers. You will activate them later, when Windows 3.1 is running.
+   3. If you want host-only LAN networking support in Windows 3.1 (Windows for Workgroups), you need to download the Windows 3.1 NDIS2 or NDIS3 drivers for the AMD PCNet Family card from AMD's technical support site or from the /AMD NIC Drivers directory of the included CD-ROM. Unfortunately, like the DOS packet driver, the AMD archive requires Windows 95 or better to de-archive the files, so you need to use either a Windows 95 virtual machine or another computer to unpack the driver and then transfer it via floppy or network to the DOS virtual disk. Place it in a new directory, such as C:\amd31.

> It is also possible, albeit challenging, to run bridged TCP/IP networking in Windows 3.1 or 3.11 using the AMD packet driver and an extra program in the AMD Ethernet driver package, winpkt.com. You also need Trumpet WinSock from http://www.trumpet.com.au. Configuring the Windows packet driver and Trumpet WinSock is quite a task, however.