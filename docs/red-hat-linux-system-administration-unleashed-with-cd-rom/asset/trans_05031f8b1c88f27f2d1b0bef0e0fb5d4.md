
## 开启 IP 转发

新内核安装就位且系统恢复运行后，您需要开启 IP 转发。尽管在内核配置中已选中，默认情况下它是关闭的。要开启数据包转发，请编辑文件 /etc/sysconfig/network 并将参数 FORWARD_IPV4 从 false 改为 true。这样每次重启系统时都会开启 IP 转发。

接下来，需要部署防火墙规则。过滤器需要在系统启动时适当的时机进行定义。启动防火墙的最佳时机是在使用 ifconfig 配置网络设备之前。在 Red Hat Linux 下，接口是在 /etc/rc.d/init.d/network 脚本中配置的。该脚本通常是运行级别 2、3 和 5 中最早执行的脚本之一。在这些运行级别目录中，/etc/rc.d/init.d/network shell 程序的符号链接是 S10network。在接口配置之前设置数据包过滤规则的一种可能方法是创建类似 /etc/rc.d/init.d/firewalls 的 shell 脚本。然后使用以下命令在运行级别目录中创建链接：

```
# for i in rc2.d,rc3.d,rc5.d ; do
# cd /etc/rc.d/$i
# ln -s ../init.d/firewalls S5firewalls
# cd ..
# done
```

这个小 shell 循环切换到 rc2.d、rc3.d 和 rc5.d 每个运行级别目录，并在 /etc/rc.d/init.d/ 中创建指向防火墙 shell 程序的链接，该链接将在网络启动前运行。这防止了网络接口处于活动状态但未受防火墙控制的时间窗口。

shell 程序 /etc/rc.d/init.d/firewalls 是一个简单的 Bourne shell 程序，显示在列表 26.2 中。该脚本假设以下网络拓扑：

防火墙主机: fw1.fwcorp.com
接口: eth0(内部), eth1(外部)
伪装: 否
eth0: 128.83.137.35
eth1: 128.83.155.44

### 列表 26.2 防火墙启动脚本

```
#!/bin/bash
#
# S5firewall - a simple firewall script to setup a packet filter using ipwadm
#
#
```

### 列表 26.2 继续

```
PATH=/sbin:/usr/sbin:/bin:/usr/bin
export PATH

# flush the current rules:
ipfwadm -I -f
ipfwadm -O -f
ipfwadm -F -f
ipfwadm -A -f
# deny everything first, that way we won't have to worry about some crazed
# hacker trying to get into the system before we get a login prompt.
ipfwadm -I -p deny
ipfwadm -O -p deny
ipfwadm -F -p deny

ipfwadm -F -a deny -o -P tcp -S 0.0.0.0/0 -D 128.83.137.0/24
ipfwadm -F -a deny -o -P udp -S 0.0.0.0/0 -D 128.83.137.0/24

# now, allow all traffic within the local network
ipfwadm -F -a accept -P tcp -S 128.83.137.0/24 -D 0.0.0.0/0

# deny all ICMP packets coming in except for type 3, type 8 and type 11
# These rules are tricky. The idea here is we don't want to
# allow all ICMP traffic into the network. However, we do want to
# allow some traffic for possible debugging of firewall rules. The way
# we want it set up is as follows
# 1. Deny ICMP packets by default
# 2. Allow ICMP type 3 (destination-unreachable), type 8 (echo-reply),
# and type 11 (used by traceroute) to come in from the outside
# 3. Deny type 8 (echo-reply) from within our own network -- no responses to
# any pings (not really necessary, but for extra insurance).
ipfwadm -I -a deny -P ICMP -S 0.0.0.0/0
ipfwadm -I -a accept -P ICMP -S 0.0.0.0/0 3
ipfwadm -I -a accept -P ICMP -S 0.0.0.0/0 8
ipfwadm -O -a deny -P ICMP -S 128.83.137.0/24 8

# allow SMTP, ftp, ftp-data, Secure Shell, DNS and WWW
ipfwadm -F -a deny -o -S 127.0.0.1/8 -D 128.83.137.0/24
ipfwadm -F -a reject -o -P tcp -S 0.0.0.0/0 -D 128.83.137.0/24 113
ipfwadm -F -a accept -P tcp -S 0.0.0.0/0 -D 128.83.137.0/24 20 21 22 25 53 80
ipfwadm -F -a accept -P udp -S 0.0.0.0/0 -D 128.83.137.19 53
```

在继续之前，让我们更仔细地查看上面的规则。我们首先执行的是刷新（-f）记账（-A）、转发（-F）、输入（-I）和输出（-O）规则。这提供了一个干净的基础来构建防火墙。一旦您设置了拒绝所有数据包转发的防火墙，您就可以开始允许您想要的服务。

接下来的四个命令将所有规则的默认策略设置为拒绝。这防止传入的数据包被转发到其最终目的地。“deny” 策略特别不向源提供返回响应代码。因此，对于连接的另一端，看起来发送到目的地的包就这样消失了。如果该策略是 “reject”，则会向源返回响应代码，另一端的用户将收到 “连接被拒绝” 类型的消息。

接下来的两个命令设置规则以允许来自内部网络 (128.83.137.*) 的所有流量。以下一系列规则用于控制网络中的 ICMP 流量。具体来说，被过滤掉的 ICMP 数据包类型是类型 8 数据包，也称为 ICMP “echo-request”。这是 ping 程序发送的数据包类型。过滤掉该数据包是可取的，因为 “ping of death” 攻击，即一种拒绝服务攻击，使用这种类型的数据包来实现其目标。另一个需要过滤的数据包类型是 “echo-reply” 或类型 0 ICMP 数据包。这是对类型 8 数据包的响应。该数据包被过滤以防止对类型 8 数据包的任何可能响应。当防火墙外部的某人 ping 防火墙内部的机器时，不会收到响应。就好像该机器不存在一样。过滤掉所有 ICMP 数据包类型是不理想的，因为这也会阻止诊断路由问题的能力。

下一系列防火墙规则设置了防火墙机器将允许的服务。这些服务包括 ftp (20)、ftp-data (21)、secure shell (22)、smtp (25)、DNS (53) 和 www (80)。

## 转发连接

要将网络内部的连接转发到网络的其余部分，ipfwadm 命令有一个简单的格式：

```
ipfwadm -F -a accept -b P <protocol> -S <source addr> -D <destination addr>
```

需要两条规则进行记账而转发只需要一条规则的原因是，转发规则中使用的 -b 标志不是记账规则的有效参数。就这么简单。一件必须谨慎处理的事情是 ICMP 协议。通过拒绝该协议，您将永远无法确定防火墙是否存在问题。这是 ipfwadm 的弱点之一：无法区分一种 ICMP 数据包和另一种 ICMP 数据包。为了解决这个问题以及其他问题，ipchains 是为 2.1.102 之后的内核版本编写的。

## 使用 ipchains 设置防火墙

当内核 2.1.102 发布时，关注开发内核的人发现他们的当前数据包过滤器突然不再工作。目标是通过使设置和控制防火墙变得更容易、更合乎逻辑来改进 Linux 数据包过滤代码。ipchains 对新手来说并不直观，且流量控制是单向的。对新手来说，设置防火墙是一个容易出错的过程，调试防火墙变得困难且耗时；因此，重新编写了数据包过滤代码及其配套的操纵工具。随着新操纵工具 ipchains 的发布，设置防火墙变得更容易了。

ipchains 可以通过 FTP 从 Red Hat 网站下载。RPM 位于目录 ftp://ftp.redhat.com/pub/current/1386/RedHat/RPMS/ipchains-1.3.9-3.1386.rpm。

## 安装 ipchains

要安装 ipchains，请以 root 身份登录并输入以下命令：

```
# rpm -ivh ipchains-1.3.8-3.1386.rpm
ipchains
########################################
#
```

这将在 /usr/sbin 中安装主要实用程序，并在 /usr/doc 中安装文档，并在 /usr/man 中安装手册页。像往常一样，请务必阅读手册页和随软件提供的任何文档。此外，请确保数据包过滤代码已编译到您的内核中。如果对内核配置过程中需要选择的内容有任何疑问，请参阅本章前面的 “Linux Kernel Configuration” 部分。ipchains 软件主要适用于 2.1.102 及更高版本的内核。然而，有补丁可以使其与更早的内核版本一起工作。让 ipchains 在 2.1.102 之前的内核版本上工作是一项非平凡的任务，不建议新手尝试。如果可能，请使用 2.2 系列的内核。

Linux 2.2.X 内核中的数据包过滤规则现在分为四类：

- IP 输入链
- IP 输出链
- IP 转发链
- 用户定义链
