+   • Disk Set XV—window manager for X. This disk set includes the XView libraries and the Open Look window managers. These can be used instead of the window manager included in Disk Set X.

Although Disk Set A lets you install a Linux system from a floppy, for a full installation (hard disk-based with standard utilities), you should have Disk Sets A, AP, D, and F. This collection gives you a character-based Linux system. If you want to run X, you will also need Disk Sets X and XAP. Programmers will need to load the development Disk Sets (D and XD, for X applications).

# ## Updating Existing Linux Systems

If you've already got Linux up and running, it may be time to upgrade your system. In most cases, upgrading a running system is as easy as copying the new software into a directory and rebuilding your kernel to link in your existing drivers. In some cases, upgrading the system means loading everything from scratch (usually necessary only with a major version change or a change in Linux vendor).

Most Linux versions that you buy are not intended to upgrade existing software automatically (as Windows versions do, for example). Instead, you are often expected to back up everything on your disks, install the new version, and then restore the files from your backup. Luckily, usually all you have to do is copy a few kernel files over to your existing directory structure and recompile to upgrade most kernels. We will deal with upgrading existing systems in more detail in the next chapter.

# ## Summary

In this chapter we've looked at what makes up a Linux release, where you can get Linux software, and information about the disk sets that make up Linux as a whole. Now you can get your software ready for the next step, which is installing and configuring Linux. Here's a list of chapters with related information about:

How to install Linux, see Chapter 3, “Installing Linux” and Chapter 5, “Wrapping Up the Installation.”

How to use Linux, see Part II, including Chapter 6, “Getting Started,” and Chapter 11, “bash.”

How to install and configure the X server system, see Chapter 22, “Installing and Configuring XFree86.”

System administration issues, see the chapters in Part VI including Chapter 32, “System Administration Basics.”