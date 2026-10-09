As a compromise between speed and safety, you can combine the `su` or `sudo` and `kill` utilities by using the `su -c` or the `sudo -u` option. The following command runs the `kill` command with the identity of Sam (Sam’s privileges):

```
# su sam -c "kill -TERM 3730"
```

*or*

```
$ sudo -u sam kill -TERM 3730
```

See also killall (next) and pkill (next page).

# killall: KILLs A COMMAND

The `killall` utility is similar to `kill` (previous) but uses a command name instead of a PID number. Give the following command to `kill` all your processes that are running gnome-calculator or vi:

```
$ killall gnome-calculator vi
```

Running this command while working with root privileges kills all processes running gnome-calculator or vi. See also kill (page 465) and pkill (next page).

# lshw: DISPLAYS HARDWARE INFORMATION

The lshw utility (lshw package) lists system hardware. This utility provides complete information only when run with root privileges. Use the -short option to display a brief listing. See page 636 for more information.

# mkfs: CREATES A FILESYSTEM

The `mkfs` utility creates a new filesystem on a device, destroying all data on the device as it does so. This utility is a front end for many utilities, each of which builds a different type of filesystem. By default, `mkfs` builds an `ext2` filesystem and works on a hard disk partition. Although it can take many options and arguments, you can use `mkfs` simply as

```
# mkfs device
```

where *device* is the name of the device (e.g., /dev/hda2, /dev/sdb1, /dev/sr0) you want to make a filesystem on. Use the -t option to specify a type of filesystem. For example, the following command creates an ext4 filesystem on /dev/sda2:

```
# mkfs -t ext4 /dev/sda2
```

# pidof: DISPLAYS PID NUMBERS OF COMMANDS

The `pidof` utility displays the PID number of each process running the command you specify:

```
$ pidof httpd
567 566 565 564 563 562 561 560 553
```

If it is difficult to find the right process, try using `top`. Refer to the man pages for these utilities for more information, including lists of options.