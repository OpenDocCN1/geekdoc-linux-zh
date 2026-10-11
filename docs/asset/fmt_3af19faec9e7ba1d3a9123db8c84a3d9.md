
## Refuse packets claiming to be from the banned list
```bash
## Refuse packets claiming to be from the banned list
if [ -f /etc/rc.d/rc.firewall.blocked ]; then
. /etc/rc.d/rc.firewall.blocked
fi
```

`rc.firewall.blocked` 文件中全局丢弃规则的一个例子如下：

```bash
$IPT -I INPUT -i $INTERNET -s <address/mask> -j DROP
```

作为替代，为了避免在链的最开始处插入规则从而排除状态检查，规则可以是追加规则，并且该文件可以包含在规则集中的伪造源地址部分。

来自该源地址范围的任何数据包都被丢弃，无论消息协议类型或源/目的端口如何。

## 安装防火墙

本节假设防火墙脚本名为 `rc.firewall`。脚本也可以简单地称为 `fwscript` 或其他名称，没有理由不能这样做。事实上，在 Debian 系统中，标准名称更接近于单个名称 `fwscript`，而不是像 Red Hat 那样带有 `rc` 前缀的名称。本节涵盖的命令假设脚本安装在 Red Hat 或 SUSE 系统的 `/etc/rc.d/` 目录中，或 Debian 系统的 `/etc/init.d/` 目录中。

作为一个 shell 脚本，初始安装很简单。脚本应由 `root` 拥有。在 Red Hat 和 SUSE 上：

```bash
chown root:root /etc/rc.d/rc.firewall
```

在 Debian 上：

```bash
chown root:root /etc/init.d/rc.firewall
```

脚本应仅允许 `root` 写入和执行。理想情况下，普通用户不应具有读取权限。在 Red Hat 和 SUSE 上：

```bash
chmod u=rwx /etc/rc.d/rc.firewall
```

在 Debian 上：

```bash
chmod u=rwx /etc/init.d/rc.firewall
```

要在任何时间初始化防火墙，从命令行执行该脚本即可。无需重启：

```bash
/etc/rc.d/rc.firewall start
```

严格来说，`start` 参数在那里不是必需的，但这仍然是一个好习惯——同样，对于防火墙，我宁愿选择完整性而不是存在歧义。该脚本包含一个 `stop` 操作，它会完全清除防火墙。因此，如果您想停止防火墙，请使用 `stop` 参数调用相同的命令：

```bash
/etc/rc.d/rc.firewall stop
```

预先警告：如果您以此方式停止防火墙，您将在没有任何保护的情况下运行。律师告诉我，我应该告诉您：“始终保持防火墙启用！”

在 Debian 上，将命令路径更改为 `/etc/init.d`。启动防火墙：

```bash
/etc/init.d/rc.firewall start
```

在 Debian 上停止防火墙：

```bash
/etc/init.d/rc.firewall stop
```

## 调试防火墙脚本的技巧

当您通过 SSH 或其他远程连接调试新的防火墙脚本时，很可能会将自己锁定在系统之外。当然，当从控制台安装防火墙时，这不是一个问题，但作为管理远程 Linux 服务器的人，我发现访问控制台很少是可能的。因此，需要一种方法，以防防火墙阻止我的连接，让防火墙在启动后自动停止。Cron 来救援了。

使用 cron 条目，您可以在预定的间隔内通过运行带有 `stop` 参数的脚本来停止防火墙。我发现每 2 分钟执行一次在初始调试期间效果很好。如果您想使用这种方法，请以 `root` 身份（在 Debian 上）设置具有以下命令的 cron 条目：

```bash
crontab -e
*/2 * * * * /etc/init.d/rc.firewall stop
```

在 Red Hat 和 SUSE 上：

```bash
crontab -e
*/2 * * * * /etc/rc.d/rc.firewall stop
```

有了这个 cron 条目，您可以启动防火墙，并让它每 2 分钟 `stop` 一次。然而，使用这样的机制在某种程度上是一种权衡，因为您必须这样做

初始调试应在时钟显示的时间能被二整除之前进行！此外，记住在调试完防火墙后删除此定时任务条目是你的责任。如果你忘记删除此条目，防火墙将停止运行，你将再次处于无防火墙保护的状态！

## 在 Red Hat 和 SUSE 上启动时引导防火墙

在 Red Hat 和 SUSE 系统上，初始化防火墙最简单的方法是编辑 `/etc/rc.d/rc.local` 并在文件末尾添加以下行：

```bash
/etc/rc.d/rc.firewall start
```

在防火墙规则调试稳定后，Red Hat Linux 提供了一种更标准的启动和停止防火墙的方式。如果你使用运行级别管理器之一并选择 `iptables`，默认的运行级别目录中包含一个指向 `/etc/rc.d/init.d/iptables` 的链接。与该目录中的其他启动脚本一样，系统会在启动或更改运行级别时自动启动和停止防火墙。

然而，要使用标准的运行级别系统还需要执行一个额外的步骤。你必须首先手动安装防火墙规则：

```bash
/etc/rc.d/rc.firewall
```

然后执行命令：

```bash
/etc/init.d/iptables save
```

规则将被保存到一个文件中，即 `/etc/sysconfig/iptables`。此后，启动脚本将找到此文件并自动加载已保存的规则。

关于使用此方法保存和加载防火墙规则，有必要提请注意一些事项。`iptables save` 和 `load` 功能目前尚未完全调试。如果你的特定防火墙配置在保存或加载规则时导致语法错误，你必须继续使用前一种启动机制，例如从 `/etc/rc.d/rc.local` 执行防火墙脚本。

## 在 Debian 上启动时引导防火墙

与许多其他方面一样，在 Debian 上将防火墙脚本配置为启动时运行比其他发行版更简单。你可以使用 `update-rc.d` 命令让防火墙在启动时启动和停止。运行 `update-rc.d` 并指定位于 `/etc/init.d` 中的防火墙脚本，同时也将当前目录设置为 `/etc/init.d`：

```bash
cd /etc/init.d
update-rc.d rc.firewall defaults
```

有关超出此处所示用法的更多信息，请参阅 `update-rc.d` 的手册页。

防火墙脚本的其他方面取决于你是拥有注册的静态 IP 地址，还是动态的、由 DHCP 分配的 IP 地址。本章中介绍的防火墙脚本是为拥有静态分配永久 IP 地址的站点设置的。

## 安装具有动态 IP 地址的防火墙

如果你拥有动态分配的 IP 地址，标准的防火墙安装方法在没有修改的情况下将无法工作。防火墙规则将在网络接口启用之前、系统分配 IP 地址之前、可能甚至在被分配默认网关路由器或名称服务器之前就安装了。

防火墙脚本本身需要定义 `IPADDR` 和 `NAMESERVER` 值。DHCP 服务器和本地 `/etc/resolv.conf` 文件都可以定义最多三个名称服务器。此外，任何特定站点可能知道也可能不知道其名称服务器、默认网关路由器或 DHCP 服务器的地址。此外，随着 ISP 重新编号其网络，你的网络掩码、子网和广播地址随时间变化并不罕见。一些 ISP 经常分配不同的 IP 地址，结果导致你的 IP 地址在一次持续连接期间可能改变多次。

你的站点必须提供某种机制，在这些变化发生时动态更新已安装的防火墙规则。附录 B “防火墙示例和支持脚本”提供了旨在自动处理这些变化的示例脚本。

此外，如果你使用的是 DSL 连接，MTU 可能会导致问题。如果是这种情况，这里有一条可以解决该问题的防火墙规则：

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp --tcp-flags SYN,RST \
    SYN -j TCPMSS --clamp-mss-to-pmtu
```

防火墙脚本可以直接从环境中读取这些 shell 变量，也可以从文件中读取。无论如何，这些变量不会像本章示例中那样硬编码到防火墙脚本中。

## 摘要

本章引导你完成了使用 `iptables` 开发独立防火墙的过程。建立了默认拒绝策略。在脚本开始时修复了一些常用的攻击向量，包括源地址欺骗、保护运行在非特权端口上的服务以及 DNS。展示了流行网络服务规则的示例。还处理了 ICMP 消息，即底层 IP 网络层使用的控制和状态消息。演示了控制日志生成级别的示例。最后，描述了防火墙安装涉及的问题，既包括具有静态 IP 地址的站点，也包括具有动态分配 IP 地址的站点。
