related to performance. Using some of the parameters can be dangerous. Therefore you should be careful when using it.

# Modinfo

The modinfo command is used to list information about the Linux kernel module. For example, you must use the modinfo cdrom command for CDROM related kernel modules information.

```
root@kemal:~# modinfo cdrom
filename: /lib/modules/4.0.0-kalil-686-pae/kernel/drivers/cdrom.ko
license: GPL
depends:
intro:
vermag: 4.0.0-kalil-686-pae SMP mod_unload versions 686
parm: debug:autoclose
parm: autoeject:bool
parm: lockdoor:bool
parm: check_media_type:bool
parm: mrw_format_restart:bool
```

If you want to see the module list, you can use the lsmod command.

# Stat

Get to information about status of file or directory, stat command is used. It can be used either without parameters or with -f as stat -f.

```
root@kemal:~# stat /etc
File: "/etc" Blocks: 24 10 Block: 4096 dizin
Size: 12288 Device: 801/2649d Inode: 17006069 Links: 179
Access: [0755/drwxr-xr-x] Uid: 0/root Gid: 0/root)
Access: 2015-11-12 16:52:11.8637477 +0200
Modify: 2015-11-12 16:17:52.22489130 +0200
Change: 2015-11-12 16:17:52.22489130 +0200
Birth:
root@kemal:~# stat -f /etc
File: "/etc"
ID: c6233bcc30090e Name: 255 Type: ext2/ext3
Block size: 4096 Fundamental block size: 4096
Blocks: Total: 9327789 Free: 702615 Available: 6547025
Inodes: Total: 2379216 Free: 2027069
```