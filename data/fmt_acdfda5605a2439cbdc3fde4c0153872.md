
# 而不会产生瞬间的安全漏洞；

## 14.2 自适应防火墙：使用破解者陷阱升起闸桥

```bash
# blockip 可能位于其他地方。
ALL: ALL: \
spawn=((sleep 3;tail -10 /var/log/messages) | \
/usr/sbin/blockip "%h" "%a" "%d" "%c" "%u")) &: deny
```

### 14.2.6 `/etc/hosts.deny` 文件

如果你使用的是通过向 `/etc/hosts.allow` 文件中添加条目来阻止后续访问的 Cracker Trap 版本，那么它在更新时不会出现短暂的失效。在这种情况下，必须在 `/etc/hosts.deny` 文件中设置一条规则来阻止所有服务。建议采用以下配置：

- `# 如果你有即使在不到一秒的时间也不允许允许的关键服务，请在此之前添加带有 :allow 的条目`
- `# 注意，在某些系统中，邮件程序是 /bin/mailx`
`ALL: ALL: spawn=((sleep 3;tail -10 /var/log/messages) | \`
`/bin/Mail -s 'DENIEDefault_%h/%d/%a/%u' \`
`bob@homes.com bob@pentacorp.com) &: deny`

### 14.2.7 使用端口重定向捕获服务器攻击

| 危险等级 | ☠ ☠ ☠ ☠ |

如前所述，如果 Cracker Trap 运行在防火墙而不是单个服务器或工作站上，它将把攻击者锁定在整个网络之外。然而，攻击者必须首先攻击防火墙本身的端口才能被捕获。取决于你的 IP 地址分配，以及破解者攻击的是分配 IP 地址的系统还是随机地址的系统，破解者可能会先攻击其他系统。一种解决方案是让防火墙位于最低的可用 IP 地址。尽管如此，这仍然无法防止破解者随机化攻击的 IP 地址。

完整的解决方案是将端口重定向与 Cracker Trap 结合，以便即使目标 IP 是防火墙后的系统也能触发它。通过使用 IPs 的 `REDIRECT` 目标可以轻松实现。`REDIRECT` 允许指定将指向防火墙后其他系统的入数据包重定向到防火墙自身的某个端口。来自防火墙的任何数据包都将修改为来自原始目标 IP。困难的部分在于决定在每个系统上捕获哪些端口。必须在尽可能捕获破解者与由于无辜人员误操作导致低误报率之间取得平衡。

你想要避免的误报陷阱示例是在普通 Web 服务器上捕获 `https`，或在仅支持安全 HTTP 协议的服务器上捕获 `http`。如果你捕获来自你组织内部的攻击，你可能不想捕获来自内部网络发往防火墙的 DNS 请求，因为某些人在配置其桌面系统时，会混淆哪个 IP 是路由器，哪个是 DNS 服务器。请记住，意外捕获某人并不是世界末日。如果用户或其他人抱怨被锁定在外，且他们的触发因素似乎是意外的，只需编辑 `/etc/rc.d/fw.trouble` 文件并通过以下或类似的命令重启防火墙规则。

注意，我们 `REDIRECT` 了我们整个完全可见的 IP 地址范围。如果我们有 DMZ，它的地址将作为完全可见范围的子集被包含。只有当内部网络的地址范围经过 IP 伪装（NAT）时，才需要包含在独立的 `REDIRECT` 中，因为这是一个不同的范围。这同样适用于其他内部网络，例如任何仅限内部的 DMZ。

```bash
cd /etc/rc.d
.rc.fw foo 2>&1
more foo
/bin/rm foo
```

```tcsh
tcsh:
cd /etc/rc.d
.rc.fw >&! foo
more foo
/bin/rm foo
```

接下来的 shell 脚本 `redir_pre` 将为 IP Tables 或 IP Chains 端口重定向设置几个变量。如果你正在使用第 446 页的“带有 IP Tables 的防火墙”或第 514 页的“带有 IP Chains 的防火墙”技术，这些变量已经通过 `rc.vars` 或 `rc.fw` 脚本设置好了。为了对 Cracker Trap 重定向进行实验，即使防火墙是开放的，当 Cracker Trap 检测到攻击时，入侵者将被锁定。要从 bash 激活重定向，使用 dot 命令 `source redir_pre`：

```bash
cd /etc/rc.d
.redir_pre
```

然后 `source redir_iptables` 或 `redir_ipchains`。这些示例中列出的第一个是 Cracker Trap 变量设置，第二个是带有 IP Tables 的 Cracker Trap 重定向 (`DNAT`)。

```bash
#!/bin/sh
# 文件是 crackstrap/redir_pre
# 下面是建议的值
IFC=/sbin/ifconfig
EXTIF="eth0"
EXTIP=$IFC | sed 's.*addr:\(.*\)/'
EXTMSK=$IFC | sed 's.*Mask:\(.*\)/'
# 如果 IP 伪装也是 "on"，则设置 DOMK 为 "yes"
DOMK="yes"
INTIF="eth1"
INTIP=$IFC | sed 's.*addr:\(.*\)/'
INTMSK=$IFC | sed 's.*Mask:\(.*\)/'
EXTNET=$EXTIP/$EXTMSK
# 不要包含任何系统，例如：
# http, dns, socks, kazaa 等，在以下
CRACKER_PORTS_TCP*=137:139:445
CRACKER_PORTS_UDP*=137:139:445
# 结束
我们可以捕获邮件服务器上的攻击。
MAILIP=198.155.7 # 为你的网络设置
HTPIP=198.155.8 # 为你的网络设置
```

`redir_iptables` bash 脚本在下一个示例中给出。它将激活 Cracker Trap 的 IP tables 重定向。它可以从第 446 页“带有 IP Tables 的防火墙”中讨论的 `rc.fw` 脚本中 `source`，只需在 `rc.fw` 脚本末尾包含行：

`/etc/rc.d/redir_iptables`

它不会将端口重定向到自身。这允许我们将整个网络的 Kazaa 端口路由到防火墙上的 Kazaa 端口。如果防火墙上的 Kazaa 端口受到攻击，`DNAT` 规则将无效，数据包将传递到 Cracker Trap 处理。对于带有 IP Tables 的 Cracker Trap 重定向 (`NAT`)，使用此脚本：

```bash
#!/bin/sh
# 文件是 crackstrap/redir_iptables
# 可能位于不同的目录
IPT=/sbin/iptables
# 在重定向之前创建一个日志链，
# 因为 Tables 缺少记录日志的标记
#（带日志的 Cracker Trap 重定向）
$IPT -t nat -X CTRL 2> /dev/null
$IPT -t nat -X CTRL
$IPT -t nat -A CTRL -j LOG --log-prefix "R:" --log-level err
$IPT -t nat -A CTRL -j REDIRECT
```

“启用 IP Tables 的 Cracker Trap REDIRECT (DNAT)”：

```bash
echo -n "TCP port"
for i in $CRACKER_PORTS_TCP; 
do
  echo -n "$i"
  ipt -t nat -A PRERUTING -p TCP -d $EXTNET --dport $i -j CTRL
  if [ "$DOMK" = "yes" ]; then
    ipt -t nat -A PRERUTING -p TCP -d $INTNET --dport $i -j CTRL
  fi
done
echo ""
```

```bash
echo -n "UDP port"
for i in $CRACKER_PORTS_UDP; 
do
  echo -n "$i"
  ipt -t nat -A PRERUTING -p UDP -d $EXTNET --dport $i -j CTRL
  if [ "$DOMK" = "yes" ]; then
    ipt -t nat -A PRERUTING -p UDP -d $INTNET --dport $i -j CTRL
  fi
done
echo ""
```

“HTTP AND SMTP IPs”：

```bash
if [ "$MAILIP" -a "$MAILIP" != "$HTPIP" ]; then
# 捕获邮件服务器上的 http 端口攻击
ipt -t nat -A PRERUTING -p TCP -d $MAILIP --dport http -j CTRL
```
