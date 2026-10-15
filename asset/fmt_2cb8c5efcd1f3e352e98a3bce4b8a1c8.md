
```bash
echo "Reload not possible, use restart."
;;
restart|force-reload)
 /etc/init.d/mdutils stop
 /etc/init.d/mdutils start
;;
*)
 echo "Usage: mdutils [start] [stop]" >&2
 false
esac
```

## 附录 D：初始化脚本

### modutils

此脚本管理在启动过程中添加到内核的各种模块。

```bash
# /bin/sh
# /etc/init.d/modules：在'boot' 中加载相应的模块。
```

```bash
PATH="/sbin:/bin:/usr/sbin/bin"
echo -n "Calculating module dependencies..."
depmod -a > /dev/null
echo "done."
```

```bash
# 首先测试我们是否拥有带有 kmod 的内核
kernel=0
startkerneld=1
```

```bash
else
startkerneld=0;
fi
```

```bash
# 遍历 /etc/modules 中的每一行。
echo -n 'Loading modules: '
(cat /etc/modules; echo) | # 确保结尾有换行符 LF
while read module args
do
    case "$module" in
        auto) [ "$($startkernel)" -eq 0 -a -x /sbin/kernel ] && \
            echo && /etc/init.d/kernel start & startkernel=1;
            continue;
        noauto) continue;
        ""|"*") continue;
    esac
    echo -n "$module" *
    modprobe $module args
done
```

```bash
# 以万一系统管理员倾向于在 /lib/modules/boot 中
# 为启动模块使用通用符号链接，我们将加载这些模块
if [ -n "modprobe -l -t boot" ]
then
    modprobe -a -t boot *
fi
```

### mountall.sh

`mountall.sh` 挂载所有本地文件系统，而不是要求用户在需要时挂载单独的文件系统。

```bash
# mountall.sh 挂载所有文件。
# Version: @(#)mountall.sh 2.76 10-Dec-1998 miquels@cistron.ml
# /etc/default/rcS
# 挂载 /etc/fstab 中的本地文件系统。
# [ "$VERBOSE" != no ] && echo "Mounting local file systems..."
mount -avt nonfs,nproc
```

```bash
#
# 我们可能在 /dev 上挂载了某些，检查 /dev/initctl 是否存在。
#
if [ ! -p /dev/initctl ]
then
    rm -f /dev/initctl
    mknod -m 600 /dev/initctl
fi
kill -USR 1
```

```bash
#
# 再次执行 swap 命令，以防我们需要在新的挂载
# 文件系统上交换文件。
#
apon -a 2>/dev/null
```

### mountnfs.sh

`mountnfs.sh` 一次挂载所有网络文件系统，而不是让用户在需要时挂载单独的文件系统。

```bash
#
# mountnfs.sh 现在既然 TCP/IP 已经配置好，如果需要
# 挂载 /etc/fstab 中的 NFS 文件系统。如果可能，
# 在挂载之前启动 portmapper（这对 Linux 2.1x 及更高版本是需要的）。
# Version: @(#)mountnfs.sh 05-Oct-1998 miquels@cistron.nl
#
/etc/default/rcS
```

```bash
#
# 在子壳中运行是因为使用了 I/O 重定向。
# test -f /etc/fstab && (
# 逐行读取 fstab。如果是 NFS，则设置挂载
# 文件系统的标志。如果发现任何 NFS 分区
# 且未使用 nolock 选项挂载，则启动 portmapper。
portmap=no
mount_nfs=no
```

```bash
while read device ftype options
do
    if [ "$fstype" = nfs ]
    then
        mount_nfs=yes
        case $options in
            *nolock*)
                ;;
            *)
                portmap=yes
        esac
    fi
    if [ "$portmap" = yes ]
    then
        if [ -x /sbin/portmap ]
        then
            echo -n "Starting portmapper..."
            start-stop --quiet /sbin/portmap
            sleep 2
        fi
    fi
    if [ "$mount_nfs" = yes ]
    then
        echo "Mounting remote filesystems..."
        mount -a -t nfs
    fi
done < /etc/fstab
# netbase 脚本负责设置一些网络功能
# 包括基础安全。该脚本因使用 ipfwadm 程序
# 而很有趣，它很好地说明了这一点。
# 启动/停止守护进程。
test -f /sbin/portmap || exit 0
```

```bash
case "$1" in
  start)
    spoofprotect
    echo -n "Starting base networking daemons:"
    echo -n " portmap"; start-stop-daemon --start --quiet --exec /bin/portmap
    echo -n " inetd"; start-stop-daemon --start --quiet --exec /usr/sbin/inetd
    echo "."
    ;
  stop)
    start-stop-daemon --stop --quiet --okno --pidfile /var/run/inetd.pid ---exec /usr/sbin/inetd
    start-stop-daemon --stop --quiet --okno --exec /sbin/portmap
    ;
  reload)
    start-stop-daemon --stop --quiet --okno --pidfile /var/run/inetd.pid ---signal 1 --exec /usr/sbin/inetd
    ;
  restart)
    start-stop-daemon --stop --quiet --okno --pidfile /var/run/inetd.pid ---exec /usr/sbin/inetd
    pmap_dump >/var/run/portmap.state
    start-stop-daemon --stop --quiet --okno --exec /sbin/portmap
    start-stop-daemon --start --quiet --exec /sbin/portmap
    if [ -f /var/run/portmap.upgrade-state ]; then
      pmap_set < /var/run/portmap.state
    elif [ -f /var/run/portmap.state ]; then
      pmap_set < /var/run/portmap.state
    fi
```
