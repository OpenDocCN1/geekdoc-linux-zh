
现在让我们输入用于允许发送邮件的 SMTP 规则。这些规则显示在**示例 16-35** 中。请注意，SMTP 仅使用 TCP。

## 示例 16-35 允许 SMTP 发送邮件的规则

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d mail smtp -j ACCEPT
[root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d mail smtp -j ACCEPT
[root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s mail smtp -j ACCEPT ! -y
[root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s mail smtp -j ACCEPT
```

**Web 访问规则。** 类似地，我们允许访问万维网（WWW）。Web 访问的端口号是 80，其名称为`www`。这些规则与之前的规则类似，并显示在**示例 16-36** 中。请注意，在此示例中，我们仅允许访问 80 端口。许多 Web 服务器会使用其他端口号。如果你希望允许特定的端口号（例如 8080 和 8008），你需要添加类似**示例 16-36** 中所示的规则来实现这一目的。如果你希望允许任何端口号用于 Web 访问，你可以复制**示例 16-36** 中显示的规则，并将其中的`www`替换为`1024:65535`。这种方法允许所有内部发起的 TCP 流量通过防火墙。请确保你的安全策略允许这样做。为了完整性，我们在**示例 16-37** 中展示了这种宽松的规则，但请注意，这些规则并不支持我们在示例描述中指定的要求（参见第 469 页的*简单内部网络*及其后续小节）。

使用**示例 16-37** 中概述的规则虽然使规则集更简单，但也意味着实现了一种限制性较少的配置。这些规则未在第 481 页的后续**示例 16-41** 中使用。

## 示例 16-36 允许 Web 访问的规则

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d 0/0 www -j ACCEPT
[root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d 0/0 www -j ACCEPT
[root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s 0/0 www -j ACCEPT ! -y
[root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s 0/0 www -j ACCEPT
```

## 示例 16-37 允许所有使用非特权端口的内部发起流量的规则

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d 0/0 1024:65535 -j ACCEPT
[root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d 0/0 1024:65535 -j ACCEPT
[root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s 0/0 1024:65535 -j ACCEPT
[root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s 0/0 1024:65535 -j ACCEPT
```

这完成了第 469 页*简单内部网络*开头部分指定的必需服务的规则。需要注意的是，这些规则允许我们的任何内部主机以及 topcat 本身访问指定的服务。

**允许内部 SSH** 为了符合本例设定的要求（参见第 469 页*简单内部网络*开头部分），我们需要做的最后一件事是允许来自内部网络的 SSH 连接到 topcat-in。SSH 的端口号是 22，其名称是 ssh。由于我们不需要允许 SSH 连接通过我们的防火墙，因此这比其他端口组更容易。必要的规则在示例 16-38 中给出。

## 示例 16-38 允许从内部网络到 topcat-in 的 SSH 规则

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 1023:65535 -D topcat-in ssh -j ACCEPT
[root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 1023:65535 -S topcat-in ssh -j ACCEPT
```

> **注意**
> 如果我们还希望允许 topcat-in 通过 SSH 连接到内部网络，我们可以通过在示例 16-38 的每条规则中添加 -b（双向）来实现这一点。

**最后！** 我们差不多完成了！还有几个步骤。首先，让我们拒绝所有我们未明确允许的内容，并记录此类活动。这将使我们的日志文件迅速增长，因此我们需要按照第 466 页*规则编写和日志记录技巧*中所述进行管理。这些是捕获所有（catchall）规则。我们将它们附加到每个链的末尾，如示例 16-39 所示。

## 示例 16-39 捕获所有 REJECT 规则

```
[root@topcat]# ipchains -A input -1 -j REJECT
[root@topcat]# ipchains -A output -1 -j REJECT
[root@topcat]# ipchains -A forward -1 -j REJECT
```

现在让我们移除我们在修改链之前输入的初始阻塞规则（参见第 471 页的*初始步骤*和*默认策略*）。执行示例 16-40 中给出的命令即可完成此操作。

## 示例 16-40 移除阻塞规则

```
[root@topcat]# ipchains -D input 1
[root@topcat]# ipchains -D output 1
[root@topcat]# ipchains -D forward 1
```

我们现在已经实现了防火墙，以满足第 469 页*简单内部网络*开头部分设定的要求。此时，你希望保存你的配置，使用 ipchains-save，并且/或者编写一个脚本以在每次重启时恢复此规则库（参见第 467 页的*ipchains 启动脚本*）。在下一节中，我们将查看一组包含本例中讨论的所有内容的启动脚本示例。

## 使用 DHCP 的简单内部网络

“但是，”你会说，“我使用 PPP！我该如何在 PPP 上做到这一点？”或者也许你使用 DSL、电缆调制解调器，或任何其他需要动态主机配置协议（DHCP）的机制。没问题。

让我们假设我们的示例与第 469 页*简单内部网络*中给出的示例相同。该示例与使用具有动态寻址的 DHCP 或 PPP 之间的主要区别在于我们获取外部接口 IP 地址的方式。

### 注意

> 如果你不熟悉 PPP 和/或 DHCP 的基本配置，请查看第 487 页*ISP 连接相关资源*中引用的资源。

示例 16-41 中的脚本整合了我们在第 469 页*简单内部网络*中实现的所有规则。它使用 shell 环境变量使脚本更适用于许多情况。它还添加了允许 DHCP 工作所需的规则，并获取动态分配的 IP 地址。脚本已添加注释，但为了简化，DHCP（PPP、DSL、电缆调制解调器等）的额外条目以**粗体**显示。如果你使用的是 DHCP，你不一定使用所有**粗体**条目，因为其中一些仅适用于 PPP。因此，请适当地使用这些条目。

使用此脚本或类似的脚本作为启动脚本，以便在开机时启动防火墙。有关设置启动脚本的详细信息，请参见第 467 页的*ipchains 启动脚本*。

## 示例 16-41 防火墙启动脚本

```
#!/bin/bash

# Begin with setting some environment variables—first PATH
PATH=/sbin:/usr/sbin:/bin:/usr/bin;export PATH
# External Interface—uncomment the one you use or set appropriately
EXIF="eth0"
# EXIF="ppp0"

# Internal Interface—set appropriately
INIF="eth1"
# DMZ Interface—set appropriately
DMZIP="eth2"

# If you are using static IP addresses, set it below
EXIP="202.7.1.19"    # loopca
# If you use DHCP, you’ll need to fetch the address
# Uncomment the next line if you use DHCP, such as DSL, PPP, etc.
# EXIP=`/sbin/ifconfig $grep -A 2 $EXIF|awk '/inet/ { print $2 }'`
# `sed -e s/addr://`
```

## 示例 16-41 防火墙启动脚本（续）

```
#
# DHCP addresses are "leased" for a period of time after which
# the address may change, so make sure that this script is
# re-run each time the IP address changes.  See DHCP documentation
#
# Now set the external broadcast address.
# This script only uses the broadcast for DHCP.
#EXXCAST="202.7.1.31"
#
# To get the broadcast address for DHCP uncomment the next line
# EXXCAST=`ifconfig|egrep -A 2 \$EXTIF|awk '/inet/ { print $4 }'\
#   |sed -e s/Bcast\///`
# Now set your internal IP address
INIP="10.1.1.1"       # tocat-ip
# Now set the network variables
INNET="10.0.0.0/8"
# DMZNET="202.7.1.24/30"      # Uncomment this if used
#End of variable section
# Let's be paranoid and enter blocking rules to start
# We'll disable them at the end.  Also we'll allow lo here and
# set up the REJECT policy.
ipchains -F
ipchains -I input 1 -j REJECT
ipchains -I output 1 -j REJECT
ipchains -I forward 1 -j REJECT
ipchains -A input -i lo -s 0/0 -d 0/0 -j ACCEPT
ipchains -A output -i lo -s 0/0 -d 0/0 -j ACCEPT
ipchains -P input REJECT
ipchains -P output REJECT
ipchains -P forward REJECT
#
# initial masquerading requirements
depmod -a
modprobe ip_masq_ftp
echo "1" > /proc/sys/net/ipv4/ip_forward
ipchains -M -S 3600 10 50
# end initial masquerading requirements
# DHCP support requires this...uncomment if necessary
echo "1" > /proc/sys/net/ipv4/ip_dynaddr
# anti-spoofing
for file in /proc/sys/net/ipv4/conf/*/rp_filter
  do
    echo "1" > $file
done
ipchains -A input -i 1 lo -s 127.0.0.0/8 -j REJECT -1
# end anti-spoof
# Internet input rejects
ipchains -A input -i $EXIF -p tcp -d $INNET -j REJECT -1
ipchains -A input -i $EXIF -p tcp -d $EXIP -j REJECT
# end input rejects
# ICMP Custom Chain-catch important ICMP messages
# our catch-all reject rule will drop the rest.
# First create the chain...no problem if it already exists.
# Real problems if it doesn't.
ipchains -N icmperr 2>/dev/null
# Now add the rules
ipchains -A icmperr -p icmp --icmp-type destination-unreachable -j ACCEPT
ipchains -A icmperr -p icmp --icmp-type parameter-problem -j ACCEPT
ipchains -A icmperr -p icmp --icmp-type source-quench -j ACCEPT
```

