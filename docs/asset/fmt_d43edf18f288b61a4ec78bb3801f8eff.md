
```
cp /mnt/cdrom/book/arpwatch.bob.tar.gz
zcat arpwatch.bob.tar.gz | tar -xovf-
cd arpwatch-bob
./configure
make
make install
make install-man
man arpwatch
man arpsnp
```

接下来，向 `/etc/rc.d/rc.local` 文件中添加类似下方的命令，以便其在重启动时自动启动：

```
# "-0" 增强：用于抑制 Apple 0.0.0.0 的无效信息
# "-m foo" 增强：将邮件发送到指定地址而非 root
# "-w from" 增强：指定地址（包括哪个办公室）
# "-u MAC" 增强：指定我们上游路由器的 MAC 地址
# 避免 bogon 检测中的产生误报
echo "Starting arpwatch on each Ethernet interface"
ARPWATCH=/usr/local/sbin/arpwatch
ARPARGS="-0 -m sasdmin@pentacorp.com"
# 指定上游路由器的 MAC 地址，如果有
ARPUPS="-u 00:07:4C:92:68"
killall arpwatch
$ARPWATCH -f /var/log/eth0 -i eth0 -w "arpwatch (NYC:eth0)" \
  $ARPARGS $ARPUPS
$ARPWATCH -f /var/log/eth1 -i eth1 -w "arpwatch (NYC:eth1)" \
  $ARPARGS $ARPUPS
$ARPWATCH -f /var/log/eth2 -i eth2 -w "arpwatch (NYC:eth2)" \
  $ARPARGS
```

最后，初始化其可读数据库并首次启动：

```
cd /var/log
touch eth0 eth1 eth2
chmod 600 eth0 eth1 eth2
/etc/rc.d/rc.local
```

此防火墙在 `eth2` 上有一个内部网络和一个 DMZ。`-w` 参数的参数将显示为“来自”地址。我们通过此指示是我们的哪个办公室的防火墙生成的消息，以及数据包源自哪个网卡。每个运行的 Arpwatch 都会构建 IP 地址-MAC 地址对的内存数据库，并每 15 分钟备份到磁盘（`/var/log/eth?`）。如果你的上游路由器通过以太网连接到此系统，应使用 `-u` 参数指定其 MAC 地址以便进行智能检测。

通常，Arpwatch 会派生到后台运行。当发生值得事件时，它使用 Syslog 生成日志项并发送电子邮件。一个常见的“坑”是将数据库文件创建为零字节。如果 Arpwatch 启动时该文件不存在，它将通过 Syslog 和其本身生成日志项。对于普通观察者来说，这种行为与正确启动没有区别。

```
最初配置 Arpwatch 时，执行 `ps -axlw grep arp` 查看它是否保持运行。此外，请记住它会向数据库文件写入新条目（每隔 15 分钟可以使用 more 查看），或者在调用中断、kill 或 HANGUP 信号并带有调试模式 (`-d`) 时，它将在前台运行并将消息写入标准错误，生成日志消息和电子邮件。如果你在大型网络上首次启动它，可能希望带有调试模式运行它，直到它建立起运行系统的数据库为止。
```

当看到新的 IP 地址时，它将生成一封邮件说明这是一个新站点。邮件包含 IP 地址、主机名、以太网卡供应商和时间戳。产生伪造（bogus）的机器要么配置不当，要么是你网络上的黑客。所有这些消息值得调查，尽管 DHCP 配置会导致误报。

当数据包通过路由器来自互联网来时，数据包的源 IP 地址将是互联网上系统的地址，但将具有路由器的 MAC 地址。将其与伪造区分开来的唯一方法是，如果 MAC 地址与 `-u` 参数指定的路由器 MAC 匹配，则抑制警告。如果一个网络有直接连接的路由器，可以多次使用 `-u` 参数。如果你的上游路由器通过以太网连接（例如，如果防火墙使用内部 T1 卡进行路由），则不应使用 `-u`。Arpwatch 还识别出它运行的系统可能是路由器，因此任何 MAC 地址与其任一个接口匹配的数据包都是被路由的。

当黑客接管一个系统并计划使用一段时间来更改其 IP 地址以制造麻烦时，这样做并不是为了让你更难追踪他。不过，大多数人并不会更改以太网地址。如果你跟踪哪个系统拥有哪个 MAC 地址，这些问题系统很容易追踪。如果黑客更改了网卡的 MAC 地址，Arpwatch 将通知你网络上接入了一台新机器（或现有机器更改了其 MAC 地址）。你就可以调查该案件。一个典型的新站点邮件看起来如下：

```
From: arpwatch@redshift (ATL:eth1)
To: bob@redshift
Subject: new station (redshift)
hostname: redshift (eth1)
ip address: 10.0.2
ethernet address: 00:87:72:23:7F:AA
ethernet vendor: INTEL
timestamp: Tuesday, June 11, 0:52
```

如果你使用 DHCP，可以通过为用户建立静态 IP 地址并将它们放入 DNS 数据库或至少放入防火墙的 `/etc/hosts` 文件中来让自己的生活更轻松。如果你的防火墙是 Linux 或 UNIX 系统，那么 Arpwatch 应该在上面运行。以下是 DHCP 服务器配置文件中典型的静态 IP 条目：

```
host warpdevel {
    hardware 00:27:37:24:36:69;
    fixed-address 10.0.19.62;
    option hostname "warpdevel"
}
```

任何伪造系统都会作为新系统或更改了地址的系统出现在网络上。以下是可能发生安全漏洞的极佳且时的警告。以下是一个典型的警报：

```
From: arpwatch@redshirt (ATL:eth1)
To: bob@redshirt
Subject: changed ethernet address (10.0.3)
hostname: redshirt (eth1)
ip address: 10.0.2
ethernet address: 00:56:97:86:39:A7
ethernet vendor: Centauri
old ethernet address: 08:72:23:7F:AA
ethernet vendor: APPLE CORP
timestamp: Tuesday, June 11, 0:14:37
previous timestamp: Tuesday, June 11, 0:24:32
delta: 32 minutes
```

如果你网络上有两个具有相同 IP 地址的系统，你确实有一个问题要处理。一个 IP 地址与其子网不匹配的系统将显示为伪造包（bogus）。以下是典型情况：在这种情况下，某人开启了一个 Windows 系统，但没有费力配置其使用机构的 DHCP 服务器。用户很多的网络会频繁看到这些：

```
From: arpwatch@redshirt (ATL:eth1)
To: bob@redshirt
Subject: bogus new station (169.254.173.57)
hostname: 169.254.173.57 (eth1)
ip address: 169.254.173.57
ethernet address: 00:71:67:23:13:17
ethernet vendor: 3COM
timestamp: Tuesday, June 11, 0:31:48
```

有些 Mac 有一个故障，即它们在启动时在设置 IP 地址之前就开始发送数据包。在这种情况下，IP 地址将是 0.0.0.0。Arpwatch `-0` 标志会导致它在 Syslog 中记录这一点，而不将其视为问题。只有当以太网供应商为 Apple 时，它才会对 0.0.0.0 IP 地址进行这种特殊处理。

当使用 DHCP 的新机器进入网络时，其初始 IP 地址可能保持为 0.0.0.0 足够接收租约。另一种可能发生这种情况的情况是 DHCP 租约过期并在计算机断开时给了另一台机器。当该计算机（通常是笔记本电脑）重新加入网络时，它将呈现新机器的特征，同样足够获取一个新的租约。

## 16.11 端口使用监控

## 16.12 使用 Ethereal 监控攻击
