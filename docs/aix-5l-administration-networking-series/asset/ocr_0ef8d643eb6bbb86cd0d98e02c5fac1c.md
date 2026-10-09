The **linkbased** command will create symbolic links pointing the system to the documentation on the CD-ROM. The basic operation of both DocSearch and the **man** pages is the same in this case as when the documentation is loaded onto a local hard disk. However, the response time may be very poor.

When you give up using CD-ROMs and want to install the documentation on the server disks, you first need to remove all of the previously created symbolic links. IBM thought of this and also created an unlink program. To break all of the links, run the **unlinkbased** command and remove the CD-ROM filesystem.

```
```
# mount /infocd
# cd /infocd
# ./unlinkbased
# umount /infocd
# rmfs [-r] /infocd
```
```

> NOTE The -r switch on the **rmfs** command will remove the mount point, or directory.

# ## DocSearch on Fixed Disk

The entire documentation search services library should be installed on a fixed disk local to the documentation server for optimal performance. An NFS installation will work, but the availability is then dependent upon the NFS server. The extra layer of complexity is not recommended. You can also install the DoSearch core and leave the documentation CD-ROM mounted as you did in the preceding section. This method can be extremely slow, depending on the speed of the CD-ROM, and we all know that IBM has not been known for having the latest and fastest CD-ROM drives, but the servers really smoke! You could also NFS-mount the CD-ROM for even poorer performance. We will next show how to install DocSearch on both AIX 4.3.3 and 5L, version 5.1.

# ## Installing DocSearch on AIX 4.3.3

You start by defining a new user and group on the system for the documentation search service, if the **imadmd** user and group do not already exist. First, create a group called **imadmn**, and then create a new user named **imadm**. The **imadm** user should have the **imadmn** group as the primary group. Ensure that the language environment variable is set to the correct value, **en_US** for United States English.

```
```
# echo $LANG
```
```

Use the following SMIT FastPath to change the language variable:

```
```
# smitty chlang
```
```

Next, install the following filessets. In each case, the residing CD-ROM is listed along with the specific filessets.