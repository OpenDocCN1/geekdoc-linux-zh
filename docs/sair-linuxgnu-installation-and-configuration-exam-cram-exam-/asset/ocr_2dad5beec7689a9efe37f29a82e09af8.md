# Question 2

You have a computer with a dual boot configuration. In other words, both Linux and Microsoft Windows are installed. For some reason, you don't see any LILO boot prompt when you boot your computer, and your system locks up when you try to boot. You suspect that your MBR is corrupt or missing. Which of the following options would restore your MBR?

+   - a. Boot Linux into single-user mode. Use the `/sbin/lilo` command to restore the contents of the lilo.conf file to your MBR.
+   - b. Start your computer with an MS-DOS boot disk. Use the `fdisk /mbr` command to restore generic settings to your MBR.
+   - c. Start your computer with any Linux installation CD. Go into restore or recovery mode. Access the lilo.conf file on your hard drive. Use the `/sbin/lilo` command to restore the contents of the lilo.conf file to your MBR.
+   - d. Start your computer with a Linux boot disk. Access the lilo.conf file on your hard drive. Use the `/sbin/lilo` command to restore the contents of the lilo.conf file to your MBR.

Answer d is correct. These steps would restore the contents of your original lilo.conf file to your MBR. Because you aren't getting a LILO boot prompt, you can't go into single-user mode normally. Therefore, answer a is incorrect. Because the MS-DOS `fdisk /mbr` command installs an MS-DOS MBR, you then would not be able to access Linux. Therefore, answer b is incorrect. Although some Linux installation CDs do have a restore or recovery mode, this is not true of all installation CDs. Therefore, answer c is incorrect.