# Installing CentOS

If you are using CentOS as a desktop system, you probably don't need a lot of different partitions within your Linux system. There are, however, some very good reasons for having multiple partitions for Linux systems that are shared by a lot of users or are public Web Servers or File servers. Multiple partitions within CentOS offer these advantages:

+   **Protection from Attacks** — Denial-of-service attacks sometimes take action that tries to fill up your hard disk. If public areas, such as /var, are on separate partitions, a successful attack can fill up a partition without shutting down the whole computer. Because /var is the default location for Web and FTP servers, and therefore might hold a lot of data, often entire hard disks are assigned to the /var file system alone.

+   **Protection from Corrupted File Systems** — If you have only one file system (//), corruption of that file system can cause the whole CentOS system to be damaged. Corruption of a smaller partition can be easier to correct and can often allow the computer to stay in service while the corruption is fixed.

Here are some directories that you may want to consider making into separate file system partitions:

+   **/boot** — Sometimes the BIOS in older PCs can access only the first 1,024 cylinders of your hard disk. To make sure that the information in your /boot directory is accessible to the BIOS, create a separate disk partition (of only about 100 MB) for /boot and make sure that it exists before cylinder 1,024. Then, the rest of your Linux system can exist outside of the 1,024-cylinder boundary if you like. Even with several boot images, there is rarely a reason for /boot to be larger than 100 MB. For newer hard disks, there can sometimes avoid this problem by selecting the “Linux Mode” checkbox during installation. Then the boot partition can be anywhere on the disk.

+   **/usr** — This directory structure contains most of the applications and utilities available to CentOS or RHEL users. Having /usr on a separate partition lets you mount that file system as Read Only after the operating system has been installed. This prevents attackers from replacing or removing important system applications with their own versions that may cause security problems. A separate /usr partition is also useful if you have diskless workstations on your local network. Using NFS, you can share /usr over the network with those workstations.

+   **/var** — Your FTP (var/ftp) and Web Server (var/www) directories are, by default, stored under /var. Having a separate /var partition can prevent an attack on those facilities from corrupting or filling up your entire hard disk.

+   **/home** — Because your user account directories are located in this directory, having a separate /home account can prevent an indiscriminate user from filling up the entire hard disk. (Disk quotas represent another way of controlling disk use. See Chapter 9.) Also, some people have a /home file system on a separate hard disk so they can reinstall the operating system, erasing the root (//) partition, and simply remounting the /home partition.

+   **/tmp** — Protecting /tmp from the rest of the hard disk by placing it on a separate partition can ensure that applications that need to write to temporary files in /tmp are able to complete their processing, even if the rest of the disk fills up.