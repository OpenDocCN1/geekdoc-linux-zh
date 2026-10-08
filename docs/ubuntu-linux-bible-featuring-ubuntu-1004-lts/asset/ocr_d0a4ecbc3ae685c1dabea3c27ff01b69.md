manually modify the Samba configuration file, as discussed later in the section, "Samba Server Configuration Essentials."

Interoperability between Linux and Windows systems requires much more than just Samba. While Samba provides support for networked Windows filesystems, the Linux kernel provides built-in support for the protocols to access physical Windows filesystems as FAT and NTFS, enabling Linux users to mount Windows filesystems via entries in /etc/fstab, just like any other filesystem resource.

# Note

The Ubuntu repositories provide both the current version of Samba and preliminary packages for the next version of Samba, Samba 4. This chapter focuses on the current version of Samba (Samba 3.x) because it is completely stable. Although Samba will deliver improvements in performance, power, and flexibility, it's not ready for prime-time use at the moment. Stay tuned!

# Installing the Samba Server and Friends

Samba client packages are installed by default on Ubuntu desktop systems, making it easy for any Ubuntu system to access and connect SMB/CIFS shared directories from Microsoft Windows systems or Samba servers. To install the packages required to run and monitor a Samba server so that you can share directories from your Ubuntu system, you must install the samba package using your favorite package management tool: Synaptic, Adept, or apt-get. See Chapter 19, "Adding, Removing, and Updating Software," for more detailed information on installing and using these package-management tools.

When installing the samba package, you may also want to install the samba-doc packages, which provide HTML and PDF versions, respectively, of all the official project documentation, plus PDF copies of the first edition of an entitled Samba-3 by Example: Practical Exercises in Successful Samba Deployment (Prentice Hall, 2005, ISBN:013188221X) by one of leaders of the Samba project, John H. Terstra (The first edition of this book is now GPL—newer editions are available in print).

# Samba Server Configuration Essentials

While graphical utilities for configuring Samba exist, they are in a state of flux on Ubuntu systems. Previous releases of Ubuntu included a Shared Folders tool that enabled you to identify the Linux directories that you wanted to export via NFS or Samba, but that is no longer part of Ubuntu. A tool called system-config-samba, originally developed for the Red Hat Linux distribution, is available for Ubuntu systems but doesn't provide access to all of the configuration options that you will want to use in most cases. As a graphical tool, it cannot be used on Ubuntu Server systems unless you install a window manager or desktop environment.