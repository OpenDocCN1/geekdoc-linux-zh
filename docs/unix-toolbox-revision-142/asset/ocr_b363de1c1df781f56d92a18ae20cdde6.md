# 3 FILE SYSTEM

Disk info (p9) | Boot (p9) | Disk usage (p9) | Opened files (p9) | Mount/remount (p10) | Mount SMB (p11) | Mount image (p12) | Burn ISO (p12) | Create image (p13) | Memory disk (p14) | Disk performance (p14)

# 3.1 Permissions

Change permission and ownership with chmod and chown. The default umask can be changed for all users in /etc/profile for Linux or /etc/login.conf for FreeBSD. The default umask is usually 022. The umask is subtracted from 777, thus umask 022 results in a permission 0f 755.

```
1 --x execute          # Mode 764 = exec/read/write | read/write | read
2 -w- write            # For:      |-- Owner --|  |- Group -|  |Oth|
4 r-- read             
ugo=a                  u=user, g=group, o=others, a=*everyone
```

```
# chmod [OPTION] MODE[,MODE] FILE      # MODE is of the form [ugoa]*([+-=])[(rwxXst])
# chmod 640 /var/log/maillog           # Restrict the log -rw-r-----
# chmod u=rw,g=r,o= /var/log/maillog   # Same as above
# chmod -R o-r /home/*                 # Recursive remove other readable for all users
# chmod u+s /path/to/prog              # Set SUID bit on executable (know what you do!)
# find / -perm -u+s -print             # Find all programs with the SUID bit
# chown user:group /path/to/file       # Change the user and group ownership of a file
# chgrp group /path/to/file            # Change the group ownership of a file
# chmod 640 `find ./ -type f -print`   # Change permissions to 640 for all files
# chmod 751 `find ./ -type d -print`   # Change permissions to 751 for all directories
```

# 3.2 Disk information

```
# diskinfo -v /dev/ad2           # information about disk (sector/size) FreeBSD
# hdparm -I /dev/sda              # information about the IDE/ATA disk (Linux)
# fdisk /dev/ad2                  # Display and manipulate the partition table
# smartctl -a /dev/ad2            # Display the disk SMART info
```

# 3.3 Boot

# FreeBSD

To boot an old kernel if the new kernel doesn't boot, stop the boot at during the count down.

```
# unload
# load kernel.old
# boot
```

# 3.4 System mount points/Disk usage

```
# mount | column -t          # Show mounted file-systems on the system
# df                         # display free disk space and mounted devices
# cat /proc/partitions       # Show all registered partitions (Linux)
```

# Disk usage

```
# du -sh *                   # Directory sizes as listing
# du -csh *                   # Total directory size of the current directory
# du -ks * | sort -n -r       # Sort everything by size in kilobytes
# ls -lSr                     # Show files, biggest last
```

# 3.5 Who has which files opened

This is useful to find out which file is blocking a partition which has to be unmounted and gives a typical error of: