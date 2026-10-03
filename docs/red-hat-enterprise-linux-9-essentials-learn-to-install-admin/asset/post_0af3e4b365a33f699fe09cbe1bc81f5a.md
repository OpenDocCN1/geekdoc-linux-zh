
the mail credentials:

```
# postmap /etc/postfix/sasl_passwd
```

Before proceeding, take some additional steps to secure your postfix credentials:

```
# chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
# chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

Edit the main.cf file once again and add an entry to specify the relay server:

```
relayhost = [smtp.myprovider.com]:587
```

Remaining within the main.cf file, add the following lines to configure the authentication settings for the SMTP server:

```
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-bundle.crt
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
```

Finally, restart the postfix service:

```
# systemctl restart postfix
```

Once the service has restarted, try sending and receiving mail using either the mail tool or your preferred mail client.

### 30.11 Summary

A complete, end-to-end email system consists of a Mail User Agent (MUA), Mail Transfer Agent (MTA), Mail Delivery Agent (MDA), and the SMTP protocol. RHEL 9 provides several options in terms of MTA solutions, one of the more popular being Postfix. This chapter has outlined how to install, configure and test postfix on a RHEL 9 system to act as a mail server and send and receive email using a third-party SMTP relay server.

## 31. Adding a New Disk Drive to a RHEL 9 System

One of the first problems users and system administrators encounter is that systems need more disk space to store data. Fortunately, disk space is now one of the cheapest IT commodities. In this and the next chapter, we will look how to configure RHEL 9 to use the space provided when a new physical or virtual disk drive is installed.

### 31.1 Mounted File Systems or Logical Volumes

There are two ways to configure a new disk drive on a RHEL 9 system. One straightforward method is to create one or more Linux partitions on the new drive, create Linux file systems on those partitions and then mount them at specific mount points to be accessed. This approach will be covered in this chapter.

Another approach is adding new space to an existing volume group or creating a new one. When RHEL 9 is installed, a volume group named rhel is created. Within this volume group are three logical volumes named root, home, and swap, used to store the / and /home file systems and swap partitions, respectively. We can increase the disk space available to the existing logical volumes by configuring the new disk as part of a volume group. For example, using this approach, we can increase the size of the /home file system by allocating some or all of the space on the new disk to the home volume. This topic will be discussed in detail in “Adding a New Disk to a RHEL 9 Volume Group and Logical Volume”.

### 31.2 Finding the New Hard Drive

This tutorial assumes that a new physical or virtual hard drive has been installed and is visible to the operating system. Once added, the operating system should automatically detect the new drive. Typically, the disk drives in a system are assigned device names beginning hd, sd, or nvme, followed by a letter to indicate the device number. The first device might be /dev/sda, the second /dev/sdb, etc.

The following is the output from a typical system with only one disk drive connected to a SATA controller:

```
# ls /dev/sd*
/dev/sda  /dev/sda1  /dev/sda2
```

This shows that the disk drive represented by /dev/sda is divided into two partitions, represented by /dev/sda1 and /dev/sda2.

The following output is from the same system after a second hard disk drive has been installed:

```
# ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb
```

The new hard drive has been assigned to the device file /dev/sdb. The drive has no partitions shown (because we have yet to create any).

At this point, we can create partitions and file systems on the new drive and mount them for access or add the disk as a physical volume as part of a volume group. To perform the former continue with this chapter; otherwise, read “Adding a New Disk to a RHEL 9 Volume Group and Logical Volume” for details on configuring Logical Volumes.

### 31.3 Creating Linux Partitions

The next step is to create one or more Linux partitions on the new disk drive. This is achieved using the fdisk utility, which takes as a command-line argument the device to be partitioned:

```
# fdisk /dev/sdb
```

```
Welcome to fdisk (util-linux 2.37.4).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0x64d68d00.

Command (m for help):
```

To view the current partitions on the disk, enter the p command:

```
Command (m for help): p
Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors
Disk model: USB 2.0 FD
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x64d68d00
```

As we can see from the above fdisk output, the disk currently has no partitions because it was previously unused. The next step is to create a new partition on the disk, a task which is performed by entering n (for new partition) and p (for primary partition):

```
Command (m for help): n
Partition type
  p   primary (0 primary, 0 extended, 4 free)
  e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1):
```

In this example, we only plan to create one partition, which will be partition 1. Next, we need to specify where the partition will begin and end. Since this is the first partition, we need it to start at the first available sector, and since we want to use the entire disk, we specify the last sector as the end. Note that if you wish to create multiple partitions, you can specify the size of each partition by sectors, bytes, kilobytes, or megabytes:

```
Partition number (1-4, default 1): 1
First sector (2048-30322687, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-30322687, default 30322687):
```

```
Created a new partition 1 of type 'Linux' and of size 14.5 GiB.
```

```
Command (m for help):
```

Now that we have specified the partition, we need to write it to the disk using the w command:

```
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

If we now look at the devices again, we will see that the new partition is visible as /dev/sdb1:

```
# ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb /dev/sdb1
```

The next step is to create a file system on our new partition.

### 31.4 Creating a File System on a RHEL 9 Disk Partition

We now have a new disk installed, it is visible to RHEL 9, and we have configured a Linux partition on the disk. The next step is to create a Linux file system on the partition so that the operating system can use it to store files and data. The easiest way to create a file system on a partition is to use the mkfs.xfs utility:

```
# mkfs.xfs -f /dev/sdb1
meta-data=/dev/sdb1              isize=512      agcount=4,  agsize=947520 blks
         =                      sectsz=512      attr=2,  projid32bit=1
         =                      crc=1          finobt=1, sparse=1, rmapbt=0
         =                      reflink=1      bigtime=1 inobtcount=1
data     =                      bsize=4096     blocks=3790080, imaxpct=25
         =                      sunit=0        swidth=0 blks
naming   =version 2              bsize=4096     ascii-ci=0, ftype=1
log      =internal log          bsize=4096     blocks=2560,  version=2
         =                      sectsz=512      sunit=0 blks, lazy-count=1
realtime =none                  extsz=4096     blocks=0, rtextents=0
```

In this case, we have created an XFS file system. XFS is a high-performance file system that is the default filesystem type on RHEL 9 and includes several advantages in terms of parallel I/O performance and the use of journaling.
