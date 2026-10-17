
```bash
ipchains -A input -i eth0 -s 192.168.1.0/24 -d 0/0 -j DENY
```

如果你收到来自外部世界并声称来自受保护局域网使用地址的数据包，请丢弃它，因为这只会在在 TCP 包中欺骗（伪造）其返回 IP 地址时发生。这通常是有人尝试破坏你的安全，我们会记录这些数据包。

```bash
ipchains -A input -i eth0 -p tcp -y -j ACCEPT
```

允许从外部世界进入的对受保护局域网 TCP 请求响应的数据包。此规则查看 TCP 连接位（SYN, ACK, FIN）以判断数据包是新连接的请求（SYN 位设置，ACK 和 FIN 位清除），还是对来自受保护局域网的请求的响应（SYN 位清除，ACK 或 FIN 位设置）。记住，当由会解释 `!` 的 shell（例如 `csh` 和 `tcsh`）运行该命令时，要转义 `!`（使用 `\` 字符）。

```bash
ipchains -A input -i eth0 -p tcp -s 0/0 -d 0/0 80 -j ACCEPT
```

来自外部世界目标为端口 `80` 的入数据包被接受。由于我们除了面向世界的唯一真实 IP（ISP 分配）外没有使用其他，因此没有指定实际目的地。如果需要，可以使用 `-d 10.5.8.19 -d 0/0`（其中 `10.5.8.19` 是分配给你的 `eth0` 接口的真实世界 IP 地址）。

![](img/9102b40bb114da6b158a518630807d57_229_0.png)

（注：原文在第 230-231 页存在重复或合并，我已根据提供的片段进行了处理。）

## IP 转发

为了使用可路由地址或使用 IP 伪装，内核需要转发包。默认情况下，IP 转发是禁用的。要启用 IP 转发，你需要执行以下命令：

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

你的下次重启将清除此值，它在启动时默认不转发。我们稍后会介绍如何处理。

# 应用程序与 IP 伪装

许多应用程序在 IP 伪装下的工作方式与非伪装环境一样。但某些程序存在问题。为了让 IP 转发与这些应用程序协同工作，你需要加载一些可加载内核模块。以下是一些已知应用程序及其在 IP 伪装环境下正常工作所需的模块列表：

表 11-3 伪装需要加载模块的应用程序

| 应用程序 | 所需模块 | |
| --- | --- | --- |
| ftp | ip_masq_ftp | |
| irc | ip_masq_irc | |
| CU-SeeMe | ip_masq_cuseeme | |
| Real Audio | ip_masq_vdaudio | *没有也可以工作，但配合使用效果更好 |
| VDOLive | ip_masq_vdolive | |
| Quake | ip_masq_quake | *仅当超过 1 个网络玩家时需要 |

要加载这些模块中的任何一个，使用 `insmod`。例如：

```bash
insmod ip_masq_ftp
```

## 使更改持久化

现在你已经实现了防火墙，开启了 IP 转发并加载了应用程序所需的任何内核模块（如果你正在使用伪装技术），你已经有了一个正在运行的防火墙。

遗憾的是，下次重启时，你的防火墙将不会自动初始化。`iptchains` 命令不会保存你的规则，它将规则安装到运行中的内核中（而不是磁盘上的内核）。`iptchains-save` 和 `iptchains-restore` 命令可以保存你的工作。建议你将链保存到 `/etc/iptchains.rules` 文件中。操作如下：

```bash
iptchains-save > /etc/iptchains.rules
```

这将保存规则，随后后可以通过以下命令进行恢复：

```bash
iptchains-restore < /etc/iptchains.rules
```

尽管如此，重启也不会对该文件产生任何作用，因为它没有作为系统启动脚本的一部分被查找。为了让你的防火墙设置链和 IP 转发，我们需要创建一个启动脚本并将其安装到正确的位置。你可以创建一个名为 `/etc/rc.d/init.d/firewall` 的脚本来启动防火墙：

```bash
#!/bin/sh
# 控制数据包过滤的脚本。
# 如果没有创建任何规则，则什么都不做。
[ -f /etc/iptchains.rules ] || exit 0
case "$1" in
start)
    echo -n "Turning on packet filtering"
    /sbin/iptchains-restore < /etc/iptchains.rules || exit 1
    echo 1 > /proc/sys/net/ipv4/ip_forward
    echo "."
    ;;
stop)
    echo -n "Turning off packet filtering"
    echo 0 > /proc/sys/net/ipv4/ip_forward
    iptchains -X
    iptchains -F
    iptchains -P input ACCEPT
    iptchains -P output ACCEPT
    iptchains -P forward ACCEPT
    ;;
*)
    echo "Usage: /etc/rc.d/init.d/firewall (start|stop)"
    exit 1
    ;;
esac
exit 0
```

当你使用上述脚本停止防火墙时，它将禁用所有通过系统的数据包。如果你只想删除所有规则并允许所有数据包通过，请删除关闭 IP 行的代码：

`echo 0 > /proc/sys/net/ipv4/ip_forward`

![](img/9102b40bb114da6b158a518630807d57_233_0.png)

除了启动脚本外，你还需要将任何支持受保护局域网客户端应用程序的可加载内核模块添加到 `/etc/modules/default` 文件中。为了支持 ftp 和 irc，你需要添加：

```text
ip_masq_ftp
ip_masq_irc
```

现在我们已经有了启动脚本和伪装模块，我们需要在 `/etc/rc.d/rc.3` 目录中插入一个符号链接，指向我们创建的脚本，这样系统会在启动过程中适当的时间运行我们的脚本。操作如下：

```bash
ln -s /etc/rc.d/init.d/firewall /etc/rc.d/rc.3/S00firewall
ln -s /etc/rc.d/init.d/firewall /etc/rc.d/rc.5/S000firewall
```

我们使用 `00` 是为了让它在级别 3 下最先运行。它将在网络接口启动之前运行。这样做是为了确保规则在接口启动之前已经到位。现在，我们的防火墙是完全自动的。防火墙因断电或其他原因重启，当它重启时，你需要的规则和伪装模块将被自动处理。

创建完成后，为所有者（root）添加执行权限：

```bash
chmod u+x /etc/rc.d/init.d/firewall
```

数字 `15` 是任意数字，但脚本是按数字顺序启动的，确保防火墙在网络之前启动。网络通常是第一个启动的，即 `S1network`。在这种情况下，输入：

```bash
mv S1network S2network
```

### 应用程序与 IP 伪装

确保你的防火墙通过此时创建符号链接或移动它来启动。你可以通过输入类似的命令来实现：

```bash
mv S15firewall S15firewall
```

此时，你的防火墙将自动启动。

#### 测试接受或拒绝的数据包

一旦你完成了创建防火墙并配置其在开机时自动启动的所有工作，你可能希望确保其质量。一种方法是进入一台位于内部网的机器，并测试适用于内部网的防火墙规则。你也可以从家里访问电脑并从外部测试你的防火墙。为了防止安全漏洞，可以使用 `ipchains` 选项在没有网络连接的情况下测试防火墙。使用之前创建的一些规则进行配置，以确保返回预期的答案：

```bash
ipchains -C forward -i eth0 -p tcp -s 192.168.1.100 2048 -d 10.1.2.3 80
```

系统回复为：

```text
masqueraded
```

输入：

```bash
ipchains -C input -i eth0 -p tcp -s 192.168.1.200 2048
```

系统回复为：

```text
masqueraded
```

输入：

```bash
ipchains -C input -i eth0 -p tcp -s 192.168.1.200 2048
```

系统回复为：

```text
masqueraded
```

输入：

```bash
ipchains -C input -i eth0 -p tcp -s 192.168.1.200 2048
```
