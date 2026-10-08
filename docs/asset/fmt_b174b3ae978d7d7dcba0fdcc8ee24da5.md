
Kernel 2.4.2-2 on i686

login: linda

Password:

Last login: Fri Jun 22 14:12:55 from 192.168.1.101

`[linda@HostA linda]$ su - root`

Password:

`[root@HostA]#`

### 步骤 3. 验证 NFS 软件包已安装

```
[root@HostA /root]# rpm -qa | grep -i nfs
nfs-utils-0.3.1-5
```

如果未安装 NFS，现在安装该软件包。

```
[root@HostA /root]# mount /dev/cdrom
[root@HostA /root]# cd /mnt/cdrom/RedHat/RPMS
[root@HostA RPMS]# rpm -install nfs-utils-0.3.1-5.i386
```

### 步骤 4. 验证 NFS-server 守护进程正在运行

```
[root@HostA /root]# ps aux | grep -i nfs
root 855 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 856 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 859 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 860 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 861 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 862 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 863 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 864 0.0 0.0 0 ? SW 08:34 0:00 [nfsd]
root 14413 0.0 0.0 1620 592 pts/0 S 14:16 0:00 grep -i nfs
[root@HostA /root]#
```

如果它们没有启动，启动守护进程最简单的方法是找到启动文件。进入运行时目录，找到启动脚本，并使用 `S60nfs` 脚本启动它。如果你对脚本更加熟悉，可以直接使用完整的 `root#` 运行它。现在，我们可以使用这种技术：

```
[root@HostA]# cd /etc/rc3.d
[root@HostA] rc3.d]# ls
K01dkrocote K50smpd S40atd S85g
K15httpd K50utx S12syslog S55sshd S90crond
K03rhns K65ident S13portmap S56rawdevices S90xifs
K20stand K73ypbind S14nfslock S56xinet S95anacron
K20users K74nscd S17keytable S60lpd S99local
K20walld K74pyvers S20random S60ifs
K20words S80kndu S25netfs S80isdn
K34pyassswd S80iptables S26amd S28outs S80ppoe
K45arpwitch [root@HostA] rc3.d]# ..S60n start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS mount: [ OK ]
Starting NFS daemon: [ OK ]
[root@HostA] rc3.d]#
```

### 步骤 5. 记录 NFS 服务器的 IP 地址详细信息

你需要这些信息提供目标安装系统，以便它可以找到导出的目录。使用以下 `ifconfig` 语法：

```
[root@HostA] /etc]# ifconfig eth0
eth0 Link encap:Ethernet Hwaddr 00:50:BA:DB:A1:9D
inet addr:192.168.1.206 Bcast:192.168.1.255
Mask:255.255.255.255 Metric:1
UP BROADCAST MULTICAST MTU:1500
RX packets:10439 errors:0 dropped:0 overflows:0 frame:0
TX packets:3955 errors:0 dropped:0 overflows:0 collisions:8 txqueuelen:1000
Interrupt:1 Base address:0xd00
[root@HostA] /etc]#
```

### 步骤 6. 将文件复制到硬盘

检查并确保你有至少 2GB 的空间用于源文件。我们在 `/home/inst_files` 挂载点创建了一个目录，并将两个 CD 中的 RedHat 复制到其中。以下列表显示了所需的磁盘空间。你必须从两个 CD 复制文件。如果你的驱动器没有打开，你可能需要退出目录、卸载 CD 并移除 CD。

```
[root@HostA@root]# mount /dev/cdrom
[root@HostA@root]# cp -R /mnt/cdrom/RedHat /home/inst_files/
[root@HostA@root]# cd
[root@HostA@root]# unmount /cdrom
[root@HostA@root]# mount /dev/cdrom
[root@HostA@root]# cp -R /mnt/cdrom/RedHat /home/inst_files/
```
`df -h`

| 文件系统 | 大小 | 可用 | 挂载点 |
|---|---|---|---|
| /dev/sda | 251M | 128M | / |
| /dev/sda1 | 53M | 3.5M | /boot |
| /dev/sda6 | 1.6G | 1G | /home |
| /dev/sda7 | 1.6G | 804M | /usr |
| /dev/sda9 | 251M | 19M | /var |

### 步骤 7. 通过 NFS 导出目录

不设置安全性是为了确保不熟悉 NFS 的用户也能成功导出。这里的安全性由 `*` 符号表示，意味着任何主机都可以挂载此导出目录。如果启用安全性，目标客户端（即 HostB）将无法连接到 NFS 服务器。换句话之，任何安全设置都会在安装开始停止。要让 NFS 服务器导出名为 `/home/inst_files` 的目录，请向 `/etc/exports` 文件添加以下条目。然后 `exports` 命令就可以导出该目录了。

```
[root@HostA@root]# cat /etc/exports
# This is the exports file for HostA
/mnt/cdrom * (ro)
/home/inst_files * (ro)
[root@HostA@root]#
```

文件显示了挂载在 `/mnt/cdrom` 的 CD-ROM 以及 `/home/inst_files` 目录为只读且没有其他参数。

```
[root@HostA@root]# exportfs
[root@HostA@root]# exportfs -a
```

```
[root@HostA /root]# exportfs
/home/inst_files <world>
/mnt/cdrom <world>
[root@HostA /root]#
```

你会收到一些可以忽略的警告。如果你看到 `/home/inst_files <world>` 响应，说明导出成功。`world` 条目表示任何拥有 NFS 客户端的用户都可以挂载你的导出目录。`exportfs` 命令在无参数使用时仅报告导出列表的状态。`exportfs -a` 命令处理并导出 `/etc/exports` 中的所有目录。使用 `exportfs -ua` 无论 `/etc/exports` 文件中内容都导出。完成后，你可能想从 `/etc/exports` 文件中删除条目。

回顾：HostA 现在正在运行 NFS 守护进程并正在导出 `/home/inst_files` 目录。在构建 NFS 客户端之前，此配置只完成了 50%。接下来是 NFS 客户端的说明。

## 准备 NFS 客户端

在这种情况下，NFS 客户端用于启动安装并为从 NFS 服务器 (HostB) 复制文件提供协议路径。安装完成后（需要几分钟），NFS 客户端将重启（届时它将是一个 Linux 主机）。

### 步骤 1. 创建 NFS 启动磁盘

创建此启动磁盘的过程与创建普通启动磁盘的过程相同。使用 `bootnet.img` 文件而不是 `boot.img` 文件。进入 `/mnt/cdrom` 目录并列出内容以确认 `bootnet.img` 文件是否存在：

```
[root@HostA cd]# cd /mnt/cdrom/images
[images]# ls -l
total 5333
-r--r--r-- 1 root root 485 Aug 30 2000 TRANS.TBL
-r--r--r-- 1 root root 14756 Aug 30 2000 boot.img
-r--r--r-- 1 root root 14756 Aug 30 2000 bootnet.img
-drwxr-xr-x 2 root root 80616 Aug 30 2000 de
-drwxr-xr-x 2 root root 20480 Aug 30 2000 drivers.img
-drwxr-xr-x 2 root root 20480 Aug 30 2000 pcmia.img
-drwxr-xr-x 2 root root 20480 Aug 30 2000 pxeboot
-drwxr-xr-x 2 root root 20480 Aug 30 2000 sv
```

# 使用 NFS 安装 Linux 111

你需要 IP 地址和子网掩码；默认网关（IP）和主域名服务器可以在主机重启时重新配置。

在提供上述信息后，系统将要求你输入 NFS 客户端预期的主机名。

域名：

主机名：HostB

二级域名服务器 (IP)：

三级域名服务器 (IP)：

你输入 HostB 是因为我们的网络没有配置本地名称服务；我们对所有服务器都使用平面的 `/etc/hosts` 文件。此时，你应该能够在两个系统之间进行 ping 通。在 NFS 客户端系统上，你可以使用 Alt-F1 和 Alt-F2 键在屏幕之间切换，以获得可以让你执行 `ping` 命令的命令行。

如果你还没有猜到的话，这个 `bootnet.img` 文件支持的网络驱动数量有限，仅供你工作使用。此时，必须使用正式支持且列在列表中的网卡作为 NFS 客户端。

# 步骤 5. 提供有关 NFS 服务器的信息

接下来，系统将要求你提供有关所设置的 NFS 服务器的信息。这些信息是你在上一步中记录的 NFS 服务器的 IP 地址。这里将使用你提供的 IP 地址构建一个命令，并命名导出的文件系统。换句话说，它将在系统 192.168.1.206 上挂载 `/home/inst_files`，此时 `/home/inst_files` 目录在两个系统上似乎是一个本地实体。

- NFS 服务器名称：192.168.1.206
- Red Hat 目录：/home/inst_files

此时，目标安装系统将使用这些信息构建指向 NFS 服务器的命令。如果情况不顺利，使用 Alt-F1、Alt-F2 和 Alt-F3 键在屏幕和命令行之间切换，以获得执行 `ping` 命令的命令行。

# 步骤 6. 继续其他“正常”安装

安装的其余部分将正常继续。

TEAM LinG - 现场、信息丰富、免费且正版！

## 定制和升级 Linux

# 典型的 NFS 文件共享

我们设置之前的场景是为了方便远程安装。NFS 更常被用作通过网络共享 Unix 类型文件系统的方法。我们准备了一个配套场景，我们将从 HostA 导出名为 `/home/monthly/reports` 的目录，并让 HostB 挂载它。一旦 HostB 通过网络挂载了 NFS 目录，它就可以在 HostA 上使用。通常，这些挂载的目录会被应用程序和用户共同使用（见图 4.2）。

为了引发讨论，了一个简单的场景。在 HostA 上创建了三个用户 Sancho Panza（用户名 panzasan）、Don Quixote（用户名 quixoted）和 Lady Dulcinea（用户名 dulceina）作为示例。在 HostB 上创建了老板 Fernando（用户名 fernando）。这三个人都是米格尔·德塞万提斯 1964 年小说《堂吉诃德》中的著名人物（伦敦：Macmillan & Co）。

查看以下信息并特别注意两点。首先，注意他们分配的用户和组。他们的用户和 gids 处于 500 范围内，这表示非特权用户。其次，注意他们在 HostA 上。NFS 和 gids 在设置 NFS 时起着重要作用。我们将稍后讨论如何使用它们。

```
[root@HostA RPM]# cat /etc/passwd
root:x:0:0:root:/root/bash
bin:x:1:1:bin:/bin/
daemon:x:2:2:daemon:/sbin/
mad:x:3:4:adm:/var/adm/
lp:x:4:7:1:lp:/var/spool/lpd
sync:x:5:0:sync:/sbin/bin/sync
shutdown:x:6:0:shutdown:/sbin/sbin/shutdown
```

![](img/cf6993b0699c37d6fb92721201c599d8_130_0.png)

export /home/monthly/reports mount /home/monthly/reports

TEAM Ling - 现场、信息丰富、免费且正版！

# 使用 NFS 安装 Linux 113

```
halt:x:7:0:halt:/bin/halt
mail:x:8:12:mail:/var/spool/mail/
news:x:9:13:news:/var/spool/news/
uuccp:x:10:14:uucp:/var/spool/uucp/
operator:x:11:0:operator:/root
games:x:12:100:games/
gopher:x:13:0:gopher:/usr/lib/gopher-data/
ftp:x:14:50:FTP:/var/ftp
nobody:x:99:99:Nobody/
sncd:x:28:28:NSCD Daemon::/bin/false
mailnull:x:47:47:giant:/var/spool/dev/null
ident:x:98:98:giant::/bin/false
rpc:x:32:32:Portmarker RPC::/bin/false
rpuser:x:29:29:RPC Service:/var/nfs:/bin/false
xfs:x:43:43:XFS Server:/etc/xfs/bin/false
apache:x:48:48:Apache:/var/www/bin/false
linda:x:500:500:/home/linda
panzan:x:501:501:/home/panzan
quixoted:x:502:502:/home/quixoted
dulcinea:x:503:503:/home/dulcinea
keeler:x:505:505:/home/keeler
teammx:x:506:506:/home/teammx
teamy:x:507:507:/home/teamy
[root@HostA #]
```

该目录将包含每月信息。每个 report 都在用户的主目录下创建并复制到 `/home/reports`。`/home/reports` 目录的基础权限允许 reports 组的任何人将文件复制到该目录。这些用户都是 reports 组的成员。同样重要的是，此目录中的每个文件分别属于某个用户。

```
[root@HostA #] ls -l /home/monthly
total 4
drwxwx---- 2 root 4096 Jun 22 reports
[root@HostA #] ls -l /home/reports
total 12
-rw-rw-r-- 1 dulcinea 13 Jun 22 dulcinea-report
-rw-rw-r-- 1 pansanz 100 Jun 22 pansanz-report
-rw-rw-r-- 1 quixoted 88 Jun 22 quixoted-report
```

此代码代表了从 HostB 导出的目录。与之前的示例不同，我们能够挂载 HostB 的目录。`/etc/exports` 文件通过名称引用 HostB，因此 TEAM Lin - 现场、互动、免费且正版！

## 定制和升级 Linux

必须更新 `/etc/hosts` 文件以便 NFS 将 HostB 解析为 IP 地址 192.168.1.208。另一种替代方案是确保可以通过 DNS 解析 HostB。

```
[root@HostA /root#] cat /etc/hosts
# 删除以下行，或者各种程序
# 网络功能将失败。
127.0.0.1               localhost.localdomain
192.168.1.208           HostB
192.168.1.206           HostA
192.168.1.222           HostC
```

```
[root@HostA /root#] cat /etc/exports
