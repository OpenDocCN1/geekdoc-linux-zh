
进入`/path/to/xxx`目录，找到`xxx.json`。

上述示例是一个限制性配置。它允许从某些主机到`imap`、`ipop3d`和`telnet`服务的连接，但拒绝所有其他连接。让我们详细检查这些文件。

和通常一样，以`#`字符开头的行是注释，`xinetd`在解析文件时会忽略它们。每行非注释行都由用逗号分隔的守护进程列表组成，后面跟着一个冒号`(:)`，然后是用逗号分隔的待检查客户端地址列表。在这种背景下，客户端是指任何尝试访问你系统上网络服务的计算机。

客户端可以是一个数字 IP 地址（例如`199.170.177.25`）或主机名（例如`dexter.glaci.com`），但更多时候是指定整个地址范围的通配符变体。客户端条目可以采取四种形式。`hosts.allow`文件的在线手册页对它们的描述如下：

- 以点`.`字符开头的字符串。如果主机名的最后部分与指定模式匹配，则匹配主机名。例如，模式`.tue.nl`匹配主机名`wzw.win.tue.nl`。
- 以点`.`字符结尾的字符串。如果主机地址的前几个数字字段与给定字符串匹配，则匹配主机地址。例如，模式`131.155`匹配埃因德霍芬大学（Eindhoven University）网络上（几乎）每个主机的地址（`131.155.x.x`）。
- 以`@`字符开头的字符串。用于引用`/etc/hosts`文件中定义的主组。
- 关键字`ALL`，匹配任何地址。

# 第 14 章：计算机安全问题 515

代理防火墙从互联网上“隐藏”了你的计算机存在的这一事实。此外，代理防火墙通常会处理来自互联网的所有入站连接（例如 Web 流量、FTP 下载和电子邮件投递）。再次，这样做是为了最大限度地减少你的内部网络对外部世界的可见性。

## 配置 ipchains 过滤防火墙

`Ipchains`的工作原理是检查在网络接口上发送和接收的数据包，并决定哪些数据包应该被传递，哪些数据包应该被停止。它通过检查规则列表（也称为链，`chain`）来实现这一点。它会在匹配数据包的第一条规则处停止，并检查该规则的目标。

> 注意：在 Red Hat Linux 8 中，`iptables`取代了`ipchains`成为安装期间创建的防火墙。要使用`ipchains`，你必须关闭`iptables`并手动创建`ipchains`规则。然后，你必须按照本章后面介绍的方法启动`ipchains`服务。

要使用`ipchains`功能，你必须安装`ipchains` RPM。要检查`ipchains`是否已安装并在你的系统上运行，请使用``ipchains -L``命令。如果未配置`ipchains`，你将看到消息"`ipchains with this kernel`" 。如果`ipchains`正在运行，你看到的输出将如下所示：

```
# ipchains -L

Chain input (policy ACCEPT):

target prot opt source      destination ports

ACCEPT all             anywhere      n/a

ACCEPT udp            a.mysip.net anywhere      domain - any

ACCEPT udp            b.mysip.net anywhere      domain - any

DENY tcp               ---anywhere      any - any

DENY udp             anywhere      any - any

Chain forward (policy ACCEPT):

Chain output (policy ACCEPT):
```

上述输出代表一个高度安全的防火墙。注意，只有输入（`input`）受到了限制。换句话说，对用户可以请求哪些服务的限制是明确的。第一条`ACCEPT`行源于允许来自本地系统用户所有请求的规则（即，它允许了环回驱动程序，如端口下的`n/a`所示）。启用该项后，你可以从本地系统请求任何服务，而数据包不会被拒绝。

接下来的两条`ACCEPT`行允许被标记为我的 DNS 服务器（来自`/etc/resol.conf`）的计算机请求 DNS 服务（`domain`）。最后两条规则（`DENY`）导致所有不匹配之前规则的`tcp`和`udp`请求被拒绝。

此防火墙配置设置在`/etc/sysconfig/ipchains`文件中。`ipchains`服务在系统启动时启动（`/etc/init.d/ipchains`），该服务从`/etc/sysconfig/ipchains`读取规则。以下是该文件中的规则对应上述配置的样式：

516 第三部分：管理 Red Hat Linux

```
:input ACCEPT

:forward ACCEPT

:output ACCEPT

-A input -s 0/0 -d 0/0 -i lo -j ACCEPT

-A input -s 192.160.0.254 53 -d 0/0 --udp -j ACCEPT

-A input -s 192.160.0.254 53 -d 0/0 --udp -j ACCEPT

-A input -s 0/0 -d 0/0 --tcp -y -j DENY

-A input -s 0/0 -d 0/0 --udp -j DENY
```

因为`ipchains`每次启动系统时都会清除并重新加载，因此`/etc/sysconfig/ipchains`是设置规则的好地方。随着计算机破解者攻击的增加，安全专家建议的当前方法是“默认安全”。这意味着你应该从限制大多数服务开始，然后只添加你启用的服务。先将允许服务的规则放在前面，然后在最后两行拒绝所有其他服务。

## 理解 ipchains 防火墙规则

目标（`target`）可以是一个简单的命令，如`ACCEPT`或`DENY`，也可以是另一个规则链的名称以开始检查。内核始终会执行三条默认规则链，它们是`input`、`output`和`forward`链。你可以创建额外的用户定义链，并从这原始三条链中调用它们，但对于简单的防火墙配置，标准的三条链就足够了。

> 提示：`ipchains`在找到匹配项后会停止检查规则链，因此请注意规则的顺序。具有特定条件的规则应该放在具有相似但范围更广的条件的规则之前。如果你用一条规则接受后续所有的 TCP 连接，再用一条规则拒绝`telnet`访问，那么`telnet`（作为 TCP 服务）将会被允许。反转规则顺序（先拒绝`telnet`，后接受 TCP）才能产生正确的效果。

通用语法是调用`ipchains`并带有一个指定执行操作的参数，随后是执行该操作的规则链。后面可能紧跟规则描述和规则目标。表 14-4 显示了你可以配合`ipchains`使用动作参数。

### 表 14-4：Ipchains 动作参数

| 动作参数 | 描述 |
| :--- | :--- |
| `-A`, `--append` | 将新规则添加到指定列表末尾。 |
| `-D`, `--delete` | 从指定列表中删除规则。你可以通过规则在列表中的数字位置或匹配它的规则参数来指定规则。 |
| `-R`, `--replace` | 用新规则替换规则。 |

第 14 章：计算机安全问题 517

| 动作参数 | 描述 |
| :--- | :--- |
| `-I`, `--insert` | 将新规则插入列表的特定位置。 |
| `-L`, `--list` | 列出规则。 |
| `-F`, `--flush` | 清空规则。 |
| `-Z`, `--zero` | 计数器清零。 |
| `-N`, `--new` | 创建新链。 |
| `-X`, `--delete` | 删除链。 |
| `-P`, `--policy` | 设置策略。 |
| `-M`, `--masquerade` | 伪装地址。 |
| `-S`, `--set` | 设置规则。 |
| `-C`, `--check` | 检查规则。 |
| `-h`, `--help` | 显示帮助信息。 |

如表 14-4 所示，`ipchains`参数可以用单个连字符后加字母，或双连字符后加单词的形式表示。通常，我们在动作后面跟随你偏好的。数据包在`forward`链中。

### 表 14-5：Ipchains 可选参数

| 参数 | 描述 |
| :--- | :--- |
| `-p`, `--protocol` | 指定规则匹配的协议。这应该是 TCP、UDP 或 ICMP。 |
| `-s`, `--source` | 指定匹配的源地址。可以是单个地址，也可以通过在地址后加上 `/` 和网络掩码位数来指定整个子网。因此，地址 `199.170.0/24` 的网络掩码为 `255.255.255.0`。 |
| `-d`, `--destination` | 指定匹配的目的地址。可以是单个地址，也可以通过在地址后加上 `/` 和网络掩码位数来指定整个子网。因此，地址 `199.170.0/24` 的网络掩码为 `255.255.255.0`。 |
| `--source-port` | 指定 `/etc/services` 中定义的源 TCP 或 UDP 端口。你也可以通过列出用冒号分隔的端口范围来指定端口。 |
| `--destination-port` | 指定 `/etc/services` 中定义的目的 TCP 或 UDP 端口。你也可以通过列出用冒号分隔的端口范围来指定端口。 |
| `--icmp-type` | 设置要使用的 ICMP 包类型。 |
| `-j`, `--jump` | 规则匹配时执行的目标（动作）名称。这可以是另一个 `ipchain` 的名称或几个预定义目标之一。 |
| `-i`, `--interface` | 规则应用的网络接口名称。如果没有提供此项，规则适用于所有接口。 |
| `-f`, `--fragment` | 规则仅适用于分片数据包，不包括第一个。换句话说，它适用于第一个分片之后的所有数据分片。 |
| `-b`, `--directional` | 规则应适用于入站和出站包。 |
| `-v`, `--verbose` | 在处理此 `ipchains` 命令时打印调试信息。 |
| `-n`, `--numeric` | 在屏幕输出时使用 IP 地址而不是主机名。 |

## 第 14 章：计算机安全问题 519

| 参数 | 说明 |
| :--- | :--- |
| `-l`, `--log` | 开启匹配数据包的内核日志。这会减慢速度并填满硬盘。主要用于调试。 |
| `-o`, `--output [maxsize]` | 将数据包重定向到用户空间进程。另一个调试功能。 |
| `-m`, `--mark markvalue` | 为数据包标记一个 32 位的签名。这可能在你是一个内核黑客时才有用。 |
| `-t`, `--TOS andormask` | 使用提供的位掩码检查并检查数据包的 TOS 字段。关于此选项的完整讨论请阅读 `ipchains` 页面。 |
| `-x`, `--exact` | 显示包计数器的精确值，而不是四舍五入到 KB 的数字。 |
| `-y`, `--syn` | 检查正在查看的 TCP 数据包中的 SYN 位。用于阻止 TCP 连接从一个方向建立而非另一个。 |
| `--line-numbers` | 在列出规则时显示行号。如果你计划按位置编号删除或修改规则，这很有用。 |
| `--no-warnings` | 禁用所有警告消息。 |

在为特定类型的数据包指定规则+ 后，你必须使用 `-j` 或 `--jump` 选项为其指定目标（`target`）。这告诉 `ipchains` 在找到匹配的规则时对该数据包执行什么操作。目标可以是另一个要遍历的规则链名称，但通常是表 14-6 中描述的预定义操作之一。

### 表 14-6：Ipchains 目标

| 目标 | 说明 |
| :--- | :--- |
| `ACCEPT` | 接受数据包并按正常方式递交。 |
| `DENY` | 完全丢弃数据包。 |
| `REJECT` | 丢弃数据包并向发送主机发送带有解释的 ICMP 包。这主要用于调试。 |

## 520 第三部分：管理 Red Hat Linux

| 目标 | 说明 |
| :--- | :--- |
| `MASQ` | 对此类类型的数据包使用 IP 伪装。关于伪装的解释请参考第 16 章。 |
| `REDIRECT` | 将数据包重定向到新位置。 |
| `RETURN` | 从此链返回到调用它的链。在调用链中你离开的地方继续检查规则。 |

我已经向你展示了 `ipchains` 命令的各种组件。可以将这些组件组合成一些实用的示例。使用 `ipchains` 可以创建非常复杂且复杂的规则列表，但我将保持我的示例尽可能简单。保持简单通常是一个好策略，因为大型、复杂的规则链会影响系统性能。花费更多时间检查规则意味着递交数据包和提供信息的时间更少。你的 Linux 机器流量水平越高，这些复杂规则链对性能的影响就越大。

## 修改 ipchains 防火墙规则

现在让我们尝试一条规则。例如，假设我们想要阻止 ICMP 包以不允许对我们的 Linux 机器进行“ping”。你可以这样做来避免针对你的系统发起的各种拒绝攻击。使用类似下面的命令阻止 ICMP：

```
# ipchains -A input -p icmp -j DENY
```

这表示我们正在向输入链（`input chain`）添加一条规则。它将匹配任何 ICMP 包并将其丢弃而不允许通过。如果你对 Linux 机器使用 `ping` 命令，你应该收不到任何响应。再次输入 `ipchains -L` 命令，你将看到类似的内容：

```
Chain input (policy ACCEPT) :

  target prot opt            destination ports

  DENY icmp            anywhere       any -> any

Chain forward (policy ACCEPT) :

  Chain output (policy ACCEPT) :
```

你可以看到你的新规则列表。这将阻止所有进入系统的 ICMP 包，无论它们是由哪条链发送的。如果你的 Linux 系统充当路由器，它还将阻止从互联网转发到你的网络的 ICMP 包，反之亦然。互联网上的人将无法 ping 你网络上的任何内容。同样，你也将无法 ping 互联网上的任何内容。也许这不是你想要的。让我们假设你想阻止互联网上的人 ping 你网络上的系统，但允许 ping 并允许路由器 ping 互联网上的主机。

首先，我们应该使用 `-F` 参数清空 `iptables` 链的内容；然后我们可以添加新规则。

```
# ipchains -F input

# ipchains -A forward -p icmp -j DENY
```

现在我们可以 ping Linux 系统和任何其他机器，但 ping 请求不会通过 Linux 系统。如果你愿意，可以使用 `ipchains` 命令验证规则现在已添加到转发链（`forward chain`）而不是输入链。

你可能还想阻止来自互联网的 `telnet` 协议。在这个示例中，让我们假设我们的路由器通过一个名为 `ppp0` 的拨号连接到互联网，并通过名为 `eth0` 的以太网连接到我们的内部局域网。在这种情况下，你可以可以使用下面的命令阻止 `telnet`：

```
# ipchains -A input -i ppp0 -p tcp --dport 23 -j DENY
```

此规则基本上规定任何目标端口为 23（`/etc/services` 中指定的 `telnet` 端口）且到达 `ppp0` 接口的 TCP 数据包都将被丢弃。它并没有阻止你从内部网络 `telnet` 到你的 Linux 机器，但它阻止了来自互联网的访问。（注：后续 OCR 文本包含大量重复和伪影，已在翻译中处理）。

# 第 14 章：计算机安全问题 523

3. 现在，你可以重启 Red Hat Linux，或者按照如下方式停止 `iptchains` 并卸载 `ipchains` 模块：

```
# /etc/init.d/iptchains stop

# modprobe -r iptables
```

4. 在启动 `iptables` 之前，你必须拥有一组已经配置并放置在你的 `/etc/sysconfig/iptables` 文件中的可以运行的规则。要创建这些规则，请参考接几个章节中的示例（如果没有准备好配置文件，`iptables` 将静默失败。）

5. 如果你正在进行 NAT 或 IP 伪装（IP Masquerading），则需要开启 IP 数据包转发功能。实现此功能的一种方法是将 `/etc/sysctl.conf` 文件中的将 `net.ipv4.ip_forward` 的值改为 `1`。以 root 用户身份使用任何文本编辑器编辑此文件，并将该行修改如下所示：

```
net.ipv4.ip_forward = 1
```

6. 一旦规则就绪，启动 `iptables`：
```
# /etc/init.d/iptables start
```
