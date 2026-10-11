
9. Save and exit the file.
10. Reboot the machine.

## Setting The Quotas

To set user and/or group quotas, do the following:

1. Log in as root.
2. Choose which type of quota you want to assign, user or group. For a user quota, type “edquota -u user”, or for a group quota, type “edquota -g group”.

> **TIP:** This is where it is helpful if you have all of your users in a "users" group, in case you want to give all the users the same quota assignment.

This command opens a file containing text similar to the following:

```
Quotas for user sally:
/dev/hdb3: blocks in use: 153, limits (soft - 0, hard - 0)
inodes in use: 95, limits (soft - 0, hard - 0)
```

3. Fill in the soft and hard limits you want to use for the user, either as inodes (bottom line) or blocks (middle line), or both if you want to limit both the total space used and the total number of inodes used. See “Limiting User Storage Space” in the In Depth section if you are unsure of what the terms mean. The editor used for this command is vi, so you need to enter Insert mode by pressing “i” before you can change values.
4. Press the Esc key when you are finished.
5. Type “ZZ” or “wq” to save and exit the file.
6. Type “edquota -t” to set the grace period. You cannot set this period individually, you have to set it for the entire file system. This command opens a file containing text similar to the following:

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/hdb3: block grace period: 0 days, file grace period: 0 days
```

7. Notice that there are two different grace periods available. These two periods correspond to the two different types of quotas available. If you set only a block or inode quota, set the respective grace period. If you set both quotas, be sure to set both grace periods. The editor used for this command is vi, so you need to enter Insert mode by pressing “i” before you can change values.
8. Press the Esc key when you are finished.
9. Type “ZZ” or “:wq” to save and exit the file.
10. Type “quotaon” to turn on quotas to start working at this moment. This command is later executed during the boot scripts.

## Shutting Down And Rebooting

It is imperative that you properly shut down or reboot a Linux machine. Do not just shut off the power or press the Reset switch! A proper shutdown or reboot makes sure that all information held in RAM is properly written to disk, and in general it ensures that everything is neat and tidy.

Typically, the **shutdown** command is used to manage both shutting down and rebooting, though alternative choices are listed in Table 3.13. This command is versatile, offering not only choices involving whether the machine should prepare to be powered off or just reboot itself, but also when this should happen and what message users should be warned with. A selection of **shutdown** options is listed in Table 3.14.

**Table 3.13 Alternative commands used to shut down and reboot Linux machines.**

| Command | Result | Equivalent To |
| :--- | :--- | :--- |
| halt | Shuts down the machine. | shutdown -h now |
| init 0 | Shuts down the machine. | shutdown -h now |
| init 6 | Reboots the machine. | shutdown -r now |
| reboot | Reboots the machine. | shutdown -r now |

**Table 3.14 Flags available for the shutdown command.**

| Flag | Purpose | Arguments | Example |
| :--- | :--- | :--- | :--- |
| None | Warning to give to users so they have time to stop and save their work. | Warning in quotes | shutdown -ht 300 “System going down for maintenance. Back up in 3 hours.” |
| -c | Cancels a shutdown or reboot queued up to go. | None | shutdown -c |
| -f | Marks the file system to not be checked during the next boot. | None | shutdown -rf now |
| -h | Shuts down the machine. | None | shutdown -h now |
| -r | Reboots the system. | None | `shutdown -r now` |
| -t | The time to wait before the command should go into effect. | Seconds to wait, using the word **now** signifies that the event should happen immediately (the flag is not necessary with **now**) | `shutdown -ht 30` |

## Making A Custom Boot Disk

The boot disk you got with the distribution materials is not sufficient if the machine is already installed and not booting properly. You need to have a custom boot disk on hand that has the information necessary for your configuration. To make this disk, do the following as root:

1. Type "uname -r" to get the exact version of the kernel you are using.
2. Put a floppy in the floppy drive—it must be a floppy disk, you cannot use another type of media to make a boot disk.
3. Type "mkbootdisk --version *version*", where *version* is the result of the command in Step 1. Press Enter.
4. Be sure the floppy is in the drive, and then follow the instructions on the screen. Once the program is finished writing to the floppy, it is safe to remove it from the drive.
5. Clearly label the floppy as a boot disk for the particular machine in question and put it in a place you can find it easily if needed.

> *NOTE: This process works on most current Linux distributions.*

## Making A Rescue Disk

Red Hat offers a special rescue disk to make system recovery easier, in conjunction with the custom boot disk. Do the following as root to create a rescue disk:

1. Place a floppy in the floppy drive.
2. Mount the Red Hat distribution CD, or copy the *rescue.img* file onto the file system from its FTP site.
3. Type "dd if=/mnt/cdrom/images/rescue.img of=/dev/fd0 bs=1440k".
4. When the image is finished writing, clearly label the disk as a rescue disk and put it with the boot disk(s). Rescue disks are not individual to particular machines, so you don't need a specific one for each machine.

# Chapter 4

# Package Management

| **If you need an immediate solution to:** | **See page:** |
| :--------------------------------------------- | :------------ |
| Creating **gzipped** Files | 108 |
| Opening **gzipped** Files | 108 |
| Creating Z **compressed** Files | 108 |
| Opening Z **compressed** Files | 109 |
| Creating **tar** Files | 109 |
| Examining The Contents Of **tar** Files | 110 |
| Opening **tar** Files | 110 |
| Opening Or Creating Tarballs | 110 |
| Installing A Binary | 111 |
| Creating RPMs | 111 |
| Installing RPMs | 114 |
| Viewing The Contents Of An RPM File | 115 |
| Listing Which RPMs Are Installed | 115 |
| Removing An RPM | 115 |
| Verifying An RPM File | 115 |
| Checking A PGP-Signed RPM | 116 |
| Using GNOME’s RPM Tool | 116 |
| Opening GNOME RPM | 116 |
| Installing RPMs With GNOME RPM | 117 |
| Removing RPMs With GNOME RPM | 119 |
| Using KDE’s RPM Tool | 120 |
| Opening Kpackage | 120 |
| Installing RPMs With Kpackage | 120 |
| Removing RPMs With Kpackage | 121 |

## In Depth

There are a variety of tools available in the area of package management. These tools are needed on a regular basis, especially when you get into installing new software, backing up file systems, and updating your Linux installation. In this chapter, you will learn how to recognize package types on sight, when to use the various types available, and how to manipulate them.

### Types Of Tools

The tools used in package management can be classed roughly into two categories: compression tools and packaging tools. Each of the available items has its own features, weaknesses, and capabilities. Become familiar with them so that you know which tool to choose when it comes time to use these programs to prepare files or packages to share with other people or to store for archival.

### Compression Tools

There are essentially two different file compression tools commonly used in Linux: **gzip** and **compress**. The **gzip** command is a GNU compression utility that creates files with the .gz extension. Most compressed files in the Linux world were created with this tool. The **compress** program, on the other hand, makes files with the .Z extension.

These two programs use different compression algorithms. The **compress** tool is not used as heavily today as **gzip**, simply because **gzip** is a newer program with more efficient compression methods. However, you will still run across .Z files, because **compress** is a utility found across all flavors of Unix.

### Packaging Tools

On the other end of the scale are the packaging tools. These items may or may not include a compression aspect, but their primary purpose is to bundle files such that they can be installed on the recipient's machine in the right place, with the right permissions, and potentially include other considerations depending on the program you choose. A number of distributions now make their own package management tools to try to make life a little easier for the average Linux administrator.
