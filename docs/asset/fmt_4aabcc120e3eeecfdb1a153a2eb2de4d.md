
### firewall-cmd 示例

```
[master@fedora-server ~]$ firewall-cmd --get-zone-of-interface=ens10
```

列出预定义的服务：

```
[master@fedora-server -]$ firewall-cmd --get-services
```

列出预定义的 ICMP 类型：

```
[master@fedora-server -]$ firewall-cmd --get-icmypes
```

查询 firewalld 中 drop 区域的服务：

```
[master@fedora-server -]$ sudo firewall-cmd --list-services --zone=drop
```

列出 home 区域的服务：

```
[master@fedora-server -]$ sudo firewall-cmd --list-services --zone=home
```

列出默认区域中的所有内容：

```
[master@fedora-server -]$ sudo firewall-cmd --list-all
```

列出 external 区域中的所有内容：

```
[master@fedora-server -]$ sudo firewall-cmd --list-all --zone=external
```

假设 home 区域当前未启用 https 服务，使用 `firewall-cmd` 为该区域永久启用它：

```
[master@fedora-server -]$ sudo firewall-cmd --permanent \
--add-service=https --zone=home
```

运行以下命令以在不中断任何当前连接的情况下重载防火墙规则：

```
[master@fedora-server -]$ sudo firewall-cmd --reload
```

通过从 home 区域中删除 https 服务来撤销上一个命令：

```
[master@fedora-server -]$ sudo firewall-cmd --remove-service=https \
--zone=home
```

将端口 80 上的所有流量转发到 IP 地址为的另一台服务器的 443 端口。

## 简单防火墙：iptables

在本节中，我们将从两种情况的“拒绝所有”防火墙开始：一种是未配置任何服务器，另一种是在同一网络内但配置了某些服务器。在第一种情况下，我们假设一个包含两个部分的简单网络：内部是 `10.1.1.0/24` 网络（`eth1`），外部是互联网（`eth0`）。我们所说的“服务器”是指任何可以接受连接到它以提供服务的节点。例如，这可能意味着一个运行 ssh 守护进程的 Linux 系统，或者一个运行 Web 服务器的 Windows 服务器。

让我们从没有需要支持的服务器的情况开始。

首先，我们需要确保 NAT 模块已加载，并且 NAT 的 FTP 支持也已加载。我们通过 `modprobe` 命令来实现：

```
[master@server ~]$ sudo modprobe iptables_nat
[master@server ~]$ sudo modprobe ip_nat_ftp
```

加载了必要的模块后，我们为所有链（chains）定义了默认策略。对于 filter 表中的 INPUT、FORWARD 和 OUTPUT 链，我们将目标分别设置为 DROP、DROP 和 ACCEPT。对于 POSTROUT 和 PREROUTING 链，我们将它们的默认策略设置为 ACCEPT。这是 NAT 正常工作的必要条件。

```
[master@server ~]$ sudo iptables -P INPUT DROP
[master@server ~]$ sudo iptables -P FORWARD DROP
[master@server ~]$ sudo iptables -P OUTPUT ACCEPT
[master@server ~]$ sudo iptables -t nat -P POSTROUT ACCEPT
[master@server ~]$ sudo iptables -t nat -P PREROUTING ACCEPT
```

默认策略到位后，我们需要定义基础防火墙规则。我们要实现的目标是：允许内部网络（`eth1`）的用户或节点连接互联网，但不允许互联网连接回内部。为了实现这一点，我们定义了一个名为“block”的新链，用于分组状态跟踪规则。该链中的第一条规则规定，任何属于已建立连接或与已建立连接相关的包都允许通过。第二条规则规定，为了创建一个数据包，其源不能来自 `eth0`（面向互联网的）接口。如果数据包不匹配上述任一条规则，最后的规则将强制丢弃该包。

```
[master@server ~]$ sudo iptables -N BLOCK
[master@server ~]$ sudo iptables -A BLOCK -m state \
--state ESTABLISHED,RELATED -j ACCEPT
[master@server ~]$ sudo iptables -A BLOCK -m state \
--state NEW -i eth0 -j ACCEPT
[master@server ~]$ sudo iptables -A BLOCK -j DROP
```

建立拦截链后，我们需要在 INPUT 和 FORWARD 链中调用它。我们不需要担心 OUTPUT 链，因为它们只来自防火墙自身的包。相反，INPUT 和 FORWARD 链需要经过检查。记住，在进行 NAT 时，INPUT 链不会被触发，因此我们需要——

我们可以应用类似的思路让 BitTorrent 运行。假设 Windows 将使用 IP `172.16.1.2` 的 BitTorrent。BitTorrent 协议使用 `6881–6889` 端口处理返回客户端的连接。因此，我们在 `iptables` 命令中使用端口范围设置，如下：

```
$ sudo iptables -t nat -A PREROUTING -i eth0 \
-p tcp --dport 6881:6889 -j DNAT --to-destination 172.16.1.2
$ sudo iptables -I FORWARD -p tcp -d 172.16.1.2 --dport 6881:6889 -j ACCEPT
```

大搞定！我们现在有了一个可以工作的防火墙，并为网络内部的 SSH 服务器和 BitTorrent 用户的支持。

## 总结

在本章中，我们讨论了 Linux 防火墙 Netfilter 的细节。特别是，我们讨论了 `iptables`、`ip6tables` 和 `nft` (`nftables`) 命令的使用。有了这些信息，你应该能够构建、维护和管理基于 Linux 的防火墙了。

虽然这可能有些废话之嫌，但 Netfilter 是一个令人印象深刻复杂且丰富的系统！人们已经编写了专门介绍 Netfilter 和防火墙的书；因此，你应该将本章对该主题的涵盖仅视为一个入门介绍——一种引起你胃口的方式。你可以在 `www.netfilter.org` 项目网站上学到更多关于 Netfilter 的知识。

# 第 15 章：本地安全

本地安全解决的是攻击者需要在系统本身执行某些操作以获取提升权限的攻击问题。

缺乏适当本地安全控制的系统可能会引发真实问题并导致攻击。教育环境和学校通常是此类攻击的温床：学生可能需要访问服务器来完成作业和进行其他学术工作，但当学生感到无聊、测试其访问边界和个人创造力，或者他们有时不考虑行为的后果和影响时，这种情况就会对系统构成威胁。

本地安全问题也会由网络安全问题触发。如果网络安全问题导致攻击者能够调用服务器上的任何程序或应用程序，攻击者就可以利用本地安全漏洞不仅让自己获得对服务器的完全访问权限，而且——对于那些使用这些方法获取未经授权访问的“脚本小子”（script kiddies）也是如此。本章介绍了保持系统安全的基础知识。安全是一个不断演变的领域，因此你应该跟上最新动态。

在本章中，我们查看了常见的风险来源，并研究了你可以做些什么来缓解这些风险。

### 常见风险来源

安全是对风险的规避。每一项缓解风险的努力都伴随着相应的代价。代价并不总是金钱上的；它们可能表现为访问限制、功能丧失或时间流逝。作为管理员，你的工作之一就是平衡缓解风险的成本与风险被利用后可能造成的潜在损害。例如，考虑一个 Web 服务器。运行一个可以被探测、探测和可能被利用的服务，这种风险是面向公众或公开访问的 Web 服务器所固有的。然而，你可能会发现，由于 Web 服务器得到了良好维护并在出现安全问题时立即进行了修补，暴露的风险非常低。如果一个 Web 服务器的益处足以维持其运行，那么它就是值得的投入。

### SetUID 程序
