```
$ ./.ph Mary
Mary Jones 608-555-1212
```

The `chmod` command makes the `ph` script executable. The `./ph` command runs the `ph` command from the current directory with the `new` option. This adds Mary Jones as the name and 608-555-1212 as the phone number to the database (`$HOME/.phone.txt`). The next `ph` command searches the database for the name Mary and displays the phone entry for Mary. If the script works, add it to a directory in your `PATH` (such as `$HOME/bin`).

# ### A simple backup script

Because nothing works forever and mistakes happen, backups are just a fact of life when dealing with computer data. This simple script backs up all the data in the home directories of all the users on your Fedora or RHEL system.

```
#!/bin/bash
# (@)/my_backup
# A very simple backup script
#
# Change the TAPE device to match your system.
# Check /var/log/messages to determine your tape device.
# You may also need to add ascii-tape support to your kernel.
TAPE=/dev/rft0

# Rewind the tape device $TAPE
mt $TAPE rew
# Get a list of home directories
HOMES=`grep /home /etc/passwd | cut -f6 -d':' `
# Backup the data in those directories
tar cvf $TAPE $HOMES
# Rewind and eject the tape.
mt $TAPE rewoff
```

> **CROSS-REFERENCE:** See Chapter 13 for details on backing up and restoring files and getting the `mt` command (part of the tape-tools packages that must be installed separately).

# ## System Initialization

When you turn on your computer, a lot happens even before Fedora or RHEL starts up. Here are the basic steps that occur each time you boot up your computer to run Fedora or RHEL:

+   1. **Boot hardware** — Based on information in the computer’s read-only memory (referred to as the BIOS), your computer checks and starts up the hardware. Some of that information tells the computer which devices (floppy disk, CD, hard disk, and so on) to check to find the bootable operating system.