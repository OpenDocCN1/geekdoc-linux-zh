
它自行处理各种网络服务，而不是直接转发。在这个意义上，它是发起请求系统的“代理”。

代理防火墙对互联网服务器“隐藏”了你的计算机存在的事实。此外，代理防火墙通常还会处理来自互联网的所有传入连接（例如 Web 流量、FTP 下载和电子邮件投递）。再次强调，这是为了最大限度地减少外部世界看到你内部网络的机会。

## 配置 ipchains 过滤防火墙

Ipchains 通过检查在网络接口上发送和接收的数据包，并决定哪些数据包应被投递，哪些应被阻止来工作。它通过检查一个规则列表（也称为链）来实现这一点。它会在第一个匹配数据包的规则处停止，并检查该规则的目标。

如果你在 Red Hat Linux 安装过程中配置了防火墙，那么一些规则已经为你设置好了。这些规则可能相当严格。安装后系统启动并运行，你应该做的第一件事就是检查防火墙的当前状态。作为 root 用户输入以下内容即可做到：

```
# ipchains -L
Chain input (policy ACCEPT):
target  prot opt source       destination  ports
ACCEPT  all  --  anywhere       anywhere     n/a
ACCEPT  udp  --  a.myisp.net  anywhere     domain - any
ACCEPT  udp  --  b.myisp.net  anywhere     domain - any
DENY    tcp  --  anywhere       anywhere     any - any
DENY    udp  --  anywhere       anywhere     any - any
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

上述是在 Red Hat Linux 安装期间选择默认防火墙设置（高安全性）时我得到的输出结果。请注意，只有输入受到限制。换句话说，限制的是外部用户可以请求的服务。第一个 ACCEPT 行是由一条允许本地系统用户发起的所有请求的规则产生的（即，它允许回环驱动程序，如端口列下的 n/a 所示）。启用此规则后，你可以请求本地系统的任何服务，而数据包不会被拒绝。

接下来的两个 ACCEPT 行允许我指定为 DNS 服务器的计算机（`from /etc/resolv.conf`）请求我计算机的 DNS 服务（`domain`）。最后两条规则（DENY）导致所有不匹配之前规则的 tcp 和 udp 请求被拒绝。

这个默认防火墙配置在 `/etc/sysconfig/ipchains` 文件中设置。当 ipchains 服务在系统启动时启动（`/etc/init.d/ipchains`）时，服务从 `/etc/sysconfig/ipchains` 读取规则。以下是该文件中的规则，用于创建上述配置：

```
:input ACCEPT
:forward ACCEPT
:output ACCEPT
-A input -s 0/0 -d 0/0 -i lo -j ACCEPT
-A input -s 192.160.0.253 53 -d 0/0 -p udp -j ACCEPT
-A input -s 192.160.0.254 53 -d 0/0 -p udp -j ACCEPT
-A input -s 0/0 -d 0/0 -p tcp -j DENY
-A input -s 0/0 -d 0/0 -p udp -j DENY
```

由于 ipchains 规则在每次启动系统时都会从此文件清除并重新加载，我建议使用 `/etc/sysconfig/ipchains` 文件作为设置防火墙规则的好地方。随着计算机破解攻击的日益增多，专家推荐当前的安全方法是默认安全。这意味着你应该从限制大多数服务开始，然后只添加你想要启用的那些服务。先放入允许服务的规则，然后在最后两行拒绝所有其他服务。

### 理解 ipchains 防火墙规则

ipchains 目标可以是像 `ACCEPT` 或 `DENY` 这样的简单命令，也可以是另一个规则链的名称，以便开始检查。内核始终会检查三个默认规则链。它们是 input、output 和 forward 链。你可以创建额外的用户定义链，并从这三个原始链中调用它们，但对于简单的防火墙配置，标准的三个链就足够了。

> **提示：** ipchains 在找到匹配项后停止检查规则链，因此请注意规则的顺序。具有特定条件的规则应放在具有类似但更宽泛条件的规则之前。如果你接受所有 TCP 连接，但随后有一条拒绝 telnet 访问的规则，那么 telnet（作为 TCP 服务）将被允许。反转规则顺序（先拒绝 telnet，然后接受 TCP）才能产生正确的效果。

一般的语法是调用 `ipchains`，指定要执行的操作参数，后跟要应用的规则链。这后面可能跟有规则描述和规则目标。表 14-4 显示了你可以与 `ipchains` 一起使用的操作参数。

#### 表 14-4: Ipchains 操作参数

| 操作参数 | 描述 |
| :--- | :--- |
| -A, --append | 将新规则追加到指定列表的末尾。 |
| -D, --delete | 从指定列表中删除规则。你可以通过其在列表中的数字位置或匹配它的规则参数来指定该规则。 |
| -R, --replace | 用新规则替换旧规则。 |
| -I, --insert | 将新规则插入列表中的特定位置。 |
| -L, --list | 列出链中的所有规则。如果省略链名称，则列出所有链中的所有规则。 |
| -F, --flush | 清除链中的所有规则。 |
| -Z, --zero | 将所有链的数据包计数器清零。 |
| -N, --new-chain | 创建具有指定名称的新链。 |
| -X, --delete-chain | 删除具有指定名称的链。 |
| -P, --policy | 将链的策略设置为指定的目标。链的策略描述了如果没有规则匹配数据包时采取的操作。所有链的默认策略都是 ACCEPT。 |
| -M, --masquerading | 允许查看伪装连接。IP 伪装在第 16 章中讨论。 |
| -S, --set | 设置 TCP、TCPFIN 和 UDP 数据包的超时时间。 |
| -C, --check | 针对给定的链检查提供的数据包。这主要用于调试。 |
| -h | 打印描述 ipchains 参数的帮助消息。 |

如表 14-4 所示，ipchains 操作参数可以表示为两种形式，一种是破折号后跟一个大写字母，另一种是两个破折号后跟一个描述性单词。两者都可以工作，因此请使用你更喜欢的那个。在本章的示例中，我将使用缩写版本。

通常，我们在操作参数后跟随要应用的规则链。添加到 input 链的规则仅在过滤 Linux 机器接收的网络数据包时进行检查。类似地，output 链仅在检查从 Linux 机器传输的数据包时进行检查。forward 链仅针对由 Linux 系统接收但将投递到其他网络系统的网络数据包进行检查。数据包转发仅在你的系统配置为路由器时发生。

在指定要操作的链之后，你可以指定一些可选参数来定义规则。表 14-5 列出了可用的可选参数。

#### 表 14-5: Ipchains 可选参数

| 参数 | 描述 |
| :--- | :--- |
| -p, --protocol [!] protocol | 指定规则应匹配的协议。这应该是 TCP、UDP 或 ICMP。 |
| -s, --source [!] address | 指定要匹配的源地址。这可以是一个单独的地址，或者你可以通过在地址后跟 / 和子网掩码左侧的 1 位数量来指定整个子网。因此，地址 199.170.177.0/24 的子网掩码为 255.255.255.0。 |
| --source-port [!] port | 在 /etc/services 中指定的源 TCP 或 UDP 端口号。你还可以通过列出第一个和最后一个端口号，中间用 `:` 冒号字符分隔，来指定端口范围。 |
| -d, --destination [!] address | 指定要匹配的目的地址。这可以是一个单独的地址，或者你可以通过在地址后跟 / 和子网掩码左侧的 1 位数量来指定整个子网。因此，地址 199.170.177.0/24 的子网掩码为 255.255.255.0。 |
| --destination-port [!] port | 在 /etc/services 中指定的目的 TCP 或 UDP 端口号。你还可以通过列出第一个和最后一个端口号，中间用 `:` 冒号字符分隔，来指定端口范围。 |
| --icmp-type [!] typename | 设置要使用的 ICMP 数据包类型。 |
| -j, --jump target | 当规则匹配时执行的目标（操作）的名称。这可能是另一个 ipchain 的名称或几个预定义目标之一。 |
| -i, --interface [!] name | 此规则适用的网络接口的名称。如果未提供此选项，该规则将适用于所有接口。 |
| [!] -f, --fragment | 规则仅适用于碎片数据包，不包括第一个数据包。换句话说，它适用于第一个数据包之后的所有数据包碎片。 |
| -b, --bidirectional | 规则应适用于传入和传出数据包。 |
| -v, --verbose | 在处理此 ipchains 命令时打印调试消息。 |
| -n, --numeric | 在将输出打印到屏幕时使用 IP 地址而不是主机名。 |

