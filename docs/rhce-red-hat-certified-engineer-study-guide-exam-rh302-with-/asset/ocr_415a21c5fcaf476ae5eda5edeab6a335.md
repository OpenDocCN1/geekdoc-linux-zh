# 124 Chapter 6 • Installation Planning

In some circumstances, additional information will be needed. But, generally, this information will be enough to let you complete the installation procedure. Once the installation procedure is complete, you can configure special options as needed.

In addition to information on the hardware of the target system, you should have available the Red Hat Linux Installation Guide and other Linux documents, particularly the HOWTOs. If necessary, you can use any Linux system or a Microsoft Windows system to read documentation stored on the documentation CD-ROM or to access Web sites and newsgroups that provide pertinent information. Having this information available will help you complete the installation procedure; otherwise, you may find it necessary to terminate the installation procedure, obtain the needed information, and then restart the installation.

# Selecting the Installation User Interface

Red Hat Linux supports two installation types: Install and Upgrade. You should choose Install when installing Linux on a target system that doesn't currently host Red Hat. Choose Upgrade when the system already hosts an earlier version of Red Hat Linux. The Upgrade procedure saves the existing configuration files, rather than overwriting them. The existing files are renamed with the extension .rpmsave.

Red Hat Linux 6.1 introduced a graphical mode installation procedure based on X. The initial screen of the installation procedure lets you choose the graphical mode installation procedure or a text mode installation procedure. Beginners generally find the graphical mode installation procedure easier to use. However, you may prefer the text mode installation for the following reasons:

+   * The graphical mode installation procedure may fail if the target system has unusual video characteristics, such as an old or uncommon video adapter.

+   * The text mode installation procedure can recover from some errors—such as running out of disk space—that cause the graphical mode installation procedure to fail.

+   * The text mode installation will run better and faster than the graphical mode installation on computers having a slow processor or a small amount of RAM.

+   * The graphical mode installation supports only media mounted as a file system, such as an existing drive partition, a CD-ROM, or media available via NFS.

Copyright©2000 SYBEX, Inc., Alameda, CA    www.sysex.com