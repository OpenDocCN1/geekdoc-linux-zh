

NIS 可以在安装期间进行配置，也可以在安装完成后通过 `setup` 或 `linuxconf` 程序进行配置。要连接到 NIS 服务器，必须拥有域名和服务器名称。

## NIS

我们之前讨论过的工具用于管理单台 Linux 机器。NIS（Network Information Service，网络信息服务）是用于一组联网机器的工具。NIS 提供由数据库和进程组成的简单网络查找服务。NIS 的目的是为网络中的所有机器提供信息，它可以托管登录 ID 和密码、组信息，或主机名和 IP 值等数据。

NIS 服务器的一个常见用途是为网络中的所有计算机提供一个中心位置进行身份验证。NIS 允许管理员仅在一台机器上添加新用户，并将结果提供给网络中的任意机器。

网络中可以有一个或多个 NIS 服务器。这些服务器可以支持同一个域，也可以支持独立的域。如果它们支持同一个域，则有一个主服务器和一个或多个从服务器。从服务器会收到 NIS 的任何变更通知，并自动获取必要的变更以同步其数据库。

## 配置 NIS

在此配置中，我们首先将配置一个名为 NFSServer 的 NFS 服务器和一个名为 NFSClient 的 NFS 客户端。在配置好 NFS 服务器和客户端后，我们随后将在 NFSServer 上配置 NIS，以实现以下功能。

首先，向用户授予对 /home 目录的访问权限。通过在 /etc/exports 文件中添加以下条目，允许以读写权限挂载 /home 目录的 NFS：

```
/home *(rw,sync)
```

让 NFS 读取 /etc/exports 文件中的新条目，并向网络用户开放 /home：

```bash
exportfs -a
```

确保所需的 NFS、NFS 锁和端口映射守护进程都在运行，并配置为在下次重启后启动。

```
# exportfs -a
# chkconfig nfslock on
# chkconfig nfs on
# chkconfig portmap on
# /etc/init.d/portmap start
Starting portmapper: [ OK ]
# /etc/init.d/nfslock start
# /etc/init.d/nfs start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS daemon: [ OK ]
Starting NFS mountd: [ OK ]
#
```

在 NFSClient 上，将现有的旧 /home 目录移动，并创建一个名为 /nfs/home 的新目录，然后创建一个指向新主目录 /home 的逻辑链接。

```
# mv /home /home.save
# ls /home
ls: /home: No such file or directory
# ln -s /nfs/home /home
# ll /
. . .
drwxr-xr-x 66 root root 8192 Jul 27 20:34 etc
lrwxrwxrwx 1 root root 9 Jul 27 20:55 home -> /nfs/home
drwxr-xr-x 12 root root 4096 Jul 27 20:49 home.save
...
```

确保能够在 NFSclient 的 /nfs/home 目录上挂载 NFSserver 的 /home 目录。

```
# mount NFSserver:/home /nfs/home/
# ls /home
davidengle guest home ksmith myuser test1
dengle hello jsmith lsmith rbrown test2
# umount /nfs/home/
#
```

配置 autofs 自动挂载。编辑 `/etc/auto.master` 文件，使其在访问 /nfs 目录时引用文件 `/etc/auto.nfs` 进行挂载。五分钟后，autofs 将卸载该目录。

```
# cat /etc/auto.master
# $Id: auto.master,v 1.2 1997/10/06 21:52:03 hpa Exp $
# Sample auto.master file
# Format of this file:
# mountpoint map options
# For details of the format look at autofs(8).
# /misc /etc/auto.misc --timeout=60
/nfs /etc/auto.nfs --timeout=600
```

编辑文件 `/etc/auto.nfs`，以便在访问 /home 目录时执行 NFS 挂载。

```
# cat /etc/auto.nfs
# $Id: auto.misc,v 1.2 1997/10/06 21:52:04 hpa Exp $
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage
cd -fstype=iso9660, ro, nousid, nodev :/dev/cdrom
# the following entries are samples to pique your imagination
#linux -ro,soft,intr
ftp.example.org:/pub/linux
#boot -fstype=ext2 :/dev/hda1
#floppy -fstype=auto :/dev/fd0
#floppy -fstype=ext2 :/dev/fd0
#e2floppy -fstype=ext2 :/dev/fd0
#jaz -fstype=ext2 :/dev/sdc1
#removable -fstype=ext2 :/dev/hdd
home -fstype=nfs NFSserver:/home
```

启动 autofs，并使用 chkconfig 命令确保其在下次重启后启动。

```
# chkconfig autofs on
# /etc/init.d/auto.fs restart
Stopping automount: [ OK ]
Starting automount: [ OK ]
#
```

NIS 以前被称为 Sun Yellow Pages（YP）。NIS 只是一个名称变更。服务本身没有变化。更改名称是因为版权侵权；然而，这些程序仍以 yp 开头命名。

首先告诉 Linux 添加将使用的 NIS 域。编辑 /etc/sysconfig/network 文件并添加要使用的 NIS 域名。在本例中，我们将使用名称 NIS-LINUX-NETWORK。

```
# cat /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=localhost.localdomain
NISDOMAIN="NIS-LINUX-NETWORK"
```

NIS 服务器也必须作为 NIS 客户端。接下来，我们将编辑 NIS 客户端配置文件 /etc/yp.conf，将域的 NIS 服务器列为 localhost。

```
# cat /etc/yp.conf
# /etc/yp.conf - ypbind configuration file
# Valid entries are
#
#domain NISDOMAIN server HOSTNAME
#    Use server HOSTNAME for the domain NISDOMAIN.
#
#domain NISDOMAIN broadcast
#    Use broadcast on the local net for domain NISDOMAIN
#
#ypserver HOSTNAME
#    Use server HOSTNAME for the local domain. The
#    IP-address of server must be listed in /etc/hosts.
#
ypserver 127.0.0.1
```

在 /etc/init.d 目录中启动必要的 NIS 守护进程。使用 chkconfig 命令确保守护进程在下次重启后启动，然后初始化 NIS 域。将使用六个命令来启动 NIS：portmap、yppasswd、ypserv、ypbind 和 ypxfrd。

- **portmap** NIS 运行的 RPC 守护进程。
- **yppasswd** 允许 NIS 用户通过 NIS 客户端在 NIS 服务器上更改密码。
- **ypinit** ypinit 命令为当前默认域构建 /var/yp 的域子目录，并为系统构建完整的管理员映射集。
- **ypserv** 主要的 NIS 服务器进程。
- **ypbind** 主要的 NIS 客户端进程。
- **ypxfrd** 用于加速传输非常大的 NIS 映射的程序。

```
# /etc/init.d/yppasswd start
Starting YP passwd service:    [ OK ]
# /etc/init.d/ypserv start
Setting NIS domain name NIS-LINUX-NETWORK: [ OK ]
Starting YP server services: [ OK ]
# chkconfig yppasswd on
# chkconfig ypserv on
#
```

使用 **ypinit** 命令初始化 NIS 域。此程序将使普通用户账户对 NIS 客户端可用。

```
# /usr/lib/yp/ypinit -m
```

```
At this point, we have to construct a list of the hosts
which will run NIS
servers. davelinux is in the list of NIS server hosts.

Please continue to add
the names for the other hosts, one per line. When you
are done with the
list, type a <control D>.
  next host to add: NISServer
  next host to add:
The current list of NIS servers looks like this:

NISServer
Is this correct? [y/n: y] Y
We need a few minutes to build the databases . . .
Building  /var/yp/NIS-LINUX-NETWORK/ypservers . . .
Running /var/yp/Makefile . . .
gmake [1]: Entering directory `/var/yp/NIS-LINUX-NETWORK`
Updating passwd.byname . . .
Updating passwd.byuid . . .
Updating group.byname . . .
Updating group.bygid . . .
Updating hosts.byname . . .
Updating hosts.byaddr . . .
Updating rpc.byname . . .
Updating rpc.bynumber . . .
Updating services.byname . . .
Updating services.byservicename . . .
Updating netid.byname . . .
Updating protocols.bynumber . . .
Updating protocols.byname . . .
Updating mail.aliases . . .
gmake [1]: Leaving directory `/var/yp/NIS-LINUX-NETWORK`
NISServer has been set up as a NIS master server.

Now you can run yppinit -s NISServer on all slave servers.
#
```

在创建 NIS 域文件后，你可以启动 **ypbind** 和 **ypxfrd** 守护进程。

```
# /etc/init.d/ypbind start
Binding to the NIS domain:
              [ OK ]
Listening for an NIS domain server.
# /etc/init.d/ypxfrd start
Starting YP map server:
              [ OK ]
# chkconfig ypbind on
# chkconfig ypxfrd on
```

使用 **useradd** 命令添加 NIS 用户。使用 **passwd** 命令更改密码。创建用户后，必须通过在 /var/yp 目录中执行 **make** 命令来更新 NIS 域的身份验证文件。此过程将使所有普通用户账户对 NIS 可用，包括存储在 /etc/passwd 和 /etc/group 文件中的数据。

```
# useradd -g users nisuser1
# passwd nisuser1
Changing password for user nisuser1.
New password:
Retype new password:
password: all authentication tokens updated
successfully.
```

