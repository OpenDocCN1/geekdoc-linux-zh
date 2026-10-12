limited by the bandwidth of your network, and is only slightly slower than a hard drive install. In addition to the requirement that the Red Hat installation files be on an exported filesystem, this installation method also requires that you create a different boot disk from the bootnet.img file on the install CD. This boot floppy can be created with the following command on another Linux system:

```
[root@nomad images]# dd if=bootnet.img of=/dev/fd0 bs=512
2880+0 records in
2880+0 records out
```

If you do not have another Linux system available, you can create the network boot floppy under Windows using the rawrite utility, which is also found on the installation CD. This installation looks just like the normal install, except instead of presenting a dialog with options to install from a local CD-ROM or hard drive, you will be presented with a dialog box asking whether you want to install from an NFS image, an FTP site, or an HTTP install as shown in Figure 3.4. If you select this install method, you will then be presented with the dialog box shown in Figure 3.5, in which you specify the NFS server and the directory containing the Red Hat install files.

# FIGURE 3.4
Selecting an NFS install.

![](bbox=[0.27, 0.6, 0.55, 0.77])

# FIGURE 3.5
The NFS install options dialog box.

![](bbox=[0.27, 0.78, 0.6, 0.92])

If you frequently install Linux on machines that do not have CD-ROM drives, such as to a laptop, the NFS installation option may be a good one to consider.