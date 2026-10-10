
**8.** A. Symbolic links can point across filesystems, so creating a symbolic link from one filesystem (in which your home directory resides) to another (on the CD-ROM) isn't a problem. Hard links, as in options B and C, are restricted to a single filesystem and so won't work for the described purpose. Because symbolic links will work as described, option D is incorrect.

**9.** D. Option D is the correct command. Typing `chown ralph:tony somefile.txt`, as in option A, sets the owner of the file to `ralph` and the group to `tony`. The `chmod` command used in option B is used to change file permissions, not ownership. Option C reverses the order of the filename and the owner.

**10.** C, D. The `d` character that leads the mode indicates that the file is actually a directory, whereas the `r` symbol in the `r-x` triplet at the end of the symbolic mode indicates that all users of the system have read access to the directory. Symbolic links are denoted by leading `l` characters, which this mode lacks, so option A is incorrect. Although the `x` symbols usually denote executable program files, as specified in option B, in the case of directories this permission bit indicates that the directory's contents may be searched; executing a directory is meaningless.

**11.** C. The set user ID (SUID) bit enables programs to run as the program's owner rather than as the user who ran them. This makes SUID root programs risky, so setting the SUID bit on root-owned programs should be done only when it's required for the program's normal functioning, as stated in option C. This should certainly *not be* done for all programs because the SUID bit is *not* required of all executable programs as option A asserts. Although the SUID root configuration does enable programs to access device files, the device files' permissions can be modified to give programs access to those files, if this is required, so option B is incorrect. Although SUID root programs are a security risk, as stated in option D, they're a necessary risk for a few programs, so option D goes too far.

**12.** D. Using symbolic modes, the `o+r` option adds read (r) permissions to the world (o). Thus, option D is correct. Option A sets the mode to `rwxr----x`, which is a bit odd and doesn't provide world read access to the file, although it does provide world execute access. Option B sets the mode to `rw-r-----`, which gives the world no access whatsoever to the file. Option C adds read access to the file for the owner (u) if the owner doesn't already have this access; it doesn't affect the world permissions.

**13.** D. Option D, 027, removes write permissions for the group and all world permissions. (Files normally don't have execute permissions set, but explicitly removing world execute permissions when removing read permissions ensures reasonable behavior for directories.) Option A, 640, is the octal equivalent of the desired `rw-r-----` permissions; but the umask sets the bits that are to be *removed* from permissions, not those that are to be set. Option B, 210, would remove write permission for the owner, but it wouldn't remove write permission for the group, which is incorrect. This would also leave all world permissions open. Finally, option C, 022, wouldn't remove world read permission.

**14.** B. Using quotas requires kernel support, the `usrquota` or `grpquota` (for user or group quotas) filesystem mount option, and activation via the `quotactl` command (which often appears in `SysV` startup scripts). Thus, option B is correct. Option A suggests that `quotao` is not necessary, and option C suggests that `quotaon` is sufficient, but neither is true. The `usrquota` and `grpquota` options are both valid, so option D is incorrect.

**B.** The `requota` utility is used to summarize the quota information about the filesystem. When used with the `-a` option, it shows this information for all filesystems. The `quotacheck` utility checks quota information about a disk and writes corrections.

**16.** **D.** The `/opt` directory tree exists to hold programs that aren't a standard part of a Linux distribution, such as commercial programs. These programs should install in their own directories under `/opt`; these directories usually have `bin` subdirectories of their own, although this isn't required. The `/usr/sbin` directory holds programs that are normally run only by the system administrator, and `/bin` holds critical basic binary files. The `/etc/X11` directory holds X-related configuration files. None of these directories is an appropriate place for a spreadsheet program.

**17.** **A.** The `find` utility operates by searching all files in a directory tree, and so it's likely to take a long time to search all of a computer's directories. The `locate` program uses a precompiled database, and `whereis` searches a limited set of directories, so these commands will take less time.

**18.** **C.** The `type` command identifies a command, as executed by the `shell`, as being a built-in shell command, a shell alias, or an external command, whereas `whereis` command helps find the location of external command files. Neither `type` nor `whereis` identifies the CPU architecture of a program file, can locate commands based on intended purpose, or complete an incompletely typed command.

**19.** **B.** The `find` command includes the ability to search by username using the `-user *name*` option, where *name* is the username; thus, option B is correct. The `-uid` option to `find` can also locate files owned by a user; it takes a numeric user ID (UID) number as an argument, so option A isn't quite correct. The `locate` command provides no ability to search by user, so options C and D are incorrect.

**20.** **D.** The `which` program searches the path just as `bash` does, but it prints the path to the first executable program it finds on the path. Thus, option D is correct. The `which` program doesn't conduct an exhaustive search of the system, so there could be many more files called `man` on the system, contrary to option A. System package tools and which aren't closely related; option B is incorrect. Although `/usr/bin/man` would be run when the user whose `which` output matches that in the question types `man`, this may not be true of others because the path can vary from one user to another. Thus, option C is incorrect.

## Chapter 5
### Booting Linux and Editing Files

![](img/f339a9f48c4b443e61c74acb4c9c3da4_284_0.png)

THE FOLLOWING COMPTIA LINUX+ OBJECTIVES ARE COVERED IN THIS CHAPTER:

- 1.101.2: Boot the system
- 1.101.3: Change runlevels and shutdown or reboot system
- 1.102.2: Install a boot manager
- 1.103.8: Perform basic file editing operations using vi

![](img/f339a9f48c4b443e61c74acb4c9c3da4_285_0.png)

So far, this book has dealt largely with a running Linux system, but from time to time, you’ll need to boot Linux. Ordinarily this process is a painless one: You press the power button, wait a couple of minutes, and see a Linux login prompt. Sometimes, though, you’ll have to intervene in this process in one way or another.

Linux boot loaders can be configured to boot Linux with particular options and even to boot other operating systems, so knowing how to configure them and use them can help you to accomplish your boot-related goals. Once the system is booted, you should know how to study log files related to the boot process. This can help you to diagnose problems or verify that the system is operating the way it should be.

Finally, this chapter looks at editing files with Vi. Vi isn’t particularly boot-related, knowing how to edit files is vital to many administrative tasks, including editing the boot loader configuration files.

## Installing Boot Loaders

Hard disks contain more than partitions and their contents. One very small part of the disk is unusually important: The *master boot record* (MBR) contains the MBR partition table and a *boot loader* (also sometimes called a *boot manager*). The boot loader is the software that the BIOS reads and executes when the system begins to boot. The boot loader, in turn, is responsible for loading the Linux kernel into memory and starting it running. Thus, configuring a hard disk (or at least your boot hard disk) isn’t complete until the boot loader is configured. Although Linux distributions provide semi-automated methods of configuring a boot loader during system installation, you may need to know more, particularly if you recompile your kernel or need to set up an advanced configuration—say, one to select between several OSs.

In practice, two boot loaders are important in Linux: the *Linux Loader* (LILO) and the *Grand Unified Boot Loader* (GRUB). LILO is older, and it’s slowly being replaced by GRUB as the most common Linux boot loader, but LILO is still common.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_285_1.png)

> **NOTE** LILO and GRUB are both x86 and x86-64 boot loaders. Other platforms have their own boot loaders. Some of these are similar to LILO in operation (and may even be called LILO), but they aren’t quite identical. You should consult platform-specific documentation if you need to reconfigure a non-x86 boot loader.
