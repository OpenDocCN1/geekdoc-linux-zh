
# Maintaining Filesystem Health 153

described in "Checking Filesystems." This task is usually handled automatically when the system boots, but it takes time—probably several minutes, or perhaps more than an hour on a large filesystem or if the computer has many smaller filesystems.

The solution to this problem is to change to a *journaling filesystem*. Such a filesystem maintains a *journal*, which is a data structure that describes pending operations. Prior to writing to the disk's main data structures, Linux describes what it's about to do in the journal. Thus, at any moment the journal should contain a list of disk structures that might be undergoing modification. The result is that, in the event of a crash or power failure, the system can examine the journal and choose only those data structures. If inconsistencies occur, the system can roll back or complete the changes, returning the disk to a consistent state without checking every data in the filesystem. This greatly speeds the disk-check process after power failures and system crashes. Today, journaling small partitions (such as a /boot partition, if you use one) and small removable disks (such as Zip disks) often lack journals,

Five filesystems on Linux: ext3, ext4, ReiserFS, XFS, and JFS. Of these, the last three require little in the way of journal configuration. Ext3fs is a bit different; it is just ext2 with a journal added. This fact means you can add a journal to an ext2 filesystem, converting it into an ext3 filesystem. This is what the -j option to tune2fs does, as described in *Adjusting Tunable Filesystem Parameters*. Ext4fs is a further enhancement of this filesystem family.

> Although tune2fs on a mounted filesystem is generally advisable, it's safe to use its -j option on a mounted filesystem. The result is a file called journal that holds the journal. If you add a journal to an unmounted filesystem, the file will be invisible.

![](img/35f616c7eba4e79e12bfd762129c5d27_207_0.png)

Adding a journal alone won't do much good, though. To use a journal, you must mount the filesystem with the correct filesystem type code—rather ext2 for ext3, or ext4 for ext4fs. (The upcoming section *Mounting and Unmounting Filesystems* describes how to do this.)

The journal, like other filesystem features, has its own set of parameters. You can set these with the -j option to tune2fs. In particular, the size=journal-size and device=external journal enable you to set the journal's size and the device on which it's stored. By default, the system creates a journal that's the right size for the filesystem and stores it on the itself.

# Checking Filesystems

Tuning a filesystem is a task you're likely to perform once in a while—say, when making changes to an installation. Another task is much more common: checking a filesystem for errors. Bugs, power failures, and mechanical problems can cause all the

# Chapter 3 • Configuring Hardware

data structures on a filesystem to become corrupted. The results are sometimes subtle, if they're left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a filesystem's integrity and for correcting any problems that may exist. The main tool you'll use for this purpose is called fck. This program is actually a front end to other tools, as e2fsck (fsck.ext2, fsck.ext3, and fsck.ext4) or XFS' xfs_check and xfs_repair. The syntax for fck is as follows:

```
fsck [-saCVRTNP] [-t ftype] [--fsck-options] filesystems
```

The exam objectives include both e2fsck and fsck, but because fsck is the more general tool's useful on more filesystems, it's the form described in detail in this book.

The more common parameters to fsck allow you to perform useful actions:

- **Check All** The -A option allows fsck to check all the filesystems marked to be checked in /etc/fstab. This option is normally used in system startup scripts.
- **Indicate Progress** The -C option displays a text-mode indicator of the check process. Most filesystem programs don't support this feature, but e2fsck does.
- **Show Verbose Output** The -V option produces verbose output of the check process.
- **No Action** The -N option tells fsck to display what it would normally without actually doing it.
- **Set the Filesystem Type** Normally, fsck determines the filesystem type automatically. You can force it with the -t ftype flag, Used in conjunction with -A, this causes the program to check only the specified filesystem types, even if others are marked to be checked. If ftype is prefixed with no, then all the specified type are checked.
- **Filesystem-Specific Options** Filesck program for specific filesystems often have their own options. The fsck command passes options doesn't support, or those that follow a double dash (--), to the underlying program. Common options include a -p (perform an automatic check), -r (perform an interactive check), and -f (force a full filesystem check even if the filesystem initially appears to be clean).
- **Filesystem List** The final parameter is usually the name of the filesystem or filesystems being checked, such as /dev/sda.

Normally, you run fsck with the filesystem device name, as in fsck /dev/sda. You can add options as needed, however. Check fsck's man page for less common options.

Run fsck only on filesystems that are not mounted or are mounted read-only.

# Maintaining Filesystem Health

Five filesystems on Linux: ext3, ext4, ReiserFS, XFS, and JFS. Of these, the last three require little in the way of journal configuration. Ext3fs is a bit different; it is just ext2 with a journal added. This fact means you can add a journal to an ext2 filesystem, converting it into an ext3 filesystem. This is what the -j option to tune2fs does, as described in *Adjusting Tunable Filesystem Parameters*. Ext4fs is a further enhancement of this filesystem family.

The solution to this problem is to change to a *journaling filesystem*. Such a filesystem maintains a *journal*, which is a data structure that describes pending operations. Prior to writing to the disk's main data structures, Linux describes what it's about to do in the journal. Thus, at any moment the journal should contain a list of disk structures that might be undergoing modification. The result is that, in the event of a crash or power failure, the system can examine the journal and choose only those data structures. If inconsistencies occur, the system can roll back or complete the changes, returning the disk to a consistent state without checking every data in the filesystem. This greatly speeds the disk-check process after power failures and system crashes. Today, journaling small partitions (such as a /boot partition, if you use one) and small removable disks (such as Zip disks) often lack journals,

Adding a journal alone won't do much good, though. To use a journal, you must mount the filesystem with the correct filesystem type code—rather ext2 for ext3, or ext4 for ext4fs. (The upcoming section *Mounting and Unmounting Filesystems* describes how to do this.)

The journal, like other filesystem features, has its own set of parameters. You can set these with the -j option to tune2fs. In particular, the size=journal-size and device=external journal enable you to set the journal's size and the device on which it's stored. By default, the system creates a journal that's the right size for the filesystem and stores it on the itself.

# Checking Filesystems

Tuning a filesystem is a task you're likely to perform once in a while—say, when making changes to an installation. Another task is much more common: checking a filesystem for errors. Bugs, power failures, and mechanical problems can cause all the data structures on a filesystem to become corrupted. The results are sometimes subtle, if they're left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a filesystem's integrity and for correcting any problems that may exist. The main tool you'll use for this purpose is called fck. This program is actually a front end to other tools, as e2fsck (fsck.ext2, fsck.ext3, and fsck.ext4) or XFS' xfs_check and xfs_repair. The syntax for fck is as follows:

```
fsck [-saCVRTNP] [-t ftype] [--fsck-options] filesystems
```

The exam objectives include both e2fsck and fsck, but because fsck is the more general tool's useful on more filesystems, it's the form described in detail in this book.

The more common parameters to fsck allow you to perform useful actions:

- **Check All** The -A option allows fsck to check all the filesystems marked to be checked in /etc/fstab. This option is normally used in system startup scripts.
- **Indicate Progress** The -C option displays a text-mode indicator of the check process. Most filesystem programs don't support this feature, but e2fsck does.
- **Show Verbose Output** The -V option produces verbose output of the check process.
- **No Action** The -N option tells fsck to display what it would normally without actually doing it.
- **Set the Filesystem Type** Normally, fsck determines the filesystem type automatically. You can force it with the -t ftype flag, Used in conjunction with -A, this causes the program to check only the specified filesystem types, even if others are marked to be checked. If ftype is prefixed with no, then all the specified type are checked.
- **Filesystem-Specific Options** Filesck program for specific filesystems often have their own options. The fsck command passes options doesn't support, or those that follow a double dash (--), to the underlying program. Common options include a -p (perform an automatic check), -r (perform an interactive check), and -f (force a full filesystem check even if the filesystem initially appears to be clean).
- **Filesystem List** The final parameter is usually the name of the filesystem or filesystems being checked, such as /dev/sda.

Normally, you run fsck with the filesystem device name, as in fsck /dev/sda. You can add options as needed, however. Check fsck's man page for less common options.

Run fsck only on filesystems that are not mounted or are mounted read-only.

# Maintaining Filesystem Health

Five filesystems on Linux: ext3, ext4, ReiserFS, XFS, and JFS. Of these, the last three require little in the way of journal configuration. Ext3fs is a bit different; it is just ext2 with a journal added. This fact means you can add a journal to an ext2 filesystem, converting it into an ext3 filesystem. This is what the -j option to tune2fs does, as described in *Adjusting Tunable Filesystem Parameters*. Ext4fs is a further enhancement of this filesystem family.

> Although tune2fs on a mounted filesystem is generally advisable, it's safe to use its -j option on a mounted filesystem. The result is a file called journal that holds the journal. If you add a journal to an unmounted filesystem, the file will be invisible.

![](img/35f616c7eba4e79e12bfd762129c5d27_207_0.png)

Adding a journal alone won't do much good, though. To use a journal, you must mount the filesystem with the correct filesystem type code—rather ext2 for ext3, or ext4 for ext4fs. (The upcoming section *Mounting and Unmounting Filesystems* describes how to do this.)

The journal, like other filesystem features, has its own set of parameters. You can set these with the -j option to tune2fs. In particular, the size=journal-size and device=external journal enable you to set the journal's size and the device on which it's stored. By default, the system creates a journal that's the right size for the filesystem and stores it on the itself.

# Checking Filesystems

Tuning a filesystem is a task you're likely to perform once in a while—say, when making changes to an installation. Another task is much more common: checking a filesystem for errors. Bugs, power failures, and mechanical problems can cause all the data structures on a filesystem to become corrupted. The results are sometimes subtle, if they're left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a filesystem's integrity and for correcting any problems that may exist. The main tool you'll use for this purpose is called fck. This program is actually a front end to other tools, as e2fsck (fsck.ext2, fsck.ext3, and fsck.ext4) or XFS' xfs_check and xfs_repair. The syntax for fck is as follows:

```
fsck [-saCVRTNP] [-t ftype] [--fsck-options] filesystems
```

The exam objectives include both e2fsck and fsck, but because fsck is the more general tool's useful on more filesystems, it's the form described in detail in this book.

The more common parameters to fsck allow you to perform useful actions:

- **Check All** The -A option allows fsck to check all the filesystems marked to be checked in /etc/fstab. This option is normally used in system startup scripts.
- **Indicate Progress** The -C option displays a text-mode indicator of the check process. Most filesystem programs don't support this feature, but e2fsck does.
- **Show Verbose Output** The -V option produces verbose output of the check process.
- **No Action** The -N option tells fsck to display what it would normally without actually doing it.
- **Set the Filesystem Type** Normally, fsck determines the filesystem type automatically. You can force it with the -t ftype flag, Used in conjunction with -A, this causes the program to check only the specified filesystem types, even if others are marked to be checked. If ftype is prefixed with no, then all the specified type are checked.
- **Filesystem-Specific Options** Filesck program for specific filesystems often have their own options. The fsck command passes options doesn't support, or those that follow a double dash (--), to the underlying program. Common options include a -p (perform an automatic check), -r (perform an interactive check), and -f (force a full filesystem check even if the filesystem initially appears to be clean).
- **Filesystem List** The final parameter is usually the name of the filesystem or filesystems being checked, such as /dev/sda.

Normally, you run fsck with the filesystem device name, as in fsck /dev/sda. You can add options as needed, however. Check fsck's man page for less common options.

Run fsck only on filesystems that are not mounted or are mounted read-only.

# Maintaining Filesystem Health

Five filesystems on Linux: ext3, ext4, ReiserFS, XFS, and JFS. Of these, the last three require little in the way of journal configuration. Ext3fs is a bit different; it is just ext2 with a journal added. This fact means you can add a journal to an ext2 filesystem, converting it into an ext3 filesystem. This is what the -j option to tune2fs does, as described in *Adjusting Tunable Filesystem Parameters*. Ext4fs is a further enhancement of this filesystem family.

The solution to this problem is to change to a *journaling filesystem*. Such a filesystem maintains a *journal*, which is a data structure that describes pending operations. Prior to writing to the disk's main data structures, Linux describes what it's about to do in the journal. Thus, at any moment the journal should contain a list of disk structures that might be undergoing modification. The result is that, in the event of a crash or power failure, the system can examine the journal and choose only those data structures. If inconsistencies occur, the system can roll back or complete the changes, returning the disk to a consistent state without checking every data in the filesystem. This greatly speeds the disk-check process after power failures and system crashes. Today, journaling small partitions (such as a /boot partition, if you use one) and small removable disks (such as Zip disks) often lack journals,

Adding a journal alone won't do much good, though. To use a journal, you must mount the filesystem with the correct filesystem type code—rather ext2 for ext3, or ext4 for ext4fs. (The upcoming section *Mounting and Unmounting Filesystems* describes how to do this.)

The journal, like other filesystem features, has its own set of parameters. You can set these with the -j option to tune2fs. In particular, the size=journal-size and device=external journal enable you to set the journal's size and the device on which it's stored. By default, the system creates a journal that's the right size for the filesystem and stores it on the itself.

# Checking Filesystems

Tuning a filesystem is a task you're likely to perform once in a while—say, when making changes to an installation. Another task is much more common: checking a filesystem for errors. Bugs, power failures, and mechanical problems can cause all the data structures on a filesystem to become corrupted. The results are sometimes subtle, if they're left unchecked, they can cause severe data loss. For this reason, Linux includes tools for verifying a filesystem's integrity and for correcting any problems that may exist. The main tool you'll use for this purpose is called fck. This program is actually a front end to other tools, as e2fsck (fsck.ext2, fsck.ext3, and fsck.ext4) or XFS' xfs_check and xfs_repair. The syntax for fck is as follows:

```
fsck [-saCVRTNP] [-t ftype] [--fsck-options] filesystems
```

The exam objectives include both e2fsck and fsck, but because fsck is the more general tool's useful on more filesystems, it's the form described in detail in this book.

The more common parameters to fsck allow you to perform useful actions:

- **Check All** The -A option allows fsck to check all the filesystems marked to be checked in /etc/fstab. This option is normally used in system startup scripts.
- **Indicate Progress** The -C option displays a text-mode indicator of the check process. Most filesystem programs don't support this feature, but e2fsck does.
- **Show Verbose Output** The -V option produces verbose output of the check process.
- **No Action** The -N option tells fsck to display what it would normally without actually doing it.
- **Set the Filesystem Type** Normally, fsck determines the filesystem type automatically. You can force it with the -t ftype flag, Used in conjunction with -A, this causes the program to check only the specified filesystem types, even if others are marked to be checked. If ftype is prefixed with no, then all the specified type are checked.
- **Filesystem-Specific Options** Filesck program for specific filesystems often have their own options. The fsck command passes options doesn't support, or those that follow a double dash (--), to the underlying program. Common options include a -p (perform an automatic check), -r (perform an interactive check), and -f (force a full filesystem check even if the filesystem initially appears to be clean).
- **Filesystem List** The final parameter is usually the name of the filesystem or filesystems being checked, such as /dev/sda.

Normally, you run fsck with the filesystem device name, as in fsck /dev/sda. You can add options as needed, however. Check fsck's man page for less common options.

Run fsck only on filesystems that are not mounted or are mounted read-only.

# Disk Use

One common problem with disks is that they can fill up. To avoid this, you need tools to show how much space is consuming. The simplest case is df's syntax:

```
| Filesystem | 1K-blocks | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 | 5088364 | 2441444 | 52% | / |
| /dev/sda2 | 2048576 | 1024288 | 50% | /home |
| /dev/sda3 | 1048576 | 524288 | 50% | /var |
| /dev/sda4 | 524288 | 262144 | 50% | /root |
| /dev/sda5 | 262144 | 131072 | 50% | /tmp |
| /dev/sda6 | 131072 | 65536 | 50% | /dev |
| /dev/sda7 | 65536 | 32768 | 50% | /bin |
| /dev/sda8 | 32768 | 16384 | 50% | /run |
| /dev/sda9 | 16384 | 8192 | 50% | /boot |
| /dev/sda10 | 8192 | 4096 | 50% | /etc |
| /dev/sda11 | 4096 | 2048 | 50% | /usr |
| /dev/sda12 | 2048 | 1024 | 50% | /sbin |
| /dev/sda13 | 1024 | 512 | 50% | /lib |
| /dev/sda14 | 512 | 256 | 50% | /boot |
| /dev/sda15 | 256 | 128 | 50% | /opt |
| /dev/sda16 | 128 | 64 | 50% | /root |
| /dev/sda17 | 64 | 32 | 50% | /srv |
| /dev/sda18 | 32 | 16 | 50% | /mnt |
| /dev/sda19 | 16 | 8 | 50% | /media |
| /dev/sda20 | 8 | 4 | 50% | /lost |
| /dev/sda21 | 4 | 2 | 50% | /lost |
| /dev/sda22 | 2 | 1 | 50% | /lost |
```

**Summarize In**

One common problem with disks is that they can fill up. To avoid this, you need tools to show how much space is consuming. The simplest case is df's syntax:

```
| Filesystem | 1K-blocks | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 | 5088364 | 2441444 | 52% | / |
| /dev/sda2 | 2048576 | 1024288 | 50% | /home |
| /dev/sda3 | 1048576 | 524288 | 50% | /var |
| /dev/sda4 | 524288 | 262144 | 50% | /root |
| /dev/sda5 | 262144 | 131072 | 50% | /tmp |
| /dev/sda6 | 131072 | 65536 | 50% | /dev |
| /dev/sda7 | 65536 | 32768 | 50% | /bin |
| /dev/sda8 | 32768 | 16384 | 50% | /run |
| /dev/sda9 | 16384 | 8192 | 50% | /boot |
| /dev/sda10 | 8192 | 4096 | 50% | /etc |
| /dev/sda11 | 4096 | 2048 | 50% | /usr |
| /dev/sda12 | 2048 | 1024 | 50% | /sbin |
| /dev/sda13 | 1024 | 512 | 50% | /lib |
| /dev/sda14 | 512 | 256 | 50% | /boot |
| /dev/sda15 | 256 | 128 | 50% | /opt |
| /dev/sda16 | 128 | 64 | 50% | /root |
| /dev/sda17 | 64 | 32 | 50% | /srv |
| /dev/sda18 | 32 | 16 | 50% | /mnt |
| /dev/sda19 | 16 | 8 | 50% | /media |
| /dev/sda20 | 8 | 4 | 50% | /lost |
| /dev/sda21 | 4 | 2 | 50% | /lost |
| /dev/sda22 | 2 | 1 | 50% | /lost |
```

**Summarize In**

By default, df summarizes available and used disk space. You can instead receive a report on available and used inodes by passing the -i or --inodes option. This information can be helpful if a partition has very many small files, which can deplete available inodes sooner than they deplete disk space.

> NOTE The -i option works for ext2, ext3, ext4, XFS, and some other filesystems that create a fixed number of inodes when the filesystem is created. Other filesystems, such as ReiserFS and Btrfs, create inodes dynamically, rendering the -i option meaningless.

**Local Filesystems Only** The -l or --local option causes df to omit network systems. This can speed up operation.

**Display Filesystem Type** The -T or --type option shows the filesystem type to the information df displays.\Limit by Filesystem Type** The -t ftype or --type=fstype displays only information about filesystems of the specified type. The -x ftype or --exclude-type=fstype has the opposite effect; it excludes filesystems of the specified type from the report.
