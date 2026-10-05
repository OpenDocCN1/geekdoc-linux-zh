# 482 COMMAND REFERENCE

# sum file

sum calculates a 16-bit checksum and determines the number of blocks the file occupies on the hard disk (see also checksum on page 446).

# swapoff device

swapoffactivates the specified swap file or hard disk partition (see swapon).

# swapon device

swapon activates the device (usually a hard disk partition), or the file specified instead of it, a swap area. The partition or file must previously have been formatted with mkswap as a swap area. swapon is automatically executed at Linux startup for all swap areas listed in /etc/fstab. The command can only be executed by root. The correct setting of fstab in the context of system configuration is described on page 147.

# sync

Executes all buffered write operations on all hard disks. When an orderly termination of Linux is not possible, that is, when the commands shutdown, reboot and halt can no longer be executed and the computer does not react to `Ctrl+Alt+Del`, sync should be executed immediately before switching off. This is, however, only an emergency solution!

# tac file

tac displays the specified text file on screen in reverse order. that is, last line first (see also cat on page 443).

# tail [options] file

tail displays the last ten lines of a text file on screen.

+   -n lines displays the specified number of lines.

+   -f reads the file at regular intervals and displays all new lines. In this form, tail is particularly useful for viewing log files.

# Example

```
root# tail -f /var/log/messages
```

displays the last ten lines of messages. When new lines are added, these are displayed as well (so that after a short time the whole screen is used – not just ten lines).