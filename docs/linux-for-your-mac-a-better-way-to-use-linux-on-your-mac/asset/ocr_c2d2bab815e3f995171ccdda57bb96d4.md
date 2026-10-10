> There are additional arguments, such as `mkfr` (for controlling the video clock) and `pil`, which are not documented (except in the Linux kernel source). The Linux kernel recognizes many different arguments. Different video drivers (such as Matrox) can recognize more than 40!

If you click on the BootX Options button, you see a dialog box, as shown in Figure 4.2. Use this dialog box to enable cache on G3 PowerPC Macs, force the use of SCSI, force video settings, or select a RAMdisk image (only required during a Linux install—which may be discarded afterwards). When finished, click OK or Cancel to return to the main dialog box. Use Cmd+s to save your BootX preferences at any time.

When you turn on your Power Mac, BootX appears shortly after the initial Mac OS dialog box. You have about 10 seconds to choose either the Mac OS or Linux.

# ### Configuring Yaboot

Yaboot, like BootX, is a bootloader for PPC Linux. This is the preferred bootloader to use with NewWorld Power Macs, and is relatively easy to configure. You will need to know the partition number of your root Linux partition, along with any desired kernel arguments. This loader, also by Ben Herrenschmidt, attempts to boot Linux using Apple’s Open Firmware. If Yaboot is properly configured, it does not require the use of the Open Firmware prompt (accessed by holding down the Opt+Cmd+o+f keys at startup).

The basic approach to using this bootloader is to create a small, separate Mac OS HFS volume to hold a pseudo-System Folder, Finder, Yaboot, a PPC Linux kernel, and Yaboot’s configuration file named `yaboot.conf` (see Figure 4.3).

![](bbox=[0.09, 0.82, 0.79, 0.94])