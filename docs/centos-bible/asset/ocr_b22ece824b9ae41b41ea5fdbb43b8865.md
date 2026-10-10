When you do the CentOS kickstart installation, **have this floppy disk with you**. As an alternative, you can copy the ks.cfg file to a hard disk partition, CD drive, Web Server, or NFS share. Being able to place the ks.cfg file on a computer on the network requires a bit more configuration. The network must have a DHCP or a BOOTP server configured that is set up to provide network information to the new install computer. The NFS server containing the ks.cfg file must export the file so that it is accessible to the computer installing Linux. To use a ks.cfg file from the local hard disk, you can place the file on any partition that is a Windows (VFAT) or Linux (ext3) partition.

# ### Booting a Kickstart Installation

If the kickstart file (ks.cfg) has been created and installed in an accessible location, you can start the kickstart installation. Here is an example of how you can do a kickstart installation using the CentOS DVD and a floppy containing a ks.cfg file:

+   1. Insert the CentOS DVD and restart the computer.
+   2. When you see the boot screen, insert the floppy containing the ks.cfg file, and type the following at the boot line:
+      ```
+      linux ks=floppy
+      ```
+      You should see messages about formatting the file system and reading the package list. The packages should install without any intervention. Next you should see a post-install message. Finally, you should see the Complete message.
+   3. Remove the floppy, then press the spacebar to restart your computer.

> **TIP** You can install using kickstart over NFS (ks=nfs:server:/path/ks.cfg), from a Web Server (ks=http://server//path/ks.cfg), or from your hard drive (ks=hd:device/ks.cfg).

# ## Special Installation Topics

Some things that you run into during installation merit whole discussions by themselves. Rather than bog down the procedures with details not everyone needs, I have included instructions in this section to address issues such as setting up a dual-boot Linux and Windows system, disk partitioning, and boot loaders.

# ### Setting up to Dual-Boot Linux and Windows

It is possible to set up your computer so that you can have two (or more) complete operating systems installed on it. When you power up your computer, you can choose which operating system you want to boot. This setup is referred to as a *dual-boot computer*.

If a Microsoft Windows operating system was installed when you got your PC, it's likely that the entire hard disk is devoted to Windows. CentOS installation procedures retain existing Windows