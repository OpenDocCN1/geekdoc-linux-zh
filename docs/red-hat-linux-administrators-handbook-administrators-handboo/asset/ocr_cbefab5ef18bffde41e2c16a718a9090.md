# Using Disk Quotas for Users

Disk space on a multiuser system can be quite a scarce resource. Experience shows that as soon as you plug in a new drive with lots of space, users tend to use it up quite rapidly. So, the more you add, the more you need. The best way to ensure that you have enough disk space for your system is to enforce disk quotas. This section explains how.

# Installing disk quota software

The official Red Hat CD-ROM comes with quota software. For example, to install the quota software for an x86 machine, the following command can be run from the CD-ROM's /RedHat/RPMS directory:

```
rpm -ivh quota-version.i386.rpm
```

After the quota software is installed, you are ready to configure it.

# Configuring your system to support disk quotas

First, decide which partitions you want to bring under disk quotas. Typically, these are the partition(s) for user home directories and Web space. Also decide whether you want to enforce quotas per user, per group, or both. This discussion assumes that you want to enable disk quotas for the /home and /www partitions, and want to enforce only the per-user disk quota for the /home partition and the per-group disk quota for the /www partition. It also assumes that you have a /etc/fstab file that looks like the following:

```
/dev/sda1  /home  ext2  defaults  1 2
/dev/sda5  /www   ext2  defaults  1 2
```

To enforce user-level disk quotas on /home, you have to modify the first line as follows:

```
/dev/sda1  /home  ext2  defaults,usrquota  1 2
```