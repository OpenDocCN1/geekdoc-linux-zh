Some Linux LiveCDs, such as Puppy Linux, are designed with a minimum number of Linux system files and copy them directly into memory when the CD boots, which allows you to remove the CD from the computer as soon as Linux boots. Not only does it make your applications run much faster (because applications run faster from memory), but it frees up your CD tray for ripping audio CDs or playing video DVDs from the software included in Puppy Linux.

Other Linux LiveCDs use an alternative method that allows you to remove the CD from the tray after booting. It involves copying the core Linux files onto the Windows hard drive as a single file. After the CD boots, it looks for that file and reads the system files from it. The Ubuntu Wubi project uses this technique to move the LiveCD contents to a single file stored in the Windows drive on the PC. From there you can boot directly into Ubuntu (more on this in Chapter 2, "Playing with the LiveCD").

> A popular technique for storing data from a live Linux CD session is to use a USB Memory Stick (also called a flash drive and a thumb drive). Just about every Linux LiveCD can recognize a plugged-in USB Memory Stick (even if the stick is formatted for Windows) and read and write files from it. This capability allows you to boot a Linux LiveCD, use the Linux applications to create files, store them on your Memory Stick, then access them from your Windows applications later (or from a different computer).

# What Is Ubuntu?

Now that you've seen what's behind a Linux distribution, it's time to turn our attention to the Ubuntu Linux distribution. Even within Ubuntu, there are several features that you have to choose from before running your system. This section walks through the different versions and choices available.

# Ubuntu Versions

The Ubuntu Linux distribution is based on Debian Linux. As was discussed in the Core Linux Distributions section, the Debian distribution contains a variety of software and features. The Ubuntu developers created two subsets of the main Debian Linux system for specialized use:

+   - Ubuntu workstation
+   - Ubuntu server

The Ubuntu workstation distribution includes only the software that's most commonly used in a desktop environment:

+   - The OpenOffice.org office productivity suite
+   - The Firefox web browser software
+   - The Evolution email and calendar software
+   - Tomboy note-taking software
+   - F-spot digital image editing
+   - Totem video player
+   - Rhythmbox music player