
然而，你很快就会看到 Red Hat 防火墙配置工具仅为 FTP 服务打开 TCP 通信，并且第 1 章中配置的默认 vsFTP 服务器在这种情况下工作正常。

## TABLE 4-5
### Common TCP/IP Ports

| Port | Description |
|------|-------------|
| 21 | FTP |
| 22 | Secure Shell (SSH) |
| 23 | Telnet |
| 25 | Simple Mail Transfer Protocol (SMTP), e.g., Postfix, sendmail |
| 53 | Domain Name Service servers |
| 80 | Hypertext Transfer Protocol (HTTP) |
| 88 | Kerberos |
| 110 | Post Office Protocol, version 3 (POP3) |
| 139 | Network Basic Input/Output System (NetBIOS) session service |
| 143 | Internet Mail Access Protocol (IMAP) |
| 443 | HTTP, secure (HTTPS) |

## A Focus on iptables

`iptables` 背后的理念基于 "`chains`"。这些是应用于每个网络数据包的一组规则，彼此链接在一起。每条规则做两件事：它指定数据包必须满足的条件以匹配规则，并指定数据包匹配时的操作。

`iptables` 命令使用以下基本格式：

```
iptables -t tabletype <action direction> <packet pattern> -j <what to do>
```

现在逐步分析此命令。首先是 `-t tabletype` 开关。`iptables` 有两个基本 `tabletype` 选项：

- `filter` Sets a rule for filtering packets.
- `nat` Configures Network Address Translation, also known as masquerading, discussed later in this chapter.

默认值为 `filter`；如果未指定 `-t tabletype`，`iptables` 命令假定命令作为数据包过滤规则应用。

接下来是 `<action direction>`。`iptables` 规则有四个基本操作：

- `-A (--append)` Appends a rule to the end of a chain.
- `-D (--delete)` Deletes a rule from a chain. Specify the rule by the number or the packet pattern.
- `-L (--list)` Lists the currently configured rules in the chain.
- `-F (--flush)` Flushes all of the rules in the current `iptables` chain.

如果你要追加到 (`-A`) 或从 (`-D`) 链中删除，你希望将其应用于沿三个方向之一传输的网络数据：

- `INPUT` All incoming packets are checked against the rules in this chain.
- `OUTPUT` All outgoing packets are checked against the rules in this chain.
- `FORWARD` All packets being sent to another computer are checked against the rules in this chain.

通常，每个方向都是一个链的名称。接下来，你需要配置一个 `<packet pattern>`。所有 `iptables` 防火墙都会将每个数据包与此模式进行检查。最简单的模式是按 IP 地址：

- `-s ip_address` All packets are checked for a specific source IP address.
- `-d ip_address` All packets are checked for a specific destination IP address.

数据包模式可以更复杂。在 TCP/IP 中，数据包使用 TCP、UDP 或 ICMP 协议传输。你可以使用 `-p` 开关指定协议，后跟目标端口 (`--dport`)。例如，`-p tcp --dport 80` 扩展会影响尝试使用 HTTP 连接的网络外部用户。

一旦 `iptables` 命令找到数据包模式匹配，它需要知道对该数据包做什么，这就引出了命令的最后一部分，`-j <what to do>`。有三个基本选项：

- `DROP` The packet is dropped. No message is sent to the requesting computer.
- `REJECT` The packet is dropped. An error message is sent to the requesting computer.
- `ACCEPT` The packet is allowed to proceed as specified with the `-A` action: `INPUT`, `OUTPUT`, or `FORWARD`.

看一些如何使用 `iptables` 命令配置防火墙的示例。第一步始终是查看当前配置，使用以下命令：

```
# iptables -L
```

如果 `iptables` 配置正确，它应返回三个不同类别的链规则：`INPUT`、`FORWARD` 和 `OUTPUT`。更多示例在第 10 章中描述。

## Keep That Firewall in Operation

基于 `iptables` 命令的 Linux 防火墙基于同名服务。要查看当前规则，请运行 `iptables -L` 命令。假设你看到的只是以下空白规则列表：

```
Chain INPUT (policy ACCEPT)

target     prot opt source            destination

Chain FORWARD (policy ACCEPT)

target     prot opt source            destination

Chain OUTPUT (policy ACCEPT)

target     prot opt source            destination
```

`iptables` 服务可能未运行。确保启动它，并确保在下次重新启动后防火墙正在运行，运行以下命令：

```
# /etc/init.d/iptables start

# chkconfig iptables on
```

Red Hat 防火墙使用的规则基于 `/etc/sysconfig/iptables` 文件，在下一节中描述。

## The Default RHEL 6 Firewall

当前 RHEL 6 防火墙显示在 `iptables -L` 命令的输出中。默认 `server1.example.com` 系统上的输出显示在图 4-4 中。防火墙规则根据数据的方向分为三个类别。`INPUT` 规则应用于目标为本地系统的数据包。`FORWARD` 规则限制通过本地系统到另一系统的数据。`OUTPUT` 规则可能限制从本地系统发出的数据。

## 图 4-4

默认 RHEL 6 防火墙规则

```
[root@server1 ~]# iptables -L

Chain INPUT (policy ACCEPT)

target     prot opt source               destination

ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED

ACCEPT     icmp --  anywhere             anywhere

ACCEPT     all  --  anywhere             anywhere

ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh

REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)

target     prot opt source               destination
```
