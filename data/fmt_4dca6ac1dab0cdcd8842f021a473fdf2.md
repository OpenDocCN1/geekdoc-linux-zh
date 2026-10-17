
`n= root@192.168.1.132#tty1 =`

this is a test

用户名和终端的指定方式与 `talk` 相同，但你必须用井号 (`#`) 将它们放在在一起。

`ytalk` 提供了几个优势：

- 它支持两个以上的用户。
- 一个可以随时通过 `Esc` 调出的选项菜单。
- 你可以在保持 `talk` 会话的同时调用 `shell`（`shell out`）。
- 更多更多……

如果你是服务器管理员，你需要确保在 `/etc/inetd.conf` 中启用了 `ntalk` 端口。`ytalk` 需要它才能正常工作。

# 安全

任何系统的安全性都至关重要；它可以防止人们从你的机器发起攻击，并保护敏感数据。本章将介绍如何开始保护你的 Slack 系统免受脚本小子、破解者和破坏份子的攻击。请记住，这只是系统安全的开始；安全是一个过程，而不是状态。

## 14.1 禁用服务

安装 Slackware 后第一步应该是禁用任何你不需要的服务。任何服务都可能带来安全风险，因此尽可能运行少的服务（即仅运行所需的））。服务从两个主要地方启动——`inetd` 和 `init` 脚本。

### 从 *inetd* 启动的服务

Slackware 自带的大多数守护进程从 `inetd(8)` 运行。`inetd` 是一个守护进程，它监听所有配置由它启动的服务所使用的端口，并在尝试建立连接时派生相关守护进程的实例。从 `inetd` 启动的守护进程可以通过注释掉 `/etc/inetd.conf` 中的相关行来禁用。要此操作，请用你喜欢的编辑器（例如 `vi`）打开此文件，你应该会看到类似下面的行：

```
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```

你可以通过注释掉这些行（即在行首添加 `#`（井号）符号）来禁用此服务以及任何你不需要的其他服务。执行操作后，上述行将变为：

```
#telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```

在 `inet` 重启后，该服务将被禁用。你可以使用命令重启 `inet`：

```
# kill -HUP $ (cat /var/run/inetd.pid)
```

### 从 init 脚本启动的服务

机器启动时启动其余服务是从 `/etc/rc.d/` 中的 `init` 脚本启动的。这些服务可以通过两种不同的方法禁用，第一种是移除相关 `init` 脚本的执行权限，第二种是注释掉 `init` 脚本中的相关行。

例如，`SSH` 由其位于 `/etc/rc.d/rc.sshd` 的 `way` 脚本启动。你可以使用以下命令禁用它：

```
# chmod -x /etc/rc.d/rc.sshd
```

对于没有自己独立 `init` 脚本的服务，你需要注释掉 `init` 脚本中的相关行来禁用它们。例如，`portmap` 守护进程是由 `/etc/rc.d/rc.inet2` 中的以下行启动的：

```
# This must be running in order to mount NFS volumes.

# Start the RPC portmapper:

if [ -x /sbin/rpcmap ]; then

echo "Starting RPC portmapper: /sbin/rpcmap"

/sbin/rpcmap

fi

# Done starting the portmapper.
```

可以通过在不以 `#` 开头的行开头添加 `#` 符号来禁用它，例如：

```
# This must be running in order to mount NFS volumes.

# Start the RPC portmapper:

# if [ -x /sbin/rpcmap ]; then

# echo "Starting RPC portmapper: /sbin/rpcmap"

# /sbin/rpcmap

# fi
```

这些更改只有在重启或从运行级别（`runlevel`） 3 或 4 切换后才会生效。你可以通过在控制台上输入以下内容来实现这一点（切换到运行级别 1 后你需要重新登录）：

- `telinit 1`
- `telinit 3`

## 14.2 主机访问控制

### iptables

`iptables` 是 Linux 2.4 及以上版本的包过滤程序。2.4 内核（准确地说）首次在 Slackware 8.0 版本中引入（作为可选方案），并在 Slackware 8.1 中成为默认。本节仅涵盖其用法，你应该检查 `http://www.netfilter.org/` 获取更多详细信息。命令可以输入 `/etc/rc.d/firewall`。注意，为了让规则生效，`iptables` 必须被启动。为了防止人们从你的机器发起攻击并保护敏感数据，可以将默认策略设置为 `DROP`：

```
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```

在某些情况下，你需要允许已建立的（`ESTABLISHED`）和相关的（`RELATED`）的流量。你可以通过以下命令来实现：

```
iptables -m state --state ESTABLISHED,RELATED -j ACCEPT
```

允许回环接口

```
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
iptables -A FORWARD -i lo -o lo -j ACCEPT
```

允许 `ICMP` 流量对于诊断很有用。要此此，你可以使用如下规则：

```
iptables -A INPUT -p icmp -j ACCEPT
```

大多数人还想在网关机器上设置网络地址转换 (`NAT`)，以便网络上的其他机器可以通过它访问互联网。你会使用以下规则来实现：

```
iptables -t nat -A POSTROUTING -o ppp0 -j MASQUERADE
```

你还需要启用 IP 转发。你可以使用以下命令临时执行：

```
### echo 1 > /proc/sys/net/ipv4/ip_forward
```

永久启用 IP 转发（即重启后更改仍然有效），你需要打开 `/etc/rc.d/rc.inet2` 文件并修改以下行：

```
IPV4_FORWARD=0
```

...改为：

```
IPV4_FORWARD=1
```

有关 `NAT` 的更多信息，请参见 `NAT HOWTO`。

### tcpwrappers

`tcpwrappers` 在应用层控制对守护进程的访问，而不是在 IP 层。在 IP 级访问控制（例如 `Netfilter`）无法正常工作时，这可以提供额外的安全保障。例如，如果你重新编译内核但忘记包含 `iptables` 支持，你的 IP 级保护将失效，但 `tcpwrappers` 仍然有助于保护系统。

受 `tcpwrappers` 保护的服务访问可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 进行控制。

大多数人在 `/etc/hosts.deny` 文件中有一行，用于默认拒绝对所有守护进程的访问。该行是：

```
:: all
```
