
## 使用 firewalld 配置 RHEL 9 防火墙

```
success
```

为了验证服务是否已永久添加，请在请求服务列表时务必包含 --permanent 标志：

```
# firewall-cmd --zone=public --permanent --list-services
```

```
cockpit dhcpv6-client http https ssh
```

请注意，作为永久性更改，此新规则要到系统重启或 firewalld 重新加载后才会生效：

```
# firewall-cmd --reload
```

使用 --remove-service 选项从区域中删除服务。由于这是运行时更改，规则将在系统下次重启时重新生效：

```
# firewall-cmd --zone=public --remove-service=https
```

要永久删除服务，请使用 --permanent 标志，记得如果需要立即生效则重新加载 firewalld：

```
# firewall-cmd --zone=public --permanent --remove-service=https
```

### 14.3.4 使用基于端口的规则

要启用特定端口，请使用 --add-port 选项。请注意，手动定义端口时，需要同时提供端口号和协议（TCP 或 UDP）：

```
# firewall-cmd --zone=public --permanent --add-port=5000/tcp
```

在向区域添加规则时，也可以指定端口范围：

```
# firewall-cmd --zone=public --permanent --add-port=5900-5999/udp
```

### 14.3.5 创建新区域

可以通过运行以下命令创建全新区域。创建后，该区域可以像任何预定义区域一样进行管理：

```
# firewall-cmd --permanent --new-zone=myoffice
```

```
success
```

添加新区域后，需要重启 firewalld 才能使该区域可用：

```
# firewall-cmd --reload
```

```
success
```

### 14.3.6 更改区域/接口分配

如前所述，系统上的每个接口都必须分配给一个区域。接口分配到的区域也可以使用 firewall-cmd 工具进行更改。在以下示例中，eth0 接口被分配到 public 区域：

```
# firewall-cmd --zone=public --change-interface=eth0
```

```
success
```

### 14.3.7 伪装

Masquerading 在网络管理领域更广为人知的名称是网络地址转换（NAT）。当使用 RHEL 9 系统作为计算机网络的互联网网关时，伪装允许所有内部系统在使用互联网通信时使用该 RHEL 9 系统的 IP 地址。这具有隐藏任何系统内部 IP 地址以免受恶意外部实体的侵害的优点，也避免了为网络上的每台计算机分配公共 IP 地址的必要性。

使用以下命令检查防火墙上是否已启用伪装：

```
# firewall-cmd --zone=external --query-masquerade
```

使用以下命令启用伪装（如果更改为永久性，请记得使用 --permanent 标志）：

```
# firewall-cmd --zone=external --add-masquerade
```

### 14.3.8 添加 ICMP 规则

互联网控制消息协议（ICMP）用于网络上的客户端系统之间发送信息，例如错误消息。它也是 ping 命令的基础，网络管理员和用户都使用该命令来检测特定客户端是否在网络上处于活动状态。ICMP 类别允许阻止特定 ICMP 消息类型。例如，管理员可能会选择阻止传入的 ping（Echo Request）ICMP 消息，以防止 ping 式拒绝服务（DoS）攻击的可能性（服务器被恶意轰炸大量 ping 消息，导致无法响应合法请求）。

要查看可用于 firewalld 规则的 ICMP 类型，请运行以下命令：

```
# firewall-cmd --get-icmptypes
```

```
address-unreachable bad-header beyond-scope communication-prohibited destination-unreachable echo-reply ...
```

以下命令例如永久添加一条规则，用于阻止 public 区域的 echo-reply（ping 请求）消息：

```
# firewall-cmd --zone=public --permanent --add-icmp-block=echo-reply
```

### 14.3.9 实现端口转发

当 RHEL 9 系统充当内部计算机网络的互联网网关时，端口转发会与伪装一起使用。端口转发允许通过互联网到达防火墙的特定端口上的流量被转发到内部网络上的特定系统。这最好通过示例来描述。

假设 RHEL 9 系统充当内部计算机网络的防火墙，并且网络上的一台系统配置为 Web 服务器。假设 Web 服务器系统的 IP 地址为 192.168.2.20。托管在此系统上的网站的域名记录配置为 RHEL 9 防火墙系统所在的公共 IP 地址之后。当 HTTP 网页请求到达端口 80 时，充当防火墙的 RHEL 9 系统需要知道如何处理它。通过配置端口转发，可以将所有 Web 流量定向到托管 Web 服务器的内部系统（在本例中为 IP 地址 192.168.2.20），要么继续使用端口 80，要么将流量重定向到目标服务器上的不同端口。事实上，端口转发甚至可以配置为将流量转发到防火墙同一系统上的不同端口（称为本地转发）。

要使用端口转发，首先按如下方式启用伪装（在此情况下，假设连接到互联网的接口已分配给 external 区域）：

```
# firewall-cmd --zone=external --add-masquerade
```

要从一个端口转发到另一个本地端口，可使用类似以下命令：

```
# firewall-cmd --zone=external --add-forward-port=port=22:proto=tcp:toport=2750
```

在上面的示例中，任何端口 22 上的 TCP 流量都将被转发到本地系统上的端口 2750。另一方面，以下命令将本地系统上的端口 20 转发到 IP 地址为 192.168.0.19 的系统上的端口 22：

```
# firewall-cmd --zone=external \
    --add-forward-port=port=20:proto=tcp:toport=22:toaddr=192.168.0.19
```

同样，以下命令将本地端口 20 转发到 IP 地址为 192.168.0.18 的系统上的端口 2750：

```
# firewall-cmd --zone=external --add-forward-port=port=20:proto=tcp:toport=2750:toaddr=192.168.0.18
```

### 14.4 从 Cockpit 界面管理 firewalld

到目前为止，本章提供了 firewalld 的概述，并探讨了使用 firewall-cmd 命令行工具管理防火墙区域和接口。虽然 firewall-cmd 提供了管理 firewalld 配置最灵活的方式，但也可以在 Cockpit Web 控制台中查看和管理默认区域的服务。

要访问 firewalld 设置，请登录 Cockpit 界面并从导航面板中选择 Networking。在网络页面上，找到如下面图 14-1 所示的 Firewall 部分并单击 Edit rules and zones 按钮：

![](img/be1f159c3cc937d7b264dc5b134856dc_126_0.png)

图 14-1

Firewall 页面显示默认区域配置的当前服务规则（并允许删除服务），允许向区域添加新服务，并打开和关闭防火墙：

网络 > 防火墙

### 防火墙

默认情况下阻止传入请求。传出请求不被阻止。

![](img/be1f159c3cc937d7b264dc5b134856dc_127_0.png)

图 14-2

### 14.5 使用 firewall-config 管理 firewalld

如果您有权访问图形桌面环境，还可以使用 firewall-config 工具配置防火墙。虽然默认未安装，但 firewall-config 可以按如下方式安装：

```
# dnf install firewall-config
```

启动时，主 firewall-config 屏幕如图所示 14-3 所示：

![](img/be1f159c3cc937d7b264dc5b134856dc_127_1.png)

图 14-3
