# Trying mtools

To try out mtools, follow these steps:

+   1. **Log in as root or type su - and then enter the root password.**
+   2. **Place an MS-DOS floppy disk in your system's A drive.**
+   3. **Type mdir.**
+      You should see the directory of the floppy disk (in the standard DOS directory-listing format).

Typically, you would use the mtools utilities to access the floppy disks. The default configuration file, /etc/mtools.conf, is set up to access the floppy drive as the A drive. Although you can edit that file to define C and D drives for your DOS hard-drive partitions, you can also access the hard drive partitions by using the Linux mount command to mount them. Because you can mount the hard-drive partitions automatically at startup, accessing them through the Linux commands is normally just as easy.

You also can access Iomega Zip drives through mtools. Simply specify a drive letter and the appropriate device's filename. For built-in IDE (ATAPI) Zip drives, try /dev/hdd4 as the device file and add the following line in the /etc/mtools.conf file:

```
drive e: file="/dev/hdd4"
```

After that you should be able to use mtools commands to access the Zip drive (refer to it as the E drive). For example, to see the directory listing, place a Zip disk in the Zip drive and type:

```
mdir e:
```

# Learning the mtools commands

The mtools package is a collection of utilities. So far, I have been using mdir — the mtools counterpart of the DIR command in DOS. The other mtools commands are fairly easy to use.

![](bbox=[0.15, 0.82, 0.22, 0.93])

If you know MS-DOS commands, using the mtools commands is easy. Type the DOS command in lowercase letters, and remember to add m in front of each command. Because the Linux commands and filenames are case-sensitive, you must use all lowercase letters as you type mtools commands.

Table 3-4 summarizes the commands available in mtools.