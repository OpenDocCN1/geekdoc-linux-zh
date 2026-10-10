```
# (lines which begin with a '#" are comments)
#
/mount/point   map-file          global-options
/home          auto.home
/usr/local     auto.local
/misc          auto.misc
```

The first column tells you the mount point; the second column lists the files containing details about the mapping for that mount point; and the last column contains any NFS options you want to apply to all mounts.

The map files look a little different from the auto.master file. For example, here's the auto.misc file:

```
#
# auto.misc
#
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage
kernrel        -ro,soft,intr   {exp,kernel.org:/pub/linux
           cd   -fstype=iso9660,ro /dev/cdrom
# the following entries are samples to pique your imagination:
#floppy    -fstype=auto   :/dev/fd0
#2floppy   -fstype=ext2   :/dev/fd0
#cd2floppy -fstype=ext2   :/dev/fd0
#j2z      -fstype=smb2    :/dev/sd1
```

Here, the first column is the key, the second column holds the mount options; and the last column is the location from which to mount. If the location entry begins with a colon, it's a signal to the system that the mount is local. Thus, **misc/sd** would mount **/dev/cdrom** with the following mount options:

    -fstype=iso9660,ro

> NOTE: Unlike NFS, which requires that the directory already exist in order for you to mount it, the automounter does not. In the case of the **/misc** mount point, all that needs to exist is the **/misc** directory. All subdirectories would be created by the automounter daemon as needed.

If you change any of the map files while the automounter is running, you'll need to re-start the automounter so that it can reread the configuration files. This is done by using **autos** as follows:

```
[root@tord /root]#  /etc/rc.d/init.d/autofs reload
```