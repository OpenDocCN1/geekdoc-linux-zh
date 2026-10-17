
```
Barracuda# ls -l /
total 2124
lrwx-xr-x 1 root 7 Mar 18 05:30 -> /usr/bin
-r-xr-- 1 root 110352 Mar 18 05:31 boot
drwxr-sr-x 5 root 2048 Mar 19 12:32 dev
drwxr-sr-x 5 root 512 Mar 18 04:56 etc
drwxr-sr-x 4 root 512 Oct 14 1994 export
drwxr-sr-x 27 root 1024 home
-rwx-xr-x 1 root 252913 Mar 18 05:31 kadb
lrwx-xr-x 1 root 7 Mar 18 05:30 -> /usr/lib
drwxr-sr-x 2 root 8192 Mar 18 04:53 lost+found
drwxr-sr-x 2 root 512 Oct 14 1994 mnt
drwxr-sr-x 2 root 512 Mar 18 04:56 pcfs
drwxr-sr-x 1 root 512 Mar 18 05:31 sbin
lrwx-xr-x 1 root 13 Mar 18 05:30 sys -> /usr/kvm/sys
drwxr-sr-x 2 root 512 Mar 18 05:33 tftboot
drwxrwsrt 2 root 512 Mar 18 04:15 tmp
drwxr-sr-x 27 root 1024 Mar 18 05:22 usr
drwxr-sr-x 10 root 512 Oct 14 1994 var
-rwx-xr-x 1 root 1740338 Mar 18 05:30 vmnix
```

注意某些目录名称后面有 `->`，这表示它们指向其他地方。在这台机器上，`vmnix` 是内核。

> 如果你不熟悉链接的概念，可以把它理解为一种让物理上位于某处的文件同时出现在另一个位置的方法。在前面的列表中，`lib` 是指向 `/usr/lib` 的链接。也就是说，根目录中有一个你可以像访问根目录一样访问，但在这种情况下，`usr/lib` 是一个目录，所以你实际上可以 `cd /lib` 并进入 `/usr/lib`。

# 穿行系统

这是 IRIX 机器上的另一个目录：

```
SUZIE 71 > ls -l
ntotal 38303
drwxr-xr-x 2 root sys Jan 28 13:40 CDROM
drwxr-xr-x 2 root sys Jan 15 19:10 Desktop
lrwxr-xr-x 1 root sys Jan 15 15:24 bin -> usr/bin
drwxr-xr-x 1 root sys Jan 15 19:05 debug -> proc
drwxr-xr-x 13 root sys Mar 5 18:10 dev
drwxr-xr-x 2 root sys Jan 15 19:10 dumpster
drwxr-xr-x 16 root sys Mar 18 14:16 etc
drwxr-xr-x 2 root sys Mar 19 15:24 hw
drwxr-xr-x 2 root sys Feb 15 22:23
drwxr-xr-x 2 root sys Feb 12 13:43 lib
drwxr-xr-x 5 root sys Feb 5 13:35 lib32
drwxr-wx 1 root sys Mar 5 18:00 nr
drwxr-xr-x 2 root root sys Jan 9 12:15 nmail
drwxr-xr-x 2 root sys Jan 15 17:25 opt
drwxr-xr-x 8 root sys Jan 15 17:25 opt
drwxr-xr-x 33 root sys Jan 25 09:06 var
d-xr-x 2 root root sys    19:24


-----       1 111111


----          11111

------         11::22
drwxr----  2 root       1:55

--------  2 root      11:11
--------  2 root      1:
-
-rw-k-x 8     11:11
drwxr-xr-x 42 root sys Mar 5 18:09 usr
--------      
 
drwxr-xr-x 33 root sys Jan 15 09:0
 
```

这里有几个目录也指向其他地方。在这台机器上，内核是 `unix`。

注意这里也存储了一个 `unix-old` 文件吗？你一眼就能看出内核最近被重新配置过。

# 中央配置位置：/etc

正如你在昨天的讨论中所注意到的，`/etc` 是搜索你机器配置文件的重要地方。

以下是我 SunOS 机器上的 `/etc` 目录的一部分：

```
Barracuda# is /etc
.install.d fastboot      link            publickey sm
adm             fasthalt      magic           rc              sm.bak
ialias       fbtab         mkfs            root.boot      spool
alias.dir  filetype      mkknod         rc.ip           state
alaliases.pag  format.dat    modt            rc.local       svdtab
arp              fsc own         mount           rc.local-orig syslog.conf
bootperms      stab         mount_rfs     rc.single     syslog.pid
chown           fuser        mtab            rdump          termcap
```

![](img/74418f52d5d454acca60721059dbdc99_146_0.png)

# 第128 天

```
chroot gettytab ncheck reboot tmp
clri group netmasks remote ttys
config halt netmasks-orig renice ttytab
```

在 IRIX 上，这里是 `/etc` 的部分内容预览：

```
SUZIE joray 101 > ls /etc
config init prfstat stdlogin
cpr_proto init.d profile sulgin
cron inittab project swap
cron.d install projid sys_id
cshrc iocctnfig.conf protocols sysinfo
cshrc-orig irix.cap prtvtoc syslog.conf
datemsk pwck telnit
default killall rc0
device_tab labelit rc0.d tt
devmm link ttytype
dmedia_tools_cap insycron rc2.d uadmin
dump magic rc3 umcount
dvtool mipsaversion rc3.d umontfs
```

在 SunOS 机器上，许多项目实际上指向 `/etc`，而在 IRIX 机器上，情况有所不同。

# 漫游你的系统

这里是 SunOS 上 `/var` 的情况：

```
Barracuda# ls /var
adm      log      preserve tmp
crash   net      spool   yp
```

这里是 IRIX 上的情况：

```
SUZIE joray 105 > ls /var
X11     dmedia  ns       sysadm
adm     flexlm  opt      sysadmindktop
arch    inst    preserve sysgen
boot    lib     preserve      tmp
cms     mail    saf      tmp_rex
config        share   www
cron    netls   spool   xfsdump
dhcp    netscape statmon  yp
```

以下是你会在日志中找到的类型信息示例。它来自我 SunOS 机器的 `/var/adm/messages` 文件：
