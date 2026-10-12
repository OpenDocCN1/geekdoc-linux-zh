The best time to deal with a system crash is before the crash happens. This means being prepared with a good backup plan, good backups, emergency boot disks, and copies of important files. These issues are covered in this section, along with tips and hints for maintaining your file system integrity and system security.

Here are some Do's to help you avoid problems:

+   - Do make a backup after a clean install and setup.
+   - Do create a set of emergency boot disks with your current kernel.
+   - Do use the `shutdown` command.
+   - Do consider using an uninterruptible power supply (UPS).
+   - Do use `fsck`, `mbadblocks`, or `badblocks` to check floppy disks.
+   - Do make backups of important files on floppy disks or other removable media.
+   - Do use your filesystem tools.
+   - Do consider using flash RAM if you use a laptop.
+   - Do read Lars Wirzenius's *Linux System Administrators' Guide 0.6.2* (available from [http://www.linuxdoc.org/LDP/sag/index.html](http://www.linuxdoc.org/LDP/sag/index.html)).

Here are some Don'ts that will help you avoid errors:

+   - Don't use Linux as the `root` user.
+   - Don't just turn off your computer when you finish.
+   - Don't disable `e2fsck` in `/etc/rc.d/rc.sysinit`.
+   - Don't run `fsck` on mounted filesystems.
+   - Don't worry about fragmentation of your Linux partitions.
+   - Don't fill your hard drive with unnecessary programs.

# Running as root

Don't use Linux as `root` all of the time. Although you might be tempted, some very good reasons exist for not doing this. First, even though you might have aliased the `rm` command to `rm -i` in your `.bashrc` file, a simple `rm -fr / *` will wipe out not only your Linux system but also any DOS or Windows partitions mounted under `/mnt`. Instead, create a user for yourself and use the `su` command when you need to do things as the `root` operator.