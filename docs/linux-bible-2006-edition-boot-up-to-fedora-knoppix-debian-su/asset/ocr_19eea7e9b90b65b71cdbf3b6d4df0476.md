# Chapter 16 + Running Mandriva 433

Wi-Fi network adapters, USB 2.0, and other hardware make your chances of install- and configuration success very high.

If you want to make sure your hardware is supported by Mandriva, go to www.mandrivelux.com/en/hardware.php and use the search tool to find if your hardware is on the list. The site also includes suggestions for what to do if your hardware is not on the supported/tested devices list. Hardriva is sorted into four categories: Not Supported, Known (reported working), Tested, and Certified.

This installation requires no special hard configuration. As mentioned, this install assumes a preexisting Microsoft Windows operating system using the NTFS file system. You will make "room" on the existing partition and install Mandriva there. In addition to using a boot disk (as you will here), you can take advantage of the installation options such as FTP and NFS as outlined in this chapter and more detail in Chapter 7.

Do not make your first installation attempt on a mission-critical system. Resizing an NTFS partition can have unintended effects. Back up any information you can live without, especially if you resize existing partitions with the following instructions show.

# Begin the DrakX Installation

You have a PC that can handle Mandriva, and you have your installation CDs; it is time to begin. Installation time varies based on how fast your hardware is and how big a partition you choose to resize. On a system with a PII800, 512MB of RAM, 30GB IDE hard disk, 40X CD-ROM, and an existing NTFS partition with Microsoft Windows (2000 Server SP4), the installation takes approximately 30 to 40 minutes. Here's what to do:

+   1. Back up all your virtual information.
2. With all your CDs ready to go (from the retail box set or your downloaded images), insert CD and start your computer. If the BIOS didn't catch the CD and boot from it, press Ctrl+Alt+Delete to restart. If it does not boot to the DrakX installation, make sure that your BIOS is configured to boot the CD first, and then restart.

If you don't see the installation screen, your CD-ROM drive may not be bootable. You may be able to make the drive bootable, Here's how: Restart the computer, immediately when you see a message to go into setup, by pressing the F1, F2, or Del key. Enter and look for an option as Boot Options or Boot From. If the value is A: First, Then C:, change it to CD-ROM First, Then C: or something similar. Save the changes and try to install again.