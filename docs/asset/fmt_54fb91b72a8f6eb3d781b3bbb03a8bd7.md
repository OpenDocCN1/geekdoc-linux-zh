
```bash
  --interface spp0 \
  --proto icmp --icmp-type echo-request \
  --limit 2s --limit-burst 3
```

```bash
# 剩余的被丢弃
oxygen:root> iptables --table filter -A INPUT -j DROP \
  --interface spp0 \
  --proto icmp --icmp-type echo-request
```

注意，你正在指定规则匹配数据包的条件。因此，为了真正阻止意外的流量（例如，洪水式 ping），你必须结合 `ACCEPT` 目标指定 `limit`，并确保在超过限制后，链中的另一条规则阻止该类型的数据包通过。记住，该规则影响的是路由器的输入，而不是允许通过路由器的流量（通过 `FORWARD` 链）。你应该理解，这并不是限制带宽的机制；我们将在第 8.4 节中讨论限制带宽。

## 7.3.7 输出链 (OUTPUT Chain)

我们花了一些时间讨论了 `INPUT` 和 `FORWARD`，以及一些匹配规则的机制。现在，让我们来看 `INPUT` 的另一侧：`OUTPUT` 链。由于 `netfilter` 将转发（forwarding）与本地系统的输入/输出分离开，与之前的内核过滤器相比，限制输出的动力可能没那么大。尽管如此，我想到了几个使用场景，当你需要时，它们会成为工具箱的一部分。正如你可能推测的那样，`OUTPUT` 链会对所有离开本地系统的数据包进行过滤，并可用于（速率限制）出站数据包流。

一种方法是限制你认为应该从你的路由器产生的流量（然后看看会发生什么）。另一种方法是使用输出规则专门阻止来自你路由器提供的网络服务的数据包，作为第二道防线。（你肯定不希望配置不当的路由向外部广播关于你网络拓扑的各种信息。）第三种方法是，为了确保磁盘空间使用充足，限制路由器的所有输出（节省 DNS 查询）。如果这确实是你的防火墙，你应该对本地运行了什么程序有非常清楚的认识。只要加载了 `iptables_filter`，就可以向 `OUTPUT` 链添加规则，你还可以额外使用 `--interface itf` 来指定规则所属的接口。以下是一些示例：

```bash
# 我们不想对许多 ping 响应
root@> iptables --table filter -A OUTPUT -j ACCEPT \
    --proto icmp --icmp-type response \
    --out-interface ppp0 \
    --limit 5/s --limit-burst 10

root@> iptables --table filter -A OUTPUT -j DROP \
    --out-interface ppp0 \
    --proto icmp --icmp-type echo-response

# 禁止明文密码协议：
root@> iptables --table filter -A OUTPUT -j REJECT \
    --proto tcp \
    --match multiport --dport 21,23
```

上述操作绕过了我们的输入限制，并欺骗路由器生成一系列 ping 响应包（或者在口语中称为 pongs）。我们在第 4 章中提到过 `--match multiport` 引入了 `netfilter`，但这是我们第一次使用它。它允许我们指定一个用逗号分隔的端口列表，而不是生成两个独立的规则。在这种情况下，你不需要管理员从防火墙安装 telnet 或 ftp，以防窃听者可能会监控连接并获取管理员的密码之一。

类似于控制用户在系统上可以执行的操作，还有另一个匹配目标可以用于匹配用户 ID (`UID`)、组 ID (`GID`)、进程 ID (`PID`) 或会话。你需要在内核中启用 Owner 匹配（在 `IP: Netfilter Configuration` 中找到），并加载 `ipt_owner` 以访问该扩展。该扩展仅对本地系统的输出有效，这应该是合理的——如果流量不是来自这个系统，那么就有必要使用 `ident` 等设施询问其他用户数据包的源头。这在时间上是昂贵的，而且你根本无法真正信任任何你未管理的系统来告诉你是哪个用户 ID 发起了数据包。

但在系统上实施本地策略时，例如只允许某个组（`gid 17`）的成员可以从这台机器发起 ssh 连接，这是一个非常实用的匹配扩展。在示例中，我们同时利用了 `owner` 和 `state` 匹配扩展，允许只有我们网络管理员组的成员发起 ssh 连接。

```bash
# 允许 netmins 组的成员发起 ssh
root@> iptables --table filter -I OUTPUT -j ACCEPT \
    --match owner --gid-owner 17 \
    --match state --state NEW,ESTABLISHED \
    --proto tcp --dport 22
```

在 `--match owner` 之后，你可以指定以下内容：`--uid-owner uid`、`--gid-owner gid`、`--pid-owner pid` 或 `--sid-owner sid`，这些 id 是具体的数字。（不要让内核每发送一个数据包就都去遍历 `/etc/passwd` 来匹配用户名和 uid！）最后，尽管我们还没有讨论过，但 mangle 表也挂钩到了 `OUTPUT` 链，因此我重申我的建议：始终使用 `--table` 或 `-t` 来指定所需的表。

## 7.3.8 netfilter LOG 目标

本章中涵盖的 `netfilter` 最后一部分是上述 `LOG` 目标。该目标通过 `-j LOG` 指定，简单地记录数据包的通过。它可以与任何表（内置或用户定义）配合使用。最小的内核配置仅包含对 `iptables` 和 `LOG` 目标本身的支持。

```text
网络选项 --->
* 网络数据包过滤（替换 ipchains）
* TCP/IP 网络
* IP: Netfilter 配置 --->
* IP tables 支持（过滤/地址转换/NAT 需要）
* LOG 目标支持
```

一旦你加载了生成的模块（`modprobe ipt`——注意目标与匹配扩展的区别在于，目标在模块名和命令行中始终大大写），你就可以使用以下参数：

```text
LOG v1.2 options:

--log-level level 日志级别（参考 syslog.conf）
--log-prefix prefix 使用此前缀日志消息
--log-tcp-sequence Log TCP 序列号
--log-tcp-options TCP 选项
--log-ip-options IP 选项
```

日志级别有 `DEBUG`, `NOTICE`, `WARNING`, `CRIT`, `ALERT` 和 `KERNEL`。默认是 `KERNEL`。

```text
Nov 23 10:14:15 hostname: [1234] IN=eth0 OUT=eth0 PROTO=TCP SRC=192.168.1.10 SPT=54321 DPORT=22 LOG="OUTPUT:"
```
