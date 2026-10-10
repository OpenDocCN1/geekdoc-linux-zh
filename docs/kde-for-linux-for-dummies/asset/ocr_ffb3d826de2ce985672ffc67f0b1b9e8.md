# Chapter 13: It May Look Different, but It’s Still Linux

![](bbox=[0.05, 0.28, 0.18, 0.42])

The advantages outweigh the inconveniences, though. With the mounting method, you have greater control over the file systems. If there appears to be a problem with your floppy drive, such as signs of corruption, you can just unmount the file system and work on the problem without compromising your main system. You also have the ability to mount file systems from remote machines and work with them just like they were part of your own computer. This is done using the Network File System, or NFS.

If you’re interested in the possibilities of remote file sharing across a network, but you’re the only Linux fan in a roomful of Windows users, take a look at a nifty program called Samba. Samba allows you to share file systems across a mixed-OS network composed of Linux and Windows machines; much of this book was written across a Samba network. Windows 98 Networking shares some features with the Linux implementation of NFS; after you have the network set up, both the Windows machines and the Linux machines can use file systems on all the machines in the network.

True to form, KDE gives you a specialized tool that makes the mounting and unmounting of file systems a snap.

+   1. Log in as root.
+      If you’re logged in to your user account, you can either log out and log in again as root, or you can use the KFM superuser mode described in the “Using KFM as the superuser” section of this chapter.

+   2. Open the KDE menu and choose System->KDiskFree.
+      The KDiskFree screen appears. If you’ve looked at Chapter 14, you’ll remember KDiskFree as a helpful tool to assess the fullness of your drive, but it’s also a useful mounting tool if you’re logged in as root.

The KDiskFree screen displays the various file systems available on your computer. If the file system is already mounted, it is black and clickable. If the file system is available but unmounted, it is greyed out.

+   3. Click the icon of the file system you want to mount or unmount.
+      KDiskFree displays a message and then mounts or unmounts, as you selected.

+   4. Choose File->Exit after you have finished.

# Keeping Your Privacy Intact

Linux is a multiuser system, even if you’re the only user. One of the problems that arises from the capability to set up accounts is the issue of security and privacy. Think about it: When you log in to your Internet provider to check your mail, or you save a document to your hard drive, or you visit sites on the Web that give you cookies, that information is stored in your user account files.