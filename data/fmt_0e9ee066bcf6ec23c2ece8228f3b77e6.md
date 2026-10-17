
```
root@RHEL:~# cat /etc/sysconfig/iptables
# Firewall configuration written by system-config-level
# Manual customization of this file is not recommended.
#filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-RH-Firewall-1 [0:0]
-A INPUT - RH-FIREWALL-1-INPUT
-A FORWARD - RH-FIREWALL-1-INPUT
-A RH-Firewall-1-INPUT -i lo -j ACCEPT
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
-A RH-Firewall-1-INPUT -p 50 -j ACCEPT
-A RH-Firewall-1-INPUT -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A RH-Firewall-1-INPUT -m state -m NEW -p tcp --dport 22 -j ACCEPT
-A RH-...NINPUT -m state -m NEW -p tcp --dport 80 -j ACCEPT
-A RH-...NINPUT -m state -m NEW -p tcp --dport 21 -j ACCEPT
-A RH-...NINPUT -m state -m NEW -p tcp --dport 25 -j ACCEPT
-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited
COMMIT
root@RHEL:~#
```

启动服务，执行服务的启动命令。你可以通过 `chconfigfig` 配置 `iptables` 在启动机时启动。

```
root@RHEL:~# service iptables start
Applying iptables firewall rules: [ OK ]
root@RHEL:~# chconfigfig iptables
root@RHEL:~#
```

`iptables` 的一个非常实用的特性是，当使用 `service iptables status` 命令进行查询时，它会显示详细的状态信息。

```
root@RHEL4:~# service iptables status
Table: filter
Chain INPUT (policy ACCEPT)
target prot opt source destination
RH-Firewall-1-INPUT all 0.0.0.0/0 0.0.0.0/0
Chain FORWARD (policy ACCEPT)
target prot opt source destination
RH-Firewall-1-INPUT all 0.0.0.0/0 0.0.0.0/0
Chain OUTPUT (policy ACCEPT)
target prot opt source destination
Chain RH-Firewall-1-INPUT (2 references)
target prot opt source destination
ACCEPT all 0.0.0.0/0 0.0.0.0/0
ACCEPT icmp 0.0.0.0/0 0.0.0.0/0 icmp type 255
ACCEPT esp 0.0.0.0/0 0.0.0.0/0
ACCEPT ah 0.0.0.0/0 0.0.0.0/0
ACCEPT udp 0.0.0.0/0 224.0.0.251 udp dpt:5353
ACCEPT udp 0.0.0.0/0 0.0.0.0/0 udp dpt:631
ACCEPT all 0.0.0.0/0 0.0.0.0/0 state RELATED, ESTABLISHED
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:21
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:25
REJECT all 0.0.0.0/0 0.0.0.0/0 reject-with icmp-host-prohibited
```

`root@RHEL4:~#`

精通防火墙配置需要对 `tcp/ip` 有深入了解。可以在这里找到良好的 `iptables` 教程：http://iptables-tutorial.frozentux.net/iptables-tutorial.html 以及这里 http://tldp.org/HOWTO/IP-Masquerade-HOWTO/

## 27.2. 练习：`iptables`

1. 验证防火墙是否正在运行。

2. 停止运行中的防火墙。

## 27.3. 答案：`iptables`

1. 验证防火墙是否正在运行。

```
root@hel55 ~# service iptables status | head
Table: filter
Chain INPUT (policy ACCEPT)
num target prot opt source destination
1 RH-Firewall-1-INPUT all -- 0.0.0.0/0 0.0.0.0/0
Chain FORWARD (policy ACCEPT)
num target prot opt source destination
1 RH-Firewall-1-INPUT all -- 0.0.0.0/0 0.0.0.0/0
Chain OUTPUT (policy ACCEPT)
```

2. 停止运行中的防火墙。

```
root@hel55 ~# service iptables stop
Flushing firewall rules: [ OK ]
Setting chains to policy ACCEPT: filter [ OK ]
Unloading iptables modules: [ OK ]
root@hel55 ~# service iptables status
Firewall is stopped.
```

## 27.4. `xinetd` `inetd`

### 27.4.1. 超守护进程 (superdaemon)

在内存有限的时代，设计出了一种超级服务器（super-server）来监听所有套接，并在需要时启动相应的守护进程。能够、`telnet` 和 `ftp` 等服务通常由这种超级服务器提供。`xinetd` 超守护进程比 `inetd` 更新。我们将讨论这两个守护进程的配置。

现代 Linux 发行版如 `RHEL5` 和 `Ubuntu 10.04` 默认不会激活 `inetd` 或 `xinetd`，除非应用程序需要。

### 27.4.2. `inetd` 或 `xinetd`

首先验证你的计算机是否正在运行 `inetd` 或 `xinetd`。`Debian 4.0 Etch` 正在运行 `inetd`。

```
root@barry#:# ps fax | grep inetd
3870 ?      Ss     0:00 /usr/sbin/inetd
```

这台 `Red Hat Enterprise Linux 4` 正在运行 `xinetd`。

```
root@RHEL4b ~)# ps fax | grep inetd
3003 ?      0:00 xinetd-stayalive -pidfile /var/run/xinetd.pid
```

这两个守护进程具有相同的功能（监听许多端口，在需要时启动守护进程），但它们有不同的配置文件。

### 27.4.3. `xinetd` 超守护进程

`xinetd` 守护进程通常被称为超守护进程，因为它监听许多入站连接并在需要时启动其他守护进程。当接收到连接时，`xinetd` 会首先检查 `TCP wrappers`（`/etc/hosts.allow` 和 `/etc/hosts.deny`），然后将配置交给另一个守护进程。这个超守护进程通过 `/etc/xinetd.conf` 以及 `/etc/xinetd.d` 目录下的文件进行配置。
