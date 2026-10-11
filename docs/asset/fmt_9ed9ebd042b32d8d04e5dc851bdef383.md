
`[root@server ~]# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`

在完成所有的检查和操作后，我们启用了 IP 转发（NAT 所必需）以及 SYN cookie 保护，并且开启了防止防火墙受 ICMP 广播包攻击（Smurf 攻击）的开关。

```
[root@server ~]# echo 1 > /proc/sys/net/ipv4/ip_forward
[root@server ~]# echo 1 > /proc/sys/net/ipv4/tcp_sync_cookies
[root@server ~]# echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```

到此时，我们已经为简单环境配置了一个可以运行的防火墙。如果没有任何服务器，我们可以保存此配置并认为大功告成了。另一方面，假设我们有两个想要通过此防火墙运行的应用程序：内网中一台我们希望通过 SSH 访问远程位置的 Linux 系统，以及一台我们想要从上面使用 BitTorrent 的 Windows 系统。让我们先从 SSH 的情况开始。

要让端口通过防火墙可用，我们需要定义一条规则，写道：“如果 `eth0`（面向互联网的接口）上的任何数据包是 TCP 协议且目标端口为 22，则将其目标 IP 地址更改为 `172.16.1.3`。” 这通过在 `PREROUTING` 链上使用 `DNAT` 操作来实现，因为我们希望在数据包被任何其他链看到之前更改其 IP 地址。

我们需要解决的第二个问题是如何在 `FORWARD` 链上插入规则，允许任何目标 IP 为 `172.16.1.3` 且目标端口为 22 的数据包通过。关键词是插入 (`-I`)。如果我们将规则追加 (`-A`) 到 `FORWARD` 链，数据包将被重定向到 `block` 链，因为规则 `-A FORWARD -j block` 会先被应用。

```
[root@server ~]# iptables -t nat -A PREROUTING -i eth0 \
  -p tcp --dport 22 -j DNAT --to-destination 172.16.1.3
[root@server ~]# iptables -I FORWARD -p tcp -d 172.16.1.3 --dport 22 -j ACCEPT
```

我们可以应用类似的思路让 BitTorrent 工作。假设 Windows 机器使用端口 6881-6889。

```
[root@server ~]# iptables -t nat -A PREROUTING -i eth0 \
  -p tcp --dport 6881:6889 -j DNAT --to-destination 172.16.1.3
[root@server ~]# iptables -I FORWARD -p tcp -d 172.16.1.3 --dport 6881:6889 -j ACCEPT
```

# 第 14 章：本地安全 359

必须接受某种程度的风险——你所接受的风险水平将决定你在时间和金钱上的投入。例如，一个在低带宽链上发布你假期照片的 Web 服务器，其风险低于一个为华尔街处理巨额金融交易的服务器。

“越简单越好”是工程学的 101 逻辑——简单的系统更不容易出现问题，更容易理解，而且不可避免地更加可靠。保持服务器的简单是一个理想的目标。

## 风险的常见来源

安全是对风险的缓解。每一个缓解风险的努力都伴随着相应的成本。成本并不一定是财务上的；它们可以表现为访问限制、功能丧失或时间消耗。作为管理员，你的工作是在缓解风险的成本与风险被利用可能造成的潜在损害之间取得平衡。

以 Web 服务器为例。托管一个可以被探测、攻击并可能被利用的服务，这种风险是任何网络可用性固有的。然而，你可能会发现，只要维护 Web 服务器 并在安全问题出现时及时补丁，暴露的风险就是很小的。如果运行 Web 服务器的收益足以抵消你维护它的成本，那么它就是一项值得的尝试。

在本节中，我们将查看常见的风险来源，并研究你可以做什么来缓解这些风险。

## SetUID 程序

SetUID 程序是在其权限中设置了特殊属性（标记）的可执行文件，它允许用户在可执行文件所有者的环境中运行该程序。这使得管理员能够向普通用户提供更高权限的应用或文件，而无需授予任何管理员权限。此类程序的示例是 `ping`。由于创建原始数据包受限于 `root` 用户（创建原始数据包允许应用程序在包内添加任何内容，包括攻击），`ping` 必须在启用 SetUID 位且所有者设置为 `root` 的情况下运行。因此，例如，尽管你启动了 `ping` 程序，该程序仍可以在 `root` 用户环境中运行，其目的是向网络发送互联网控制消息协议（ICMP）数据包。这种工具的用途被称为“SetUID root”。

以 `root` 权限运行的程序的问题在于，它们也有义务对安全保持高度的“意识”。普通用户无法使用该程序在系统上执行任何危险的操作。这意味着需要在程序中编写许多检查，并且必须仔细移除潜在的漏洞。理想情况下，这些程序应该是小型的且只做一件事。这使得更容易评估可能损害系统或允许用户获得不应拥有的权限的潜在漏洞。

# Linux 管理：入门指南

从日常角度来看，让系统尽可能保留少量的 SetUID 程序符合管理员的最大利益。这里的风险平衡是用户对功能/服务的可用性与坏事发生的可能性之间的权衡。对于 `ping`、`mount`、`traceroute` 等一些常见程序，相对于它们为系统带来的价值，其风险很低。众知的 SetUID 程序（如 X Window System）提供了中等风险；然而，考虑到 X Window System 的暴露性，它不太可能是任何问题的根源。如果你运行的是纯服务器环境且不需要 X Window System，那么移除它也无害处。

Web 服务器执行的 SetUID 程序始终是一件坏事。对于这类应用程序要格外小心，并寻找替代方案。其暴露性大得多，因为网络输入（可能来自任何地方）可能会触发此类应用程序及其执行。

如果你发现必须以 `root` 权限 SetUID 运行某个应用程序，另一种替代方案是查找是否可以在 `chroot` 环境中运行该程序（在本章稍后的“使用 chroot”部分进行讨论）。

## 查找和创建 SetUID 程序

SetUID 程序具有一种特殊属性，内核使用该属性来确定是否应该覆盖授予应用程序的默认权限。当你处理目录列表时：

```
[root@server ~]# ls -1 /bin/ping
-rwsrxr-x. 1 root root 43160 Jul 13 2018 /bin/ping
```

与 `ping` 一样，权限字段中的第四字符是 `s`，该应用程序是 SetUID 的。如果文件的所有者是 `root`，那么该应用程序就是 SetUID root。在 `ping` 的情况下，我们可以看到它将带有 `root` 权限运行。

这是另一个例子——X（X Window System）程序：

```
[root@server ~]# ls -1 /usr/bin/Xorg
-rws--x--x. 1 root root 1667576 Oct 13 11:31 /usr/bin/Xorg
```

与 `ping` 一样，权限的第四个字符是 `s`，所有者是 `root`。因此，`Xorg` 程序是 SetUID root。

要确定一个运行中的进程是否为 SetUID，你可以使用 `ps` 命令同时查看进程的实际用户和有效用户，例如：

```
[root@server ~]# ps ax -o pid,user,user,comm
```

这将输出所有运行的程序及其进程 ID (`PID`)、有效用户 (`euser`)、实际用户 (`user`) 和命令名称 (`comm`)。如果有效用户与实际用户不同，它可能是一个 SetUID 程序。

# 第 14 章：本地安全 361

注意 某些应用程序由 `root` 用户启动，请将它们赋予较低权限的用户以提高安全性。例如，Apache Web 服务器可能由 `root` 用户启动以绑定传输控制协议（TCP）端口 80（特权用户可以绑定低于 1024 的端口），但它以非用户用户（通常是“nobody”、“apache”或“www”）启动线程。使用 4 可以开启 SetUID 位。使用 2 将启用 SetGID 位，它提供组权限而不是用户权限。

例如，如果我们有一个 `myprogram` 并希望将其 SetUID root，我们执行以下操作：

```
[root@server ~]# chmod root myprogram
[root@server ~]# chmod 4755 myprogram
[root@server ~]# ls -l root
-rw-xr-xr- 1 root root 43160 Jul 13 2018 myprogram
```
