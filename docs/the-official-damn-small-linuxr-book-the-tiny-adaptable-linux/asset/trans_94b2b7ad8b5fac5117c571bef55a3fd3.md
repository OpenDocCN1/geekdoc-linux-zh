
另一个独立的防火墙。有关使用 rc.firewall 配置 DMZ 或其他更复杂安排的更多信息，请参阅本项目的 Linux 防火墙配置页面 (http://lfw.sourceforge.net/config.html)。

## 启动你的防火墙

编辑好 rc.firewall 文件后，你可以通过手动运行 rc.firewall 脚本来试用新的防火墙配置，如下所示：

```
# /opt/rc.firewall
-> Projectfiles.com Linux Firewall version 2.0rc9 running.
-> Performing sanity checks..... [ PASSED ]
-> Building firewall.... [ DONE ]
-> Successfully secured the following addresses: 10.0.0.100
```

上面示例中没有错误提示。请确保 rc.firewall 文件中的信息格式正确。要查看防火墙上当前设置的规则，请使用以下方式运行 iptables 命令：

```
# /sbin/iptables -L
Chain INPUT (policy DROP)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:www
ACCEPT     udp  --  anywhere             anywhere             state NEW udp dpt:www
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ftp
ACCEPT     udp  --  anywhere             anywhere             state NEW udp dpt:fsp
...
```

iptables 的部分输出显示了防火墙 INPUT 链的处理情况。策略是丢弃任何传入的连接请求，除非该连接与已建立的连接相关（ presumably 由防火墙后面的客户端发起）。然而，最后四条条目显示，来自任何地方的新传入连接将被允许建立，用于 tcp 和 udp www（端口 80）连接，以及 tcp 和 udp ftp 和 fsp（端口 21）连接。（FSP 协议类似于匿名 FTP，也在端口 21 上接受连接。）

此时，你可以通过登录另一台计算机（在你的局域网或互联网上）并尝试连接服务器来确保可以连接到你的 XAMPP 服务器。要检查 Web 服务，请将你的 Web 浏览器指向服务器的 IP 地址（如 http://10.0.0.100，前面已描述）。或者你可以连接 FTP 服务（例如，ftp://nobody@10.0.0.100 并输入前面创建的密码）。据推测，你将使用 FTP 向 Web 服务器添加内容或向用户提供文件下载服务。

## 配置你的 XAMPP 服务器

用于管理 XAMPP 服务器的工具也包含在 XAMPP 软件包中。与许多 Linux 服务一样，XAMPP 软件包中的大多数服务都可以使用纯文本文件进行配置。然而，还有几个图形化工具可用于通过浏览器管理 XAMPP。设置服务器的另一部分是为其分配静态 IP 地址，以便寻找你的 Web 服务器的人可以找到它。

### 设置你的网络接口

对于桌面系统，在启动时由 DHCP 服务分配一个任意 IP 地址通常工作得很好。然而，对于你希望人们找到的 Web 服务器，你通常希望分配一个永久的 IP 地址，该地址不会在每次重启时发生变化。

如果你创建 Web 服务器用于临时情况（如在课堂环境中），你可以简单地让 DHCP 服务器分配服务器的 IP 地址。然后，你可以告诉你的客户（或学生）该 IP 地址是什么以便他们连接到你的服务器。然而，对于更永久的 Web 服务器，你需要分配一个静态 IP 地址。

要在家庭或小型企业中运行永久 Web 服务器，你可能需要联系你的互联网服务提供商，申请一个静态 IP 地址并为你的服务器购买一个域名。ISP（或其他域名注册商）将收取每年维护互联网域名注册的费用，并且可能还会收取静态 IP 地址的费用。

无论你是从 ISP 获取静态 IP 地址和 DNS 名称，还是只是在家庭或企业防火墙后面使用一个私有的静态 IP 地址（这对你来说是免费的），你都可以使用 DSL Netconfig 工具来尝试你的静态 IP 地址。

从 DSL 桌面，选择 System→ Net Setup→ netcardconfig（假设你为有线以太网连接配置服务器）。然后，按以下方式配置你的静态 IP 地址：

- 1. 当被问及是否使用 DHCP 广播时，选择 No。你将被要求输入以太网接口的 IP 地址（很可能是 eth0）。
- 2. 输入 ISP 分配的 IP 地址或私有 IP 地址，然后选择 OK。（如果你仅在局域网上使用 Web 服务器，请从未被使用且未被本地 DHCP 服务器分配的私有 IP 地址池中选择一个。例如，192.168.0.1 到 192.168.0.254 的地址通常用于私有局域网。）

