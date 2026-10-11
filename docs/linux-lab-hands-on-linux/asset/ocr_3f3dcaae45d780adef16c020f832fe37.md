First of all, let's perform the following steps to create an installation image Server:

+   1.  Setting up FTP and HTTP Server as Installation Image Server
+       Creating Installation Directory (Distribution)for FTP and HTTP Server:
+   2.  Because there are three or more CDs in the Linux distribution (Red Hat and Fedora). You must install all the contents of available CDs in the same directory structure on the server's hard disk.

```
# mkdir /tmp/rh
# mount /mnt/cdrom                                  With first CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom; eject /mnt/cdrom
# mount /mnt/cdrom                                    With second CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom; eject /mnt/cdrom
# mount /mnt/cdrom                                    With third CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom; eject /mnt/cdrom
```

Just type y when it asks to overwrite some files. The distribution directory must contain at least RPMS and base directories, which must include all necessary software packages.

After creating an installation directory, now let's configure different servers required to set up the Linux install image server.

# ## Setting up NFS as Installation Image Server

# ■  Creating ISO images

Create ISO images of the installation CDs, and place them in the /distro/fc6 directory as discussed below. This requires about 4GB space as well. You can download the ISO images from the Fedora Web site or use the Fedora CDs. If you create the ISO files from the given CDs, they must have the same file names as the ones you can download from the Fedora Web site.

```
Create a directory distro for Linux distribution under / directory.
[root@netmon tmp]# mkdir /distro
[root@netmon tmp]# mkdir /distro/fc6
```

For the first CD, the code you need is:

```
[root@netmon tmp]# cd /distro/fc6
[root@netmon fc6]# dd if=/dev/cdrom of=FC6-i386-disc1.iso bs=32k
...
[root@netmon fc6]# eject cdrom
```

For the second CD, use:

```
[root@netmon fc6]# dd if=/dev/cdrom of=FC6-i386-disc2.iso bs=32k
[root@netmon fc6]# eject cdrom
```