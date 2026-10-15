
```
sendmail  0:off 1:off 2:on 3:on 4:on 5:off 6:off

autofs    0:off 1:off 2:off 3:off 4:on 5:off 6:off

nsmpd     0:off 1:off 2:off 3:off 4:off 5:off 6:off

hnsd      0:off 1:off 2:off 3:off 4:off 5:off 6:off

rawdevices 0:off 1:off 2:off 3:off 4:on 5:off 6:off

netfs     0:off 1:off 2:off 3:off 4:on 5:off 6:off

network   0:off 1:off 2:off 3:off 4:on 5:off 6:off

random    0:off 1:off 2:off 3:off 4:on 5:off 6:off

ipchains 0:off 1:off 2:off 3:off 4:on 5:off 6:off

apmd      0:off 1:off 2:off 3:off 4:on 5:off 6:off

iptables  0:off 1:off 2:off 3:off 4:on 5:off 6:off

is       0:off 1:off 2:off 3:off 4:on 5:off 6:off

ident     0:off 1:off 2:off 3:off 4:off 5:off 6:off

portmap   0:off 1:off 2:off 3:off 4:on 5:off 6:off

nfs       0:off 1:off 2:off 3:off 4:on 5:off 6:off

fsock      0:off 1:off 2:off 3:off 4:on 5:off 6:off

radvd      0:off 1:off 2:off 3:off 4:off 5:off 6:off

crond     0:off 1:off 2:off 3:off 4:on 5:off 6:off

acron    0:off 1:off 2:off 3:off 4:on 5:off 6:off

xfs       0:off 1:off 2:off 3:off 4:on 5:off 6:off

xinetd    0:off 1:off 2:off 3:on 4:on 5:on 6:off

sshd      0:off 1:off 2:on  3:on 4:on 5:off 6:off

httpd     0:off 1:off 2:on  3:on 4:on 5:off 6:off

linuxconf 0:off 1:off 2:on  3:on 4:on 5:on 6:off
```

# 第 26 章：防火墙与网络安全

你如何确定当前的运行级别（run level）？它可能是 3，但如果正在使用 X 窗口管理器，它很可能是 5。如下例所示，使用 `runlevel` 命令：

```
$ runlevel

N 3
```

`runlevel` 返回上一个运行和当前的运行级别。在没有运行级别的情况下，`runlevel` 会显示为 N，如示例所示。

`chkconfig` 有几种操作模式；恰恰刚才演示的列出模式只是其中一种。其他模式允许 `chkconfig` 向 `/etc/init.d` 启动层次结构中添加或删除服务，或者在任何运行级别下开启或关闭服务。这是一种控制级别，在通常情况下，大多数控制都是并不需要的。很少有必要更改 `/etc/init.d` 中符号链接的排序；默认设置对于正常使用已经完全足够。关于在启动时启动服务，或防止服务在启动时启动，将在下一个小节中讨论 `ntsysv` 工具。

## NTSYSV

`ntsysv` 提供了一个接口，允许对 `chkconfig` 列出的任何服务在当前运行级别（即启动 `ntsysv` 时的生效运行级别）进行开启或关闭。可以通过在命令行上传递它们的数字来编辑其他运行级别，但在使用此功能时必须非常小心。正如所提到的，更改各种服务和守护进程（daemon）为自己安装的默认运行级别是一项风险操作。

对于之前提出的问题“应该运行哪些服务？”，简短的回答是“无”。如果这看起来像是一个不加区分的泛泛谈，请从理解主机角色的角度再重新审视这个问题。也就是说，“应该运行哪些服务？”只有在对给定主机的角色产生模糊时才会出现。当然，在设置 Web 服务器时，你绝不会要求运行任何主机并未设计为提供给其他主机的网络服务。对于许多计算机（即网络上的工作站），人们简单地运行 `ntsysv` 并关闭除 `syslog`、`crond` 和 `xindet` 之外的所有项，这些服务对于整个系统的运行总是更好。

这并不是故事的结束。相反，它是添加更多服务的起点。例如，`Sendmail` 并不是获取或发送邮件邮件（即使 `fetchmail` 使用 `procmail` 作为其传输代理会更好），但另一方面，使用 `-q` 参数在后台运行 `Sendmail` 并不是一个坏主意，这样邮件就不会无意中永远滞留在队列中。基本方法应该是：禁用除 `syslog`、`crond` 和 `xindet` 之外的所有内容，然后在需求明确且已彻底检查过安全影响的地方启用其他服务。

## 监控网络流量

网络或系统管理员通常希望快速“看一眼”给定主机上的实际网络流量。这种愿望可能是某些系统功能的可疑行为或异常硬件性能的结果。事实上，任何可能的事件演变都可能引发“线路上有什么？”的问题。当发生这种情况时，人们不想在日志文件或由入侵检测系统（IDS）软件生成的报告中费费精力；他们需要的是快速、直接且即时地查看网络流量。接下来的章节将讨论每个系统中应该具备的工具：`tcpdump`、`tcpresh` 和 `snort`。

## TCPDUMP

`tcpdump` 是嗅探器中的元老级。在实践中，当你想要查看网络上的流量时，它通常是你首先考虑的工具。在给定接口上进行数据包嗅探的基本语法非常简单（实际地址和主机名在整个章节中已模糊处理）：

```
# tcpdump -i eth1

tcpdump: listening on eth1
```

下面的示例引导 `tcpdump` 在 `eth1` 接口（`-i eth1`）上监听 100 个包（`-c 100`），并将它们存储在名为 `my_sniffed_packets` 的输出文件中，格式为 `tcpdump` （`-w my_sniffed_packets`）：

```
# tcpdump -c 100 -i eth1 -w my_sniffed_packets
```

收集到的包可以使用 `tcpdump` 回放并打印到屏幕或重定向到文本文件，如下例所示：

```
# tcpdump -r my_sniffed_packets > my_packets_text
```
