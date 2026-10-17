
`<M>` 支持 IP tables 支持（过滤/伪装/NAT 需）  
`<M>` 完整 NAT  
`<M>` `MASQUERADE` 目标支持  

图 4.6 展示了当 `nat` 表加载时，数据包通过内核时可能经过的路径。你可以通过 `modprobe iptable.nat` 实现这一点，如果你的内核配置了卸载模块，那么当你执行 `iptables -t nat` 时，它会自动加载该模块。如你所见，该表的钩子（hooks）位于路由决策做出之前和之后。为什么要设置两个位置？一个不就够了吗？在 2.2 系列内核中，在转发代码中只有一个进入钩子。换句话说，如果你没有在转发数据包，你就无法修改它的源地址。当你想要修改源地址时这是足够的，但如果你需要在进入路由代码之前知道它，以便路由你想要隐藏的 IP 地址，这将是第 9.2.3 节的主题。为了更改源地址，`nat` 需要更改源地址，`POSTROUTING` 链就是所在的地方，因此让我们从一个简单的（且没什么用的）示例开始。

```
iptables -t nat -A POSTROUTING -j MASQUERADE
```

如果我们看这个命令，我们选择了 `nat` 表和 `POSTROUTING` 链，要跳转到的目标是 `MASQUERADE`。什么类型的数据包？所有类型的数据包。从

![](img/e98e3956bdbeb0fcebd99cf9c0434e1b_146_0.png)

图 4.6 带有 `netfilter` `nat` 表的数据包路径

什么源地址？从任何源目的地。到任何目的地。记住，左未设置的参数默认为任意。那么这符合我们 `erbium` 的需求吗？令人惊讶的是，可以的。因为它在转发时会进行伪装，并且会记住它已经伪装过的连接（通过连接跟踪代码），它将完成工作。然而，如果使用 `erbium` 路由除我们内部客户端以外的其他数据包到外网，可能会产生一些意想不到的副作用。首先，在没有防火墙的情况下，任何从外网尝试通过外网链路的连接都会到达 `erbium`，并根据 `erbium` 的路由表进入我们的网络，除了带有运动项目的 IP 地址之外。噢，防火墙匹配我们发送的数据包是完全不同的吗？这通过 `--o intf` 或 `--out-intf` 指定接口可以轻松实现。但 `erbium` 有点特殊，我们并不总是确定输出设备名称将是什么（在 PPP 连接的情况下，它将是 `pppN`，或者我们的 ISDN 有完全不同的设备名称）。这里是命令形式的另外几个示例：

```
# 伪装所有输出的所有数据包
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -o ppp+
```

```
# 伪装到给定的目的地址/子网的所有数据包
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -d 10.10.34.216
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -d 10.10.34.216/25
```

```
# 仅从特定的本地子网伪装到给定的目的子网
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
d-10.10.34.216/25 -s 192.168.16.0/24
```

```
# 仅伪装到给定的端口
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
d-10.10.34.216/25 --proto tcp --dport 22
```

在这个示例中，我们指定仅允许所有目的地为端口 22（通常用于 `ssh`）的数据包。你还可以使用 `--start:finish` 指定一个端口范围，其中 `start` 或 `finish` 都可以省略，以表示所有端口或大于所有端口的端口。（注意 `iptables` 用户）当使用由 `ipt_multport` 模块提供的 `multiport` 匹配扩展时，可以使用列出多个不同端口（例如 22, 25, 110）的能力。我们将在第 7 章中讨论匹配扩展。）有时，指定你不想伪装的内容会更容易。例如，你可能有一个拓扑结构，其中防火墙正在执行伪装，但防火墙外有几台机器从你的内部网络有路由。我们不希望从内部机器到这些机器的连接被伪装，关于源 IP 地址的任何意义信息都丢失了。如果你需要伪装的内部网络是 `192.168.0.0/16` 或 `255.255.255.192`，你可以按照如下方式设置规则：

```
# 伪装未绑定到特殊网络的连接
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
--source 192.168.0.0/16 \
--destination 172.16.64/25.255.255.255.192
```

```
# 或者，使用 ACCEPT 用于处理不带伪装的转发流量
erbier# iptables -t nat -A POSTROUTING -j ACCEPT
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
--source 192.168.0.0/16 \
-d 172.16.64/25.255.255.255.192
```

为了更改源地址，`nat` 需要更改源地址，`POSTROUTING` 链就是所在的地方，所以让我们从一个简单的（且没什么用的）示例开始。

```
iptables -t nat -A POSTROUTING -j MASQUERADE
```

如果我们看这个命令，我们选择了 `nat` 表和 `POSTROUTING` 链，要跳转到的目标是 `MASQUERADE`。什么类型的数据包？所有类型的数据包。从

![](img/e98e3956bdbeb0fcebd99cf9c0434e1b_146_0.png)

图 4.6 带有 `netfilter` `nat` 表的数据包路径

什么源地址？从任何源目的地。到任何目的地。记住，左未设置的参数默认为任意。那么这符合我们 `erbium` 的需求吗？令人惊讶的是，可以的。因为它在转发时进行伪装，并且会记住它已经伪装过的连接（通过连接跟踪代码），它将完成工作。然而，如果使用 `erbium` 路由除我们内部客户端以外的其他数据包到外网，可能会产生一些意想不到的副作用。首先，在没有防火墙的情况下，任何从外网尝试通过外网链路的连接都会到达 `erbium`，并根据 `erbium` 的路由表进入我们的网络，除了带有运动项目的 IP 地址之外。噢，防火墙匹配我们发送的数据包是完全不同的吗？这通过 `--o intf` 或 `--out-intf` 指定接口可以轻松实现。但 `erbium` 有点特殊，我们并不总是确定输出设备名称将是什么（在 PPP 连接的情况下，它将是 `pppN`，或者我们的 ISDN 有完全不同的设备名称）。这里是命令形式的另外几个示例：

```
# 伪装所有输出的所有数据包
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -o ppp+
```

```
# 伪装到给定的目的地址/子网的所有数据包
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -d 10.10.34.216
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE -d 10.10.34.216/25
```

```
# 仅从特定的本地子网伪装到给定的目的子网
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
d-10.10.34.216/25 -s 192.168.16.0/24
```

```
# 仅伪装到给定的端口
erbier# iptables -t nat -A POSTROUTING -j MASQUERADE \
d-10.10.34.216/25 --proto tcp --dport 22
```

在这个示例中，我们指定仅允许所有目的地为端口 22（通常用于 `ssh`）的数据包。你还可以使用 `--start:finish` 指定一个端口范围，其中 `start` 或 `finish` 都可以省略，以表示所有端口或大于所有端口的端口。（注意 `iptables` 用户）当使用由 `ipt_multport` 模块提供的 `multiport` 匹配扩展时，可以使用列出多个不同端口（例如 22, 25, 110）的能力。我们将在第 7 章中讨论匹配扩展。）有时，指定你不想伪装的内容会更容易。例如，你可能有一个拓扑结构，其中防火墙正在执行伪装，但防火墙外有几台机器从你的内部网络有路由。我们不希望从内部机器到这些机器的连接被伪装，关于源 IP 地址的任何意义信息都丢失了。如果你需要伪装的内部网络是 `192.168.0.0/16` 或 `255.255.255.192`，你可以按照如下方式设置规则：
