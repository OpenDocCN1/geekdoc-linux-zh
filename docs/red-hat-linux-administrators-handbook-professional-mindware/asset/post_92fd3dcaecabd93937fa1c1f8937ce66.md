
## mount

The mount command mounts a file system. Typically, the mount options for commonly used file systems are stored in /etc/fstab. For example, if `/dev/hda6 /intranet ext2 defaults 1 2` is found in /etc/fstab, you can mount the file system stored in partition /dev/hda6 as follows:

```
mount /intranet
```

The same file system can also be mounted as follows:

```
mount -t ext2 /dev/hda6 /intranet
```

The `-t` option is used to specify the file system type. To mount all the file systems specified in /etc/fstab, use the `-a` option. For example, the following mounts all ext2 file systems:

```
mount -a -t ext2
```

Commonly used arguments for the `-o` option are `ro` (read-only) and `rw` (read/write). For example, the following mounts /dev/hda6 on /secured as a read-only file system:

```
mount -t ext2 -o ro /dev/hda6 /secured
```

## quota

To find out how much of your disk space a particular user is using, run the quota command as follows:

```
quota -u username
```

For example:

```
$ quota -u kabir
Disk quotas for user kabir (uid 500):
  Filesystem blocks quota limit grace files quota limit grace
  /dev/sda5 0 1024 4096 1 128 512
```

Run the same command to monitor disk usage of a group, as follows:

```
quota -g group
```

When you find users or groups that are over the limit, you can send them e-mail messages, so that disk usage is brought down to acceptable limits.

## swapon

```
swapon -a
```

The swapon command allows you to enable swap devices. The `-a` option allows you to enable all swap partitions specified in `/etc/fstab`.

## umount

```
umount -a [-t fstype]
```

The umount command unmounts a file system from the current system. For example,

```
umount /cdrom
```

unmounts a file system whose mount point is `/cdrom` and the details of whose mount point are specified in `/etc/fstab`.

The `-a` option allows you to unmount all file systems (except for the `/proc` file system) specified in the `/etc/fstab` file. You can also use the `-t` option to specify a particular file system type to unmount. For example,

```
umount -a -t iso9660
```

unmounts all iso9660-type file systems, which are typically CD-ROMs.

## DOS-Compatible Commands

If you need access to MS-DOS files from your Linux system, you need to install the Mtools package. Mtools is shipped with Red Hat as an RPM package, so installing it is quite simple. (Refer to the description of the rpm command in the previous section "File Compression and Archive-Specific Commands" for details on how to install an RPM package.)

Mtools is a collection of utilities that allows you to read, write, and move around MS-DOS files. It also supports Windows 9x/2000–style long filenames, OS/2 Xdf disks, and 2m disks. This section covers the common utilities found in the Mtools package.

### mcopy

**Syntax:** `mcopy [-tm] source-file-or-directory destination-file-or-directory`

The mcopy utility is used to copy MS-DOS files to and from Linux. For example,

```
mcopy /tmp/readme.txt b:
```

copies the **readme.txt** file from the /tmp directory to the b: drive. The **-t** option allows you to automatically translate carriage return/line feed pairs in MS-DOS text files into line feeds. The **-m** option allows you to preserve the file modification time.

### mdel

**Syntax:** `mdel msdosfile`

The mdel utility allows you to delete files on an MS-DOS file system.

### mdir

**Syntax:** `mdir [-/] msdos-file-or-directory`

The mdir utility allows you to view an MS-DOS directory. The **-/** option allows you to view all the subdirectories, as well.

### mformat

**Syntax:** `mformat [-t cylinders] [-h heads] [-s sectors]`

The mformat utility allows you to format a floppy disk to hold a minimal MS-DOS file system. However, using an MS-DOS machine to format a disk is much easier than specifying cylinders, heads, sectors, and so on. My advice is to use an MS-DOS machine to do the job instead of using mformat.

### mlabel

**Syntax:** `mlabel [-vcs] drive:[new label]`

The mlabel utility displays the current volume label (if any) of the named drive and prompts for the new label if it is not entered after drive: in the command line. The `-v` option prints a hex dump of the boot sector of the named drive. The `-c` option clears the existing volume label. The `-s` option shows the existing label of the drive.

## System Status-Specific Commands

The commands discussed in this section deal with status information on system resources.

### dmesg

**Syntax:** `dmesg`

The dmesg program prints the status messages displayed by the kernel during bootup.

### free

**Syntax:** `free`

The free program displays memory usage statistics. An example of free's output looks like this:

| | total | used | free | shared | buffers | cached |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Mem: | 127776 | 124596 | 3180 | 30740 | 2904 | 107504 |
| -/+ buffers/cache: | | 14188 | | | 113588 | |
| Swap: | 129900 | 84 | 129816 | | | |

### shutdown

**Syntax:** `shutdown [-r] [-h] [-C] [-k] [-t seconds] time [message]`

The `shutdown` command allows a superuser or an ordinary user listed in the `/etc/shutdown.allow` file to shut down the system for a reboot or halt. To reboot the computer now, run the following command:

```bash
shutdown -r now
```

To halt the system after the shutdown, replace `-r` with `-h`. The `-k` option allows you to simulate a shutdown event without actually doing it. For example,

```bash
shutdown -r -k now "System going down for maintenance"
```

sends a fake shutdown message to all the users. The `-t` option allows you to specify a delay, in seconds, between the warning message and the actual shutdown event. In such a case, if you decide to abort the shutdown, use the `-c` option and run shutdown again to cancel it.

Note that you can use the `HH:MM` format to specify the time. For example,

```bash
shutdown -r 12:55
```

reboots the system at 12:55. You can also use `+minutes` to specify time. For example,

```bash
shutdown -r +5
```

starts the shutdown process five minutes after the warning message has been printed.

### uname

**Syntax:** `uname [-m] [-n] [-r] [-s] [-v] [-a]`

The `uname` command displays information about the current system. For example,

```bash
uname -a
```

displays a line such as the following:

```
Linux pica5o.nitec.com 2.0.36 #1 Mon Dec 3 22:17:11 EDT 2000 i586 unknown
```

The `-m` option displays the system architecture (for instance, `i586`). The `-n` option displays the host name (for instance, `pica50.nitec.com`). The `-r` option displays the release version of the OS (for instance, `2.0.36`). The `-s` option displays the OS name (for instance, Linux). The `-v` option displays the local build version of the OS (for instance, `#1 Mon Dec 13 22:17:11 EDT 2000`).

### uptime

**Syntax:** `uptime`

The uptime command displays the current time; how long the system has been up since the last reboot; how many users are connected to the server; and the system load in the last 1, 5, and 15 minutes.

## User Administration Commands

The commands in this section pertain to user administration.

### chfn

Run the chfn command to change a user's finger information. For example, the following enables you to change user jennifer's finger information, which is stored in the /etc/passwd file:

```
chfn jennifer
```

A user can change his or her own finger information by using this program, as well. A user can also create a .plan file in his or her home directory that will be appended to the information shown by the finger program.

### chsh

Use the chsh command to change a user's shell. For example, the following enables you to change user brian's current shell:

```
chsh brian
```

If you specify a shell or program name that is not in /etc/shells, the user will not be able to log in. Note that a user can change his or her own shell using this command. An ordinary user does not need to specify the username as an argument, because the only shell he or she can change is his or her own.

### groupadd

To create a new group, use the groupadd command. For example, the following adds a new group called mygroup in the /etc/group and in the /etc/gshadow file (if you are using shadow passwords):

```
groupadd mygroup
```

By default, the groupadd program creates the group with a GID above 499, because 0 through 499 are (sort of) reserved for system-level accounts such as root, bin, and mail. So if your /etc/group file has the last group GID set to 511, the new group you create with this program will have a GID of 512, and so on. If you want to set the GID of your new group specifically, use the `-g GID` option. Also, if you want to create a group with a GID in the 0 to 499 range, use the `-r` option with the `-g GID` option to force groupadd to create the new group as a system group. Note that if the group or GID you are trying to use with the program is already in use in /etc/group, you will get an error message.

### groupmod

To modify an existing group name or GID, use the groupmod command. To rename a group, use the following syntax:

```
groupmod -n new_group current_group
```
