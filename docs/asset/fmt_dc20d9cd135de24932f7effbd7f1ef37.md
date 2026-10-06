
# 脚本示例

```bash
#!/bin/sh
# 载入函数库。
./etc/rc.d/init.d/functions

# 获取配置。
./etc/sysconfig/network

# 检查网络是否已启动。
if [ "$NETWORKING" = "no" ]; then
    exit 0
fi

# 查看我们是如何被调用的。
case "$1" in
  start)
    echo -n "Starting INET services:"
    daemon rpc.portmap
    daemon inet
    touch /var/lock/subsystem
    ;;
  stop)
    echo -n "Stopping INET services:"
    killproc inet
    killproc rpc.portmap
    rm -f /var/lock/subsystem
    ;;
  *)
    echo "Usage: inet {start|stop}"
    exit 1
    ;;
esac

exit 0
```

所示，脚本调用了 `/etc/sysconfig/network` 脚本。后者遍历并执行 `/etc/sysconfig/network-scripts` 目录下的网络接口脚本。`/etc/sysconfig/network-scripts` 目录中每个网络接口有两个脚本：`ifup-xxx` 脚本（启动接口）和 `ifdown-xxx` 脚本（关闭接口），其中 `xxx` 是接口驱动程序。例如，`ifup-eth0` 是系统在启动时执行的脚本，而 `ifdown-eth0` 是关闭时执行的脚本。以下是 `/etc/sysconfig/network` 脚本：

```bash
#!/bin/sh
# network
# 启动/关闭网络

# 载入函数库。
./etc/rc.d/init.d/functions

./etc/sysconfig/network

# 检查网络是否已启动。
[ "$NETWORKING" = "no" ] && exit 0
```

```bash
# 查看我们是如何被调用的。
case "$1" in
  start)
    for i in /etc/sysconfig/network-scripts/ifup-*; do
      $i boot
    done
    touch /var/lock/subsystem
    ;;
  stop)
    for i in /etc/sysconfig/network-scripts/ifdown-*; do
      $i boot
    done
    rm -f /var/lock/subsystem
    ;;
  *)
    echo "Usage: network {start|stop}"
    exit 1
    ;;
esac

exit 0
```

以下是示例 `ifup-eth0` 脚本的列表：

```bash
#!/bin/sh
PATH=/sbin:/usr/sbin:/bin:/usr

./etc/sysconfig/network-scripts/ifcfg-eth0

if [ "$1" = "foboot" ] && [ "$ONBOOT" = "no" ]; then
    exit
fi

ifconfig eth0 ${IPADDR} mask ${MASK} broadcast ${BROADCAST}
route add -net ${NETWORK} mask ${MASK}
if [ "${GATEWAY}" != "none" ]; then
    route add default gw ${GATEWAY} metric 1
fi
```

## 234:respawn: /usr/lib/saf/sac -t 300

这保证了在重启时会尝试调用服务账户。要检查 `inetd` 是否由你启动，可以使用 `ps` 命令，或者更好是使用如下所示的 `sacadm` 命令：

```bash
# sacadm -l
PMTAG PMTYPE FLGS RCNT STATUS COMMAND
inetd inetd - 0 ENABLED /usr/sbin/inetd #inetd
demon listen
tcp - 3 ENABLED /usr/lib/saf/listen -m inetd/
tcp0 2>/dev/null
```

根据上述响应，`inetd` 已经启动并处于启用（enabled）状态。这意味着 `inetd` 正在监听服务请求，并能够启动守护进程来处理请求。

BSD、Linux 和 Solaris 2 如上述列出的脚本所示将 `inetd` 作为一个独立的守护进程启动。然而，该守护进程在所有 UNIX 单元上的配置和行为都是完全相同的。一旦启动，`inetd` 会获取并读取配置文件 `inetd.conf`（通常在 `/etc` 目录下）。该文件定义了守护进程监听服务请求的服务。使用任何编辑器，你都可以向 `inetd` 支持的服务添加或从其删除服务。以下是 SVR4 系统上存在内容的部分列表：

### Internet 服务语法

```
# <service_name> <socket_type> <proto> <flags> <user> <server_pathname> <args>
```

# Ftp 和 telnet 是标准的 Internet 服务。

```bash
ftp stream tcp nowait root /usr/sbin/in.ftpd in.ftpd
telnet stream tcp nowait root /usr/sbin/in.telnet in.telnet
# Shell, login, exec, and comsat 是 BSD 协议。
shell stream tcp nowait root /usr/sbin/in.rsh in.rsh
login stream tcp nowait root /usr/sbin/in.login in.login
exec stream tcp nowait root /usr/sbin/in.exec in.exec
comsat dgram udp wait root /usr/sbin/in.comsat in.comsat
talk dgram udp wait root /usr/sbin/in.talkd in.talkd
ntalk dgram udp wait root /usr/sbin/in.talkd in.talkd
#bootps dgram udp wait root /usr/sbin/in.bootpd in.bootpd
```

### uucp 条目

```bash
uucp stream tcp nowait uucpd /usr/sbin/in.uucpd in.uucpd
```

### Tftp 服务

```bash
#tftp dgram udp wait root /usr/sbin/in.tftpd in.tftpd -/
```

### Finger 服务

```bash
#finger stream tcp nowait nobody /usr/sbin/in.fingered in.
fingerd stream tcp nowait root /usr/bin/ps -ef
#netstat stream tcp nowait root /usr/bin/netstat -fin
```

### Time 服务

```bash
time stream tcp nowait root internal
time dgram udp wait root internal
# Echo, discard, daytime, and change 主要用于测试。
echo stream tcp nowait root internal
echo dgram udp wait root internal
discard stream tcp nowait root internal
discard dgram udp wait root internal
daytime stream tcp nowait root internal
daytime dgram udp wait root internal
charger stream tcp nowait root internal
charger dgram udp wait root internal
```

### Rpc 服务语法

```
# <prog>/vers <socket_type> rpc/<proto> <flags> <user> <pathname> <args>
```

```bash
#mountd/1 dgram rpc/udp wait root /usr/lib/nfs/mountd mount
```

```bash
# Yupdated 由支持 Y 更新的站点运行。
ypupdated/1 stream rpc/tcp wait root /usr/lib/netsvc/yp/ypupdated
```

```bash
# rusers 服务提供用户信息。关注安全性的站点可能会选择禁用它。
#usersd/1-2 dgram rpc/udp wait root /usr/lib/netsvc/users/rpc.usersd rpc.usersd
```

```bash
# spray 服务器主要用于测试。
sprayd/1 dgram rpc/udp wait root /usr/lib/netsvc/spray/rpc.sprayd rpc.sprayd
```

```bash
# rwall 服务器允许网络上的任何人骚扰你机器上的每一个人。
walld/1 dgram rpc/udp wait root /usr/lib/netsvc/rwall/rpc.rwalld rpc.rwalld
```

### TLI 服务语法

```
# <service_name> tli <proto> <flags> <user> <server_pathname> <args>
```

### TCPMUX 服务语法

```
# cmux/<service_name> stream tcp <flags> <user> <server_pathname> <args>
```

```bash
smtp stream tcp nowait root /usr/lib/mail/cmux/in.smtpd
```

列表中的第二行描绘了文件的语法。为了方便，此处重复了语法：

```bash
# <service_name> <socket_type> <proto> <flags> <user> <server_pathname> <args>
```

| 字段 | 描述 |
| :--- | :--- |
| service_name | 这是 `/etc/services` 中列出的服务的标识。例如，文件中的第一个条目匹配 `/etc/services`。 |
| socket_type | 识别数据类型。有三种类型：1) stream 是 TCP 交付的面向字节的服务；2) dgram 是 UDP 交付的事务型服务；3) 直接运行在 IP 上。 |
| Proto | 识别传输协议名称，通常为 udp 或 tcp，对应于协议文件。 |
| Flags | 该字段可以设置为 wait 或 noait。如果设置为 wait，则必须等待协议（或服务器）释放套接字。 |
| user | 这是调用服务的用户 (uid)。通常设置为 root，但也可以设置为任何有效用户。 |
| server_pathname | 指定了响应服务的程序完整路径。通过检查 `inetd.conf` 文件，你会注意到路径指定为 internal。这些通常是微小的且非请求的。因此，与其在单独程序中实现它们，它们是作为 inetd 的一部分实现的。 |
| args | 该字段包含了程序支持的命令行参数。从列表可以看出，参数列表必须以名称开头，后面跟着你认为合适的参数。 |

有时你需要修改 `inetd.conf` 文件。你可能想启用一个服务，禁用另一个。根据 `inetd.conf` 中的支持条目，修改服务涉及传递给程序的参数。这允许 root 访问。

## 由 inetd 运行和控制的守护进程

| 守护进程 | 描述 |
| :--- | :--- |
| ftpd | 在某些 UNIX 变体中名为 `in.ftpd`，是文件传输守护进程。负责处理主机的文件请求以及第三方传输和目录查找等功能。 |
| telnet | 在某些 UNIX 变体中名为 `in.telnet`，是远程会守护进程。负责提供用户服务。 |
| rshd | 也名为 `in.rsh`，是 Berkeley 远程 shell rsh 的实现，用于在远程系统上执行命令。 |
| logind | 也名为 `in.login`，是 Berkeley 远程登录能力的实现。 |
| excd | 也名为 `in.excd`，允许在系统上远程执行命令。 |
| comsat | 是邮件通知守护进程。监听传入邮件通知并通知它的进程。 |
| talkd, otalkd | talkd 和 otalkd 分别是 talk 守护的新旧版本。它们允许用户通过网络使用终端的键盘和屏幕。 |
| uucpd | 也名为 `in.uucpd`，负责通过网络传输 UUCP 数据。 |
| ftipd | 也名为 `in.ftpd`，是简单的传输协议（tftp）。主要用于支持磁盘工作站以及路由器和网关网络设备的远程启动设施。 |
| fingered | 它允许使用 finger 命令确定用户的位置。 |
| systat | 在远程系统上执行进程状态。如 `/etc/inetd.conf` 所示，inetd 分派一个命令并将输出返回给远程系统。 |
| netstat | 通过分派 netstat 命令并将输出返回给远程系统，为其提供网络状态信息。 |
| quotad | 这是磁盘服务器守护进程。它返回特定用户的磁盘配额。 |
| admin | 这是分布式系统管理工具服务器守护进程。 |
| usersd | 该守护进程返回主机上的用户列表。 |
| sprayd | 这是一个网络守护进程。向网络发送数据包以测试丢包。 |
| waldd | 这是写入所有守护进程。它向系统上的所有用户发送消息。 |
| rstatd | 该守护进程执行有关此系统的性能统计。 |
| cmsd | 这是日历管理器守护进程。 |

除了守护进程外，`inetd` 还提供以下服务：

| 服务 | 描述 |
| :--- | :--- |
| echo | 此服务支持 UDP 和 TCP。它返回发送的所有内容；因此通过比较入站流量允许环诊断。 |
| discard | 此服务简单地丢弃发送内容。 |
| daytime | 此服务返回格式为 `Day Mon dd hh:mm:ss yyyy` 的时间。 |
| charger | 这是字符生成服务，通过 UDP 和 TCP 提供。它返回 ASCII 字符集中可打印子集的副本。charge 用于执行网络诊断。 |

## 其他守护进程

| 守护进程 | 描述 |
| :--- | :--- |
| routed | 这是本章之前讨论的路由信息协议 (RIP) 的实现。 |
| gated | 该守护进程嵌入了多种路由信息协议，包括 RIP。最短路径优先算法 (OSPF)、外部网关协议 (EGP)、边界网关协议 (BGP) 和 HELLO。这些协议的讨论超出了本书的范围。SAMS 出版的《Networking》，ISBN 0-672-30584-4 对这些协议进行了深入讨论。 |
| nfsd | 这是网络文件系统 (NFS) 守护进程。运行在文件服务器上，处理客户端请求（见 NFS 部分）。 |
| biod | 这是块输入/输出守护进程。它运行在 NFS 客户端上，负责在客户端进程头部从 NFS 服务器读取和写入数据（见 NFS 部分）。 |

此守护进程运行在 NFS 服务器上，负责响应客户端 NFS 挂载请求（详情请参见 NFS 章节）。

该守护进程由客户端和服务器运行，用于处理文件锁。在客户端侧，守护进程发出这些请求；服务器的锁遵循这些请求并管理锁（详情请参见 NFS 章节）。

stat 由客户端和服务器运行，用于维护受强制执行的文件锁状态（详情请参见 NFS 章节）。

`rpcbind` 将自己绑定到 `inetd`。后者负责监听常用 TCP/IP 守护进程的网络服务请求（在 ftp 和 telnet 等许多服务中，后者负责监听作为远程过程调用（Remote Procedure Calls）的 NFS 请求），并将它们提交给相应的守护进程（如 nsfd、lockd 和 statd）。`rpcbind` 的控制是由进程启动的，这与由 `inetd` 启动并按需运行的 inet-受控 守护进程不同。

`sendmail` 依赖简单邮件传输协议（SMTP，另一种由 RFC 821 规范的 TCP/IP 协议）在网络上交换电子邮件。`sendmail` 依赖于通常所说的邮件传输代理（MTA）来提供服务。`sendmail` 是一个处理 SMTP 连接和处理电子邮件的 SMTP 代理。配置 `sendmail` 是一项复杂的任务，超出了本章的范围。

## ifconfig
