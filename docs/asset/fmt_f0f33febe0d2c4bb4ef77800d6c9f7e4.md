
这表示 `init` 应执行命令 `/etc/rc.d/rc 5` 并等待该命令完成。

`/etc/rc.d/rc` 脚本有些复杂。它的工作原理如下：

- 它切换到与运行级别对应的目录。例如，要切换到运行级别 5，脚本会切换到 `/etc/rc.d/rc5.d` 目录。
- 在与运行级别对应的目录中，它查找所有以 `K` 开头的文件并使用参数 `stop` 执行每个文件。这会终止当前正在运行的进程。然后它定位所有以 `S` 开头的文件并使用参数 `start` 执行每个文件。这会启动指定运行级别所需的进程。

要查看运行级别 5 下执行了什么，请键入以下命令：

```
ls -l /etc/rc.d/rc5.d
```

```
total 0

lrwxrwxrwx 1 root root 15 Aug 14 16:24 K01pppoe -> ../init.d/pppoe

lrwxrwxrwx 1 root root 14 Aug 14 16:08 K05innd -> ../init.d/innd

lrwxrwxrwx 1 root root 13 Aug 19 22:18 K20nfs -> ../init.d/nfs

lrwxrwxrwx 1 root root 16 Aug 14 16:24 K20rstatd -> ../init.d/rstatd

lrwxrwxrwx 1 root root 17 Aug 14 16:24 K20usersd -> ../init.d/usersd

lrwxrwxrwx 1 root root 16 Aug 14 16:24 K20rwalld -> ../init.d/rwalld

lrwxrwxrwx 1 root root 15 Aug 14 16:24 K20rwhod -> ../init.d/rwhod

lrwxrwxrwx 1 root root 19 Aug 14 16:34 K34yppasswdd -> ../init.d/yppasswdd

lrwxrwxrwx 1 root root 13 Aug 14 16:25 K35smb -> ../init.d/smb

lrwxrwxrwx 1 root root 18 Aug 14 15:56 K45arpwatch -> ../init.d/arpwatch

lrwxrwxrwx 1 root root 15 Aug 14 15:57 K45named -> ../init.d/named

lrwxrwxrwx 1 root root 15 Aug 14 16:31 K50snmpd -> ../init.d/snmpd

lrwxrwxrwx 1 root root 18 Aug 14 16:17 K60mars-nwe -> ../init.d/mars-nwe

lrwxrwxrwx 1 root root 16 Aug 14 16:34 K84ypserv -> ../init.d/ypserv

lrwxrwxrwx 1 root root 15 Aug 14 16:14 S05kudzu -> ../init.d/kudzu

lrwxrwxrwx 1 root root 18 Aug 14 16:08 S08ipchains -> ../init.d/ipchains

lrwxrwxrwx 1 root root 17 Aug 14 15:56 S10network -> ../init.d/network

lrwxrwxrwx 1 root root 16 Aug 14 15:56 S12syslog -> ../init.d/syslog

lrwxrwxrwx 1 root root 17 Aug 14 16:21 S13portmap -> ../init.d/portmap

lrwxrwxrwx 1 root root 17 Aug 14 16:19 S14nfslock -> ../init.d/nfslock

lrwxrwxrwx 1 root root 14 Aug 14 15:56 S16apmd -> ../init.d/apmd

lrwxrwxrwx 1 root root 16 Aug 14 15:56 S20random -> ../init.d/random

lrwxrwxrwx 1 root root 15 Aug 14 15:56 S25netfs -> ../init.d/netfs

lrwxrwxrwx 1 root root 16 Aug 14 16:20 S35identd -> ../init.d/identd

lrwxrwxrwx 1 root root 13 Aug 14 15:56 S40atd -> ../init.d/atd

lrwxrwxrwx 1 root root 15 Aug 14 15:56 S40crond -> ../init.d/crond

lrwxrwxrwx 1 root root 16 Aug 14 16:12 S45pcmcia -> ../init.d/pcmcia

lrwxrwxrwx 1 root root 16 Aug 14 16:33 S50xinetd -> ../init.d/xinetd

lrwxrwxrwx 1 root root 20 Aug 14 15:56 S56rawdevices -> ../init.d/rawdevices

lrwxrwxrwx 1 root root 13 Aug 14 16:16 S60lpd -> ../init.d/lpd

lrwxrwxrwx 1 root root 18 Aug 14 15:58 S75keytable -> ../init.d/keytable

lrwxrwxrwx 1 root root 14 Aug 14 16:09 S80isdn -> ../init.d/isdn

lrwxrwxrwx 1 root root 18 Aug 14 16:26 S80sendmail -> ../init.d/sendmail

lrwxrwxrwx 1 root root 13 Aug 14 16:07 S85gpm -> ../init.d/gpm

lrwxrwxrwx 1 root root 15 Aug 14 15:56 S85httpd -> ../init.d/httpd

lrwxrwxrwx 1 root root 13 Aug 14 15:58 S90xfs -> ../init.d/xfs

lrwxrwxrwx 1 root root 17 Aug 14 15:55 S95anacron -> ../init.d/anacron

lrwxrwxrwx 1 root root 19 Aug 14 16:16 S99linuxconf -> ../init.d/linuxconf

lrwxrwxrwx 1 root root 11 Aug 14 15:56 S99local -> ../rc.local
```

正如输出所示，所有以 `K` 和 `S` 开头的文件名都是指向位于 `/etc/rc.d` 和 `/etc/rc.d/init.d` 目录中的脚本的符号链接。事实上，`/etc/rc.d/rc` 脚本会严格按照它们在目录列表中出现的顺序执行这些文件。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_283_0.png)

请注意，目录列表中的最后一个文件是指向 `../rc.local` 脚本的符号链接。这意味着 `/etc/rc.d/rc.local` 在所有其他脚本之后执行。因此，你可以在该脚本中放置任何你希望在 Linux 系统启动时执行的命令。

大多数启动脚本位于 `/etc/rc.d/init.d` 目录中。你可以手动调用该目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，要停止 Web 服务器，请键入以下命令：

```
/etc/rc.d/init.d/httpd stop
```

```
Shutting down http: [ OK ]
```

通过熟悉 `/etc/rc.d/init.d` 目录中的脚本，你可以提升系统管理技能。要查看列表，请键入以下命令：

```
ls /etc/rc.d/init.d
```

```
anacron halt keytable netfs pppoe sendmail ypbind

apmd httpd killall network random single yppasswdd

arpwatch identd kudzu nfs rawdevices smb ypserv

atd innd linuxconf nfslock rstatd snmpd

crond ipchains lpd pcmcia rusersd syslog

functions isdn mars-nwe portmap rwalld xfs

gpm kdcrotate named postgresql rwhod xinetd
```
