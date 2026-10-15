

## 特殊输入规则

一个普通的防火墙不会允许互联网上的客户端发起连接。所有与互联网接口相关的输入规则都设置了 -k 选项（TCP 头中必须设置 ACK 标志）。这会带来两个问题。然而。第一个问题是，如果你的防火墙将运行 SMTP 守护进程，拒绝所有 SYNC 数据包将导致 SMTP 守护进程挂起。如果互联网上的客户端想通过 SMTP 向你发送邮件，客户端会在你的防火墙上打开 25 端口。你可以通过为 SMTP 端口指定一个特殊的输入规则来绕过此问题。SMTP 规则应指定互联网上的任何人都可以连接到 25 端口，并且仅限 25 端口。该规则可能如下例所示。

```
# Add input rule for Internet -> me for mail (stops at firewall)
ipfwadm -I -a accept -P tcp -S 0.0.0.0/0 -D 194.109.13.150 25
```

此连接将在防火墙处停止，因此不需要相应的输出或转发规则。

### Listing 12.3 Examples of firewall packet filtering rules.

```
# Add output rule for local -> Internet
ipfwadm -O -a accept -P tcp -S 194.109.13.150 -D 0.0.0.0/0
```

此规则为互联网接口定义了一个输出规则。它声明发往互联网上任何目的地的包都被允许发出。此规则仅适用于 TCP 协议的包。

```
# Add input rules for clients -> Internet (will masquerade)
ipfwadm -I -a accept -P tcp -V 193.78.174.33 -S 193.78.174.34 -D 0.0.0.0/0
ipfwadm -I -a accept -P tcp -V 193.78.174.33 -S 193.78.174.35 -D 0.0.0.0/0
```

此规则描述了本地网主机发送到互联网上目的地的包。这些包将由转发规则进行伪装。如你所见，这些包必须在受信任接口 193.78.174.33 上接收（-V 选项）。

最后一个示例向你展示了一个伪装规则。

```
# Add forwarding rules for clients
ipfwadm -F -a masquerade -P tcp -S 193.78.174.34 -D 0.0.0.0/0
ipfwadm -F -a masquerade -P tcp -S 193.78.174.35 -D 0.0.0.0/0
```

如你所见，此处的策略是伪装，因此这些包将被伪装。

拒绝 SYNC 数据包的第二个问题是由 ftp（文件传输协议）造成的。在传输文件时，ftp 会打开两个连接。第一个连接是控制通道，ftp 使用它发送诸如更改目录、获取文件列表等命令。此控制连接由本地网上的机器发起，因此遵循正常流程（输出定向流量）。

然而，当 ftp 客户端检索目录或文件时，ftp 使用其第二个连接，即传输的数据连接。客户端向服务器发送一个端口命令，告诉服务器应为传输数据而打开客户端上的哪个端口。因此，数据连接是反向发起的（从外部进入本地网）。如果所有 SYNC 数据包都被拒绝，防火墙将拒绝此类连接，从而阻止数据传输。

通用解决方案是为此 ftp 数据连接定义一组特殊规则。因为服务器也使用端口 20 作为数据连接的一端，所以你可以通过包含一条接受在该端口号上发起的连接的规则来启用数据传输。更新的 Linux 内核现在完全支持这些特定端口的规则。相关规则在 Listing 12.4 中显示。

即使没有此规则，一些 ftp 客户端也可能成功地从你的主机传输数据。一些 ftp 客户端知道“被动”模式，在该模式下，客户端要求 ftp 服务器为传输数据创建端口。由此产生的传输使用 ACK 数据包完成，避免了 SYNC 限制。

### Listing 12.4 Examples of firewall packet filtering rules for ftp.

```
# Add input rule for Internet -> me for FTP data connection (masqueraded)
ipfwadm -I -a accept -P tcp -S 0.0.0.0/0 20 -D 194.109.13.150 1024:65535

# Add output rules for FTP data connection
ipfwadm -O -a accept -P tcp -S 0.0.0.0/0 20 -D 193.78.174.34 1024:65535
ipfwadm -O -a accept -P tcp -S 0.0.0.0/0 20 -D 193.78.174.35 1024:65535
```

第一条规则指定防火墙互联网接口上的传入数据包。其他规则指定到本地网主机上的传出数据包。请记住，这些数据包是通过防火墙（伪装）防火墙规则转发。

