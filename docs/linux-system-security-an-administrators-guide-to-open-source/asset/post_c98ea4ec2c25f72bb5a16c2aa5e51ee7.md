
data is still out on the disk. Someone may access that data, either inadvertently or deliberately. To avoid this, set the secure deletion attribute on the file. When the file is deleted, all data blocks will be set to 0 and written to disk. $ ^{8} $ For example, we can set this attribute on the file really_private:

```
$ chattr -v +s really_private
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of really_private set as s-----
$
```

The -v flag of chattr is for verbose output, essentially saving the step of executing lsattr to confirm the setting. Notice that you need not be root to set the secure delete attribute. The only attributes requiring root privilege are the immutable (i) and append-only (a) attributes.

The a attribute is useful for log or similar files to which data is appended but not overwritten. When the a attribute is set, the only way to modify the file is by appending data to it. Once this bit is set, even root cannot remove the file. You can set the append-only attribute, for example, on /var/log/secure:

```
# chattr -V +a /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as ---a---
```

Let's verify that this file cannot be removed:

```
# rm /var/log/secure
rm: /var/log/secure: Operation not permitted
```

You may also set multiple flags using the = operator instead of the + operator:

```
# chattr -V =Aa /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as ----a-A
```

Here we are also setting the A attribute (no atime—see Table 4.4 on page 75), which suppresses access timestamp updating.

At some point you may need to unset an attribute. For example, to unset the a attribute on /var/log/secure:

```
# chattr -V -a /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as -------A
```

8. This does not guarantee complete erasure of the data. There are techniques to reconstruct the data on media even after the blocks are overwritten numerous times. See Chapter 15 for a more secure file deletion solution.

Of course, bear in mind that the bad-guys are reading this book, too! Always assume they know more than you do! Nothing discussed in this section will help if the root account is compromised. However, if you follow the guidelines laid out here, it will make the bad-guys execute more commands and take more time. That might just give you enough of an edge. In any event, using file attributes such as `i` and `a` will certainly prevent inadvertent actions by root on those files so protected.

### Using xlock and xscreensaver

One of the easiest things to do is to walk away from your system while you are still logged in. Maybe you want to get another cup of coffee, but instead of returning right away you end up speaking with a colleague for a time. Meanwhile, Murphy is at work.$ ^{9} $ You left your system logged in as root and *Jack the Cracker* wanders by. You know the rest.

To avoid this problem, use *xlock*. The *xlock* program will disable X Window System access to your computer until you enter your password. For example

```
# xlock -mode random
```

This invocation of *xlock* will select one of the 60 or so screensavers that come with the standard X11R6 release of X and lock your X Server (the display device, normally your monitor). You may accomplish the same thing by selecting Lock Screen from your background menu (choices may vary depending upon your window manager and/or desktop).

The problem with *xlock* is that you still have to remember to run it. So, you are effectively back to where you were at the beginning of this section. Fortunately, help is available in the form of *xscreensaver*.

The *xscreensaver* utility provides for the automatic locking of your X server. Simply place

```
xscreensaver.timeout: 2
```

in your `$HOME/.Xdefaults` file. This particular entry will cause your X server to automatically lock after two minutes of no mouse or keyboard activity. After you have changed the `$HOME/.Xdefaults` file, you will need to update your X server with

```
$ xrdb < $HOME/.Xdefaults
```

Note that these instructions will vary depending upon your choice of desktop (KDE, Gnome, etc.) and window manager (twm, fvwm, etc.). Check the appropriate documentation for details.

> 9. Murphy's Law: If something can go wrong, it will. O'Toole's comment about Murphy: He was an optimist.

## FILESYSTEM RESTRICTIONS

Another element to assist in securing your system related to the options specified when mounting local file systems. Normally a Linux system will have a number of file systems; however, it is possible to configure a Linux system with only one or very few file systems. One reason why you may want to create multiple file systems is to control access on them through the use of mount options specified in /etc/fstab.

In Example 4-6, we see an /etc/fstab file that was created, by default, at installation. For complete details on the syntax of this file and the definitions of each field, reference your system documentation or one of the System Administration references in *For Further Reading* on page 80. Our focus will be on the options field (fourth from left).

**Example 4-6 The /etc/fstab File**

| Device | Mount Point | Filesystem | Options | Dump/PASS |
| :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | / | ext2 | defaults | 1 1 |
| /dev/hda5 | /usr | ext2 | defaults | 1 2 |
| /dev/hdl1 | /home | ext2 | defaults | 1 2 |
| /dev/hda6 | /var | ext2 | defaults | 1 2 |
| /dev/fd0 | swap | swap | defaults | 0 0 |
| /dev/fd0 | /mnt/floppy | ext2 | noauto | 0 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | noauto,ro | 0 0 |
| none | /proc | proc | defaults | 0 0 |

Table 4.5 lists some of the options available to be placed in the fourth field (or as arguments of the -o flag to mount at the command line) of each record shown in Example 4-6. The table lists those options that are of interest from a security perspective.

**Table 4.5 Security Related mount Options**

| Option | Description |
| :--- | :--- |
| defaults | Sets the mount options to rw (read/write), suid (allow SUID and SGID executions), dev (allow character or block special devices), exec (allow execution of binaries), auto (-a), nouser (only root can mount the file system), and async (asynchronous I/O). |
| nodev | Do not interpret or allow the creation of character or block special files (device files) on this file system. |
| noexec | Do not allow the execution of binaries or scripts on this file system. |
| nosuid | Do not allow SUID or SGID to take effect on this file system. |
| noatime | Suppresses the updating of the access time on all files and directories in this file system. This option is available in kernel version 2.2.x (Red Hat 6.0) and not in kernel version 2.0.x (Red Hat 5.2). |
| ro | Set this file system to read-only. |
| user | Allow users other than root to mount this file system. This automatically sets the options noexec, nosuid, and nodev unless explicitly overridden. |

Prior to installing your system consider carefully the types of access required by your users. This may well dictate the filesystems you create. Consider these mount option guidelines for local filesystems:

- 1. Users' home directories should not be a breeding ground for SUID scripts and programs, and should never have character and block special files.
- 2. Any filesystem that has directories writable by other than root should minimally use the nousid option. The /var filesystem is one such filesystem and is critical to your system.
- 3. Any filesystem that does not need to be written to except occasionally should be mounted read only.

Consider Example 4-6 on page 78. We ought to apply guideline 2 to the /var filesystem and guideline 1 to the /home filesystem. For user convenience, we may also wish to add the user option to /mnt/cdrom. This will allow nonroot users to mount CDs without root intervention. The additional restrictions associated with the user option—namely nousid, noexec, and no dev—should offer sufficient security in exchange for this amenity.

Suppose that in the /usr filesystem you have a /usr/local/bin subdirectory that contains executables used by many users. If these executables don't change very often, you may wish to create a separate filesystem and to mount /usr/local/bin with the ro option. We'll show both this filesystem and /usr/local/lib (containing libraries or executables that may be invoked by other programs) with the ro option in Example 4-7. Unfortunately, if you do this, whenever you need to change something in /usr/local/bin or /usr/local/lib, you will need to remount it rw (preferably in single-user mode). With few exceptions, enhancing system and network security will have an impact on performance or convenience or both.

Example 4-7 shows our revised /etc/fstab table.

**Example 4-7 A More Secure /etc/fstab**

| Device | Mount Point | Filesystem | Options | Dump/PASS |
| :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | /usr/local/bin | ext2 | ro,nosuid | 0 0 |
| /dev/hdd4 | /usr/local/lib | ext2 | ro,nosuid | 0 0 |
| /dev/hdd5 | /usr | ext2 | ro,nosuid | 0 0 |
| /dev/hdd1 | /home | ext2 | noexec,nodev,nosuid | 0 0 |
| /dev/hda6 | /var | ext2 | nosuid | 1 0 |
| /dev/hda7 | swap | swap | defaults | 0 0 |
| /dev/fd0 | /mnt/floppy | ext2 | noauto | 0 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | nosuid,ro,user | 0 0 |
| none | /proc | proc | defaults | 0 0 |

## SUMMARY

In this chapter, we took a cursory look at security issues surrounding user and group account management, file and directory permissions, and filesystems. We also pointed to some reference material that covers the topics discussed in greater detail.
