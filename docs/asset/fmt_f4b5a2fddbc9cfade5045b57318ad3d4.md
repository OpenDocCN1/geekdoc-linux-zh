
`/media/cdrom`

`/etc/fstab` 文件是一个配置文件——包含挂载和卸载命令的文本文件。`/etc/fstab` 文件中的每一行都提供了关于设备及其在文件系统中挂载点的信息。`/etc/fstab` 将文件系统中的各个点与特定设备关联，这使得仅需挂载点或设备作为参数即可从命令行进行挂载。

这是一个来自 SUSE 系统的 `/etc/fstab` 文件。（其他 Linux 发行版中的文件具有类似的格式。）

```text
/dev/hd1 /reiserfs acl_user_xattr 1 1
/dev/hd7 /boot [ext3 acl,user_xattr 1 2
/dev/hd6 /data auto noauto 0 0
/dev/hd8 /data auto noauto 0 0
/dev/hd10 /data3 auto noauto 0 0
/dev/hd5 /data auto noauto 0 0
/dev/hd2 /windows/nfs nfs,uid=0002,umask=0002,nls=utf8 0 0
/dev/sda8 swap swap pri=42 0 0
devpts /dev/pts mode=0620,gid=5 0 0
/proc /proc proc defaults 0 0
uubfs /proc/bus/usb noauto 0 0
sys /sys sysfs noauto 0 0
/dev/cdrecorder /media/cdrom subfs=cdfs,nosid,nodev,exec,iochn-utf8 0 0
```
