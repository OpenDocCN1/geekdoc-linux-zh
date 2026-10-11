
`rtt min/avg/mdev = 0.781/0.942/1.104/0.164 ms`

```
$ ssh: connect to host 10.140.67.23 port 22: Connection timed out
```

同样，你的访问控制矩阵（见第 22 章）帮助你为 Linux 服务器上的 `netfilter-iptables` 防火墙创建必要的规则。在将任何修改应用于你的生产 Linux 系统防火墙之前，都应该在测试环境或虚拟环境中进行测试。

## 保存 iptables 配置

在你完成创建 Linux 服务器配置策略和规则的所有繁琐工作之后：

在示例中，之前做的修改是在防火墙中。在将它们保存到配置文件之前，会对原始文件进行备份。这始终是一个好主意。然后使用 `iptables-save` 命令保存修改。注意，输出使用重定向符号定向到 `/etc/sysconfig/iptables` 文件中（参见示例中的代码行）。

```bash
# iptables -vL

Chain INPUT (policy ACCEPT)
  target prot source destination
DROP tcp 10.140.67.22 anywhere tcp dpt:ssh

Chain FORWARD (policy ACCEPT)
  target prot source destination

Chain OUTPUT (policy ACCEPT)
  target prot source destination

# cp /etc/sysconfig/iptables /etc/sysconfig/iptables.bck
# iptables-save > /etc/sysconfig/iptables
```

## 第 25 章：网络环境下的 Linux 安全

你也可以使用刷新选项 `iptables -F` 来移除当前 `netfilter/iptables` 防火墙的修改。完成后，所有规则（但不包括策略）将被移除，如下面的代码所示。这对于测试单个策略和规则非常有用。

```bash
# iptables -F
# iptables -vL

Chain INPUT (policy ACCEPT)
  target prot source destination

Chain FORWARD (policy ACCEPT)
  target prot source destination

Chain OUTPUT (policy ACCEPT)
  target prot source destination
```

刷新规则不会影响 `iptables` 配置文件。要将防火墙恢复到原始状态，请使用 `iptables-restore` 命令。在下面的示例中，`iptables` 配置文件被重定向到恢复命令，并恢复了针对 `10.10.67.22` 的原始 `DROP` 规则。

```bash
# iptables-restore < /etc/sysconfig/iptables
# iptables -vL

Chain INPUT (policy ACCEPT)
  target prot source destination
DROP tcp - 10.10.67.22 anywhere tcp dpt:ssh

Chain FORWARD (policy ACCEPT)
  target prot source destination

Chain OUTPUT (policy ACCEPT)
  target prot source destination
```
