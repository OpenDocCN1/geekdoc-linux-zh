
## 使用 iptables 进行 NAT 或 IP 伪装

如 iptables 示例所述，您可以使用源网络地址转换（SNAT）或 IP 伪装（MASQUERADE）使 LAN 上具有私有 IP 地址的计算机通过 iptables 防火墙访问 Internet。如果您的 Internet 连接具有静态 IP 地址，请选择 SNAT；如果 IP 地址是动态分配的，则选择 MASQUERADE。

当您创建 MASQUERADE 或 SNAT 规则时，它将被添加到 NAT 表和 POSTROUTING 链中。对于 MASQUERADE，您必须提供接口的名称（如 eth0、ppp0 或 slip0）以标识通往 Internet 或其他外部网络的路由。对于 SNAT，您还必须标识接口的实际 IP 地址。以下是 MASQUERADE 规则的示例：

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

以下是 SNAT 规则的示例：

```
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 12.12.12.12
```

如果您有多个提供通往 Internet 路由的地址，可以添加多个源地址（例如，`--to-source 12.12.12.12,12.12.12.254`）。尽管 MASQUERADE 使用了一些额外的开销，但如果您使用拨号连接访问 Internet 且每次连接的 IP 地址都会更改，则可能需要改用 MASQUERADE 而不是 SNAT。

请记住，您需要确保内核中已打开 IP 转发。（默认情况下是关闭的。）要临时打开它，您可以执行以下操作：

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

如果您需要动态 IP 地址，请打开该服务：

```
# echo 1 > /proc/sys/net/ipv4/ip_dynaddr
```

## 使用 iptables 作为透明代理

使用 REDIRECT 目标，您可以使防火墙计算机上的特定端口流量被定向到另一个端口。使用此功能，您可以将本地 LAN 上的主机计算机定向到防火墙计算机上的代理服务，而这些主机并不知情。

以下是 iptables 命令的一组命令行选项的示例，该选项可使对 Web 服务（端口 80）的请求被定向到代理服务（端口 3128）：

```
-t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 3128
```

您只能在 nat 表中的 PREROUTING 和 OUTPUT 链中使用 REDIRECT 目标。您还可以指定一系列端口号以将重定向分散到多个端口号上。

## 使用 iptables 进行端口转发

如果您只有一个静态 IP 地址，但希望使用防火墙计算机之外的计算机提供 Web、FTP、DNS 或其他服务怎么办？您可以使用动态网络地址转换（DNAT）功能将防火墙上特定端口的流量定向到另一台计算机。

例如，如果您希望所有发往防火墙计算机（-d 15.15.15.15）的对 Web 服务（端口 80）的请求都被定向到 LAN 上的另一台计算机（如 10.0.0.25），您可以使用以下 iptables 命令：

```
# iptables -t nat -A PREROUTING -p tcp -d 15.15.15.15 -dport 80 \
-j DNAT --to-destination 10.0.0.25
```

（请注意，前面的示例实际上应出现在同一行。反斜杠表示在下一行继续。）

您还可以通过提供一系列 IP 地址（例如，--to-destination 10.0.0.1-10.0.0.25）来分担您转发的服务的负载。同样，您也可以将请求定向到一系列端口。

## 使用 iptables 进行日志记录

使用 LOG 目标，您可以记录符合您选择的条件的包的信息。特别是，您可能希望使用此功能来记录似乎在某种程度上不合适的包。换句话说，如果由于某种原因您不想丢弃一个包，您可以只记录其活动，然后再决定是否需要纠正某些问题。

LOG 目标将日志信息定向到 Red Hat Linux 中用于日志记录的标准工具：dmesg 和 syslogd。以下是使用 LOG 目标的规则示例：

```
-A FORWARD -p tcp -j LOG --log-level info
```

代替 info，您可以使用 syslogd 可用的以下任何日志级别：emerg、alert、crit、err、warning、notice、info 或 debug。使用以下 --log-prefix 选项，您还可以将信息添加到此日志操作产生的所有消息的前面：

```
-A FORWARD -p tcp -j LOG --log-level info --log-prefix "Forward INFO "
```

## 增强您的 iptables 防火墙

您可以通过多种方式修改或扩展本章中给出的 iptables 示例。iptables 具有极大的灵活性。

当您实际创建自己的 iptables 防火墙时，您应参考 iptables 手册页（输入 man iptables）以获取选项、匹配方式、输入地址方式和其他细节的详细描述。我还推荐 Oskar Andreason 的优秀 iptables 教程（http://iptables-tutorial.frozentux.net）。

以下是使用 iptables 功能的几个提示：

- **减少规则** — 尝试通过减少规则数量来提高性能。使用子链可以防止数据包看到不适用于它的规则。
- **处理分片** — 使用 -f 选项来引用被拆分为分片的数据包的第二个及后续数据包。通常，对于没有第一个数据包分片的第二个和第三个分片，安全地不丢弃它们，因为它们不会被重新组装。如果您使用 NAT，分片在过滤之前会被组装，因此您不应该出现未过滤分片被发送通过的问题。
- **相反** — 要使规则与其相反，请使用感叹号（！）。
- **所有接口** — 要匹配某类接口的所有接口，请使用加号（+），如 eth+。
- **阻止连接** — 使用 --syn 选项阻止 SYN 数据包（即请求连接的那些数据包）。此选项仅适用于 TCP 数据包。
- **限制** — 使用 --limit 选项限制导致日志消息的匹配的速率。此选项允许匹配每秒仅产生有限次数的消息（默认每小时三次，突发五次）。
- **DOS 攻击** — 您可以使用 --limit 选项来减少 DOS 攻击的影响，但它并不能完全阻止它们。只要流量指向您的服务器，您的网络带宽就会被耗尽，并且机器仍会利用资源来忽略数据。
- **表类型** — 默认表类型是 *过滤*。其他类型的表是 *nat*（用于 IP 伪装）和 *mangle*（用于修改数据包）。要使用 *过滤* 以外的表，您必须添加 `-t table_type` 选项，其中 *table_type* 为 *nat* 或 *mangle*。

## 从日志文件检测入侵

为系统准备抵御黑客攻击只是战斗的一部分。您还必须在攻击发生时识别出黑客攻击。了解 Red Hat Linux 记录重要事件的各种日志文件对于实现这一目标至关重要。Red Hat Linux 系统的日志文件可以在 /var/log 目录中找到。

Red Hat Linux 附带一个系统日志窗口（redhat-logview 命令），您可以使用它从 GUI 查看和搜索关键系统日志文件。要打开系统日志窗口，请从主桌面菜单中单击 系统工具 → 系统日志。图 14-3 显示了系统日志窗口的示例。

要查看特定日志文件，请单击左侧列中的日志名称。如果您正在查找特定消息或问题，请在“筛选条件”框中输入关键字，然后单击筛选。仅显示包含该词的行。大写字母有区别，因此使用筛选器搜索“Mem”时找不到“mem”。单击重置以再次显示整个文件。

表 14-6 包含在系统日志窗口中显示的日志文件列表，以及 /var/log 目录中可能引起您兴趣的其他文件。（* 表示不在系统日志窗口中的日志文件。请直接从 /var/log 访问这些文件。）

![](img/27a85d56d393921ced6412ae6e8336bf_546_0.png)

图 14-3：在系统日志窗口中显示系统日志文件。

## 表 14-6：/var/log 目录中的日志文件

| 系统日志名称 | 文件名 | 描述 |
|---|---|---|
| 启动日志 | boot.log | 包含指示哪些系统服务已成功启动和关闭以及哪些（如有）启动或停止失败的消息。 |
| Cron 日志 | cron | 包含来自 crond 的状态消息，crond 是一个定期运行计划作业（如备份和日志文件轮转）的守护进程。 |
| 内核启动日志 | dmesg | 系统启动时内核打印的消息记录。 |
| FTP 日志 | xferlog | 使用 wu-ftp FTP 服务传输的文件信息。 |
| Apache 访问日志 | httpd/access_log | 记录来自您的 Apache Web 服务器的信息请求。 |
| Apache 错误日志 | httpd/error_log | 记录客户端尝试访问您的 Apache Web 服务器数据时遇到的错误。 |
