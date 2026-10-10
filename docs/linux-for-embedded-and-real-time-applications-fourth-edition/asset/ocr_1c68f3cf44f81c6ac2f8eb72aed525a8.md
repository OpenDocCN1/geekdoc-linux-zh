# **Boot to the NFS File System**

Reset the board into the u-boot prompt if you are not already there. Execute the following commands:

```
```
setenv bootenv uEnvnet.txt
boot
```
```

The reason for not overwriting uEnv.txt right now is that there might be something wrong with your uEnv.txt, in which case you will need to boot back into the eMMC file system. When you are confident that uEnvnet.txt is working correctly, you can rename it uEnv.txt and boot directly into the NFS file system.

Interestingly, the boot up seems to be somewhat more verbose with the NFS file system than with the eMMC file system.

As a final step, move the samples/ directory into your target file system under /home.

# **What Can Go Wrong?**

It is not unusual to encounter difficulties when bringing up an embedded target board such as the BeagleBone Black, even though the designers have gone to great lengths to make the process as painless as possible. The most common problems fall into two broad categories. The first is the serial port. Make sure the baud rate is set correctly. This is generally not a problem, because 115 kbaud seems to be the default for minicom. A more common problem is not turning off hardware flow control.

Common networking problems include having Security Enhanced Linux enabled, and/or the firewall turned on. This will prevent the target from NFS mounting its root file system. As a starting point, disable SELinux, and turn off the firewall. Later on you can configure either of these features to allow NFS mounting, but still provide some level of protection.

Make sure the IP address is correct. Actually, this should not be a problem, because you will be getting an IP address through DHCP.

With the target board fully configured and connected to the workstation, we can turn our attention to the task of writing applications. That’s the subject of the next chapter.

# **Resources**

+   beagleboard.org — web site for the BeagleBoard series of boards  
+   debean.beagleboard.org/images — A collection of root file system images for BeagleBoards.