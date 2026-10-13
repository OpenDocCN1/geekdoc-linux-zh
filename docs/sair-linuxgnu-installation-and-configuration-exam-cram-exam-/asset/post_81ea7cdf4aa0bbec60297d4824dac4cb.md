
rates, and then go back to the tool that you used to configure your video card and monitor. Make sure that the settings for both systems do not exceed the capabilities of your monitor.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_97_0.png)

> If you configure more than one graphic mode, you can normally switch between these modes with the Ctrl+Alt+Num+ or Ctrl+Alt+Num- keys. (This key combination only works with the plus and minus keys on the numeric keypad.)

## Practice Questions

### Question 1
Which of the following ways can you set up five volumes on a single hard disk?

- a. Set up five primary partitions.
- b. Set up two primary partitions, one extended partition, and three logical drives.
- c. Set up three primary partitions and two logical drives.
- d. Set up one primary partition, one extended partition, and three logical drives.

Answer b is correct. You can only set up a logical drive within an extended partition. Because you can't set up more than four primary partitions in a hard disk, answer a is incorrect. You cannot set up a logical drive without an extended partition; therefore, answer c is incorrect. Because an extended partition is not a volume, answer d is incorrect.

### Question 2
You have a computer with Microsoft Windows installed. It is set up on one primary partition. There are no other partitions or logical drives available. Which of the following steps should you take before you split this partition to accommodate Linux? [Check all correct answers]

- a. Run the fips utility to rearrange the data on your drive.
- b. Run the Windows Defrag utility to consolidate the data on your drive.
- c. Run the Windows ScanDisk utility to make sure your drive has no errors.
- d. Back up your hard disk.

Answers b, c, and d are correct. The Windows Defrag utility consolidates the data on your drive. The Windows ScanDisk utility checks for errors on your drive. Because splitting partitions can be a dangerous business, you should always back up the data on your disk. The fips utility is used to split partitions; therefore, answer a is incorrect.

### Question 3
You used the fips utility to split your partition, and then you realized that you made a mistake. Which of the following actions should you take?

- a. Back up your hard drive, and then run fips again.
- b. Run fips again, and then use the restorebr utility. Make sure that you have the rootboot.000 file that fips created and saved on your floppy drive.
- c. Use fdisk to rebuild the partitions on your hard drive. Run the restorebr utility to re-create your original partitions.
- d. Run the restorebr utility. Make sure that you have the rootboot.000 file that fips created and saved on your floppy drive. Run fips again.

Answer d is correct. Assuming you had saved your root and boot sectors, you should have a rootboot.000 file on a bootable floppy drive. You should be able to use the restorebr utility to use this file to rewrite your original root and boot information. If you made a mistake with fips, you don't want to back up the result. Therefore, answer a is incorrect. Although answer b can work, the act of using fips to split partitions again can cause more problems. Therefore, answer b is incorrect. Because the fdisk utility won't help you recover from any mistakes that you make with fips, answer c is incorrect.

### Question 4
You just logged in to the root account in Linux and used the mount /dev/cdrom /mnt/cdrom command to access the files on your CD-ROM. Assuming that the appropriate directory already exists, what is the absolute path of your CD-ROM files?

- a. root/mnt/cdrom
- b. /root/mnt/cdrom
- c. mnt/cdrom
- d. /mnt/cdrom

Answer b is correct. Absolute paths always start with the root directory, which is labeled by a simple forward slash (/). The /root directory is the home directory for the root user. Because root/mnt/cdrom is not an absolute path, answer a is incorrect. Although you could get to your CD-ROM files from your root home directory with the cd mnt/cdrom command, mnt/cdrom is still not an absolute path. Therefore, answer c is incorrect. And although /mnt/cdrom is the standard installation directory in most Linux distributions, it does not correspond to the command in the question. Therefore, answer d is incorrect.

### Question 5
Your friend plans to install Linux as a networked system for a dozen users in her small business. She might extend this system to run the business Web site, which would involve increasingly large log files to track users' buying habits. Little growth in personnel is expected, and she wants to limit the space dedicated to her users' personal files. She also plans to upgrade Linux fairly frequently and does not want to have to reload key applications, such as Star Office. Which of the following procedures is best for her situation? Hint: When you evaluate these answers, don't forget the needs of the swap disk. And each computer includes only one physical hard drive.

- a. Divide the hard disk into a combination of primary partitions and logical drives. Make sure that the /opt, /var, /home, and / directories are mounted on different volumes.
- b. Divide the hard disk into volumes composed of several primary partitions. Make sure that the /opt, /var, /home, and / directories are mounted on different volumes.
- c. Divide the hard disk into several separate volumes. Make sure that the /bin, /usr/bin, and /boot directories are each mounted on individual volumes.
- d. None of the above.

Answer a is correct. You need the /opt directory on a separate volume to save your applications when you upgrade Linux. You need the /var directory on a separate volume so log files from the Web site don't overwhelm your computer. You need the /home directory on a separate volume if you want to limit the amount of space taken by each user's personal files. Any directory not part of a separate volume is automatically installed in the root directory's (/) volume. With the swap disk, this option requires five different volumes. Because you can't have more than four primary partitions, answer b is incorrect. And because the directories listed in answer c don't meet any of the requirements listed in the question, it is also incorrect.

### Question 6
Which of the following drivers is definitely not associated with a CD-ROM drive?

- a. /dev/sdd
- b. /dev/sbpcd
- c. /dev/hdb
- d. /dev/hda3

Answer d is correct. It is actually the third primary partition on the first regular hard disk. CD-ROMs are generally not split into separate volumes. The /dev/sdd driver is for the fourth SCSI drive. Because it does not list a volume number, it may be a CD-ROM drive. Therefore, answer a is incorrect. The /dev/sbpcd driver is the CD-ROM attachment to an older Sound Blaster card; therefore, answer b is incorrect. Because the /dev/hdb drive is a common device for a CD-ROM on a computer that also has a regular hard disk, answer c is incorrect.

### Question 7
Which of the following file systems is not "real"?

- a. /bin
- b. /opt
- c. /root
- d. /proc

Answer d is correct. The /proc file system does not list any actual files. Instead, it lists currently running programs and kernel routines. The /bin file system includes many standard Linux utilities, so answer a is incorrect. The /opt file system is where many applications are installed, so answer b is incorrect. Because the /root file system is the home directory for the root user, answer c is incorrect.

### Question 8
Which of the following programs can you use to manage the configuration of your monitor and video card on most any Linux distribution?

- a. XF86config
- b. XF86Setup
- c. xf86setup
- d. XConfigurator

Answer b is correct. The XF86Setup tool is the product of the XFree86 group, which can help you configure your monitor and video card. Although there is an xf86config tool, you can't access it from the command line by typing "XF86config". Because Linux commands are case sensitive, answer a is incorrect. For similar reasons, there is no xf86setup tool. Therefore, answer c is incorrect. The XConfigurator tool is currently available only in Red Hat Linux, so answer d is incorrect.

### Question 9
Which of the following answers affect memory requirements when you configure your video card in Linux? [Check all correct answers]

- a. Horizontal frequency
- b. Resolution
- c. Number of colors
- d. Monitor size

Answers b and c are correct. The resolution is an expression of the number of pixels that your video card can show on your screen. Each color that you add requires additional data. It takes more data to fill more pixels and colors. Although the horizontal frequency tends to increase with a higher graphic mode and number of colors, it is not a reason that your video card needs more memory. Therefore, answer a is incorrect. Although the size of your monitor is normally associated with more pixels, some larger monitors simply have larger pixels. Therefore, the monitor does not change the graphic mode that you set for your video card, and answer d is incorrect.
