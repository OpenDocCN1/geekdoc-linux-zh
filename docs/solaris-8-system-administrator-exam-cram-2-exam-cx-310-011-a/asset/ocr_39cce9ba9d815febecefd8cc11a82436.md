The **newfs** command calculates the appropriate parameters and calls the **mkfs** command to create the file system. You can specify command-line arguments to override the calculated parameters. The only required command-line argument is the raw logical device name of the partition in which the file system should be created. The following example uses the **newfs** command to create a UFS in a 1GB partition. The **-v** command-line argument specifies *verbose mode*, which causes the **newfs** command to display its actions:

```
```text
# newfs -v /dev/rdsk/c0d1s7
newfs: construct a new file system /dev/rdsk/c0d1s7: (y/n)? y
mkfs -F ufs /dev/rdsk/c0d1s7 2104515 63 240 8192 1024 ... 8 7
Warning: 12286 sectors (5) in last cylinder unallocated
/dev/rdsk/c0d1s7: 2104514 sectors in 140 cylinders of 240 tracks,
    63 sectors
 1027.6MB in 24 cyl groups (6 cg, 44.30MB/g, 10688 i/g)
super-block backups (for fsck -F ufs -o b=#) at:
  32, 90816, 181600, 272384, 363168, 454352, 545136, 635920,
  726304, 817088, 907872, 998656, 1089440, 1180224, 1271008,
  1361792, 1452576, 1543360, 1634144, 1724928, 1815712,
  1906496, 1997280, 2088064,
#
```
```

Another useful **newfs** command-line option is **-N**, which causes the **newfs** command to calculate the parameters that will be used to call the **mkfs** command; however, the **mkfs** command is not actually called, and the file system is not created. The **-v** command-line argument is used to preview the file system parameters. In addition, most of the **mkfs** command-line arguments can be specified as **newfs** command-line arguments. If any of them are specified, they override any calculated parameters and are passed to the **mkfs** command. See the **newfs(1M)** and **mkfs(1M)** manual pages for details.

If you’re using the **mkfs** command directly, you should include the **-F** command-line argument to identify the type of file system to create. If you don’t specify a file system type, the type listed in the /etc/default/fs file is used by default. The default type for local (disk-based) file systems is UFS. Additional parameters, such as block size and disk geometry (sectors per track, tracks per cylinder, and so on) can also be specified.

![](bbox=[0.122, 0.774, 0.219, 0.847])

The commands used to create file systems expect raw (character) logical device names. In addition, the only type of disk-based file system that can be created on a standard Solaris 8 operating system is UFS. However, when a floppy disk is formatted, the PCFS is created on the floppy disk automatically.

# Checking and Repairing File Systems

File systems are damaged when the data defining them is corrupted. This corruption can be caused by software errors or by failures of the underlying