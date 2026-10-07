
You can use `tar` to copy files to tapes or floppies by specifying a device name and the `f` option as a device name. To archive files in `/usr/tparker` to a floppy disk in the first drive, you could use the following command:

```
tar cvf /dev/fd0 /usr/tparker
```

This can cause a problem if the floppy doesn't have enough capacity, however, so `tar` lets you specify the capacity with the `k` option. In this case, the command for a 1.44MB floppy is as follows:

```
tar cvfk /dev/fd0 1440 /usr/tparker
```

If the floppy is full before the entire archive has been copied, `tar` prompts you for another one. It's important to keep the arguments in the right order. You see that the `f` is before the `k`, so the device name must be before the capacity. All the argument keyletters are gathered together instead of being issued one at a time followed by their value, which is one aspect of `tar` that can be very confusing.

As a last issue in backing up to floppy, it is sometimes necessary to tell the `tar` program about the blocking used (blocking identifies how many blocks are used for each chunk of information on the device). A floppy usually has a blocking factor of 4, so the command becomes the following:

```
tar cvfkb /dev/fd0 1440 4 /usr/tparker
```

A final problem with `tar` is that it can't always handle a generic device such as `/dev/fd0` and must be specifically told the disk type.

For more complete information on all the options used by `tar`, check the man pages or, even better, a good system administration book.

You can use `tar` to archive compressed files, too, in the same manner. You can also compress a `tar` file without any problems. In these cases, you might get filenames such as the following:

```
fileName.tar.gz
```

Filenames such as this show that you should run `gunzip` first to recover the `tar` file, and then run `tar` to extract the files in the archive. You can run the commands together with pipes:

```
gunzip fileName.tar.gz | tar xvf -
```

The hyphen representing the `tar` filename after the pipe symbol is standard UNIX terminology for taking the input from the pipe (stdin). The `tar` command has a lot of other options, many of which are obsolete or seldom used. We look at `tar` in more detail in Chapter 45, "Backups."

## Backups

The three rules of system administration are back up, back up, and back up. This might sound silly and trite, but a backup can save you whenever you do something silly to the file system or when problems occur. With UNIX, most backups are made to a tape device using tar, although many Linux users don't have tape units available and have to resort to floppies.

Backups are made with the tar utility, as mentioned earlier. The procedure is exactly the same as shown earlier. To back up the entire system on floppy, the command is as follows:

```
tar cvfbk /dev/fd0 1440 4 /
```

To back up to a high-capacity tape device larger than the file system (and hence not needing a capacity limit), called /dev/rct0, the command is

```
tar cvfk /dev/rct0 20 /
```

In many cases, you won't want to back up the entire system, because it's easier to reinstall off a CD-ROM. However, you should back up your user files by either backing up the entire /usr directory or specifically backing up your own home directory.

To restore a backup, you use the tar command again:

```
tar xvrf /dev/rct0
```

This recovers all files from the tape device /dev/rct0. You can explicitly restore specific files if you need to.

Several commercial products offer automated backups, although you can do this quite easily with the cron command.

## Setting Up Your System

You can perform several little tasks to tweak or optimize your Linux system, although in many cases they are dependent on the version you are running and other applications coexisting. We can look at a few of the miscellaneous tasks here.

### Setting the System Name

The system name is contained in a file called /etc/HOSTNAME. It is simply the name the system calls itself for identification, which is especially useful if you are networking your Linux machine with others. Your system name (also called a host name) is what other machines will identify your machine as, so make it a unique and descriptive name. You can call the system anything you want.

To set your system name, you can either edit the system files (which should be followed by a reboot to make the changes effective) or use the hostname command. The following command sets the machine's name to `hellfire`:

`hostname hellfire`

### Using a Maintenance Disk

Every system should have a maintenance disk that enables you to check the root file system, recover from certain disk problems, and solve simple problems such as forgetting your root password. The emergency disks, also called the boot/root floppies, are created with the setup program in most distributions of Linux when the configuration is changed.

You can usually create an emergency boot disk from the CD-ROM that the system came on, as well as obtain the necessary files from FTP sites.

After you have booted your machine with the emergency disk, you can mount the disk partitions with the `mount` command.

### Forgetting the root Password

This is an embarrassing and annoying problem, but one luckily easily fixed with Linux. (If only other UNIX systems were so easy!) To recover from a problem with the root password, use a boot floppy and boot the system. Mount the root partition, and edit the `/etc/passwd` file to remove any password for root; then, reboot from the hard disk.

After the system has booted, you can set a password again.

> **WARNING**
>
> This points out one major security problem with Linux: Anyone with a boot floppy can get unrestricted access to your system!

### Setting the Login Message

If you have more than one user on the system, you can display information about the system, its maintenance, or changes in a file called `/etc/motd` (message of the day). The contents of this file are displayed whenever someone logs in.

To change the `/etc/motd` file, use any text editor and save the contents as ASCII. You can make the contents as long as you want, but readers usually appreciate brevity. The /etc/motd file is useful for informing users of downtime, backups, or new additions. You can also use it to give a more personal feel to your system.

## Summary

System administration is not a complicated subject, unless you want to get into the nitty-gritty of your operating system and its configuration. For most Linux users who use the operating system for their personal experimentation, the administration steps explained in this chapter should be sufficient for most purposes. If you want to get into more detail, check out a good UNIX system administration book. From here, you may want to learn more about the following topics:

- SCSI (Small Computer Systems Interface) devices and how they add to your Linux system's flexibility are discussed in Chapter 36, “SCSI Device Support.”
- Setting up email on your Linux system are discussed in Chapter 40, “Configuring Linux for Mail.”
- The tar command, backups, and the importance of making backup copies of your system are discussed in Chapter 45, “Backups.”

# Devices

by Tim Parker

## In This Chapter

- Character and block mode devices 584
- Printer Administration 587
- Terminals 596
- Adding a modem 607

## CHAPTER 33

This chapter is devoted to devices that might be attached to your Linux system, such as terminals, modems, and printers. It shows you how to add and manage the different devices, and it also looks at many of the Linux commands you will need to properly administer your system.

All of this information is necessary if you are to have a smoothly running system. Even if you don’t intend to add terminals or modems, you should know about the startup process and how the configuration files are handled.

## Character and Block Mode Devices

Everything attached to the computer you are using to run Linux is treated as a device by the operating system. It doesn’t matter whether the device is a terminal, a hard disk, a printer, a CD-ROM drive, or a modem. Everything that accepts or sends data to the operating system is a device.

The concept of treating everything on the system as a device is one of the benefits of the UNIX architecture. Each device has a special section in the kernel, called a device driver, which includes all the instructions necessary for Linux to communicate with the device. When a new device is developed, it can be used with Linux by writing a device driver, which is usually a set of instructions that explains how to send and receive data.

Device drivers allow the Linux kernel to include only the operating system and support software. By having the instructions for talking to devices within a set of files, they can be loaded as needed (in the case of rarely used devices) or kept in memory all the time when the operating system boots. As refinements are made to a peripheral, small changes to the device driver file can be linked into the kernel to keep the operating system informed of the new features and capabilities.

When an application instructs a device to perform an action, the Linux kernel doesn’t have to worry about the mechanism. It simply passes the request to the device driver and lets it handle the communications. Similarly, when you’re typing at the keyboard, your terminal’s device driver accepts the keystrokes and passes them to the shell or application, filtering out any special codes that the kernel doesn’t know how to handle by translating them into something the kernel can perform.

Linux keeps device files in the /dev directory, by default and convention. It is permissible to keep device files anywhere on the file system, but keeping them all in /dev makes it obvious that they are device files.

Every type of device on the Linux system communicates in one of two ways: character by character or as a set of data in a predefined chunk or block. Terminals, printers, and
