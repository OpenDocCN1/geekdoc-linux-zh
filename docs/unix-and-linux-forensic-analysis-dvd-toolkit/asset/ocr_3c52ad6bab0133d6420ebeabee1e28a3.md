# Chapter 2 • Understanding Unix

# Linux Command

# Closest Windows Command Line Equivalent (if any)

# What it does

sudo mount -t auto /dev/device /media/mountpoint

Windows automatically attempts this at boot time when USB devices are plugged in.

To mount a file system, you need to be root, so sudo prefixes this command. This example shows mounting the disk to a blank directory, automatically detecting the type of file system on it.

sudo umount /media/mount point

Right clicking on Ej or Safely Remove Hardware icons

Unmount a file system. For example, to remove a USB flash drive from the system, or an external hard disk.

chmod file chown file chgrp file

attrib

Change file permissions, file owner ship, and group ownership of a file.

Other commands to look up that you should work into your *nix vocabulary include: top (shows programs running sorted by CPU utilization), ps -ef (shows all running processes), netstat -an (shows all network connections), last (shows users logged in), who (who is currently logged in), uname -a, cp, rmdir, touch, wc -l, passwd, su -, gunzip, gzip, tar, zcat, env, ps, cut, uniq, alias, ssh, scp, rsync, fsck, and for a little leeway around all that may work, cowsay.

```
ubuntu@ubuntu:~$ cowsay "Cus it's the bomb!"
```

```
< Cus it' da bomb! >
^ ^^
\ (oo)
  (  _ )/\\n  ||-----||
  ||     |
```

Naturally when working on a potentially compromised box, it'd be folly to trust the output of the binaries installed on that machine. Having a CD that includes statically linked versions of these commands and running those binaries instead of the (possibly modified as part of a rootkit) installed versions is always a wise idea.