
``` 
# nano /etc/rndc.conf
# Start of rndc.conf
"rndckey" {
    algorithm hmac-md5;

    # 这应该是我们在第 4 步中生成的密钥
    secret
    "生成的密钥内容";
}

options {
    default-key "rndckey"
    default-server 127.0.0.1;
    default-port 953;
}
```

``` 
# End of rndc.conf

# 在 named.conf 中配合以下内容，根据需要调整允许列表：
# "rndckey"
    algorithm hmac-md5;
    secret "Qmnaadu3sUMGB3DXQ1Gaw==";
};

# controls {
    inet 127.0.0.1 port 953
    allow { 127.0.0.1; } keys { "rndckey"; };
};
```

现在你在 `/etc/rndc.conf` 中的密钥与 `/etc/rndc.key` 文件应该是的。为了完成 `rndc` 的设置，你还需要编辑 `/etc/named.conf` 文件。

### 第 8 步。
在 `/etc/named.conf` 底部插入以下内容：

```
controls {
    inet 127.0.0.1 port 953
    allow { 127.0.0.1; } keys { "rndckey"; };
};
```

`controls` 语句指定了哪些主机或子网允许通过 `rndc` 工具管理 DNS 服务器。最后一行引用密钥文件，因此读取 `/etc/named.conf` 文件的人将看不到密钥。

### 第 9 步。
像 `/etc/named.conf` 文件一样，你为 `rndc` 创建的这两个文件也应该仅由 `named` 用户所有：

`# chown root:named /etc/rndc.*`

### 第 10 步。
你还应该包含它，并将文件更改为 root 用户只读：

`# chmod 400 /etc/rndc.*`

### 第 11 步。
在设置好之后，更改 SELinux 上下文以增强安全性：

`# chcon -t named_conf_t rndc.key rndc.conf`

尽管 `rndc` 已经设置好，但你需要在 953 端口创建一个防火墙规则以便正常运行（并让你的客户端能够连接并管理 DNS 服务器）。

### 第 1 步。
使用 `iptables` 创建额外的规则：

`# iptables -I INPUT 5 -p udp -m udp --dport 953 -j ACCEPT`

### 第 2 步。
保存你创建的防火墙规则：

`# service iptables save`

`Saving firewall rules to /etc/sysconfig/iptables: [ OK ]`

### 第 3 步。
然后重启 iptables 服务：

`# service iptables restart`

`iptables: Flushing firewall rules: [ OK ]

iptables: Setting chains to policy ACCEPT: filter [ OK ]

iptables: Unloading modules: [ OK ]

iptables: Applying firewall rules: [ OK ]`

完成这些后，还有几项收尾工作。

# 红帽考试实战指南：RHCSA™ 和 RHCE® 认证指南与实验手册

### 第 1 步。检查配置文件的语法：

```
# service named configtest
zone localhost/IN: loaded serial 42
zone 0.0.127.in-addr.arpa/IN: loaded serial 2010120710
zone example.com/IN: loaded serial 2010120711
zone 1.168.172.in-addr.arpa/IN: loaded serial 2010120710
```

### 第 2 步。重启 named 服务：

```
# service named restart
Stopping named:      [ OK ]
Starting named:      [ OK ]
```

### 第 3 步。验证 rndc 服务的状态：

```
# rndc status
number of zones: 4
debug level: 0
xfers running: 0
xfers deferred: 0
soa queries in progress: 0
query logging is OFF
recursive clients: 0/1000
tcp clients: 0/1000
server is up and running
```

我们讨论的话题涉及 chroot 环境下的 BIND 服务。这可能是 Linux 提供的最好的功能之一。当你将特定的软件软件包安装在它自己的“容器”中时。这样做的安全益处是，如果系统以后被黑客，攻击者只能访问容器内的这一个服务，而无法访问你系统的其他部分！BIND 是你可以在 chroot 环境中实现的许多优秀服务之一。要实现这一点，你需要做两件事。首先，你需要为 BIND 安装一个特殊的包，以便其在 chroot 环境中运行：

```
# yum install -y bind-chroot
```

其次，你需要编辑 `/etc/sysconfig/named` 目录，并将其更改为你想要托管 BIND 的特定目录（例如 `/var/named/chroot`）。完成此任务后，将你所有的文件和目录复制到 `/var/named/chroot` 目录，就像它是根 `/` 目录一样。你的结构可能如下所示：

```
# tree /var/named/chroot/
/var/named/chroot/
|-- dev
  |-- null
  |-- random
    |-- zero
|.. etc
| .. localtime
| var
| |-- named
|  |-- data
|  |-- slaves
| run .. named
```

特别说明，你唯一不需要放入此目录结构中的内容是 rndc 配置文件和密钥。你实际上可以从真实的 `/etc` 目录为它们创建一个链接：

```
# ln -s /var/named/chroot/rndc.conf /etc/rndc.conf
# ln -s /var/named/chroot/rndc.key /etc/rndc.key
```

## 总结

与 DNS 服务器一起工作从来不是一个简单的话题。如果你以前从未与它们工作过，那么理解 DNS 查询的过程以及让它们正常运行的设置将更加困难。然而，BIND 非常灵活，并且是世界上应用最广泛的实现。

本章详细介绍了四种不同类型的 DNS 服务器以及如何设置它们。我们还查看了与 DNS 服务器有关的安全性以及解决任何出现的问题。DNS 服务器在网络中起着巨大的作用，是现实世界网络基础设施的关键部分之一。确保你理解这些概念以及实现方法，因为你不仅要在红帽考试中处理这些，在现实世界中也是如此。

## 复习题

- 1. 有四种类型的 DNS 服务器。请列出它们。
- 2. A 记录和 PTR 记录之间的区别是什么？
- 3. 从 DNS 服务器不提供额外的益处。对还是错？
- 4. `rndc` 工具是做什么用的？
- 5. 你可以使用什么命令在启动 DNS 服务之前测试配置文件？
- 6. 你可以使用哪三个命令来帮助验证 DNS 服务器运行正常？
- 7. DNS 必须在防火墙上打开哪个端口？
- 8. `rndc-confgen` 命令的作用是什么？
- 9. `rndc` 工具默认监听在哪个端口？

## 复习题答案

- 1. 四种类型的 DNS 服务器是主服务器（master）、从服务器（slave）、仅缓存（caching-only）和转发（forwarding）。
- 2. A 记录将主机名转换为 IP 地址，而 PTR 记录则是相反的。
- 3. 错误。从 DNS 服务器提供了负载均衡和冗余益处。
- 4. `rndc` 工具提供了一种远程且安全管理 DNS 服务器的方法。
- 5. `service named configtest`
- 6. `dig`、`host` 和 `ping` 命令可以用于测试 DNS 服务器的功能。
- 7. DNS 使用端口 53。
- 8. `rndc-confgen` 命令为 `rndc` 工具生成一个 `rndc.conf` 文件。
- 9. 默认情况下，`rndc` 工具监听端口 953。

# 实验 18

## 任务 1 – DNS

- 第 1 步。在任何文本编辑器中打开 GRUB 配置文件。
- 第 2 步。在配置文件添加一个新条目：
  a. 新条目的标题应为 Red Hat Recovery。
  b. 新条目不应是默认项。
  c. 恢复条目应允许你进入恢复模式。
- 第 3 步。将超时时间更改 10 秒。

当系统启动且两个条目都正常工作时，任务完成。

## 任务 2 – 启动问题

- 第 1 步。确保你有红帽安装光盘。你会收到一个系统找不到文件的错误信息。
- 第 2 步。从光盘进入恢复模式。
- 第 3 步。删除 `/etc/inittab` 文件。
- 第 4 步。使用命令 `mount /dev/cd-rom /mnt` 访问光驱。

当系统重启并配置 SELinux 后，任务完成。

本章涵盖了以下主题：

- Xinetd：主服务——本节介绍了 `xinetd` 服务以及它是如何交互的。
- 动态主机配置协议 `DHCP`——本节介绍了 DHCP 服务以及如何分配地址。
- 网络时间协议 `NTP`——本节介绍了 NTP 以及同步时间。

涵盖的 RHCE 目标：

- 安装提供服务的包
- 配置 SELinux 以支持该服务
- 配置服务在系统启动时运行
- 配置服务的各种操作
- 配置基于主机和基于用户的安全性
- 使用其他节点同步时间

# 网络服务

需要时间吗？需要 IP 地址吗？需要 TFTP 服务器吗？这些都是提供的网络服务。本章介绍了红帽提供的各种网络服务，包括 DHCP；NTP 以及 xinetd。这些类型的服务在不同规模的网络中都很常见。每个服务在保持网络运行和为客户端服务方面都起着特定作用。`xinetd`、`DHCP` 和 TFTP 服务器在任何红帽考试指南中都没有明确定义，但它们是现实世界中的重要部分。

# 红帽®考试实战指南：RHCSA™ 和 RHCE® 认证指南与实验手册

主配置文件，单个目录 `/etc/xinetd` 包含了你希望让 `xinetd` 运行的每个服务的独立配置文件。例如，让我们设置一个 TFTP 服务器，它可以用于备份 Cisco 交换机的配置文件，或者在 PXE 启动过程（也称为网络安装）期间向客户端分发数据。我们之前在第 8 章节“网络安装”中查看过 PXE 启动。要开始开始操作，你只需要安装 TFTP 服务器包即可。

### 步骤 3. 安装所需的包：

```
# yum install -y tftp-server
```

### 步骤 4. 验证包是否安装正确：

```
# rpm -qa | grep tftp
tftp-server-0.49-5.1.el6.x86_64
```

现在软件包已经安装，你可以进入 `/etc/xinetd.d` 目录并查看新服务的配置文件。默认情况下，TFTP 服务是禁用的。让我们来看看这个配置文件，它很小且易于理解。

```
# cat /etc/xinetd.d/tftp
service tftp
{
    socket_type = dgram
    protocol = udp
    wait = yes
    user = root
    server = /usr/sbin/in.tftpd
    server_args = -s tftpboot
    disable = yes
    per_source = 11
    cps = 100 2
    flags = IPv4
}
```

在这里，你可以看到基础设置，例如启动期间向服务传递的协议和参数。你可能会疑惑，为什么在你想使用该服务时仍然建议保持其禁用状态。由 `xinetd` 控制的服务可以在启动过程中启用它们时，在配置文件进行启用。

### 步骤 5. 启用 TFTP 服务器在系统启动时启动：

```
# chkconfig tftp on
```

### 步骤 6. 验证服务是否会在启动期间启动：

```
# chkconfig tftp --list
tftp on
```

## 第 19 章节：网络服务 423

现在回头看配置文件，注意服务已经自动启用启动。你可以通过检查文件来验证这一点：

```
# cat /etc/xinetd.d/tftp | grep disable
disable = no
```

### 步骤 7. 此时，你也应该启用 `xinetd` 服务本身在系统启动时启动：

```
# chkconfig xinetd
```

### 步骤 8. 验证服务是否会在启动期间启动：

```
# chkconfig xinetd --list
xinetd 0:off 1:off 2:off 3:on 4:on 5:on
6:off
```

还有一件事你可以验证。你可以使用 `chkconfig` 命令获取启动期间启用的所有服务列表。这里的区别在于，`xinetd` 服务不仅列出了它的启动运行级别，还列出了它控制的所有服务。

### 步骤 9. 使用 `chkconfig` 查看所有 `xinetd` 服务：

```
# chkconfig --list
xinetd 0:off 1:off 2:on 3:on 4:on 5:off
6:off
xinetd based services:
chargen-dgram: off
chargen-stream: off
daytime-dgram: off
daytime-stream: off
discard-dgram: off
discard-stream: off
echo-dgram: off
echo-stream: off
tcpmux-server: off
tftp: on
time-dgram: off
time-stream: off
```

你在这里看到 `xinetd` 服务被设置为启动时启动，且 TFTP 服务是它唯一将启动的服务。

### 步骤 10. 如果想在不重启系统的情况下让服务运行，只需调整你喜欢的任何配置文件选项并重启 `xinetd` 服务：

```
# service xinetd restart
Stopping xinetd: [ OK ]
Starting xinetd: [ OK ]
```

### 步骤 11. 验证 `xinetd` 服务现在正运行在系统上，并在 UDP 端口 69 上监听连接：

```
# netstat -a | grep tftp
udp 0 *:tftp
```

# 红帽® RHCSA™ 和 RHCE® 认证指南与实验手册——实战指南

# 考试提示

请记住，尽管这里提到了 TFTP 服务器，但实际上运行的是 `xinetd` 服务，它代表任何 TFTP 请求通过 UDP 端口 69 提供所有功能。

# 考试提示

同样记住，对于你设置在 `xinetd` 下运行的任何服务，你需要制定防火墙规则来允许传入连接。

`xinetd` 服务识别来自 `/etc/services` 的服务和来自 `/etc/rpc` 的端口。这两个文件定义了系统可以使用的所有和服务端口。

## 第 19 章节：网络服务 407

`xinetd` 服务识别来自 `/etc/services` 的服务和来自 `/etc/rpc` 的端口。这两个文件定义了系统可以使用的所有和服务端口。

## 第 19 章节：网络服务 425

`xinetd` 服务识别来自 `/etc/services` 的服务和来自 `/etc/rpc` 的端口。这两个文件定义了系统可以使用的所有和服务端口。

# 红帽® RHCSA™ 和 RHCE® 认证指南与实验手册——实战指南

# 动态主机配置协议

所有网络中发现的基础之一是动态主机配置协议 `DHCP` 服务器，它是网络的重要部分。`DHCP` 使网络管理变得简单，因为你可以在单点（DHCP 服务器）进行更改，并将更改传递到网络的其他部分。虽然红帽考试备考中没有明确涵盖，但它是不可或缺的。

在开始安装或设置 DHCP 服务器之前，你需要验证服务器已配置了静态 IP 地址。要验证这一点，你可以查看接口配置文件：

```
/etc/sysconfig/network-scripts/ifcfg-eth1
DEVICE="eth1"
NM_CONTROLLED="yes"
BOOT=yes
HWADDR=00:0C:29:8E:F1:FD
TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
PEERNS=yes
PEERROUTES=yes
IPV4_FAILURE=no
IPV6INIT=no
NAME="System eth1"
UUID=5f6b6bd0-0bb0-45f1-d66d65f53e03
```

如果你的网络适配器没有设置静态 IP 地址，请查看第 5 章节“网络”以了解如何配置。如果你一直跟着实验实验，那么你的服务器应该有一个静态 IP 地址。有了静态 IP，你就可以开始安装 DHCP 服务器了。

# 安装 DHCP 服务器

奇怪的是，DHCP 服务器包名为 `dhcp`，而服务名为 `dhcpd`。

-- 步骤 1. 首先安装 `dhcp` 包：

  # yum install -y dhcp

-- 步骤 2. 验证包是否安装正确：

  # rpm -qa | grep dhcp

  dhcp-4.1.1-12.P1.e16.x86_64

第 3 步。安装软件包后，确保 `dhcpd` 服务在系统启动时也会启动：

```
# chkconfig dhcpd on
```

第 4 步。验证 DHCP 服务是否在启动时启动：
