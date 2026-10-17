
指定服务可用端口号的单单词名称。大多数常用服务都分配了数字。该字段被分为 `tcp` 或 `udp`。需要注意的是，`18/tcp` 条目与 `18/udp` 条目非常不同。没有技术原因要求同一个服务必须同时存在于两者。通常遵循常识。行中 `#` 字符之后的任何文本都会被忽略，并被视为注释。如果你恰好是从零开始构建，这里是旧 Debian 发行版提供的 `/etc/services` 文件副本：

| name | port/protocol | aliases | comment |
| :--- | :--- | :--- | :--- |
| ftp | 21/tcp | | |
| ssh | 22/tcp | | SSH Remote Login Protocol |
| ssh | 22/udp | | Remote Login Protocol |
| telnet | 23/tcp | | |
| smtp | 25/tcp | | |
| smtp | 25/udp | | |
| time | 37/tcp | | resource location |
| time | 37/udp | | |
| rlp | 39/udp | | IEN 16 |
| nameserver | 42/tcp | | |
| whos | 43/tcp | | |
| re-mail-ck | 50/tcp | | Remote Mail Checking Protocol |
| re-mail-ck | 50/udp | | Remote Mail Checking Protocol |
| domain | 53/tcp | | nameserver |
| domain | 53/udp | | name-domain server |
| bootps | 67/tcp | | deprecated |
| bootps | 67/udp | | |
| bootpc | 68/tcp | | |
| bootpc | 69/udp | | |
| tftp | 70/tcp | | |
| gopher | 70/udp | | Internet Gopher |
| finger | 77/tcp | | |
| finger | 77/udp | | |
| www | 80/tcp | | WorldWide HTTP |
| www | 80/udp | HyperText Transfer Protocol | |
| link | 87/tcp | | tty |
| kerberos | 88/tcp | kerberos kb5 | Kerberos v5 |
| kerberos | 88/udp | kerberos kb5 | Kerberos v5 |
| sudup | 95/tcp | | |
| hostnames | 101/tcp | hostname | usually from sri-nric |
| hostnames | 102/tcp | tsap | part of ISODE |
| iso-tap | 105/tcp | cso-ns | also used by CSO name server |
| csnetns | 105/udp | | |
| csnetns | 107/tcp | cso-ns | Remote Telnet |
| telnet | 109/udp | postoffice | POP version 2 |
| pop-2 | 109/tcp | | POP version 3 |
| pop-2 | 109/udp | | |
| pop-3 | 110/tcp | | |
| pop-3 | 110/udp | | |
| sunprpc | 111/tcp | portmapper | RPC 4.0 portmapper TCP |
| sunprpc | 111/udp | portmapper | RPC 4.0 portmapper UDP |
| auth | 113/tcp | authentication tap | ident |
| sftp | 117/tcp | | |
| uucp-path | 119/tcp | reads out | USEN News Transfer Protocol |
| ntp | 123/tcp | | Network Time Protocol |
| ntp | 123/udp | | |
| netbios-ns | 137/tcp | | NETBIOS Name Service |
| netbios-ns | 137/udp | | |
| netbios-dgm | 138/tcp | | NETBIOS Datagram Service |
| netbios-dgm | 138/udp | | |
| netbios-ssn | 139/tcp | | NETBIOS session service |
| netbios-ssn | 139/udp | | |
| imap2 | 143/tcp | | Interim Mail Access Protocol v2 |
| imap2 | 143/udp | | |
| snmp | 161/udp | | Simple Net Mgmt Got |
| snmp-trap | 162/tcp | snmptrap | Traps for SNMP |
| cmip-map | 163/tcp | | ISO mgmt over IP (CMOT) |

# Linux 网络 HOWTO

| 服务 | 端口 | 描述 |
|---|---|---|
| cmip-man | 163/udp | |
| cmip-agent | 164/tcp | |
| cmip-agent | 164/udp | |
| xdmcp | 177/tcp | X 显示控制协议 |
| nextstep | 177/udp | NextStep 窗口管理器 |
| nextstep | 178/udp | NextStep 服务器 |
| bgp | 179/tcp | 边界网关协议 (Border Gateway Proto.) |
| bgp | 179/udp | |
| prospero | 191/tcp | Cliff Newman 的 Prospero |
| prospero | 191/udp | |
| irc | 194/tcp | 互联网相对聊天 (Internet Relay Chat) |
| irc | 194/udp | |
| smux | 199/tcp | SNMP 多路复用 |
| smux | 199/udp | |
| at-rtmp | 201/tcp | AppleTalk 路由 |
| at-rtmp | 201/udp | |
| at-nbp | 202/tcp | AppleTalk 绑定 |
| at-nbp | 202/udp | |
| at-echo | 204/tcp | AppleTalk 回显 |
| at-echo | 204/udp | |
| at-zis | 206/tcp | AppleTalk 区域信息 |
| at-zis | 206/udp | |
| z3950 | 210/tcp wais | NISO Z39.50 数据库 |
| z3950 | 210/udp wais | |
| ipx | 213/tcp | IPX |
| ipx | 213/udp | |
| imap3 | 220/tcp | 交互式邮件访问 |
| imap3 | 220/udp | 协议 v3 |
| ulistserv | 372/tcp | UNIX 列表回声 |
| ulistserv | 372/udp | |

## UNIX 特有服务

| 服务 | 端口 | 描述 |
|---|---|---|
| exec | 512/tcp | comsat |
| biff | 512/udp | |
| login | 513/tcp | |
| who | 513/udp | whod |
| shell | 514/tcp cmd | 不使用密码 |
| syslog | 514/udp spooler | 打印打印机池化程序 |
| printer | 515/tcp | |
| talk | 517/udp | |
| ntalk | 518/tcp | RIP |
| route | 520/tcp | 路由时间服务器 |
| timed | 523/udp | newdate |
| tempo | 526/tcp | |
| courier | 530/tcp | rpc |
| conference | 531/udp | 聊天 |
| netnews | 532/tcp 只读 | 用于紧急广播 |
| netwall | 533/udp | uuc 守护进程 |
| uucp | 540/tcp uucfd | Brunhoff 远程文件系统 |
| remotesf | 556/udp rfs_server rfs | Kerberos 'login' (v5) |
| klogin | 543/tcp | Kerberos (v5) |
| kshell | 544/udp krcmd | Kerberos 'rsh' (v5) |
| kerberos-adm | 749/tcp | Kerberos 'kadmin' (v5) |
| webster | 765/tcp | 网络字典 |
| webster | 765/udp | |

## 来自“分配数字”：

> 注册端口（Registered Ports）不受 IANA 控制，在大多数系统中可以被普通进程或由普通用户执行的程序使用。

> 端口在 TCP [45,106] 中用于命名携带长时间对话的逻辑连接端点。为了向未知呼叫者提供服务，定义了服务联系端口。此列表指定了服务器进程在联系时使用的端口。IANA 无法控制其注册的端口的使用，但会注册或列出这些端口以方便社区使用。

### 5.8.1. /etc/services

```
ingress 1524/tcp
ingresslock 1524/udp
prospero-np 1525/udp # 非特权 Prospero 
prospero-np 5002/tcp
rfe 5002/udp # 自由无线以太网
rfe 7000/tcp # 实际上仅使用 UDP
bbs # BBS 服务
# Kerberos (协议 Athena/MIT) 服务 运行站点
# 注意这些是针对 Kerberos v4 的，且是非官方的。
# v4 应该取消此注释并注释上面的 v5 条目。
kerberos4 750/udp kdc Kerberos (server) urdp
kerberos4 750/tcp kdc Kerberos (server) tcp
kerberos_master 751/udp # Kerberos 身份验证
kerberos_master 751/tcp # Kerberos 身份验证
passwd_server 752/udp # Kerberos 从机传播
kb_prop 754/tcp # Kerberos 注册
krubdate 760/tcp kreq Kerberos "master"
kpasswd 761/tcp kpd # 带有 Kerberos 的 Pop
kpop 1109/tcp # Kerberos 多路复用器
kneted 2053/tcp # Zephyr 服务器
zephyr-srv 2102/udp # Zephyr serv-hm 连接
zephyr-clr 2103/udp # Zephyr 主机管理器
zephyr-hm 2104/udp # Kerberos 加密登录
# 非官方但必要的服务（针对 NetBSD）
upsrv2 871/tcp # SUP 服务器
upsfdbg 1127/tcp # SUP 调试
# 数据报传输协议服务
tmp 1/ddp # 路由表维护协议
nbp 2/ddp # 名称绑定协议
echo 4/ddp # AppleTalk 回声协议
zip 6/ddp # 区域信息协议
# Debian GNU/Linux 服务
rmtcfg 1236/tcp # Gracis 数据包远程配置服务器
xtel 1313/tcp # french minithel
finger 2003/tcp # GNU Finger
postgres 4321/tcp # POSTGRES
mandelspwan 9359/udp mandelbrot # 网络 mandelbrot
# 本地服务
```

在现实世界中，随着新服务的创建，这篇文章正变得过时。如果你觉得自己的副本不完整，我建议从最近的发行版中拷贝一个新的 `/etc/services`。

```
#pop-3 stream tcp nowait root /usr/bin/tcpd /usr/bin/pop3d
#
#cfinger 是用于 Debian 的 GNU finger 服务器。（注意：
# 当前 'finger' 守护进程的实现允许以 'root' 身份运行。

#cfinger stream tcp nowait root /usr/bin/tcpd /usr/bin/in.fingerd
#finger stream tcp nowait root /usr/bin/tcpd /usr/bin/in.fingerd
#netstat stream tcp nowait nobody /usr/bin/tcpd /bin/netstat
#sysstat stream tcp nowait nobody /usr/bin/tcpd /usr/bin/ps -auww

# Tftp 服务用于启动。大多数站点
# 仅运行在作为“启动服务器”的机器上。

#tftp dgram wait nobody /usr/sbin/tcpd /usr/sbin/in.tftpd
#tftp dgram wait nobody /usr/sbin/tcpd /usr/sbin/in.tftpd
#bootps dgram udp root /usr/sbin/bootpd  bootpd -i -t 120

# Kerberos 认证服务（这些可能需要修正）

#klogin stream tcp nowait root /usr/sbin/tcpd /usr/bin/in.rllogin -k
#eklogin stream tcp nowait root /usr/sbin/tcpd /usr/bin/in.rllogin -k-x
#shell stream tcp nowait root /usr/sbin/tcpd /usr/sbin/in.rshd -k

# 仅在 Kerberos 服务器上运行的服务（这些可能需要修正）

#krbupdate stream tcp nowait root /usr/sbin/tcpd /usr/sbin/registerd
#kpasswd stream tcp nowait root /usr/sbin/tcpd /usr/sbin/kpasswd

# 基于 RPC 的服务
#mountd/1 dgram rpc/udp root /usr/sbin/tcpd /usr/sbin/in.rpc.mountd
#rsatd/1-3 dgram rpc/udp root /usr/sbin/tcpd /usr/sbin/in.rsatd
#userserd/2-3 dgram rpc/udp root /usr/sbin/tcpd /usr/sbin/in.userserd
#walld/1 dgram rpc/udp root /usr/sbin/tcpd /usr/sbin/in.rwald

# inetd.conf 结束。
ident tcp nowait nobody /usr/sbin/identd -i
```

## 5.9. 其他杂项网络相关配置文件。

Linux 下有许多与网络配置相关的杂项文件，你可能会感兴趣。你可能不需要修改这些文件，但描述它们是值得的，以便让你知道它们包含什么以及为什么要使用它们。

### 5.9.1. /etc/protocols

`/etc/protocols` 文件是一个通过协议名称映射协议 ID 的数据库。程序员使用它来允许在程序中通过名称指定协议。它也被某些程序（如 `tcpdump`）使用，用于在输出中显示数字的名称。该文件的通用语法为：

```
protocolname number aliases
```

Debian 发行版提供的 `/etc/protocols` 文件如下：
