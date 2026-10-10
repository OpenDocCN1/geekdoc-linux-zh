# CHAPTER 2
Installing FreeBSD

Before you can use FreeBSD, you need to install it on your system's hard disk. This is a relatively painless process, and you shouldn't have any problems if you follow the directions in this chapter carefully. Depending on how fast your system and your CD-ROM drive run, the installation process will take anywhere from about 20 minutes to an hour or more. Most of this time is spent copying files, so you will not always have to sit in front of your computer.

I strongly suggest that you read this entire chapter before beginning the install. Mistakes in the install can result in losing some or possibly even all the existing data on your hard disk. Poor planning can also result in an install that has to be redone because the decisions you made don't work for the environment in which you will use FreeBSD. Read this whole chapter (and also Chapter 3, "Advanced Installation Issues," if necessary) before beginning the install. The information in these chapters will help you make the best decisions possible during the installation, because you will know what to expect.

> **CAUTION**
> Make sure to pick a time to do the installation when you will not be distracted. You will be performing actions during the installation that are potentially hazardous to existing data on your system if you make mistakes.

> **TIP**
> Now is a good time to look over the hardware compatibility list in Appendix B, "Hardware Compatibility Lists," to make sure your hardware is supported. You won't want to continue the install if you find out a key piece of hardware in your system is not supported by FreeBSD.

+   IN THIS CHAPTER
+   
+   * Checking Your Hardware
+   * Creating Boot Disks
+   * Booting into the Install Program
+   * Navigating the Sysinstall Program
+   * Creating Partitions and Assigning Mounting Points
+   * Selecting a Canned Distribution Set
+   * Choosing the Installation Media
+   * Post-installation Configuration and Customization
+   * Exiting the Install Program and Rebooting the System
+   * Booting FreeBSD for the First Time
+   * Shutting Down FreeBSD