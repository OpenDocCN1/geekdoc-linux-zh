
```
Red Hat release 7.0 (Guinness)
Kernel 2.4.2-2 on i686
login: freston
Password:
Last login: Jun 7 11:48:36 from 8.3.105.620
[freston@HostA freston@]$ su su root
Password:
[root@HostA]# mount /dev/cdrom
[root@HostA]# mount
/dev/hda1 on / type ext2 (rw)
one on /proc type proc (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/pts type devdevs (rw,gid=5,mode=620)
automount(pid469) on /misc type autofs
(rw=5,grp=46,minproto=2,maxproto=3)
# 从 CD-ROM 安装 Linux 21
```

`/dev/bdc` on `/mnt/cdrom` type iso960 (ro,nosuid,nodev)

```
[root@HostA /root] cd /mnt/cdrom
```

```
[root@HostA cdrom]# ls -l
```

total 63

`-rw-r---- 10 root 18385 Sep 7 1999 COPYING`

`-rw-r---- 10 root 47330 Aug 25 2000 README`

`-rw-r---- 5 root 25206 Aug 27 2000 RELEASE-NOTES`

`-rw-r---- 10 root 19088 Sep 25 1999 RPM-GPG-KEY`

`drwxr-xr-x 1 root 2048 Aug 30 2000 RedHat`

`-r-xr-x-- 1 root 46535 Aug 30 2000 TRANS.TBL`

`drwxr-xr-x 1 root 20486 Aug 30 2000 utils`

`drwxr-xr-x 8 root 20486 Aug 30 2000 images`

```
- 2. 需要启动文件是 `boot.img`。切换到 `/mnt/cdrom/` 目录并列出目录内容以确认 `boot.img` 文件是否存在。你的 `images` 目录列表可能不完全相同，但应该类似于：
```

```
[root@HostA cdrom]# # cd /mnt/cdrom/images
[root@HostA images]# # ls -l
```

total 5333

`-r-xr-x-- 1 root 485 Aug 30 2000 TRANS.TBL`

`-rw-r---- 2 root 1474560 Aug 30 2000 boot.img`

`-rw-r---- 2 root 1474560 Aug 30 2000 bootnet.img`

`-root-xr-x-- 1 root 485   0  00000000`

`---              000000000000             00000000000000         000000000000000000 00    00000000000000000000    000000000000000000000000  0000000000000000 0 00         000000000000000000000`
*（等一下，让我根据上一页的内容清理那个损坏的目录列表）*

```
[root@HostA cdrom]# # cd /mnt/cdrom/images
[root@HostA images]# # ls -l
```

total 5333

`-r-xr-x-- 1 root 485 Aug 30 2000 TRANS.TBL`

`-rw-r---- 2 root 1474560 Aug 30 2000 boot.img`

`-rw-r---- 2 root 1474560 Aug 30 2000 bootnet.img`

`drwxr-xr-x 1 root 2048 Aug 30 2000 de`

`-rw-r---- 1 root 860160 Aug 30 2000 drivers.img`

`drwxr-xr-x 1 root 2048 Aug 30 2000 es`

`drwxr-xr-x 1 root 2048 Aug 30 2000 fr`

`drwxr-xr-x 1 root 2048 Aug 30 2000 it`

`-rw-r---- 1 root 147456 Aug 30 2000 paride.img`

`-rw-r---- 1 root 1474560 Aug 30 2000 pccmia.img`

`drwxr-xr-x 1 root 2048 Aug 30 2000 pxeboot`

`drwxr-xr-x 1 root 2048 Aug 30 2000 sv`
