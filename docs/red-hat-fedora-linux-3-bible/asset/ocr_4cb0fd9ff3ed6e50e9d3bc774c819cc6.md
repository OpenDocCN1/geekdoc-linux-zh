useradd commands for users you added during installation. You can also use the usermod command to add the user’s password.

```
```
#post
/usr/sbin/useradd jake
chfn -f 'John W. Jones' jake
/usr/sbin/usermod -P 'S1§8raê@Ö&Ô$QUYbFPh0h79s8CknTuaH.' jake
```
```

At this point you should have a working `ks.cfg` file.

# ## Installing the kickstart file

Once the `ks.cfg` file is created, you need to put it somewhere accessible to the computer doing the installation. Typically, you will place the file on a floppy disk. However, you can also put the file on a computer that is reachable on the network or on a hard disk.

To copy the file to a floppy disk, create a DOS floppy and copy the file as follows:

```
# mcopy ks.cfg a:
```

When you do the Fedora kickstart installation, have this floppy disk with you. As an alternative, you can copy the `ks.cfg` file to a CD.

Being able to place the `ks.cfg` file on a computer on the network requires a bit more configuration. The network must have a DHCP or a BOOTP server configured that is set up to provide network information to the new install computer. The NFS server containing the `ks.cfg` file must export the file so that it is accessible to the computer installing Linux. To use a `ks.cfg` file from the local hard disk, you can place the file on any partition that is a Windows (VFAT) or Linux (ext3) partition.

# ### Booting a kickstart installation

If the kickstart file (`ks.cfg`) has been created and installed in an accessible location, you can start the kickstart installation. Here is an example of how you can do a kickstart installation using the Fedora DVD and a floppy containing a `ks.cfg` file:

+   1. Insert the Fedora DVD or first CD and restart the computer.
+   2. When you see the boot prompt, insert the floppy containing the `ks.cfg` file and type the following (quickly, before the installation boots on its own): `boot: linux ks=file:/0/ks.cfg`

You should see messages about formatting the file system and reading the package list. The packages should install, with the only intervention required being to change CDs. Next you should see a post-install message. Finally, you should see the "Complete" message.