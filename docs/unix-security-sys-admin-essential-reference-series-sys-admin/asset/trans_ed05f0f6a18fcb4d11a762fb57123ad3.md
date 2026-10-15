

## 图 11.1 筛选路由器位于外部网络（互联网）和内部网络（Macintosh）之间。

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_118_0.png)

## 图 11.2 一个 PPP 过滤器配置示例说明了了解路由器上将出现哪些内容的必要性。

```
$ cat Filter
#
#/etc/ppp/filter - PPP configuration file binding packet type to actions.
#

internet system:
    bringup intp 13/icmp 15/icmp 111/icmp !who !route !ntp
    pass nntp/137.39.1.2 !nntp
    !telnet/syn/recv
    ftp/syn/recv !login/syn/recv !shell/syn/recv !who
    !sunrpc !chargen !ftp !supdup/syn/recv !exec !syslog
    !route 16000/tcp/syn/send
    keepup !send intp 13/icmp 15/icmp 111/icmp !who !route
    log
    rejected

default bringup intp 13/icmp 15/icmp 111/icmp !who !route
    keepup !send intp 13/icmp 15/icmp 111/icmp !who !route
$
```

更糟糕的是，大多数商业路由器没有日志记录功能，这使得几乎不可能检测到防火墙的问题。筛选路由器绝非最安全的解决方案，但它们却是最流行的解决方案之一，因为它们为内部用户提供了几乎不受限制的互联网访问权限。如果私有网络中的主机上存有商业机密或敏感信息，筛选路由器将无法提供所需的安全级别。

## 堡垒主机

堡垒是防御性的据点。电子堡垒是网络安全中的坚强据点。通常，堡垒主机具有高度的安全性，会定期接受系统和安全审计，并且可能装有修改过的软件。堡垒主机通常位于与筛选路由器类似的位置（图 11.3）。

堡垒主机为每个网络提供一种配置，并允许每个网络的流量通过。由于其暴露性，堡垒主机经常成为破坏者攻击的目标。尽管如此，堡垒主机仍经常用于其他防火墙配置中，以提供所需的保护。

## 双宿主网关

双宿主网关是一种无需筛选路由器即可实现的防火墙；它可能是提供防火墙的最常用方法。双宿主网关基本上由一个不允许在互联网和私有网络之间进行 IP 转发的堡垒主机系统组成（图 11.4）。

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_119_0.png)

在双宿主网关下，访问内部网络的唯一方式是与堡垒主机协商连接，然后与内部主机发起连接。另一种看待这个问题的方式是，内部网络上的主机可以与网关通信，互联网上的主机也可以，但两个网络之间的直接流量被阻断。从互联网来看，双宿主网关就像私有网络中的所有机器；从私有网络来看，它又像互联网中的所有机器。双宿主网关实际上充当服务网关，为电子邮件和其他服务提供支持：从定义上讲，它就是一台堡垒主机。

这是一种流行的防火墙配置，因为它相当容易设置，并且提供了互联网与私有网络之间的完全阻断。用户友好程度取决于系统管理员如何设置网络之间的访问。像 SMTP 这样的服务必须将邮件投递到网关，然后由网关将消息转发到目标机器。其他服务，如 telnet 和 rlogin，必须在网关上配置用户登录的账户，或者提供应用层中继将数据包重定向到相应的主机。

## 图 11.4 双宿主网关本质上是一台堡垒主机，不允许外部和内部网络之间进行 IP 转发。

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_120_0.png)

## 图 11.5 当用户以用户名 telnet 登录网关时执行的示例登录配置文件。

```
:
# @( #) profile 23.3 91/10/24
#
trap '' 1 2 3 15

PATH=/bin:/usr/bin
#
# This code was added to provide a generic interface to allow anyone
# access to this machine without having to do the nasty things of
# automounts and # killing this machine - whose purpose is a gateway
# only anyhow.
#
# trap any user generated signals - force a logout if they occur
#
trap 'echo "SIGNAL REQUEST CAUGHT\nLogin Session ABORTED!";exit 0' 1 2 3 15
# send out a prompt
#
echo "
Welcome to the Network Access Gate
Connected at : `date`
Connected to : `hostname`
"
#
# set _NAME to nothing, and loop until weget a value this is the name of
# the user which we will use to establish an rlogin session
#
_NAME=
while [ ! $_NAME ]
do
    echo "Please enter your REAL login name : \c"
    read _NAME
done
```

