
此 `ipchains` 调用将规则（`-A`）添加到 `forward` 链，并将指向 `ppp0` 接口（`-i`）的数据包跳转（`-j`）到拒绝（DENY）。`-l` 内核记录匹配此规则的每个数据包。日志条目如下：

```
Sep 1 23:01:21 bubba kernel: Packet log: DENY ppp0 PROTO=6 192.168.0.3:1896 207.46.131.71:80 S=0x00 I=55238 F=0x00 T=127 (#1)
```

该条目主要是为网络专家而非普通人设计的，尽管如此，该输出仍然包含了有用信息。其分解如下：

- `forward` 是匹配数据包并生成日志条目的链。
- `DENY`（拒绝）是规则对数据包要执行的操作。
- `ppp0` 是接口名称。由于 `forward` 链包含了匹配规则，数据包可能是入的也可能是出的。
- `PROTO=6` 表示数据包使用了协议 6，映射到 `TCP` 协议（`UDP` 为 7）。
- `192.168.0.3:1896` 表示数据包的源 IP 地址为 `192.168.0.3`，端口为 `1896`。
- `207.46.131.71:80` 表示数据包的目的 IP 地址为 `207.46.131.71`，80（HTTP 端口）。
- `L=40` 表示数据包的总长度为 40 字节。
- `S=0x00` 表示服务类型（ToS）字段为 `0x00`。将此值（0）除以 4 转换为 `ipchains` 使用的 To 值，在这种情况下仍 0。
- `I=55238` 是 IP ID。
- `F=0x4000` 是 16 位偏移加标志。以 `0x4` 或 `0x5` 开头的值表示不分片（Dont Fragment）位已设置。
- `T=127` 表示数据包的存活时间（TTL）为 127。回想第 26 章，包的 TTL 通常从 64 或 255 开始，每跳减少 1。
- `(#1)` 指定生成日志条目的规则编号。

默认情况下，`ipchains` 日志消息进入 `/var/log/messages`。因此，为了检测尝试的入侵，请对你想监控的每个 `ipchains` 规则添加 `-l` 选项；然后配置 `LogWatch` 对内核消息使用高级别的细节。即在 `/etc/logwatch.conf` 中设置 `detail = high`。现在，当你运行 `LogWatch` 时，生成的报告中的内核部分如下：

```
# logwatch --server kernel --detail high --range today --print
---------------------------------------
Kernel Begin

Denied packets from host2.mydomain.com (192.168.0.4).
Port netbios-ns (udp,ppp0,forward): 6 packet(s).
Total of 6 packet(s).

Denied packets from bubba.possum.holler.org (192.168.0.3).
Port domain (udp,ppp0,forward): 42 packet(s).
Port http (tcp,ppp0,forward): 4 packet(s).
Total of 46 packet(s).

Kernel End
```

`LogWatch` 如何基于主机和端口对被拒绝的数据包流量进行摘要。例如，IP 地址 `192.168.0.3` 的 `bubba.possum.holler.org` 在 `ppp0` 接口上使用 `UDP` 协议向 `domain` 端口发送了 42 个数据包（这些可能是某种 DNS 消息）。`forward` 生成了这 42 个日志条目的每一个都被 `LogWatch` 检测到。虽然 `LogWatch` 提供了大量的摘要信息，你可能还想详细分析流量。为此，请使用 `grep` 命令在当天的 `/var/log/messages` 文件中搜索包含 `"Packet log"` 字符串的条目。例如：

```
# grep 'Packet log' /var/log/messages
```

```
Oct 15 00:10:51 host2 kernel: Packet log: DENY ppp0 PROTO=17
192.168.0.4:137 198.60.22.2:137 L-96 S=0000 I-3096 F=0000 T=127 (#1)
```

要使用 `iptables` 检测入侵，你可以采用为 `ipchains` 描述的方法，并考虑到 `iptables` 更丰富的日志功能。它允许你使用各种选项来控制 `iptables` 如何记录数据包。此功能由 `iptables` 模块提供。

你必须完成的任务是修改 `iptables` 规则，以记录不应通过的流量。你还可以为这些日志条目设置前缀以便于识别，并设置日志级别或设施（或两者都有），以进一步细化日志条目并使其在系统日志中易识别。

使用 `iptables` 进行入侵检测的关键组件是使用新的 `--log-target (-j LOG)`、用于设置日志级别的 `--log-level` 选项，以及用于设置日志条目前缀的 `--log-prefix` 选项。考虑以下规则：

```
# iptables -A FORWARD -p tcp -j LOG --log-prefix "SAMPLE LOG RULE"
```

该规则向转发链（`-A FORWARD`）添加了一条规则，为穿越转发链的 TCP（`-p TCP`）数据包创建一个日志条目，并在每个条目前加上字符串 `"SAMPLE LOG RULE"`。接下面的日志条目代表了此类条目的可能样式：

```
Oct 15 01:43:32 host2 kernel: SAMPLE LOG RULEIN=eth0 OUT=pp0 SRC=192.168.0.3 DST=130.236.136.130.55 LEN=48 TOS=0x00 PREC=0x00 TTL=127 ID=30691 DF= PROTO=TCP SPT=2001 DPT=80 WINDOW=8192 RES=0x00 SYN URG=0
```

按照上一节描述相同步骤配置 `LogWatch`，以创建一个列出记录流量的摘要报告。

# 总结

本章介绍了如何使用标准 Red Hat 安装中提供的工具监控 Red Hat 系统是否受到尝试性、潜在和实际的安全侵入的方法。在学习了如何配置 `Tripwire` 并解读其报告后，你学习了如何设置 `LogWatch` 来监控各种异常情况的文件。你还学习了如何使用 `iptables` 记录活动，以及如何使用 `LogWatch` 监控这些日志条目。

## 第 33 章：故障排除与问题解决

本章描述了 Red Hat Linux 各种子系统和功能可能出现的各种问题，并针对问题提供了解决方案。显然，我们无法涵盖所有可能出错的情况，但我们将涵盖我们遇到过的问题以及解决办法。如果我们的系统运行正常，我们甚至可以预见并防止一些问题。尽管在准备每个 Red Hat Linux 版本时做了大量工作和测试，但意外问题不可避免地会出现。这些问题大多数源于以下三种情况之一：

- 对 Red Hat Linux 进行硬件兼容性测试是不可能的。
- 鉴于可用硬件范围，任何组件组合（如 SCSI 控制器和 SCSI 磁盘）都可能导致细微的不兼容。
- 由于硬件迭代速度极快，为早期版本硬件编写的驱动程序可能不支持最新版本。

本章旨在帮助你排除并解决安装和使用 Red Hat Linux 时可能遇到的常见挑战。特别是本章中的章节将帮助你解决与安装、文件系统、网络和系统启动相关的问题。

### 安装问题

本节讨论的情况包括安装后无法登录系统、最常见的硬件相关陷阱，以及在笔记本电脑上安装 Red Hat Linux。

#### 安装后无法登录

安装 Red Hat Linux 时最常见的问题之一是安装后重启后无法登录。如果你在安装过程中没有创建用户账户，必须以 root 身份登录并创建一个用户账户。同样，如果你忘记了安装期间创建的用户密码，请以 root 用户身份登录并按照此步骤重置密码：

- 在控制台或终端窗口中，输入命令 `passwd`，将 `user` 替换为账户名。
- 输入新密码并按回车。
- 再次输入密码并按回车。
- 注销，然后作为新用户登录，提供你刚刚设置的密码。

如果你忘记了 root 密码，重启并按照以下步骤操作：

- 重启系统。
- 在 GRUB 启动提示符处，选择要启动的内核镜像并输入 `e`（编辑）。
- 使用方向键将光标置于以 `kernel` 开头的行上，再次输入 `e`。这会打开一个 GRUB shell 提示符。
- GRUB shell 提示符应类似于下所示：

```
grub edit> /vmlin-2.4.22-1 root=/
```

按下空格键并输入 `init=/bin/sh`。修改后的行现在应该看起来所示：

```
grub edit> /vmlin-2.4.22-1 root=/ single
init=/bin/sh
```

- 按回车，这将你返回到第 2 步中看到的相同屏幕。
