# Chapter 2 • Understanding Unix

+   /cdrom is a mount point for CD-ROM devices. What's a mount point?
We'll get to it soon, I promise!

+   /etc is a directory where nearly all configuration files are found. Remember
our password and shadow files?

+   /home is where users' home directories are located. Think "c:\Documents
and Settings\."

+   /mnt and /media are places where mount points are located. /media is not
sothing you will find outside of Ubuntu Linux. /mnt is fairly ubiqu-
tous across *nix. Don't despair if these directories are empty presently if you
are booted via a LiveCD.

+   /lib is home to shared libraries (so files) needed during boot. Imagine
Windows took all the DLLs that supported the .exe in %windir%system32
gave them their own directory to live in. /usr/lib and /usr/local/lib are
similarly,相应 corresponding to libraries in /bin and /usr
/local/bin respectively.

+   /tmp is for temporary files, not unlike %TEMP% in Windows.

+   /opt is where you may find optional software and add-on's not included in a
default installation. Yours is to be empty at this point.

+   /var is home to many log files (/var/*), mail spool files, and print spool
files. It is your forensic friend (assuming you can trust the logs not to be
tainted). The contents of /var tend to be well, rather variable.

+   /boot holds things used for booting, including /boot/grub/grub.conf which
is akin to boot. You won't see this file on a LiveCD, but it generally exists
on an installed version of Ubuntu.

+   /proc is a wacky place where it exists its own in this book. These
aren't really "files" in the sense that you and I think of. /proc can be
thought as a live mirror of what's in system memory, but presented like a
file hierarchy. Compare what you see with "ls /proc" with the output of the
process list "ps -et.". You'll notice that for every process id number
in the ps output, there's an entry in /proc. This will be leveraged in a later
chapter to grab a memory snapshot of a running system.

+   /dev is another wacky system where actual devices on the system are
represented hierarchically. /dev/sda1 for instance, represents the first partition

![](bbox=[0.048, 0.946, 0.258, 0.971])