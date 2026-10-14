
The less command is used like this:

```
less filename
```

Once started, the less program allows you to scroll forward and backward through a text file. For example, to examine the file that defines all the system’s user accounts, enter the following command:

```
[me@linuxbox ~]$ less /etc/passwd
```

Once the less program starts, we can view the contents of the file. If the file is longer than one page, we can scroll up and down. To exit less, press the Q key.

## Table 3-3: less Commands

| Command | Action |
|---|---|
| PAGE UP or b | Scroll back one page. |
| PAGE DOWN or Spacebar | Scroll forward one page. |
| Up Arrow | Scroll up one line. |
| Down Arrow | Scroll down one line. |
| G | Move to the end of the text file. |
| 1G or g | Move to the beginning of the text file. |
| /characters | Search forward to the next occurrence of characters. |
| n | Search for the next occurrence of the previous search. |
| h | Display help screen. |
| q | Quit less. |

## LESS IS MORE

The less program was designed as an improved replacement of an earlier Unix program called more. Its name is a play on the phrase “less is more”—a motto of modernist architects and designers.

less falls into the class of programs called pagers, programs that allow the easy viewing of long text documents in a page-by-page manner. Whereas the more program could only page forward, the less program allows paging both forward and backward and has many other features as well.

## A Guided Tour

The filesystem layout on your Linux system is much like that found on other Unix-like systems. The design is actually specified in a published standard called the Linux Filesystem Hierarchy Standard. Not all Linux distributions conform to the standard exactly, but most come pretty close.

Next, we are going to wander around the filesystem ourselves to see what makes our Linux system tick. This will give you a chance to practice your navigation skills. One of the things we will discover is that many of the interesting files are in plain, human-readable text. As we go about our tour, try the following:

- 1. cd into a given directory.
- 2. List the directory contents with ls -l.
- 3. If you see an interesting file, determine its contents with file.
- 4. If it looks as if it might be text, try viewing it with less.

> Note: Remember the copy-and-paste trick! If you are using a mouse, you can double-click a filename to copy it and middle-click to paste it into commands.

As we wander around, don’t be afraid to look at stuff. Regular users are largely prohibited from messing things up. That’s the system administrator’s job! If a command complains about something, just move on to something else. Spend some time looking around. The system is ours to explore. Remember, in Linux, there are no secrets! Table 3-4 lists just a few of the directories we can explore. Feel free to try more!

## Table 3-4: Directories Found on Linux Systems

| Directory | Comments |
|---|---|
| / | The root directory, where everything begins. |
| /bin | Contains binaries (programs) that must be present for the system to boot and run. |
| /boot | Contains the Linux kernel, initial RAM disk image (for drivers needed at boot time), and the boot loader. |
|  | Interesting files: |
|  | - /boot/grub/grub.conf or menu.lst, which are used to configure the boot loader |
|  | - /boot/vmlinuz, the Linux kernel |

## Table 3-4 (continued)

| Directory | Comments |
|---|---|
| /dev | This is a special directory that contains *device nodes*. “Everything is a file” also applies to devices. Here is where the kernel maintains a list of all the devices it understands. |
| /etc | The */etc* directory contains all of the system-wide configuration files. It also contains a collection of shell scripts that start each of the system services at boot time. Everything in this directory should be readable text. |
|  | Interesting files: While everything in */etc* is interesting, here are some of my all-time favorites: |
|  | - */etc/crontab*, a file that defines when automated jobs will run |
|  | - */etc/fstab*, a table of storage devices and their associated mount points |
|  | - */etc/passwd*, a list of the user accounts |
| /home | In normal configurations, each user is given a directory in */home*. Ordinary users can write files only in their home directories. This limitation protects the system from errant user activity. |
| /lib | Contains shared library files used by the core system programs. These are similar to DLLs in Windows. |
| /lost+found | Each formatted partition or device using a Linux file-system, such as ext3, will have this directory. It is used in the case of a partial recovery from a filesystem corruption event. Unless something really bad has happened to your system, this directory will remain empty. |
| /media | On modern Linux systems the */media* directory will contain the mount points for removable media such as USB drives, CD-ROMs, etc. that are mounted automatically at insertion. |
| /mnt | On older Linux systems, the */mnt* directory contains mount points for removable devices that have been mounted manually. |
| /opt | The */opt* directory is used to install “optional” software. This is mainly used to hold commercial software products that may be installed on your system. |
