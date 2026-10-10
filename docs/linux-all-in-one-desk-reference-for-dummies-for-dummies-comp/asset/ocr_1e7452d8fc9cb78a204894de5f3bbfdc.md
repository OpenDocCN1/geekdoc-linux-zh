+   5. **Select the keyboard layout and press Enter.**
+   
+   The installer detects hardware to find the CD-ROM drive and loads additional software from the CD. It detects the network hardware and configures it using DHCP. Then it prompts you for a host name.

+   6. **Type a host name for your system and press Enter.**
+   
+   The installer detects the hard drives and prompts you to select the disk partitioning method. If you have created space for Ubuntu on your hard drive (see the “Setting Aside Space for Linux” section in this chapter), select the option Use Largest Continuous Free Space for Ubuntu installation.

+   7. **Select the largest continuous free space and press Enter (or select existing partitions and assign them to specific mount points, such as the file system `/root`).**
+   
+   The installer installs the Ubuntu base system and asks if the system clock is set to GMT (Greenwich Mean Time). The answer is usually No. Then the installer prompts you for the time zone.

+   8. **Select your time zone and press Enter.**

+   9. **Create a user account.**
+   
+   Type the full name of the user, the username, and the password, as prompted by the installer. The installer configures APT — the Advanced Package Tool — used to download and install packages in the future.
+   
+   The installer lists all the operating systems that it finds installed on your PC’s hard drive and asks if you want to install the GRUB boot loader on the master boot record (MBR) of the hard drive.

+   10. **Select Yes and press Enter to install GRUB.**
+   
+   The installer finishes installing GRUB and then unmounts and ejects the CD. A message informs you that the first stage of installation is complete. Remove the CD and press Enter to reboot the PC.

After the PC reboots, Ubuntu downloads and installs many more packages from online repositories. (Your PC needs to be connected to the Internet for everything to work.)

![](bbox=[0.14, 0.84, 0.22, 0.95])

The X Window System and the GNOME GUI are among the packages Ubuntu downloads and installs. After these packages are installed and configured, Ubuntu starts a GUI login screen where you can log in using the user account that you defined earlier. If, for some reason, X Window System does not work, you have to troubleshoot X following the suggestions in Chapter 3 of this minibook.