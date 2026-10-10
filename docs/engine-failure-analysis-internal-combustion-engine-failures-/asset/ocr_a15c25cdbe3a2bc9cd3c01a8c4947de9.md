# EXAMPLES

This Command | Does the Following
---|---
`rdev /boot/vmlinuz /dev/hda5` | Sets the root device (/boot/vmlinuz) to the specified boot device (/dev/hda5).
`dd if=/boot/vmlinuz of=/dev/fd0 bs=8192` | Creates an emergency floppy boot disk.

# setfdprm

`setfdprm [ option ] device [ name ] [ parameter ]`

Set the parameters for the specified device, which is an auto-detecting floppy drive device (`/dev/fd0` or `/dev/fd1`). You can specify the parameters manually by using options, or you can specify a name (such as `720/1440`) that corresponds to a line in `/etc/fdprm`.

# OPTIONS

Use This Option | To Do This
---|---
`-c` | Clear the current parameters.
`-n` | Disable format-configuring messages.
`-P` | Set the specified parameter (dev, size, sec, heads, tracks, stretch, gap, rate, spec1, or fmt_gap). See /etc/fdprm for these values. You can specify more than one parameter in a blank, space-separated list.
`-Y` | Enable format-configuring messages.

# sync

`sync [ option ]`

Flushes the filesystem buffers. After `sync` runs, disk usage statistics are accurate.

See also df, du.