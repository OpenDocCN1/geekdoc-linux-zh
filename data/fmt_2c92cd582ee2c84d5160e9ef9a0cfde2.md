
```
joe@debian-privesc:~$ find / -writable -type d 2>/dev/null

/home/joe
/home/joe/Videos
/home/joe/Templates
/home/joe/.local
/home/joe/.local/share
/home/joe/.local/share/sounds
/home/joe/.local/share/evolution
/home/joe/.local/share/evolution/tasks
/home/joe/.local/share/evolution/tasks/system
/home/joe/.local/share/evolution/tasks/trash
/home/joe/.local/share/evolution/addressbook
/home/joe/.local/share/evolution/addressbook/system
/home/joe/.local/share/evolution/addressbook/trash
/home/joe/.local/share/evolution/mail
/home/joe/.local/share/evolution/mail/trash
/home/joe/.local/share/evolution/memos
/home/joe/.local/share/evolution/memos/system
/home/joe/.local/share/evolution/memos/trash
/home/joe/.local/share/evolution/calendar
/home/joe/.local/share/evolution/calendar/system
/home/joe/.local/share/evolution/calendar/trash
/home/joe/.local/share/jcc
/home/joe/.local/share/gnome-shell
/home/joe/.local/share/gnome-daemon
/home/joe/.local/share/keyrings
/home/joe/.local/share/tracker
/home/joe/.local/share/tracker/data
/home/joe/.local/share/folks
/home/joe/.local/share/gvfs-metadata
/home/joe/.local/share/applications
/home/joe/.local/share/nano
/home/joe/Downloads
/home/joe/.scripts
/home/joe/Pictures
/home/joe/.cache
```

### 列表 470 - 列出所有全局可写目录

> ^94 (Linux man-pages project, 2019), http://man7.org/linux/man-pages/man1/find.html

PWK - © 2023 OffSec Services Limited. All rights reserved.

所示，几个细节似乎是全球开放的，包括 `/home/joe/scripts` 目录，这就是我们之前发现的 cron 所在。这确实值得进一步调查。

让我们继续调查。在系统中，大多数驱动器在启动时自动挂载。因此，很容易找到可能包含价值信息的未挂载驱动器。我们应该始终寻找未挂载的驱动器，如果它们存在，则检查挂载权限。

在基于 Linux 的系统中，可以使用 `mount` 来列出所有文件系统。此外，`/etc/fstab` 文件列出了启动时将挂载的所有驱动器。

```
joe@debian-privesc:~$ cat /etc/fstab
UUID=60b4af9-bc53-4213-90b8-a2c09e261 / type ext4 errors=rem-ro ro,nodid,relime 0 1
swap on /dev/sda5 during installation
UUID=86dec1f3-4b41-4e6b9233ab7 none swap 0 0
/dev/sr0 media/cdrom udf,auto 0
joe@debian-privesc:~$ mount
sysfs /sys type sysfs (rw,nodid,node,noexec,relime)
proc /proc type proc (rw,nodid,node,noexec,size=255026,mode=755)
devpts /dev/pts type devpts (rw,nodid,node,noexec,gid=5,mode=620)
tmpfs /run type tmpfs (rw,nodid,node,noexec,size=20496,mode=755)
/dev/sda1 / type ext4 (rw,relime,errors=root)
security /kernel/security type sysfs (rw,nodid,noexec,relime)
tmpfs /dev/shm type tmpfs (rw,nodid,noexec,relime)
tmpfs /run type tmpfs (rw,nodid,noexec,relime,size=512k)
sysfs /fs/cgroup type sysfs (rw,nodid,noexec,mode=755)
group /sys/cgroup type group (rw,nodid,noexec,relime)
group /sys/cgroup/system type group (rw,nodid,noexec,relime)
group / (rw,nodid,node,relime,xattr,name=system)
pstore /sys/fs/pstore type pstore (rw,nodid,node,noexec,relime,mode=700)
binfmt_misc /proc/sys/binfmt_misc type binfmt_misc (rw,relime,fd=25,page=1,timeout=0,limit=5,pipe=10550)
mqueue /dev/mqueue type queue (rw,relime)
debug /sys/kernel/debug type debug (rw,relime)
hugebfs /dev/hugepages type hugebfs (rw,relime,pagesize=2M)
tmpfs /run type tmpfs (rw,nodid,noexec,relime,mode=700,uid=117,gid=124)
tmpfs /user=100 type tmpfs (rw,nodid,relime,size=204192,mode=700,uid=1000,gid=1000)
```

### 列表 471 - 列出 /etc/fstab 内容和所有已挂载驱动器

输出显示了交换分区和该 Linux 系统的主 ext4 设备。

> 请记住系统管理员可能使用了自定义配置或脚本来挂载未列在 `/etc/fstab` 中的驱动器。因此，良好的做法不仅是扫描 `/etc/fstab`，还要使用 `mount` 获取有关挂载驱动器的信息。

此外，我们可以使用 `lsblk`^647 查看所有可用磁盘。

```
joe@debian-privesc:~$ lsblk
NAME      MAJ:MIN SIZE TYPE MOUNTPOINT
sda       8:0    0   32G disk                 
|-sda1    8:1    0   31G part /
|-sda2    8:2    0    1K part                 
|-sda5    8:5    0   75M part [SWAP]
srs0      11:0   1024M M                 
```

### 列表 472 - 使用 lsblk 列出所有驱动器

我们注意到 `sda` 驱动器由三个不同的分区组成。在某些情况下，显示系统中所有磁盘的信息可能会发现未挂载的分区。根据系统配置或，我们可能挂载这些分区并搜索有趣的文档、凭据或其他允许我们提升权限或在网络中获得更好脚点的信息。

另一种常见的权限提升技术涉及设备驱动程序和内核模块的利用。我们将在本模块后面探索实际的利用战术，但让我们先检查一些枚举技术。

由于这种技术依赖于将漏洞与相应的利用程序匹配，我们需要收集加载在目标上的驱动程序和内核模块列表。我们可以使用 `lsmod` 在不带任何额外参数的情况下枚举已加载的内核模块。

# OffSec

使用 Kali Linux 进行渗透测试
