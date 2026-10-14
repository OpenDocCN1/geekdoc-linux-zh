
When removable media such as CD-ROMs are mounted, the Eject function of the drive is disabled until the device is unmounted. This is not true of removable disk drives, which means it is possible for a user to eject a removable disk while it is still mounted. This can cause minor problems, or even result in lost data. For example, files will still be marked as open even though they cannot be accessed.

## Using Networked File Systems

Although a complete discussion of networked file systems is beyond the scope of this book, you should be aware that many Linux networks use these file systems to share data transparently over the network. Additional information is provided in Chapter 15, "Advanced Topics and Troubleshooting."

> A more complete discussion of networked file systems is included in Chapter 5 of Guide to Linux Networking and Security (Course Technology 2003, ISBN 0-619-00094-5).

You already know that you can use a Web browser, an FTP client, or various command-line utilities to access data located on another computer. You can also use the mount command to make a directory on another computer appear as part of your local file system. This is similar to the idea of "mapping a network drive" in Microsoft Windows, where you assign a Windows share to a drive letter. Because Linux doesn't use drive letters, you might guess that you mount a networked file system to a subdirectory where it can be accessed.

Networked file systems in Linux are normally accessed using either the Network File System (NFS) or Server Message Block (SMB) protocols. A system administrator might tell you, for example, that you have access to a networked file system via NFS that is located on the server named glasgow in the directory /doc_archive. You decide to mount that file system on your computer in the subdirectory /glasgow_docs, which you have already created using mkdir. You can then mount the networked file system using this command, entering the password given to you by the administrator if prompted (a password is usually not needed):

```
# mount -t nfs glasgow:/doc_archive /glasgow_docs
```

## Automating File System Mounting

As a system administrator, you want to automate everything that you can so that your time is free for tasks that require new analysis and problem-solving skills. As you saw earlier, several types of file systems are mounted automatically when you start Linux. New file systems that you create from additional hard disks or other devices can also be automatically mounted at boot time.

The key to automounting file systems is the /etc/fstab configuration file. This file contains one line for each file system that you want to have automounted when Linux boots. It also

contains a line for file systems that you want to mount after booting Linux without providing all of the file system information in the mount command (as you did when mounting a CD-ROM or removable disk). A default fstab configuration file for Fedora is shown here (the exact values depend on where you have installed Linux on your system):

```
LABEL=/             /               ext3    defaults                1 1
none                /dev/pts        devpts  gid=5,mode=620          0 0
none                /proc           proc    defaults                0 0
none                /dev/shm        tmpfs   defaults                0 0
LABEL=/usr          /usr            ext3    defaults                1 2
/dev/hda3           swap            swap    defaults                0 0
/dev/cdrom          /mnt/cdrom      iso9660 noauto,owner,kudzu,ro  0 0
/dev/cdrom1         /mnt/cdrom1     iso9660 noauto,owner,kudzu,ro  0 0
/dev/fd0            /mnt/floppy     auto    noauto,owner,kudzu     0 0
```

The fields of this configuration file, from left to right, are described in the following list:

- The device where the file system is located or, if LABEL is used, the volume label on the hard disk to use for this file system. The label can provide a shortcut reference to a partition; you can have the label point to a different partition without needing to edit the fstab file.
- The mount point in the directory structure where the device is accessed after being mounted. Each file system has a mount point directory except the swap space, which is used only by the Linux kernel.
- The file system type iso9660 is the CD-ROM standard; proc and swap are examples of special file system types.
- Options that apply when this file system is mounted. You will learn more about these options later in this section.
- Whether the file system can respond to the dump command (which is not used much any more). A 1 (number one) in this field indicates that the dump command can be used to print information on the structure of the file system. Only ext2 or ext3 partitions should have this field set to 1.
- The order used to check file systems when Linux is booted. Each time Linux starts, it checks the status of file systems in fstab before mounting them. The root file system should be numbered 1; other ext2 or ext3 file systems should be numbered 2. If 0 is used, the file system is not checked. All file systems that are not automounted can have 0 in this field.

The options used to mount file systems are an effective way to increase security and ease system administration work. The options that you can use on a line within /etc/fstab depend on the type of file system being mounted. For example, many options can be used for NFS (network-mounted) file systems that are not applicable to other types of file systems. Useful options are described in Table 10-4.

## Table 10-4 Option Field Settings for the mount Command

| Mount option | Description |
|---|---|
| async | Specifies that all reads and writes to the file system should be asynchronous—in other words, that information is buffered (stored in memory) to improve access speed |
| auto | Specifies that the file system should be automatically mounted at boot time or when the mount command is used with the -a option |
| dev | Designates the file system as a special device in the /dev directory |
| exec | Permits programs stored on the file system to be executed |
| noauto | Indicates that this file system should not be automatically mounted; instead, the file system must be mounted by an explicit mount command |
| noexec | Indicates that programs stored on the file system cannot be executed |
| nousers | Specifies that no regular users can mount the file system; instead, only root can mount it |
| ro | Mounts the file system as read-only, which means no data can be written to it |
| rw | Mounts the file system as read/write—the standard mode in which data can be written to the file system |
| suid | Allows special user ID permissions to be used on this file system |
| user | Allows a regular user to mount the file system; this is useful if you are running a desktop Linux system and don’t want to switch to the root user account to mount a removable disk or CD-ROM |
| users | Functions the same as the user option except that any user can unmount the device |
| defaults | Includes the options rw, suid, dev, exec, auto, nouser, and async |

Additional options are described in the man page for the mount command.

You can add options when executing a mount command, rather than relying on the options within /etc/fstab. If you do, as shown in this example command, the options given on the command line override any listed in /etc/fstab.

```
# mount -t ext3 -o defaults /dev/sdb2 /archive
```

Consider two examples when you would add a line to /etc/fstab to automate file system mounting. Suppose you had set up a large SCSI hard disk to hold a database application. You want the database file system to be mounted automatically when you start Linux. Users should not be able to run programs off the database file system. For this situation, the fstab line might look like:

/dev/sdb2 /opt/db ext3 defaults,noexec 1 2

As a second example, suppose you are using Linux as your desktop workstation and have installed a new DVD drive. The device shouldn’t be mounted at boot time because you don’t normally keep a DVD disk in the drive, but you want to be able to mount the device without changing to the root user account. You also want to protect any writeable DVD disks from having any data damaged. You might use this line in the fstab file:
