9. Look in the /tmp directory to see whether the spamcan file was created.

10. Enter the command mailstats to see a summary of activity for your sendmail server. Have any messages been discarded (see the msgdis column)? If not, what happened to the message addressed to spam? Log off.

![](bbox=[0.03, 0.26, 0.09, 0.38])

# Project 15-8

In this project, you create a boot disk and start your computer using it. To complete this project you must have a working Linux system with root access, a blank 3.5-inch disk, and Internet access.

+   1. Log in to Linux.
+   2. Start your Web browser using an icon on the panel or a menu item.
+   3. Enter www.toms.net/rb in the Address bar of the browser and then press Enter. The tomsrtbt Web page appears.
+   4. Click the link to download tomsrtbt.
+   5. Click on one of the mirror sites. After a moment, you see a list of files.
+   6. Click on the file tomsrtbt-2.0.103.tar.gz or whatever the latest version of the file is named. When prompted, save the file on your hard disk and note the location where you saved it. (Using /tmp is a good choice.)
+   7. Uncompress the file you just downloaded. Read the tomsrtbt.FAQ file and note the installation instructions.
+   8. Following the instructions in the tomsrtbt.FAQ file, change to the appropriate directory by entering cd /tomsrtbt, then type ./install.s at the command prompt and follow the onscreen directions to install the program.
+   9. Shut down your Linux system.
+   10. With the floppy disk inserted, restart your system. The boot disk should load the operating system and eventually display a login prompt.
+   11. Log in as root. The onscreen instructions will tell you that a password is needed and what the password is.
+   12. You are now logged in to a real Linux operating system. Feel free to explore the file system and utilities included with this single-disk version of Linux.
+   13. When you have finished experimenting, remove the 3.5-inch disk and restart the system. Your regular Linux system returns.

```
tar xvfz /tmp/tomsrtbt-2.0.103.tar.gz
```