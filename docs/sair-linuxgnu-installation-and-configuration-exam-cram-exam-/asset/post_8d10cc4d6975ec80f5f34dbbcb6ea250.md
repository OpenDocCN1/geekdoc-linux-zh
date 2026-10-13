
On an older hard drive, cylinder 1023 may be as low as 512MB.

If you're removing Linux from your computer, you can remove LILO from your MBR with the MS-DOS fdisk /MBR command. If you really want to do this, load the fdisk command on a bootable floppy disk first.

## Mounts (/etc/fstab/)

The volumes that you configured when you installed Linux, plus a few more, are included in the /etc/fstab/ file. The volumes shown in Figure 6.1 are mounted when Linux boots on your computer.

## Mount File Format

The key information is shown in the first three columns of the /etc/fstab/ file. The other columns are included for reference:

- **Volume**—The first column indicates the subject volume. For example, the volume in the first line of Figure 6.1 corresponds to the first logical drive on the first hard disk on your computer.
- **Mount point**—The second column corresponds to the directory mounted on the specified volume. For example, the second line of Figure 6.1 shows the /boot directory mounted on the first partition on the first hard drive.
- **Format**—The third column corresponds to the way each volume is mounted. For example, ext2 corresponds to the second extended file system.
- **Mount option**—The fourth column specifies the types of users that can mount, whether they can read or write, and what can be run from the mounted directory.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_131_0.png)

Figure 6.1 A sample /etc/fstab file.

- Dump—The fifth column specifies whether to dump changes to the memory cache or directly to the mounted volume. If this value is 0, data is written directly to the file system. If this value is 1, data is stored in the cache.
- Mount order—The sixth column determines when the volume is mounted. If this value is 0, the volume is normally mounted by users after they log in. If this value is 1, the volume is mounted when you start Linux. Mount order is commonly associated with the root (/) directory. If this value is 2, Linux mounts another directory after the root directory.

## Mount File Flexibility

The /etc/fstab file is flexible. You can mount additional volumes through this file, but you should test this function before you add volumes. For example, if you've installed both Microsoft Windows and Linux on the same computer, you might be able to mount your Windows C: drive with the following command:

```
mount -t vfat /dev/hda2 /disks/c
```

This command mounts a volume that is formatted to VFAT (Virtual File Allocation Table), which is Microsoft's virtual file system that works with long file names (-t corresponds to type). The volume is the second primary partition (/dev/hda2). The mount point is the /disks/c directory.

If you have a VFAT volume mounted on /dev/hda2, this command should work. If it does, you can verify it with the ls /disks/c command. You can then make sure Linux mounts this volume whenever you boot by entering the following line in your /etc/fstab file:

/dev/hda2   /disks/c   vfat   defaults   0   2

The defaults option allows any user to mount, read, and write to the given directory. The 0 means that files transferred to and from this directory are cached. The 2 refers to directories that are mounted after the root directory.

If you need to add additional Linux volumes, you can use tools like fdisk or fips to create them. You can then format them with the mk2fs command to set up the Linux second extended file system (ext2fs) or the mkswap command to set up another swap partition. Once formatted, you can mount a directory on a new volume by adding its entry into the /etc/fstab file.

## Loading Sequence

To see how Linux loads on your computer, analyze the /etc/inittab file in detail. In essence, when Linux starts up, it loads scripts in a three-stage process. First, it loads system initialization scripts from an rc.sysinit file. Second, it loads scripts associated with different run levels in various rc.d directories. Third, it loads custom scripts in an rc.local file.

When these steps are complete, Linux then sets up your system in a specific run level, as defined by the initdefault variable. Whatever you do, don't set initdefault to 0 or 6. If you do, your system will shut down or reboot whenever you try to start Linux.

## Initialization Scripts (rc.sysinit)

The first resource control file to run when you boot Linux is the rc.sysinit file. It starts several programs. It also mounts volumes as defined in the /etc/mtab file as well as some basic network programs.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_133_0.png)

> The /etc/mtab file lists the volumes from /etc/fstab that are mounted when Linux starts on your computer.

The rc.sysinit script also sets up your PATH variable, which defines where Linux looks for different commands. To check your current path settings, type the command "echo $PATH". You might get the following result:

/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin:/home/mj/bin

When you type in a command such as who, Linux looks through the directories listed in the PATH variable for this command. If you don't include the current directory in PATH, this can be inconvenient. For example, let's assume you created a script named goodidea in your home directory. If you were in your home directory, you'd have to type the ./goodidea command to run the script. This would not be necessary if your PATH variable included the dot (.).

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_133_1.png)

> There are advantages and disadvantages to including a dot (.) in your PATH variable. For security reasons, this is generally discouraged; crackers (malicious users) could place destructive programs with familiar names in users' local directories. For example, if a cracker inserted a program named who in your home directory, and you had the dot in your PATH variable, you'd run whatever the cracker wanted you to run when you typed the who command. These types of programs are sometimes known as Trojan horses. This is not a problem, of course, if you're running a standalone Linux computer.

## Run Level Scripts (rc#.d)

The /etc/inittab file runs daemons and scripts at each run level. If you want to see what is run at each level, list the files in the applicable directory. For example, if you want to see what programs are started and shut down when you halt (run level 0), type the following command:

```
ls /etc/rc.d/rc0.d
```

The commands typically start with S (for start) or K (for kill). For example, if you see the K23nfsd command, you know that Linux kills the Network File System (NFS) daemon at the applicable run level. You can see a typical list of daemons and other commands used by your run level scripts in Figure 6.2.

> TIP The scripts in each rc.d run level link to files in the init.d directory. Depending on your distribution, you may find the /init.d directory under /etc or /etc/rc.d. The /init.d directory includes scripts that you can use to start or stop daemons after Linux boots on your system. Two example daemons in this directory are Apache (httpd) and the Network File System (nfsd).

## The Local Run Level Script (rc.local)

If you have your own scripts that you want run whenever you start Linux, add them to the rc.local shell script. They are run after Linux sets up in the initdefault run level.

## Common Run Levels

You learned about run levels in Chapter 3. The following is a list of run levels used by all distributions:

- Shutdown—All distributions use run level 0 for shutdowns. This level ends all programs and daemons. This level is also known as halt. The root or superuser can start this run level with the init 0 command.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_134_0.png)

Figure 6.2 Sample list of daemons.

- **Reboot**—All distributions use run level 6 to reboot. This is a two-step process. It first moves Linux to run level 0. When Linux reboots, it moves to a standard multiuser level, usually 2 or 3, depending on your Linux distribution. The root or superuser can start this run level with the `init 6` command.
- **Single User**—All distributions have a single-user mode. It is standard when you use a rescue disk to boot your Linux computer. You can also start single-user mode when you don't want anyone else using your Linux computer for administrative reasons. Generally, single-user mode is configured at run level 1 or S.
- **Multiuser**—All distributions have some form of multiuser run levels. Sometimes it's available with or without networking. It is generally at run level 2 or 3.
- **X Window**—Linux distributions use different graphical user interface (GUI) setups at run levels 3, 4, and/or 5.

You can change your default run level by changing the number associated with the initdefault variable in your /etc/inittab file. For example, you can change your default boot from the X Window to the command-line interface by entering the appropriate multiuser run level.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_135_0.png)

> Only the root or superuser can run the init command. The superuser mode is sometimes also known as sudo.

## Logins

If you've ever used Unix or Linux at the command line, you should be familiar with the following lines of code:

```
login:
Password:
```

Any successful login at the command line starts a command-line shell. The shell that it starts depends on the control files in your home directory.

## Shells

A shell is in part a command-line interface for controlling various parts of your computer through the Linux kernel. In essence, it is set up to protect the kernel. If the kernel fails, you need to restart your computer. If your shell fails, you don't have to restart. Instead, you can kill the shell and log in to Linux again.
