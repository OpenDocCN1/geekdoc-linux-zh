+   1. Verify that the system hardware is supported. For a SPARC system, see the *Solaris 8 Sun Platform Guide*. For an Intel-compatible system, see the *Solaris 8 (Intel Platform Edition) Hardware Compatibility List*.
+   2. If the system is networked (will be attached to a network), decide whether Dynamic Host Configuration Protocol (DHCP) will be used. If not, determine the hostname, IP address, and subnet mask information.
+   3. Determine the domain name. If a name service is used, determine the server hostname and IP address. The name service choices are Domain Name System (DNS), Network Information Service (NIS), or Network Information Service Plus (NIS+).
+   4. Determine the disk space required by selecting a software group (End-User, Developer, Entire Distribution, or Entire Distribution Plus OEM) and identifying additional software and space for home directories.
+   5. Determine the language used to install Solaris.
+   6. Insert the appropriate Solaris 8 Installation CD-ROM (English or Multilingual) into the CD-ROM drive. For Intel-compatible systems that cannot boot from the CD-ROM drive, insert the Solaris 8 Device Configuration Assistant floppy disk in the floppy disk drive.
+   7. Boot the system by turning the power on.
+   8. For Intel-compatible systems, the Device Configuration Assistant runs to identify the hardware configuration.
+   9. If you’re using the Multilingual CD-ROM, the Web Start Installer prompts you for the language to use during the install. Select the appropriate language.
+   10. For SPARC platforms, the Installer prompts you to select Initial Install or Upgrade. Select Initial Install.
+   11. For Intel-compatible platforms, if an appropriate partition for Solaris is not located, a utility similar to the MS-DOS FDISK program executes to define a partition.
+   12. The Installer prompts you to confirm reformatting of the default disk, requests a size for the swap space, and confirms that the swap space can be located at the beginning of the disk (or prompts for a starting location if the swap space can’t be located). The Installer copies the miniroot and platform-specific files to the disk and then reboots the system.