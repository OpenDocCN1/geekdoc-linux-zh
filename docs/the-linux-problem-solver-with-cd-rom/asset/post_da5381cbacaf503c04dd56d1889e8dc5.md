
Because more than one process may attempt to modify the passwd file at once, you have to do some locking through the file /etc/ptmp. If available, the vipw command is the preferred way to modify /etc/passwd directly. A passwd entry looks like this:

```
bob:x:3119:100:Bob the Tormented:/home/bob:/bin/bash
```

As you can see, colons (:) separate the fields, and they are fairly straightforward. Only the second field, the encrypted password, deserves some mention. The example above shows a shadow password scheme, which puts the encrypted password into /etc/shadow, where the user can’t read it. This is meant as a security measure (although its effectiveness is somewhat dubious). Most major distributions use shadow passwords or give you the option.

Unix does not keep a user’s password around in its original (plain-text or cleartext) form; that would make the password too easy to steal. Instead, it encrypts the passwords on the spot and stores them in encrypted form. When the user types a password, Unix encrypts it and matches it against the one on the system.

On larger networks, it’s a hassle to maintain passwd files for many users across machines. That’s where systems like NIS come in (see Chapter 3).

Relevant man pages: passwd (5), passwd (1), shadow (5)

## Devices

Unix programs talk to devices through device files found in /dev. Device file names include tty1, hda3, and audio. Interaction with the device files using regular programs like cat and dd yields different results depending on the kind of file and its permissions (these vary, since you may not want a regular user to scribble all over a raw hard disk device, for example).

If you look in /dev, you’ll find a lot of devices there (also called special files). Do you really have all of this stuff on your system, and what do the device names correspond to? The answer to the first question is no; if you try to do an operation on a device that doesn’t exist on your machine, either you’ll get an error message like “/dev/device: No such device” or your command will just wait forever for the nonexistent device to become available. As far as the second question goes, the device names are up to the programmers. Here is a list of a few basic device names.

- /dev/tty* Terminal devices of some sort. They all work through the same interface.
- /dev/ttyn (where n is a number) Linux virtual consoles.
- /dev/ttys* Serial ports.
- /dev/ptyq*, /dev/ptyq*, .. Pseudo-terminals: xterm, telnet, ssh, and other shell-invoking programs use these (they emulate the rather archaic interface of a real terminal in order to provide compatibility for terminal-reliant shells and programs).

/dev/hd* ATA/IDE devices; these can include ATA hard disks, CD-ROM drives, removable media, and so on. The device without any number after it refers to the whole disk; with a number, it refers to a partition. For example, /dev/hda2 is the second partition on the master disk of the primary interface.

/dev/sd* SCSI disks; can include removable media. Partitioning is similar to that of ATA/IDE devices. However, unlike schemes on other operating systems and the ATA/IDE naming convention, the SCSI disks are assigned the names /dev/sda, /dev/sdb, and so on, in the order in which they appear to the SCSI host adapter (controller). /dev/sda is the lowest SCSI ID on the first SCSI host adapter (scsi0) with disks, /dev/sdb is the next ID up. If you have multiple SCSI host adapters in your system, the assignment follows the ordering of the host adapters; first the devices on scsi0 are assigned, then scsi1, and so on.

/dev/scd* SCSI CD-ROM drives.

/dev/sg* Generic SCSI devices. With a generic SCSI device, a user program can interact directly with any SCSI device without a special kernel driver. Scanning and CD-burning programs use the generic SCSI devices.

/dev/null Anything written to /dev/null goes into the proverbial bitbucket; it's thrown away. If read from, the result is an end of file (EOF).

/dev/zero Reads from this return null characters (every bit is zero).

/dev/fd* Floppy disks (of various geometries).

/dev/audio, /dev/dsp, /dev/midi, /dev/mixer, /dev/sequencer Various sound devices.

/dev/lp* Parallel ports.

/dev/psaux The PS2 auxiliary port. Most PCs come with these mice. These are not USB mice, which may become popular in the near future.

## Examining and Creating Devices

ls -l /dev/hdb1 reveals this:

```
brw-rw---- 1 root disk 3, 65 Jul 26 1998 /dev/hdb1
```

Most of the fields appear as ls would present them for normal files, except that there is a b at the beginning of the first field, and two numbers (here, 3 and 65) have replaced the size field. The b means it is a block device (character devices have a c instead). The two numbers in place of the size are the major and minor device numbers. Each major number is assigned to one device driver, and the minor numbers go to the devices that use the driver (for example, an ATA/IDE driver, which handles disks, CD-ROMs, and other hardware). The kernel assigns the major and minor numbers.

To make a device, use the mknod command. The command to make the /dev/hda1 above would be
