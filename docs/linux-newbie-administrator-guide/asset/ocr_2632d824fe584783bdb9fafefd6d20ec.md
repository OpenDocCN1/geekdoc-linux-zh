# 4.1.3 How can I change the operating system that LILO boots on default?

There are typically two sections in the file /etc/lilo.conf. One starts with "image=" and it is relevant to Linux, the other starts with "other=" and this is the dos/win section. The first to appear in /etc/lilo.conf is booted by default. To change the system that boots on default, swap the sections. Don't forget to re-run the command

```
lilo
```

after any changes to /etc/lilo/conf .

# 4.1.4 The LILO prompt stays too short (or too long) on the screen during
the bootup

Add or adjust the line

```
delay=100
```

right before the "image=" or "append=" statement in your /etc/lilo.conf file. The number is the time of delay in tens of a second (0.1 s), so in the example above the delay will be 10 seconds. Don't forget to re-run lilo after making the changes to the /etc/lilo.conf file, or the delay will not change.

# 4.1.5 Uninstall Linux

If you really wanted to "uninstall" Linux, you can run this command (from under DOS or MS Windows):

```
FDISK/MBR
```

which will get rid of LILO overwrites the master boot record (MBR) of your first hard drive, where LILO resides. After this you can remove the Linux partitions using the DOS FDISK utility to re-claim the hard drive space.

# 4.2 Accessing the drives

# 4.2.1 Where are my drives?

Linux shows all the directories in one directory tree, respectively of what drives/hardware they are found on. Generally, this is a much better solution than the traditional DOS/Windows model-- completely abstracts the file system from the underlying hardware. You will appreciate this if you ever have to re-arrange or expand your hardware or add network resources. For the users who are accustomed to the DOS way of dealing with drives, it adds some extra complexity.

In short, don't search for drive letters. There are none under Linux; the content of your disks appears as subdirectories on your single Linux filesystem (directory tree). On default, the content of