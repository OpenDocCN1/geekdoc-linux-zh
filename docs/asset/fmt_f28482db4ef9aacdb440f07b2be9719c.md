
基于用户和基于主机的安全是另一个 Linux 安全功能。大多数与 RHCE 关联的服务都可以配置基于用户和基于主机的安全。某些服务可以通过扩展互联网服务守护进程 `xinetd` 进行保护。其他依赖于 TCP Wrappers 库的服务可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件中的规则进行保护，按顺序执行。可以通过 PAM 增强基于用户的安全；基于用户的安全示例位于 `/etc/pam.d/vsftpd` 配置文件。

# 168 第 10 章：安全概述

## 自测

以下填空题可以帮助你衡量对本章相关主题的理解程度。由于 Red Hat 考试中没有单选题，因此书中也没有单选题。如果你在这些问题中的一个或多个上遇到困难，你可能需要进一步研究相关主题。然而，在 Linux 中解决问题几乎总有不止一种方法。在 Red Hat 考试中，获得结果比记背琐碎知识更重要。

由于这是一本练习书，这些问题的答案可能位于正文中。如需更多信息，请参阅《学习指南》。

# 使用 iptables 实现包过滤并配置网络地址转换 (NAT)

- 1. 什么命令可以显示当前配置的基于 `iptables` 的防火墙规则？
- 2. 如果你想允许来自 IP 地址 `192.168.122.130` 的 TCP 包访问端口 `2345`，你会在 `iptables` 命令中添加哪些选项？提示：使用与 `/etc/sysconfig/iptables` 文件中相同的格式。
- 3. 如果你想拒绝来自 IP 地址 `192.168.122.240` 的所有包，你会在 `iptables` 命令中添加哪些选项？
- 4. `iptables` 命令的哪些选项会丢弃所有 ICMP 相关的包，包括与 `ping` 命令相关的包？

# 为服务配置基于主机和基于用户的安全

- 5. 如果 `/etc/hosts.allow` 文件为空，`/etc/hosts.deny` 文件中的哪个条目将阻止对所有使用 TCP Wrappers 服务的访问？
- 6. 如果你将此规则添加到 `/etc/hosts.deny`，则仅允许来自指定 IP 地址的访问，该地址对应于 `whitehat.example.net` 系统。还可以通过 PAM 根据 `/etc/pam.d` 目录下的文件配置基于用户的访问。以下来自 `/etc/pam.d/vsftpd` 的条目说明了拒绝来自 `/etc/vsftpd/ftpasswd` 用户中列出的用户访问的规则：

```
auth required pam_listfile.so item=user sense=deny \
file=/etc/vsftpd/ftpasswd onerr=succeed
```

如果你理解命令行，你会发现上面的反斜杠转义了回车符的含义，回车符在功能上等同于换行。当然，该行位于配置文件中；遗憾的是，反斜杠在该特定文件中同样有效。

为了解释，PAM 使用身份验证管理 `auth` 测试。系统必须通过测试才能继续。后续的规则基于 `/lib64/security` 目录下的 `pam_listfile.so` 库。关于该库如何工作的详细信息，可以在 `pam_listfile` 手页中找到。`item=user` 选项指定 PAM 将检查用户。如果有匹配，则应该拒绝该用户的访问 `sense=deny`。文件是 `/etc/vsftpd/ftpasswd`。如果无法打开文件，则允许用户访问 `onerr=succeed`。

# 172 第 10 章：安全入门

## 实验 2

拦截所有 ICMP 数据包的缺陷之一是它会阻止网络监控。虽然拦截流量有时是有意义的，但你应该知道如何仅拦截 `ping`。设置此类规则最简单的方法是在“防火墙配置”工具的“ICMP 过滤器”部分。它允许你设置防火墙拒绝回显请求 `Echo Requests`，这就是 `ping` 命令的功能。实施后，它会在本地防火墙中添加以下规则：

```
-A INPUT -p icmp -m icmp --icmp-type echo-request -j REJECT \
  --reject-with-icmp-host-prohibited
```

## 实验 3

你们大多数人都知道 `22` 端口是 SSH 服务的标准端口。黑客可能会扫描系统寻找开放的端口。提高安全性的一种方法是通过“隐性策略”。实现隐性策略的一种方法是为关键服务设置非标准端口。

虽然你可以设置 SSH 客户端自动使用非标准端口，但在各种客户端上实现这可能会非常麻烦。另一种设置“隐性”的简单方法是使用端口转发。配置工具让这一切变得简单。如果你在物理主机系统上从虚拟网络设备设置端口转发，你可以将流量从 `22` 端口重定向到指定的端口 `13579`。

```
-A PREROUTING -i eth0 -p tcp --dport 22 -j MARK --set-mark 0x64 COMMIT
-A PREROUTING -i eth0 -p tcp --dport 22 -m mark --mark 0x64 -j DNAT \
  --to-destination:13579
```

它将标准的输入防火墙规则修改为：

```
-A INPUT -i eth0 -m state --state NEW -m tcp -p tcp --dport 13579 \
  -m mark --mark 0x64 -j ACCEPT
```

如果你更改了 SSH 服务器的配置，现在应该能够从网络上的其他系统正常登录 SSH 服务器了。

为了将来，你可能想要恢复原始配置。要这样做，你需要：

- 在本地防火墙中删除指定的将 `22` 端口流量转发到 `13579` 端口的三个规则。
- 删除 `/etc/ssh` 目录下 `sshd_config` 文件中的端口 `13579` 指令，然后使用类似 `/etc/init.d/sshd reload` 的命令重新服务。

## 实验 4

首先，你可以通过以下命令确认对 SSH 服务器的访问受到 TCP Wrappers 的监管：

```
# ldd /usr/bin/sshd | grep libwrap.so.0
```

用于监管访问的 TCP Wrappers 文件是 `/etc/hosts.allow` 和 `/etc/hosts.deny`。有几种不同的指令组合可以禁止来自黑客系统的访问。实现此点的一种方法是在 `gamma.example.net` 系统的 `/etc/hosts.deny` 文件中添加以下指令：

```
sshd : 192.168.122.240
```

当然，你也可以通过基于 `iptables` 的防火墙禁止访问。假设你保留了默认的 TCP 端口 `22`，你可以在接受来自其他系统连接的规则之前添加以下规则：

```
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.122.240 --dport 22 -j REJECT
```

然而，TCP Wrappers 也是一个重要的安全工具。在某些时刻，你可能会被要求同时使用这两个系统创建一个分层安全模型。

## 实验 5

满足此实验要求有两种基本方法。你可以为 `/etc/vsusers` 中列出的用户设置 `DenUsers` 或可能是 `DenyGroups` 指令。

在 `gamma.example.net` 系统的 `/etc/hosts.deny` 文件中添加以下指令：

```
sshd : 192.168.122.240
```

- 在本地防火墙中删除指定的将 `22` 端口流量转发到 `13579` 端口的三个规则。
- 删除 `/etc/ssh` 目录下 `sshd_config` 文件中的端口 `13579` 指令，然后使用类似 `/etc/init.d/sshd reload` 的命令重新加载。
