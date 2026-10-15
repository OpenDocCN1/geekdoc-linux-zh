# Recover

The command dd will read every single block of the partition. In case of problems it is better to use the option conv=sync,noerror so dd will skip the bad block and write zeros at the destination. Accordingly it is important to set the block size equal or smaller than the disk block size. A 1k size seems safe, set it with bs=1k. If a disk has bad sectors and the data should be recovered from a partition, create an image file with dd, mount the image and copy the content to a new disk. With the option noerror, dd will skip the bad sectors and write zeros instead, thus only the data contained in the bad sectors will be lost.

```
# dd if=/dev/hda of=/dev/null bs=1m          # Check for bad blocks
# dd bs=1k if=/dev/hdal conv=sync,noerror,notrunc | gzip | ssh \ # Send to remote
# root@fry 'dd of=/dev/hdal.gz bs=1k'
# dd bs=1k if=/dev/hdal conv=sync,noerror,notrunc of=hda1.img   # Store into an image
# mount -o loop /hda1.img /mnt                 # Mount the image (page 13)
# rsync -aX /mnt/ /newdisk/                    # Copy on a new disk
# dd if=/dev/hda of=/dev/hda                   # Refresh the magnetic state
# The above is useful to refresh a disk. It is perfectly safe, but must be unmounted.
```

# Delete

```
# dd if=/dev/zero of=/dev/hdc             # Delete full disk
# dd if=/dev/urandom of=/dev/hdc           # Delete full disk better
# kill -USR1 PID                            # View dd progress (Linux)
# kill -INFO PID                            # View dd progress (FreeBSD)
```

# MBR tricks

The MBR contains the boot loader and the partition table and is 512 bytes small. The first 446 are for the boot loader, the bytes 446 to 512 are for the partition table.

```
# dd if=/dev/sda of=/mbr_sda.bak bs=512 count=1   # Backup the full MBR
# dd if=/dev/zero of=/dev/sda bs=512 count=1      # Delete MBR and partition table
# dd if=/mbr_sda.bak of=/dev/sda bs=512 count=1    # Restore the full MBR
# dd if=/mbr_sda.bak of=/dev/sda bs=446 count=1    # Restore only the boot loader
# dd if=/mbr_sda.bak of=/dev/sda bs=1 count=64 skip=446 seek=446 # Restore partition table
```

# 14.6 screen

Screen (a must have) has two main functionalities:

+   - Run multiple terminal session within a single terminal.
+   - A started program is decoupled from the real terminal and can thus run in the background. The real terminal can be closed and reattached later.

# Short start example

start screen with:

```
# screen
```

Within the screen session we can start a long lasting program (like top).

```
# top
```

Now detach with Ctrl-a Ctrl-d. Reattach the terminal with:

```
# screen -R -D
```

In detail this means: If a session is running, then reattach. If necessary detach and logout remotely first. If it was not running create it and notify the user. Or:

```
# screen -x
```

Attach to a running screen in a multi display mode. The console is thus shared among multiple users. Very useful for team work/debug!

# Screen commands (within screen)

All screen commands start with Ctrl-a.

+   - Ctrl-a ? help and summary of functions