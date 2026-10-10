shell in Chapter 4. If something goes wrong with your system, the help you will get from forums and mailing lists will almost always include commands to run from the shell.

+   - **Check non-working hardware** — If a printer, network card, or other hardware component isn’t working immediately, try tools for configuring those items under the System $\rightarrow$ Administration menu (described throughout this book). If that doesn’t work, there are a few standard places to look for information. Review the Fedora Release Notes. From the Release Notes page, look for a link to Help and Support. Visit the *Bugzilla page* (<https://bugzilla.redhat.com>) and search for the name or model number of hardware that is giving you trouble or check *Fedora’s Hardware Compatibility List* wiki at <http://fedoraproject.org/wiki/HCL>.

After you have examined these topics, you can go anywhere else in the book that interests and excites you.

The rest of this chapter is devoted to special topics relating to installing Fedora. If you’re happy with the way your Fedora system installed, you can skip to the next chapter.

# # Special Installation Procedures

If you don’t want to, or can’t, use the procedure to install Fedora from DVD or CD, the procedures in the following sections give you alternatives. The first subsection describes alternate ways of booting the installation, such as PXE or USB flash drives (if your computer doesn’t have a bootable DVD or CD drive).

After the install procedure boots, use the “Installing from other media” section that follows to learn how to install Fedora from media other than DVD or CD-ROM (using FTP, HTTP, NFS, or hard disk installs). If you want to have the installation screens appear on another computer as you install, refer to the section “Starting a VNC install.” The subsection following that describes how to do kickstart installations.

# ## Alternatives for starting installation

Your computer may not have a DVD or CD drive or may have one that is unbootable, so you need to find an alternative way to boot the install process. Although booting installation from 1.44MB floppy disks is no longer supported (the 2.6 kernel won’t fit on one), you have a few other alternatives:

+   - Boot installation from hard disk.
+   - Boot from a USB flash drive or other USB device.
+   - Do a PXE install using a preboot execution environment install server.

Procedures for starting installation in those ways are described in the following sections.

# ## Booting installation from hard disk

Booting the install process is similar to booting a regular Linux system. To start an install from your hard disk all you really need to do is: