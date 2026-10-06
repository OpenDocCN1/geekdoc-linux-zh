# 774 Linux Administration: A Beginner's Guide

In Chapter 2, we explained the installation process of Fedora and Ubuntu Linux distributions and assumed that you would use either optical media (CDs and DVDs) or flash/USB media. However, we didn't go into details about how to actually create a bootable install on either optical media or a flash/USB-based device. Because flash media often aren handy when you need them and can get scratched or go missing, this appendix presents some methods for quickly creating a Linux distributor install on inexpensive and readily available and reusable flash-based media. Flash/USB-based media include the various types of USB sticks, SD cards, Micro-SD cards, and so on.

# Creating a Linux Installer on Flash/USB Devices (via Linux OS)

Here's what you need:

+   - A system that can boot from a flash-based device
- A target flash-based device (at least 4GB in size)
- An ISO or other image of your Linux distro of choice
- A system running any Linux-based operating system (Fedora, Ubuntu, openSUSE, RHEL, CentOS, and so on)

And these are the steps to follow:

+   1. While logged into a terminal or shell prompt of your Linux distro as a user with Administrative privileges (for example, root), change to a directory on the file system with sufficient free space (use the df -sh command to check that there is space available). We'll use the /tmp folder in this example. Typen# cd /tmp
2. Download an ISO file of the Linux distribution onto an area on your file system with sufficient free space. For example, you can download the latest 64-bit Server version of Fedora from the project web site at https://fedoraproject.org (or https://getfedora.org) by typingn# wget https://<URL>/Fedora-Server-DVD-x86_64-<VERSION>.iso
where<URL> is the full path to the directory on the download server (for example, dl.fedoraproject.org/pub/fedora/linux/releases/<VERSION>/Server/x86_64/iso/).