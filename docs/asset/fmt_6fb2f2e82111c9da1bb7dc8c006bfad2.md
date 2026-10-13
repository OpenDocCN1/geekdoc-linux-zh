
你现在需要重启 SSH 守护进程。执行命令 `/etc/init.d/sshd restart` 然后尝试从另一个远程控制台以 `root` 身份登录。你会发现每次输入正确的密码时，都会得到“拒绝访问”的错误。你成功加固了 `root` 的远程权限！

你的系统真的开始成型了！你的下一步是创建一个防止任何意外访问的防火墙。

## 配置防火墙

Linux 内核带有一个名为 `iptables` 的特殊内置防火墙保护。这种保护也被称为 `netfilter/iptables`。`iptables` 防火墙通过内核进行数据包过滤、网络翻译和端口翻译工作。以下是 `iptables` 的一些主要功能：

- 状态数据包过滤 (IPv4 和 IPv6)
- 状态数据包过滤 (IPv4)
- 各种网络翻译和端口翻译手段 (NAT)
- 灵活且可扩展的基础

`iptables` 提供的某些功能超出了本书的范围。然而，随着课程的推进，我们将添加规则并开放端口。有关 Linux 安全的详细信息，请查阅《Linux Security》Ramón J (2001) 以及《Firewalls》Matthew Strebe 和 Charles Perkins (2002)。

## 创建防火墙脚本

大多数 Linux 发行版默认都会安装一套防火墙脚本。这是一种友好的做法，但涉及到安全时，我们认为你应该手动配置自己的版本。如果你感兴趣查看这些预装脚本，请检查以下文件：`/etc/rc.d/init.d/iptables`、`/etc/sysconfig/iptables` 和 `/etc/sysconfig/iptables-config`。然而，我们不会使用这些脚本。

你的第一步是创建一个包含运行防火墙所需规则的脚本。该脚本将定义服务器上哪些端口是开放的，并限制未经授权的访问。

我们习惯将防火墙脚本存在 `/usr/local/etc` 等地方，让我们进入该目录并开始。

我们使用 `pico` 作为常用的命令行编辑器，让我们开始。运行 `pico /usr/local/firewall`。现在你可以开始编写脚本。

在列表 6.3 中，你将看到完整的脚本。在列表之后，我们将为你解释每个元素。

### 列表 6.3 防火墙脚本

```
#!/bin/sh

# 将等号后面的部分改为 IPTABLES 在你系统中的位置

IPTABLES=/sbin/iptables

# 清空现有规则

IPTABLES -F INPUT

## 允许从本机发出的连接

# 回包

IPTABLES -A INPUT -j ACCEPT -m state --state ESTABLISHED -i eth0 -p icmp

IPTABLES -A INPUT -j ACCEPT -m state --state ESTABLISHED -i eth0 -p tcp

IPTABLES -A INPUT -j ACCEPT -m state --state ESTABLISHED -i eth0 -p udp

#允许入站 SSH 请求

IPTABLES -A INPUT -p tcp --dport 22 -j ACCEPT

#允许入站 DNS

IPTABLES -A INPUT -p udp --dport 53 -j ACCEPT

IPTABLES -A INPUT -p tcp --dport 53 -j ACCEPT

#允许入站 HTTP 请求（到 Web 服务器）
```

```bash
$IPTABLES -A INPUT -p tcp --dport 80 -j ACCEPT
$IPTABLES -A INPUT -p tcp --dport 443 -j ACCEPT
```

### 允许 Ping Echo

```bash
$IPTABLES -A INPUT -p icmp -j ACCEPT
```

### 加载模块
```
insmod ip_conntrack_ftp
insmod ipt_LOG
insmod ipt_REJECT
insmod ipt_limit
insmod ipt_state
```

# 设置日志记录，如果三秒内丢弃的数据包超过5个，
# 则将被忽略。这有助于防止 DOS 攻击
# 导致防火墙崩溃

```bash
$IPTABLES -A INPUT -m limit --limit 3/second \
--limit-burst 5 -i ! lo -j LOG
```

# 丢弃并记录所有其他数据

```bash
$IPTABLES -A INPUT -i lo -j DROP
```

让我们开始理解列表 6.3 中的防火墙脚本。第一行是我们的 bash shell 命令行。它被称为 shebang，某些系统可能需要它才能正常运行：
`#!/bin/sh`

接下来，你会在脚本中到处看到一些注释。这有助于跟踪你正在做什么，并且是记录笔记的一种简单方法。在编写脚本时，有时会有大量的代码，保留注释可以帮助你稍后刷新记忆。只需在每行注释的前面加一个注释符号 (`#`)，以防止脚本在运行时尝试执行你的注释：

`# 将等号后面的部分更改为你的系统中`
`# IPTABLES 所在的路径`

现在，你正在创建一个变量，或者说一个指向你的 `iptables` 可执行文件的快捷方式。这个变量可以避免你每每次需要它时都输入完整命令。在这种情况下，你将创建一个值为 `/sbin/iptables` 的 `IPTABLES` 变量：
`IPTABLES=/sbin/iptables`

你的下一个任务是清空 `INPUT` 链中任何现有的规则。这允许你在尝试设置规则之前清除任何旧信息。当你修改此脚本并删除某个规则时，`-f` 选项非常有用，因此你只需要重新运行此脚本，所有旧规则都将被移除，任何新规则将被输入：

- # 清空现有的规则

```bash
$IPTABLES -F INPUT
```

你的防火墙将被配置为阻止任何进入你未定义为开放端口的流量。如果你现在使用特定端口发送响应且该响应返回你的机器，可能会导致一些问题，因为它会被防火墙拦截。这就是 `ESTABLISHED` 状态的作用所在：

使用 `ESTABLISHED` 状态基本上意味着：“如果我从端口 99 发出响应，请允许响应从端口 99 回到我的机器，即使我没有专门为公共访问该端口。”基于此，你包含了接下来的三条规则，允许传输控制协议 (TCP)、用户数据报协议 (UDP) 和互联网控制消息协议 (ICMP) 响应返回：

- # 允许从这台机器发出的出站连接
# 回

```bash
$IPTABLES -A INPUT -j ACCEPT -m state --state \
ESTABLISHED -i eth0 -p icmp
```

```bash
$IPTABLES -A INPUT -j ACCEPT -m state --state \
ESTABLISHED -i eth0 -p tcp
```

```bash
$IPTABLES -A INPUT -j ACCEPT -m state --state \
ESTABLISHED -i eth0 -p udp
```

下一条规则允许通过 TCP 协议通过端口 22 使用 SSH。为了更好地描述这一点，你调用了 `$IPTABLES` 可执行文件并使用 `-A INPUT` 追加到 `INPUT` 链。你使用 `-p tcp` 选项将请求类型描述为 TCP，并使用 `--dport 22` 选项指定目标端口为 22。最后一个选项是 `-j`，它表示“对它做什么”，你表示接受 (`ACCEPT`) 请求。`ACCEPT` 选项的反面是 `DROP`，它会专门丢弃该端口流量。

- # 允许入站 SSH

```bash
$IPTABLES -A INPUT -p tcp --dport 22 -j ACCEPT
```

接下来，你要允许这台机器处理 DNS 请求。注意这里有两个规则：一个针对 TCP，另一条针对 UDP，因为在某些情况下 DNS 使用 UDP：

- # 入站 DNS

```bash
$IPTABLES -A INPUT -p udp --dport 53 -j ACCEPT
$IPTABLES -A INPUT -p tcp --dport 53 -j ACCEPT
```

最后一组规则用于你的 Web 器访问。这在此时并不重要，但我们现在将包含它，因为你很快就会设置 HTTP 访问。这两条规则：一条是用于端口 80 的普通 HTTP 响应，另一条是用于端口 443 的安全 Web 服务器 HTTP 响应：

## 允许入站 HTTP 请求（到 Web 服务器）

```bash
$IPTABLES -A INPUT -p tcp --dport 80 -j ACCEPT
$IPTABLES -A INPUT -p tcp --dport 443 -j ACCEPT
```

最简单的诊断工具之一是 `ping` 命令。然而，当设置了防火墙后，你必须允许系统响应你的 ping 命令。下一条规则处理了这个问题：

## 允许 Ping Echo

```bash
$IPTABLES -A INPUT -p icmp -j ACCEPT
```
