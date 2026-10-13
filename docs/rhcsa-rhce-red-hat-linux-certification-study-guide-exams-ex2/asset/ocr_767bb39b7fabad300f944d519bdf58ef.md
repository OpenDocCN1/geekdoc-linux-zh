```
```
[root@server1 root]# mount
/dev/vda2 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
/dev/vda1 on /boot type ext4 (rw)
/dev/vda5 on /home type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/tmp on /tmp type none (rw,bind)
/var/tmp on /var/tmp type none (rw,bind)
/home on /home type none (rw,bind)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/sr0 on /media type iso9660 (ro)
```
```

# The fdisk Utility

The fdisk utility is a near-universal tool available for a variety of computer operating systems. A capable version of fdisk is available on Macintosh OSes. A less capable version of fdisk is even available on older versions of Microsoft Windows. There are many commands within fdisk, more in expert mode, but you need to know only the few discussed here.

Though you can modify the physical disk partition layout using many programs, this section explores the Linux implementation of fdisk. In contrast, the Microsoft version is based on its heritage as the Disk Operating System (DOS) and works only on Microsoft partitions.

# Start fdisk: Help and More

The following screen output lists commands that show how to start the fdisk program, how to get help, and how to quit the program. The /dev/vda drive is associated with the first virtual drive on a KVM-based virtual machine. As other systems may be configured with different hard drive device files, you may need to check the output from the df and mount commands for clues.

When you start fdisk, it now includes the following warning:

```
```
WARNING: DOS-compatible mode is deprecated. It's strongly recommended to switch off the mode (command 'c') and change display units to sectors (command 'u').
```
```