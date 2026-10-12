
`/home/joe/local/share/evolution/addressbook/trash`

`/home/joe/local/share/evolution/mail`

`/home/joe/local/share/evolution/mail/trash`

`/home/joe/local/share/evolution/memos`

`/home/joe/local/share/evolution/memos/system`

`/home/joe/local/share/evolution/memos/trash`

`/home/joe/local/share/evolution/calendar`

`/home/joe/local/share/evolution/calendar/system`

`/home/joe/local/share/evolution/calendar/trash`

`/home/joe/local/share/icc`

`/home/joe/local/share/gnome-shell`

`/home/joe/local/share/gnome-settings-daemon`

`/home/joe/local/share/keyrings`

`/home/joe/local/share/tracker`

`/home/joe/local/share/tracker/data`

`/home/joe/local/share/folks`

`/home/joe/local/share/gvfs-metadata`

`/home/joe/local/share/applications`

`/home/joe/local/share/nano`

`/home/joe/Downloads`

`/home/joe/.scripts`

`/home/joe/Pictures`

`/home/joe/.cache`

### 列表 470 - 列出全局可写目录

如所示，几个目录似乎是全局可写的，包括 `/home/joe/scripts` 目录，这就是我们之前发现的 cron 任务所在地。这无疑值得进一步调查。

让我们转向配置。大多数系统在启动时会自动挂载。正因如此，很容易忘记可能包含价值价值信息的未挂载驱动器。我们应该始终寻找未挂载的驱动器，如果它们存在，则检查挂载权限。

在基于 Linux 的系统中，我们可以使用 `mount` 来列出所有挂载的文件系统。此外，`/etc/fstab` 文件列出了所有在启动时将挂载的驱动器。

```
$ cat /etc/fstab
UUID=60b8a4f9b-bc553-4213-909b-867e8adab7 ext4 0
# swap on /dev/sda5 during installation
8d6c11f3-b4a1-4be6-b923-86eadab7 none swap sw 0
/dev/sr0 /media/cdrom0 udf,iso9660 user,noauto 0 0
joe-debian-priv:\$ mount
sys on /sys type procfs (rw,nosid,nodev,noexec,relime)
proc on /proc type procfs (rw,nosid,nodev,noexec,relime)
(rw,nosid,relime,size=205266,mode=755)
devts on /dev/pts type devpts (rw,nosid,nodev,relime,gid=5,mode=620,ptxtmode=000)
tmpfs on /run type tmpfs (rw,nosid,relime,size=204196,mode=755)
/dev/sda1 on ext4 (rw,relime,errors=remount-ro)
security on /sys/kernel type securityfs (rw,nosid,nodev,noexec,relime)
tmpfs on /sys/sh type tmpfs (rw,nosid,relime,mode=777)
tmpfs on /lock type tmpfs (rw,nosid,nodev,relime,size=51280)
sysfs on /fs/cgroup type tmpfs (rw,nosid,nodev,noexec,mode=755)
croup2 on /sys/cgroup type cgroup typegroup2
(rw,nosid,relime,nodelgate)
croup on /sys/cgroup type cgroup type cgroup
(rw,nosid,relime,xattr,name=systemd)
pstore on /fs/pstore type pstore (rw,nosid,nodev,noexec,relime)
bfpf on /sys/bpf type bpf (rw,nosid,nodev,noexec,relime,mode=700)
system-1 on /proc/sys/tmpfs_misc type autofs
(rw,relime,fd=25,pgroup=1,timeout=0)
mqueue on /dev/mqueue type mqueue (rw,relime)
debugfs on /sys/kernel type debugfs (rw,relime)
hugebfs on /dev/hugepages type hugebfs (rw,relime,pagesize=2)
tmpfs on /run type tmpfs
(rw,nosid,relime,size=204196,mode=700,uid=117,gid=124)
tmpfs on /user/1000 type tmpfs
(rw,nosid,relime,size=204192,mode=700,uid=1000,gid=1000)
binfmt_misc on /proc/sys/binfmt_misc type binfmt_misc (rw,relime)
```

列表 471 - 查看 `/etc/fstab` 的内容

# OffSec

使用 Kali Linux 进行渗透测试

```
joe@debian-privesc:$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/chsh
/usr/bin/fusermount
/usr/bin/chfn
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/pkexec
/usr/bin/ntfs-3g
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/bwrap
/usr/bin/su
/usr/bin/umount
/usr/bin/mount
/usr/lib/polkit-agent-1/helper-1
/usr/lib/xorg/wrap
/usr/lib/ject/encrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/spice-gtk/spice-client-glb-usb-acl-helper
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/sbin/ppdd
```
