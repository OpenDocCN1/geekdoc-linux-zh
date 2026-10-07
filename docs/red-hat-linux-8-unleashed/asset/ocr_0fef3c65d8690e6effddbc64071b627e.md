# Configuring, Installing, and Using VMware

VMware supports a number of operating systems, including DOS, Windows 3.1, 9X, ME, NT, 2000 Professional, Server, and Advanced Server editions), XP (Home and Professional Editions), Linux, FreeBSD. VMware also offers experimental support for Windows .NET Web Server, Standard Server, Enterprise Server, VMware 6.0, and other operating systems.

![](bbox=[0.303, 0.215, 0.696, 0.513])

**Figure 27.7** The Configuration Wizard simplifies the configuration task. In this screen, selecting an operating system to install in a VMware virtual system.

> TIP
Ensure the proper CD-ROM device is used in the VMware configuration. Use the built-in editor to check. You might need to select /dev/scd0 rather than /dev/cdrom if you are using SCSI emulation for a CD writer.

**A Case of Being Too Helpful?**\If you intend to install a guest operating system by booting with a CD-ROM when using VMware, you might find Red Hat Linux will automatically mount the CD-ROM before VMware's BIOS can use the CD. To avoid this problem, don't use the daemon (which mounts devices and NFS hosts on demand) when using VMware. You can temporarily turn off this before starting a VMware session by executing /etc/rc.init.d/amd stop as root; or disable this feature entirely using the ntsysv or chconfig commands as described in Chapter 7, "Managing Services".

If you need to boot from a specific device, press F2 after using VMware's Power Button to change the virtual machine's BIOS settings. In the BIOS configuration, press the right arrow to access the BIOS Boot menu; press the plus or minus keys to reorder the virtual machine's boot devices; press F10 to save and reboot using your new settings. The new settings will be saved between VMware sessions for the configuration file.