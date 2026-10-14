
| netbios-ssn | 139 | NETBIOS 会话服务 |

## 第 3 章：安装 Linux 和互联网组件

```
nextstep 178/tcp NeXtStep NextStep # NeXtStep window
nextstep 178/udp NeXtStep NextStep # server
bgp 179/tcp # Border Gateway Proto.
bgp 179/udp
prospero 191/tcp # Cliff Neuman's Prospero
prospero 191/udp # Internet Relay Chat
irc 194/tcp
irc 194/udp
snux 199/tcp # SNMP Unix Multiplexer
smux 199/udp
nat-rtmp 201/tcp # AppleTalk routing
nat-rtmp 201/udp
at-nbp 202/tcp # AppleTalk name binding
nat-nbp 202/udp
at-echo 204/tcp # AppleTalk echo
nat-echo 204/udp
nat-zis 206/tcp # AppleTalk zone information
nat-zis 206/udp
z3950 210/tcp wais # NISO Z39.50 database
z3950 210/udp wais
ipx 213/tcp # IPX
ipx 213/udp # Interactive Mail Access
imap3 220/tcp # Protocol v3
imap3 220/udp
uulisterv 372/tcp # UNIX Listserv
uulisterv 372/udp
# UNIX specific services
exec 512/tcp
biff 512/udp comsat
login 513/tcp
who 513/udp whod. # no passwords used
shell 514/tcp cmd
syslog 514/udp
printer 515/tcp spooler # line printer spoller
talk 517/udp
ntalk 518/udp
route 520/udp routed router # RIP
timed 525/udp timeserver
tempo 526/tcp newdate
courier 530/tcp rpc
conference 531/tcp chat
netnews 532/tcp readiness # -for emergency broadcasts
netwall 533/udp
uucp 540/tcp uucpd # uucp daemon
remotefs 556/tcp rfs_server rfs # Brunhoff remote filesystem
klogin 543/tcp # Kerberized 'login' (v5)
kshell 544/tcp # Kerberized 'rsh' (v5)
kerberos-adm 749/tcp # Kerberos 'kadmin' (v5)
webster 765/tcp # Network dictionary
webster 765/udp
```

节自“分配数字”：

> 注册端口（Registered Ports）不受 IANA 控制，在大多数系统中可以被普通用户进程或由普通用户执行的程序使用。

> 端口在 TCP [45,106] 中用于命名携带长期对话的逻辑连接端点。为了向未知呼叫者提供服务，定义了服务联系端口。此列表指定了服务器进程作为其联系端口使用的端口。虽然 IANA 无法控制这些端口的使用，但为了社区的方便，它注册或使用了这些端口的列表。

```
ingresslock 1524/tcp
prospero-np 1525/tcp # Prospero non-privileged
prospero-np 1525/udp
rfe 5002/tcp # Radio Free Ethernet
rfe 5002/udp # Actually uses UDP only
```

### Kerberos (Project Athena/MIT) 服务

# 注意这些是针对 Kerberos v4 的，且是非官方的。运行 v4 的站点应该取消这些行的注释并注释掉上面的 v5 条目。

```
kerberos 750/udp kdc # Kerberos (server) udp
kerberos 750/tcp kdc # Kerberos (server) tcp
krubdate 760/tcp kreg # Kerberos registration
kpasswd 761/tcp kpwd # Kerberos "passwd"
klogin 543/tcp # Kerberos 加密登录
eklogin 2105/tcp # Kerberos 加密登录
kshell 544/tcp krcmd # Kerberos 远程 shell
```

### 非官方但必要的（针对 NetBSD）服务

```
supfilesrv 871/tcp # SUP server
supfilebdg 1127/tcp # SUP debugging
```

并不是所有的服务都与将 Linux 用作互联网服务器的讨论相关。然而，了解 TCP/IP 网络和服务的设置方式是重要的，即使是为了让你放心，Linux 完全有能力胜任功能齐全的互联网服务器。

> 注意：`/etc/services` 文件中的某些服务将在全本书中被讨论。例如，关于端口和万维网（WWW）服务器的讨论将在第 4 章进行。现在，你不需要背诵 `/etc/services` 的内容，但你应该记住它的存在以备日后参考。

## 重新编译内核以包含 TCP/IP

并不是所有的服务都与将 Linux 用作互联网服务器的讨论相关。然而，了解 TCP/IP 网络和服务的设置方式是重要的，即使是为了让你放心，Linux 完全有能力胜任功能齐全的互联网服务器。

> 注意：`/etc/services` 文件中的某些服务将在全本书中被讨论。例如，关于端口和万维网（WWW）服务器的讨论将在第 4 章进行。现在，你不需要背诵 `/etc/services` 的内容，但你应该记住它的存在以备日后参考。

你可能需要重新编译内核以包含某些功能。要做到这一点，进入内核源码目录（通常为 `/src/linux`）并运行 `make config` 命令。这将打开一个交互式菜单，你可以在其中选择各种选项。

```bash
cd /src/linux
make config
```

配置菜单中有许多选项，大多数是默认设置的。你只需要更改与你的特定需求相关的选项。一旦完成配置，通过运行 `make` 来编译内核：

```bash
make
```

编译需要一些时间。一旦完成，你将获得一个新的内核镜像，可以将其安装到你的系统中。

# 第3章：安装 Linux 和网络组件

```bash
#
# 顺便说一下，Arnt Gulbrandsen <agulbra@nvg.unit.no> 表示 127.0.0.1
# 绝对不应该命名为机器的名字。这会导致某些（愚的）程序、rc
# 以及据说的 talk 出现问题：^
#
```

```bash
# 用于回环地址。
127.0.0.1 localhost

# 局域网上的其他主机
245.330.210.123 kevin.kreichard kevin
```

```bash
# hosts 文件结束。
```

# /etc/HOSTNAME

该文件存储了你机器的主机名。这是一个单行文件：

```
kreichard.com
```

该文件是强制性的，如果你没有安装网络并使用默认设置，将被分配一个名为 `darkstar.frop.org` 的主机名。

# /etc/rc.d/rc.inet1

该文件存储了几个重要的地址：

- 你的 IP 地址

- 你的子网掩码

- 你的网络地址

- 你的广播地址（如果有的话）

- 你的网关地址（如果有的话）

该文件如下：

```sh
#!/bin/sh
#
# rc.inet1 此 shell 脚本启动基础 INET 系统。
#
# 版本: @(@)/etc/rc.d/rc.inet1 1.01 05/27/93
#
```

```bash
HOSTNAME=`hostname`
```

# 挂载回环设备。

`/sbin/ifconfig lo 127.0.0.1`

`/sbin/route add -net 127.0.0.0`

# 如果你有以太网连接，请使用以下行来配置

# eth0 接口。如果你只使用回环或 SLIP，请不要包含

# 文件中的剩余行。

# 根据你的设置进行编辑。# 替换为你的 IP 地址！

#IPADDR="128.253.154.302"

#NETMASK="255.255.255.0" # 替换为你的子网掩码！
