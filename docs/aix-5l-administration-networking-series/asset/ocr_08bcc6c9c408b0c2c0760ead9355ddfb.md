This process is beyond the scope of this chapter, but I feel confident that someone could someday write a **reducelv** wrapper script to make it useful. Another problem comes when you have a filesystem on top of the logical volume you want to reduce. There are no supported or unsupported commands to deal with this that I know of. So please do not try it unless you have a system you can destroy. *Use at your own risk* and for more details read **AIX Logical Volume Manager from A to Z: Troubleshooting and Commands** from Redbooks and IBM: http://www.redbooks.ibm.com/ pub s/ pd fs /rebooks/sg245433.pdf.

# Defragment a Filesystem with defragfs

The **defraglv** command attempts get more contiguous PP for the file system. If your file systems consist of PPs scattered over the disk, you will see some benefit, but it is usually negligible. To defrag the /bigdata 01 file system issue the following command:

```
`# defragfs /bigdata01`
```

# syncvdam Command

The **syncvdam** command synchronizes or rebuilds the logical volume control block (LVCB), the device configuration database in the ODM, and the volume group descriptor areas on each of the physical volumes in the specified volume group.

Remember that if you run this command on a system that is running raw logical volumes, all of the raw devices in the /dev/*r* directory will be owned by the **root** user and the **system** group! If you are running a database under raw logical volumes, just remember to go back and change the raw device file ownership accordingly.

> **NOTE** In AIX 4.3 IBM added the *-P* flag to the **syncvdam** command that preserves the ownership and permissions of the logical volume raw devices. Always use the *-P* flag to preserve raw device settings!

It is rare that you need to run this command, but if for some reason the device configuration database becomes inconsistent, you can run the following command:

```
`# syncvdam -v -P rootvg`

`(or)`

`# syncvdam -v -P rootvg lvol1 lvol2 hdl`
```

# FILESYSTEMS (JFS AND JFS2)

The most common use of logical volumes is to contain filesystems. *A filesystem* is the structure that supports a UNIX directory and file tree. A file system tree begins with the root directory at the top, with subdirectory branches proceeding down from the root.