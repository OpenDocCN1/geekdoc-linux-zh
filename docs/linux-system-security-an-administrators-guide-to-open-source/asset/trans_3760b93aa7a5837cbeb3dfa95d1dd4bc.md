

![](img/7933c44717ab0711177ea7153f959fc5_516_0.png)

## **图 16.4** ftp 的双重连接需求

这会生成一个数据包，其源 IP 地址来自 10.0.0.0 网络，目标端口号设置为 ftp。它将到达 topcat-in（eth1）。因此，编写如下规则：

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 1024:65535 -d 0/0 ftp -j ACCEPT
```

此规则允许数据包通过 input 链。现在我们需要让它通过 forward 链。请注意，我们将源端口限制为特权端口以外的端口。这是一个好主意，为了保险起见，只要可能我们都会这样做。

**伪装规则（Masquerade Rule）。** 我们之前在第 473 页示例 16-31 的步骤 2 中添加了伪装规则。这是一个非特定规则，将通过 *eth0* 将来自 10.0.0.0 到 202.7.1.19 的所有流量进行伪装。接下来要处理的链是 *output* 绑定链。

**FTP 规则 2。** 我们需要允许被 **FTP 规则 1** 接受的数据包通过 *eth1* 进入 *eth0* 的 output 链。请使用以下命令：

```
[root@topcat]# ipchains -A output -i eth0 -p tcp --dport 1024:65535 -d 0/0 ftp -j ACCEPT
```

注意，我们将源指定为 *topcat*，而不是 10.0.0.0 网络。这是因为数据包已经被伪装了。此时，来自内部客户端的 *ftp* 请求将能够穿过防火墙到达互联网上的服务器。

**FTP 规则 3。** 现在我们需要反转这个过程，允许服务器回复客户端。服务器将生成一个数据包，其源端口号设置为 *ftp*（端口 21），目标 IP 地址为 *topcat*。该数据包将到达 *eth0*。因此规则如下：

```
[root@topcat]# ipchains -A input -i eth0 -p tcp -s 0/0 21 -d topcat 1024:65535 -j ACCEPT ! -y
```

由于此传入响应是针对一个被伪装的数据包，该地址将被解除伪装，forward 链将被跳过，并且数据包将被发送到 output 链进行处理。

> **注意**
> 由于 **FTP 规则 3** 发生在 TCP SYN REJECT 规则之后（因为使用了 -A，该规则作为第 472 页示例 16-30 中的第一个命令输入），来自互联网的 ftp 连接请求永远不会到达此规则。但我们非常谨慎，因此在此规则中添加了 ! -y。我们将对 **FTP 规则 7** 也这样做。

**FTP 规则 4。** 我们需要允许数据包传回最初请求 *ftp* 服务的内部主机。使用以下命令完成：

```
[root@topcat]# ipchains -A output -i eth1 -p tcp -s 0/0 ftp -d 10.0.0.0/8 1024:65535 -j ACCEPT
```

注意，我们可以再次指定真实的内部网络地址（这次作为目标地址）。此时，ftp 连接将正常工作。你将能够通过 ftp 登录。试试看！然后，尝试执行 *ls* 并观察它失败！让我们接下来修复这个问题。

**FTP 规则 5。** 客户端接下来想要做的是建立数据连接。当客户端执行 *ls*、*get*、*put* 等命令时，它将生成一个 *ftp-data*（端口号 20）数据包。此规则与 **FTP 规则 1** 中的规则相同，只是端口不同。

```
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 1024:65535 -d 0/0 ftp-data -j ACCEPT
```

一旦数据包通过此规则，它将进入 forward 链。我们已经在第 476 页的伪装规则中设置好该规则，因此没有其他需要做的事情。数据包将通过 forward 链，源 IP 地址被伪装，然后进入 output 链。因此，我们将接下来添加该规则。

**FTP 规则 6。** 此步骤与 **FTP 规则 2** 相同，只是端口不同。规则如下：

```
[root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat 1024:65535 -d 0/0 ftp-data -j ACCEPT
```

此时，互联网 ftp 服务器可以接收来自我们内部客户端的 ftp-data 请求。接下来我们需要允许服务器响应该请求。

**FTP 规则 7。** 此步骤与 **FTP 规则 3** 相同，只是端口是 ftp-data。

```
[root@topcat]# ipchains -A input -i eth0 -p tcp -s 0/0 21 -d topcat 1024:65535 -j ACCEPT ! -y
```

再次强调，在此链之后会发生解除伪装，forward 链被跳过，处理将传递给 output 链。

**FTP 规则 8。** 此规则与 **FTP 规则 4** 相同，只是端口不同。

```
[root@topcat]# ipchains -A output -i eth1 -p tcp -s 0/0 ftp-data -d 10.0.0.0/8 1024:65535 -j ACCEPT
```

完成了！现在内部网络上的用户可以通过 ftp 访问互联网（那是很多工作——要求加薪吧）。

## **允许 DNS、POP3 和网络访问**

从概念上讲，这些服务所需的每条规则都与 ftp 类似。主要区别在于我们不会有两个不同的端口要处理。DNS 和 POP3 都使用 TCP 和 UDP，因此我们需要处理这一点。我们将在单独的小节中介绍每项服务。

### **DNS 规则。**

我们需要允许来自内部主机和 topcat 的 DNS 查询到达互联网中的 DNS 服务器。DNS 的端口号是 53，其在 /etc/services 中的等效名称是 domain。示例 16-33 提供了必要的规则。再次强调，我们按照第 475 页图 16.4 所示的事件流程编写规则。（左侧的数字仅供描述使用。）

- 规则 1 到 4 接受通过 eth1 进入 input 链的内部网络 DNS 查询。规则 5 到 8 允许这些查询通过 eth0 发送到互联网。规则 9 到 11 允许 DNS 响应通过 eth0 返回。请注意，我们再次禁止 TCP SYN 数据包。对于 UDP 我们无法做到这一点。规则 12 到 15 允许 DNS 响应流回内部客户端。

**示例 16-33 允许 DNS 查询的规则**

1. [root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d dnssvr1 domain -j ACCEPT
2. [root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d dnssvr2 domain -j ACCEPT
3. [root@topcat]# ipchains -A input -i eth1 -p udp -s 10.0.0.0/8 -d dnssvr1 domain -j ACCEPT
4. [root@topcat]# ipchains -A input -i eth1 -p udp -s 10.0.0.0/8 -d dnssvr2 domain -j ACCEPT
5. [root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d dnssvr1 domain -j ACCEPT
6. [root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d dnssvr2 domain -j ACCEPT
7. [root@topcat]# ipchains -A output -i eth0 -p udp -s topcat -d dnssvr1 domain -j ACCEPT
8. [root@topcat]# ipchains -A output -i eth0 -p udp -s topcat -d dnssvr2 domain -j ACCEPT
9. [root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s dnssvr1 domain -j ACCEPT ! -y
10. [root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s dnssvr2 domain -j ACCEPT
11. [root@topcat]# ipchains -A input -i eth0 -p udp -d topcat -s dnssvr2 domain -j ACCEPT
12. [root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s dnssvr1 domain -j ACCEPT
13. [root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s dnssvr2 domain -j ACCEPT
14. [root@topcat]# ipchains -A output -i eth1 -p udp -d 10.0.0.0/8 -s dnssvr1 domain -j ACCEPT
15. [root@topcat]# ipchains -A output -i eth1 -p udp -d 10.0.0.0/8 -s dnssvr2 domain -j ACCEPT

*POP3 规则。* 接下来我们将添加电子邮件访问的规则。由于 POP3 使用 SMTP（端口 25，也称为 smtp）发送电子邮件，因此我们也需要包含这些。我们在示例 16-34 中列出了 POP3 的规则。与 DNS 一样，POP3 使用 UDP 和 TCP，因此我们应该允许它们。

**示例 16-34 允许 POP3 检索电子邮件的规则**

- [root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8 -d mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A input -i eth1 -p udp -s 10.0.0.0/8 -d mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat -d mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A output -i eth0 -p udp -s topcat -d mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A input -i eth0 -p tcp -d topcat -s mail pop-3 -j ACCEPT ! -y
- [root@topcat]# ipchains -A input -i eth0 -p udp -d topcat -s mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A output -i eth1 -p tcp -d 10.0.0.0/8 -s mail pop-3 -j ACCEPT
- [root@topcat]# ipchains -A output -i eth1 -p udp -d 10.0.0.0/8 -s mail pop-3 -j ACCEPT

