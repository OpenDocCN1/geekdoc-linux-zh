
for its shared directories, whereas SMB/CIFS uses the term share. SMB/CIFS also uses usernames and passwords to control access, which complicates matters. The best way to pass this information is to include a `credentials=filename` option in `/etc/fstab` and place the username and password in the specified file:

```
username=george
password=somepassword
```

![](img/f430a19bdf014c43ad7c2d594afd5b21_243_0.png)

> A configuration such as the one shown here also requires configuring the NFS server computer. This is done by editing the `/etc/exports` file on the server. The server computer must be told to enable specific clients (or groups of clients) to access what it exports. This topic is covered in Phase 6.

## Adding User-Controlled Mounts

Linux requires filesystems to be mounted in order to access them in an ordinary way, but Linux doesn't permit ordinary users to mount and unmount arbitrary filesystems. This can lead to a problem: How can an ordinary user access a floppy disk, CD-ROM, or other removable media? This problem can even extend to network mounts, which if keeping them permanently mounted is unnecessary or undesirable. One solution to these problems is to use an automounter, which is a software tool that checks for accesses to particular directories and automatically mounts a filesystem when it detects such accesses. Many Linux distributions that are intended for use on desktop computers ship with automounter support. Another approach is to enable ordinary users to mount and unmount filesystems that are specified in `/etc/fstab`. This is done by adding options to the `/etc/fstab` entry for a file:

- **users**: This option enables ordinary users to mount and unmount the filesystem using a simplified syntax, as described shortly.
- **user**: This option works just like `users` except that the system remembers who mounted the filesystem. Only that user (or `root`) may unmount the filesystem.
- **owner**: This option works very much like `user` except that only the user who owns the mount point (or `root`) may mount the filesystem. This is handy if you want to give just one user the right to mount a filesystem.
- **noauto**: This option tells Linux to not automatically mount the filesystem when it boots or when you type `mount -a`. This is most helpful for removable media, but you can use it with any filesystem except those that are required for system operation.

The Scenario specifies that you want to enable ordinary users to mount and unmount a Zip disk that you've added to the computer. Zip disks are ordinarily partitioned so that the fourth primary partition holds the disk's single partition. (They can be repartitioned in other ways, though.) Thus, assuming your Zip disk is accessible as `/dev/sdb`, you could create an entry like the following to do the job:

```
/dev/sdb4 /mnt/zip auto users,noauto 0 0
```

You will, of course, need to create the mount point—`/mnt/zip` in this example. Because the filesystem type is specified as `auto`, Linux should auto-detect the filesystem type, whether it's FAT, ext2fs, HFS, or anything else. You could use the `user` or `owner` option in place of `users`, depending on the precise rules you want to use for who may mount and unmount Zip disks. To test this change, you should first try `mount -a` as root. This command is necessary to register the new entry with Linux, even though Linux won't automount the disk. You can then type `mount /mnt/zip` as an ordinary user. The Zip disk should mount and become accessible. Typing `umount /mnt/zip` should unmount it.

### Criteria for Completion

To complete this task, you should have successfully added `/etc/fstab` entries for four items: a new `/home2` filesystem, additional swap space, an NFS export, and a user-mountable Zip disk. Each of these entries takes just one line in `/etc/fstab`.

## Task 5.6: Check Filesystem Integrity

Unfortunately, computers aren't perfect. Bugs, hardware failures, power outages, and other problems can cause data corruption. If left uncorrected, such problems can cause further data corruption, possibly leading to the loss of all the data on a disk. For this reason, Linux provides a tool, `fsck`, which checks the integrity of your filesystem's basic data structures. Knowing how to use `fsck` can help you keep your system healthy and fix problems when they occur.

> The `fsck` tool checks the *filesystem*'s data structures. It won't help you if *individual data files* become garbled unless that problem is directly related to a filesystem issue.

![](img/f430a19bdf014c43ad7c2d594afd5b21_244_0.png)

### Scenario

After your `/home2` filesystem has been in operation for some time, you begin hearing complaints from users about files vanishing, filenames changing, and other mysterious disk-related issues. You suspect the filesystem may have been damaged, so you want to check and repair it with `fsck`.

### Scope of Task

This task involves using a single `fsck` command and a couple of preparatory and clean-up commands, so the task itself is fairly limited. You should understand some of what `fsck` can and cannot do before you proceed, though.

### Duration

This task should take about half an hour to complete. A single run of `fsck` can take anywhere from a few seconds to many minutes (perhaps even over an hour), depending on the size of the filesystem, the speed of the disk, the number of files stored on the filesystem, and so on.

### Setup

You should have access to the disk you prepared in Tasks 5.2 and 5.3 or to some other convenient partition that's not required for system operation. (If necessary, you can create a filesystem on a floppy disk and use it to complete this task.) You must have superuser access to check a filesystem, so log in and acquire **root** privileges.

### Caveats

The usual caveats concerning **root** access apply to this task. Beyond these cautions, checking a filesystem is theoretically safe, even if you accidentally enter the wrong partition device code. Checking a filesystem that's currently mounted, though, is not safe; changes made by the filesystem check code can cause the kernel to become confused and result in additional corruption. Fortunately, `fsck` checks to see if you're calling it on a mounted filesystem and warns you about this. Be sure to read all the messages displayed by `fsck` as it operates. If you see a warning you don't understand or that causes you concern, tell the software to stop and research that message before proceeding.

### Procedure

To perform a disk check, you use the filesystem check (`fsck`) program. Ordinarily, its use is fairly straightforward. On occasion, though, you might want to use additional tools to give your filesystem a tune-up.

#### Basic Disk Checking

To check the integrity of a filesystem and automatically repair any damage, you can pass the device filename to `fsck`. If necessary, unmount the filesystem first:

```bash
# umount /dev/sda1
# fsck /dev/sda1
```

> As noted earlier, you should be sure the filesystem is unmounted before using `fsck`. Failure to unmount the filesystem can, paradoxically, cause filesystem damage.

The `fsck` program, like `mkfs`, is actually a front end to other programs, named `fsck.filesystem`, where `filesystem` is the filesystem name. Some filesystem utility packages provide additional links to their filesystem check programs, such as `e2fsck` for ext2 and ext3 file systems. Thus, you may have multiple options for how to check a file system, but `fsck` should always work—at least if a file system check program for your file system is installed.

> **NOTE**
> 
> Filesystem check programs are delivered in packages of support tools for particular filesystems. If you haven’t installed the relevant package, the appropriate filesystem check tool won’t exist. Linux lacks support entirely for checking some non-Linux file systems, although filesystem check tools for some common ones, such as FAT, do exist (called `fsck.msdos`).

The details of what happens when you use `fsck` depends on the file system and its specific checking program. In some cases, you’ll see one or more lines summarizing the actions the program is taking, which in the case of a clean file system will be nothing but checks. In other cases you’ll be asked to authorize certain actions, even including initiating the check operation. If the file system contains errors, you may be asked what to do about them. These prompts can be quite confusing, so taking the default action is usually the best approach unless you have expert knowledge. You can pass the `-a` option to have `fsck` perform file system cleaning options without prompting you about them.

Because each file system has unique features, file system check programs also support unique features. You can pass file system-specific options to the check programs by calling them directly or by passing them via `fsck` after a double dash (`--`) option. For instance, the `fsck.ext2` program doesn’t ordinarily perform a full check unless it finds that the file system hasn’t been cleanly unmounted. You can force it to check a file system by passing it the `-f` option:

```
# fsck /dev/sda1 -- -f
```

If you prefer, you can call `fsck.ext2` (or `e2fsck`) directly:

```
# fsck.ext2 -f /dev/sda1
```

All file system check programs support a wide variety of options. You may want to review the man pages for `fsck` and for the check programs for your most important file systems.

#### Tuning Your File System

Some file systems provide maintenance tools beyond their `fsck.filesystem` programs. The most notable of these tools is `tune2fs`, which is used to adjust the features of an ext2 or ext3 file system. You can change parameters that you ordinarily set at file system creation time and you can fine-tune the file system in other ways. This tool supports a very large number of options, so you should consult its man page for a complete listing. Some of the more interesting features you can change include the following:

**Adjust maximum mount count** Ext2fs and ext3fs require a periodic disk check with `fsck`. This check is designed to prevent errors from creeping into the disk undetected, and it’s normally performed automatically at boot time. You can adjust the maximum number of times the disk may be mounted without a check with the `-C` `mounts` option, where `mounts` is the number of mounts. You can trick the system into thinking the file system has been mounted a certain number of times with the `-C` `mounts` option; this sets the mount counter to `mounts`.
