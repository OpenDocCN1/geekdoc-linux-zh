# Configuring an install server using files

To do an FTP or HTTP install, you must copy the files from the installation CDs to a directory that you make available to the network. Because there are three installation CDs in the Red Hat Linux distribution, you can’t just identify the location of a mounted CD. You must install the contents of all three CDs in the same directory structure on the server’s hard disk. For example, you could do the following:

```
# mkdir /tmp/rh
# mount /mnt/cdrom	With first CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	With second CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	With third CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
```

Just type y when it asks to overwrite some files. The distribution directory must contain at least the RPMS and base directories, which must include all necessary software packages. In this example, all files were copied. Setting up an NFS install server requires copying CD images to the shared NFS directory.

# Configuring an install server using disk images

Instead of copying all files from the three installation CDs, you can copy the entire images of each of the three disks to your hard disk for NFS or hard disk installs. To do this, insert the first installation CD and type the following:

```
# mkdir /tmp/rh
# dd if=/dev/cdrom of=/tmp/rh/disk1.iso	With first CD inserted
# mount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk2.iso	With second CD inserted
# umount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk3.iso	With third CD inserted
# umount /mnt/cdrom ; eject /mnt/cdrom
```

# NFS server

Add an entry to the /etc/exports file to share the distribution directory you created. Remember, that for NFS installs, this directory must contain CD ISO images. The following entry would make the directory available in read-only form to any computer:

```
/tmp/rh	(ro)
```

Next, restart NFS by typing the following as root user:

```
# /etc/init.d/nfs restart
```

To set the NFS service to be on permanently (it is off by default), type the following as root:

```
# chkconfig nfs on
```