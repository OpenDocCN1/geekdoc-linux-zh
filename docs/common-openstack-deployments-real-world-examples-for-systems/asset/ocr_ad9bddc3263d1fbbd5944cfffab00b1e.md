Now you'll want to create a basic filesystem on the new disk. It's only a 1GB volume, and this is a demonstration, so we'll use the ext2 filesystem:

```
```bash
$ sudo mkefs.ext2 /dev/vdb1
mke2fs 1.42.2 (27-Mar-2012)
Filesystem label=OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
65536 inodes, 321888 blocks
31094 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=268435456
9 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376

Allocating group tables: done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```
```

The last step is creating a mount point and mounting your new volume. Let's say that you want to use this volume for photos and create a directory for that. Then we'll check to confirm it's the size we expect it to be.

```
```bash
$ mkdir photos
$ sudo mount /dev/vdb1 photos/
$ df -h -i /dev/vdb1
Filesystem     Size  Used Avail Use% Mounted on
/dev/vdb1      100G  9.9M  95.4M 0% /home/cirros/photos
$ df -h /dev/vdb1
Filesystem     Size  Used Avail Use% Mounted on
/dev/vdb1      100G  9.9M  95.4M 0% /home/cirros/photos
```
```

Congratulations! A 1GB volume from the block storage service Cinder is now mounted on your system. Note that this was mounted using the root user, so you will need to either change the ownership to your user or use root to place files on it.

# **Tip**

File permissions with block storage in Cinder can be a tricky thing to master. When using a Linux filesystem, files are referenced by user and group ID (UID and GID). Unless you are very diligent about keeping things consistent across your instances through something like custom images with default users and group or configuration management where IDs are specifically defined, these IDs can easily be different between machines.

As a result of these potential differences in IDs, mounting a volume from the block storage device on one instance and then detaching it to add it to another instance may land you in a situation where the ownership of files looks all wrong. Keep this in mind as you begin experimenting with moving volumes and always make checking permissions a step in your plans to move a volume to another instance.