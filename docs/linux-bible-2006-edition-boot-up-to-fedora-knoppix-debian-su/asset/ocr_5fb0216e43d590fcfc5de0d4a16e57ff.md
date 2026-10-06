# Chapter 7 + Installing Linux 261

Protection from attacks— Denial of Service attacks sometimes takes actions that try to fill up your hard disk. If public areas, such as /var, are on separate partitions, a successful attack can fill a partition without shutting down the whole computer. Because /var is the default location for Web and FTP servers, and expected to hold a lot of data disks are often assigned to the /var file system.

Protection from corrupted file systems— If you have only one file system (/), its corruption can cause the Linux system to be damaged. Corruption of a smaller partition can be easier to fix and often allows the computer to stay in service while the correction is made.

Table 7-2 lists directories that you may want to consider making into separate file partitions.

# Table 7-2
Assigning Partitions to Particular Directories

| Directory | Explanation |
| --- | --- |
| /boot | Sometimes the BIOS in older PCs can access only the first 1,024 cylinders of your hard disk. To make sure that the information in your /boot directory is accessible to the BIOS, create a separate partition (of about 100MB) for /boot and make sure it exists below 1,024-cylinder. The rest of your Linux system can exist out of that 1024-cylinder boundary if you like. With several better images, there is rarely for /boot to be larger than 100MB. (For never harder disks, you can select the Linear Mode during installation. The boot partition can be anywhere on the disk.) |
| /usr | This directory contains many of the applications and utilities available to Fedora Linux users. Having /usr on a separate partition lets you mount file system as read-only after the operating system has been installed. This prevents attackers from replacing or removing system applications with their own versions that may cause security problems. A separate partition is also useful if you have diskless workstations on your local network. Using NFS, you can share /usr over the network with those workstations. |
| /var | Your FTP (/var/ftp) and Web-server (/var/www) directories are, by default in many Linux systems, stored under /var. Having a /var partition can prevent an attack on those facilities from corrupting or filling your hard disk. |
| /home | Because your user accounts are located in this directory, having a separate /home account can prevent a reckless user from filling up the hard disk. |
| /tmp | Protecting /tmp from the rest of the hard disk by placing it on a separate partition can ensure that applications that need to temporary files in /tmp are able to complete their processing, even if the rest of the disk fills up.