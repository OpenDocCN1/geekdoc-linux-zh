
如果一个网络应用在位于伪装服务器后停止工作，它可能在某个端口上创建了服务器。如果该服务器位于随机端口（而不是定义良好的端口），那么该程序能够轻松与伪装配合工作的概率很小。下一节将讨论使用代理来访问合成网络上的服务器。

伪装规则可以与其他转发规则共存。它们也可以适用于真实的互联网 IP 地址。在下面的示例中，允许所有外部主机访问 `1.2.3.0` 网络上的 Web 服务和邮件服务，但所有源自 `1.2.3` 主机的其他其他流量都将进行伪装：

```
ipchains -P forward DENY
ipchains -F
ipchains -A forward -s 0.0.0.0/0 -p TCP -d 1.2.3.0/24 http -j ACCEPT -b
ipchains -A forward -s 0.0.0.0/0 -p TCP -d 1.2.3.0/24 smtp -j ACCEPT -b
ipchains -A forward -j MASQ -s 1.2.3.0/24 -d 0.0.0.0/0
```

`ipfwadm` 版本如下：

```
ipfwadm -F -p deny
ipfwadm -F -f
ipfwadm -I -f
ipfwadm -O -f
ipfwadm -A -f
ipfwadm -F -a accept -P S 0.0.0.0/0 -D 1.2.3.0/24 http -b
ipfwadm -F -a accept -P tcp s 0.0.0.0/0 -D 1.2.3.0/24 smtp -b
ipfwadm -F -a m -s 1.2.3.0/24 -D 0.0.0.0/0
```

这将仅开放位于内部网络服务器上的 HTTP 和 SMTP 端口；所有其他端口都将被阻塞。这些端口上的连接将使用内部主机的真实 IP 地址。内部网络的任何其他出通信都将进行伪装。

请注意，最后三个命令的顺序是重要的。该序列可以如下所示重新表述：

```
ipchains -A forward -j MASQ -s 1.2.3.0/24 -d 0.0.0.0/0
ipchains -A forward -s 0.0.0.0/0 -p TCP -D 1.2.3.0/24 http -j ACCEPT -b
ipchains -A forward -s 0.0.0.0/0 -p TCP -D 1.2.3.0/24 smtp -j ACCEPT -b
```

或者，使用另一种语法：

```
ipfwadm -F -a m -s 1.2.3.0/24 -D 0.0.0.0/0
ipfwadm -F -a accept -P tcp -s 0.0.0.0/0 -D 1.2.3.0/24 -b
ipfwadm -F -a accept -P tcp -s 0.0.0.0/0 -D 1.2.3.0/24 smtp -b
```

然而，这种序列将永远无法允许 Web 或邮件流量通过。规则是从上到下解析的，因此连接将始终被伪装。

防止 IP 欺骗（即主机通过伪造其 IP 来获取通常被拒绝的访问权限）可能也很重要。如果是这样，内核有一个简单的配置指令，可以启用源地址验证（Source Address Verification）。要设置源地址验证并防止欺骗，请将列表 4.1 中找到 Shell 脚本片段放置在网络设备启动后执行的启动文件中。

## 列表 4.1 源地址验证脚本。

```
## 这是最好的方法：开启源地址验证
## 并在所有当前和未来的接口上
## 开启欺骗保护。

if [ -f /proc/sys/net/ipv4/conf/all/rp_filter ]; then
    echo -n "Setting up ipv4 spoofing protection..."
    for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
        echo 1 > $i
    done
    echo "done."
else
    echo "ipv4 spoofing protection failed"
    echo "There is no support in this kernel"
fi
```

# 内核 IP 转发与伪装规则

使用原始（合成的）IP 地址和端口号发送返回数据包，然后将该数据包转发到内部网络。外部主机会认为防火墙正在发起所有流量，但内部主机完全察觉不到区别。

伪装（Masquerade）适用于大多数协议，但并非所有协议。FTP（活动模式）在运行于此类网络后会特别地停止工作。然而，针对某些协议的伪装服务器可以作为内核模块的形式提供。以下命令加载了所有额外的可用伪装协议模块：

```
depmod -a
modprobe ip_masq_autofw
modprobe ip_masq_cuseeme
modprobe ip_masq_ftp
modprobe ip_masq_irc
modprobe ip_masq_mfw
modprobe ip_masq_portfw
modprobe ip_masq_quake
modprobe ip_masq_radio
modprobe ip_masq_user
modprobe ip_masq_vdolive
```

显然，应该只加载所需的伪装模块。其他模块应该被省略。加载额外的内核模块会增大内核体积，并可能留下攻击路径。

如果一个网络应用在位于伪装服务器后停止工作，它可能在某个端口上创建了服务器。如果该服务器位于随机端口（而不是定义良好的端口），那么该程序能够轻松与伪装配合工作的概率很小。下一节将讨论使用代理来访问合成网络上的服务器。

伪装规则可以与其他转发规则共存。它们也可以适用于真实的互联网 IP 地址。在下面的示例中，允许所有外部主机访问 `1.2.3.0` 网络上的 Web 服务和邮件服务，但所有源自 `1.2.3` 主机的其他流量都将进行伪装：

```
ipchains -P forward DENY
ipchains -F
ipchains -A forward -s 0.0.0.0/0 -p TCP -d 1.2.3.0/24 http -j ACCEPT -b
ipchains -A forward -s 0.0.0.0/0 -p TCP -d 1.2.3.0/24 smtp -j ACCEPT -b
ipchains -A forward -j MASQ -s 1.2.3.0/24 -d 0.0.0.0/0
```

`ipfwadm` 版本如下：

```
ipfwadm -F -p deny
ipfwadm -F -f
ipfwadm -I -f
ipfwadm -O -f
ipfwadm -A -f
ipfwadm -F -a accept -P S 0.0.0.0/0 -D 1.2.3.0/24 http -b
ipfwadm -F -a accept -P tcp s 0.0.0.0/0 -D 1.2.3.0/24 smtp -b
ipfwadm -F -a m -s 1.2.3.0/24 -D 0.0.0.0/0
```

这将仅开放位于内部网络服务器上的 HTTP 和 SMTP 端口；所有其他端口都将被阻塞。这些端口上的连接将使用内部主机的真实 IP 地址。内部网络的任何其他出通信都将进行伪装。

请注意，最后三个命令的顺序是重要的。该序列可以如下所示重新表述：

```
ipchains -A forward -j MASQ -s 1.2.3.0/24 -d 0.0.0.0/0
ipchains -A forward -s 0.0.0.0/0 -p TCP -D 1.2.3.0/24 http -j ACCEPT -b
ipchains -A forward -s 0.0.0.0/0 -p TCP -D 1.2.3.0/24 smtp -j ACCEPT -b
```

或者，使用另一种语法：

```
ipfwadm -F -a m -s 1.2.3.0/24 -D 0.0.0.0/0
ipfwadm -F -a accept -P tcp -s 0.0.0.0/0 -D 1.2.3.0/24 -b
ipfwadm -F -a accept -P tcp -s 0.0.0.0/0 -D 1.2.3.0/24 smtp -b
```

然而，这种序列将永远无法允许 Web 或邮件流量通过。规则是从上到下解析的，因此连接将始终被伪装。

防止 IP 欺骗（即主机通过伪造其 IP 来获取通常被拒绝的访问权限）可能也很重要。如果是这样，内核有一个简单的配置指令，可以启用源地址验证（Source Address Verification）。要设置源地址验证并防止欺骗，请将列表 4.1 中找到的 Shell 脚本片段放置在网络设备启动后执行的启动文件中。

## 列表 4.1 源地址验证脚本。
