
# Chapter 5 • Managing Users

9. D. Although Red Hat and Mandriva use the user private group strategy by default, you can design and use another strategy. Likewise, you *may* use the user private group strategy with any Linux distribution, even if it doesn't use that strategy by default. Ordinary users can't create groups by themselves, although if they're group administrators in a user private group system, they may add other users to their own existing groups.

10. C. The `newgrp` command changes the user's active group membership, which determines the group associated with any files the user creates. This command is *not* required to give the user access to files with other group associations if the user is a member of the other group and the file has appropriate group access permissions. Files have exactly one group association, so a user who belongs to multiple groups must specify to which group any created files belong. This is handled at login by setting a default or primary group recorded with the user's other account defaults in `/etc/passwd`.

11. A. Education helps users to understand the reasons to be concerned, which can motivate conformance with password procedures. Cracking procedures are common knowledge, so withholding general information won't keep that information out of the hands of those who want it. Copying password files and sending unencrypted passwords through e-mail are both invitations to disaster; encrypted files can be cracked, and e-mail can be intercepted.

12. B. One or both of `daemon` and `mail` might be required by the mail server or other system software, so these are poor prospects for removal. Likewise, `nobody` is used by a variety of processes that need only low-privilege access rights. The `games` account is most frequently used for games for high-score files and the like and so is most likely unused on a mail server.

13. D. When an `x` appears for entries in the second field of the `passwd` file, it indicates that the passwords are stored elsewhere—in the `/etc/shadow` file. Expiration information is stored in `/etc/shadow`, not `/etc/passwd`. An account that does not require a password for login has an empty password field in `/etc/passwd` or `/etc/shadow`.

14. C. The `pwconv` utility is used to convert conventional passwords to shadow passwords (the opposite of this action is performed by `pwunconv`). `skel` is a file, not a utility, that holds a “skeleton” of settings to be applied to newly created users. The shadow file (`/etc/shadow`) is where the passwords are stored, but it is not a utility. `crypt` is a utility that hashes data; it can be used to encrypt passwords, but doesn't convert conventional to shadow passwords or vice versa.

15. B, D. The `who` and `w` commands both display lists of currently logged-in users, as the question specifies. The `login` program manages text-mode console logins and some types of remote logins; it presents the `login:` and `password:` prompts and then, if the user is authenticated, launches a shell. The `which` command tells you whether a command is internal to the shell, a shell alias, or an external command; it has nothing to do with who's logged in.

16. A. The `whoami` command displays the effective user ID—the username associated with the command, which will in turn be the username associated with the current shell. Option B will display the current account database file, but this information won't help answer the question of what account you're using. Even if a desktop environment has a File > User menu item, that item won't reliably tell you whose account you're using at a command shell. Any shell you launch from the current one will run with the current shell's privileges, so option D won't be effective.

17. A. Linux’s password tools support passwords longer than eight characters for MD5 or SHA hashes, but not for 3DES hashes. 3DES hashes are limited to passwords of eight characters or less.

18. C. Linux supports multiple simultaneous logins through its standard console through the use of virtual terminals (VTs). From a text-mode login, pressing the Alt key along with a function key from F1 to F6 typically switches to a different virtual screen. Multitasking allows the machine to do more than one task at a time, while multithreading simply means that more than one thread can be executed at a time. Concurrency is not a common term used other than describing how many different users can log on at one time.

19. B. While the **userdel** utility removes the user, the `-r` parameter causes the system to remove all files from the user’s home directory, as well as the home directory itself. There is no `-a` option for the **userdel** utility, and there is no standard utility in Linux named **deluser**.

20. B. The **sudo** program restricts **root** access to a single command at a time, thus minimizing the risk of mistakenly running a command as **root** when an ordinary user account would suffice. Of the options listed, options A and C are both somewhat less secure than using **sudo**, while option D is downright dangerous because of the risk of data interception.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_276_0.png)

# Chapter 6

# Managing Disks

**THE FOLLOWING COMPTIA OBJECTIVES ARE COVERED IN THIS CHAPTER:**

- ☑ **1.2 Implement partitioning schemes and filesystem layout using the following tools and practices (LVM, RAID, fdisk, parted, mkfs).**
- ☑ **1.3 Explain the purpose for using each of the following filesystem types (Local: EXT2, EXT3, Reiser, FAT, NTFS, VFAT, ISO9660. Network: NFS, SMBFS/CIFS).**
- ☑ **1.4 Conduct routine mount and unmount of filesystems (mount, umount, /etc/fstab).**
- ☑ **1.5 Explain the advantages of having a separate partition or volume for any of the following directories (//boot, /home, /tmp, /usr, /var, /opt).**
- ☑ **1.6 Explain the purpose of the following directories (/, /bin, /dev, /etc, /mnt, /proc, /root, /sbin, /usr/bin, /usr/local, /usr/lib, /usr/lib64, /usr/share, /var/log).**
- ☑ **2.7 Manage filesystems using the following (check disk usage [df, du], Quotas [edquota, repquota, quotacheck], check and repair filesystems [fsck], Loopback devices [ISO filesystems], NFS [configuration, mount], Swap [mkswap, swapon, swapoff]).**

![](img/9903a4d3f7abd8dcbef1035fa04a3406_277_0.png)

Most computers’ actions are tied very closely to their disk partitions and the files they contain. Web servers must be able to deliver Web files stored on disk, workstations must be able to run applications and store data on disk, and so on. Therefore, it’s important that you can manage these files and the filesystems that contain them where you work with a Linux computer. Much of this chapter is devoted to this topic, starting with a look at the underlying hardware and Linux’s interfaces to it, then moving on to partition management, and finally looking at the Linux filesystem layout.

> Objective 2.7 is covered partly in this chapter and partly in Chapter 10, “Configuring Network Servers.”

> The term “filesystem” has two meanings. First, it may refer to an organized collection of files, stored in some specific set of directories. For instance, certain filesystem standards for Linux specify in what directories certain types of files reside. Second, “filesystem” may refer to the low-level data structures used to organize files on a hard disk partition or removable disk. Several different filesystems of this second variety exist, such as ext3fs, ReiserFS, and FAT. This chapter covers both types of filesystems; which meaning is intended is usually clear from the context. When it isn’t, I clarify by using terms such as “directory structure” or “directory tree” for the first type or “low-level filesystem” for the second variety.

## Storage Hardware Identification

Before delving into the details of how Linux manages partitions and files, you should understand some of the basics of storage devices. Several types of storage devices exist, and specific types have characteristics that can influence how Linux interacts with them. Understanding how Linux interacts with the hardware (device filenames, for instance) is also critically important.

> Chapter 1, “Getting Started with Linux,” describes low-level hardware concerns in more detail.
