
要使用 `xinetd` 拒绝所有机器对所有服务的访问，相当于在 `/etc/hosts.deny` 中设置 `ALL:ALL` 是在 `/etc/xinetd.conf` 的 `defaults` 部分中使用 `no_access` 属性：

```
no_access = 0.0.0.0
```

`0.0.0.0` 匹配所有 IP 地址（类似于 TCP wrappers 中的 `ALL`）。

另一种方法是使用 `only_from` 属性并不给该属性分配任何值：

```
only_from =
```

这种方法更好，因为稍后我们将添加要连接的特定主机。因此，我们将从设置 `only_from` 为空开始。

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

现在，我们的防御措施（拒绝来自黑客的 telnet 连接并仅允许来自 `server1.example.com` 的 telnet 连接）需要在 `telnet` 服务部分中添加以下内容：

```
only_from += server1.example.com
```

## 第 13 章：访问控制与防火墙

提示 我们可以使用 `access_times` 属性限制时间段的访问：`access_times=8:00 - 17:00`

### 伪造“信任”的反向 DNS 条目

| 流行度: | 7 |
| 简单性: | 10 |
| 影响: | 8 |
| 风险等级 | 7 |

黑客知道你的 wrapper 机器所在的域名。他可能假设你的域中的所有机器都允许 TCP wrapper 访问，这通常是事实。因此，他可能会尝试为他的主机反向 DNS 条目使其显示在你的域名中，如下：

```
hackmachine$ host hackmachine.example.com

hackmachine.example.com has address 192.168.15.10

hackmachine$ host 192.168.15.10
```

10.15.168.192.IN-ADDR.ARPA 域名指针 trusted.target_network.com

> 黑客希望进入 `target_network.com`，他设置了他的反向 DNS 条目使其显示在信任域中。

### 伪造反向 DNS 条目的防御措施

这种攻击对于没有采取一个简单预防措施的软件非常有效：同时检查正向和反向 DNS 查询。TCP wrappers 查找 IP 地址（192.168.15.10（上述情况）），如下所示它返回 `trusted.target_network.com`。然而，TCP wrapper 库随后查找 `trusted.target_network.com`：

```
target$ host target_network.com

target_network.com has address 10.28.62.502
```

由于反向和正向映射不匹配，TCP wrapper 库将不允许 `/etc/hosts.allow` 中的任何主机名匹配。

注意 软件曾犯过不检查反向 DNS 的错误。因此，如果你编写或下载了一个 socket 程序，请用 TCP wrappers 包装它，它将保护你免受此漏洞的侵害。如果你自己开发网络程序，可以通过链接 TCP wrapper 库来自动包含 TCP wrapper 支持（即使对于不依赖 `inetd` 的守护程序）。我们将在本章后面提供此方面的示例。

# 破解 Linux 暴露：Linux 安全秘密与解决方案

当 TCP wrappers 使用 `-DPARANOID` 选项编译时，它们将丢弃任何正向和反向 DNS 条目不匹配的机器的连接。这让许多无法修复其 DNS 条目的系统管理员警觉。然而，拥有匹配的记录是你开始相信主机确实是其声称的身份的唯一方法。毕竟，如果管理员不能保持其记录同步，你如何信任这些系统呢？

如果你自己编译 TCP wrappers，请指定 `-DPARANOID` 选项。大多数发行版默认如此。

### 信任域中的攻击者

| 流行度: | 4 |
| 简单性: | 10 |
| 影响: | 9 |
| 风险等级 | 8 |

你怀疑 IP 为 `trouble.example.org` 的员工准备离开公司。他有些心存不满，并一心想要损害公司。你想保护你的数据不被盗取。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

现在，我们的防御措施（拒绝来自黑客的 telnet 连接并仅允许来自 `server1.example.com` 的 telnet 连接）需要在 `telnet` 服务部分中添加以下内容：

```
only_from += server1.example.com
```

## 第 13 章：访问控制与防火墙

注意 软件曾犯过不检查反向 DNS 的错误。因此，如果你编写或下载了一个 socket 程序，请用 TCP wrappers 包装它，它将保护你免受此漏洞的侵害。如果你自己开发网络程序，可以通过链接 TCP wrapper 库来自动包含 TCP wrapper 支持（即使对于不依赖 `inetd` 的守护程序）。我们将在本章后面提供此方面的示例。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

### 非 inetd/xinetd 的攻击

| 流行度: | 6 |
| 简单性: | 8 |
| 影响: | 6 |
| 风险等级 | 7 |

并不是所有的互联网服务都是由 `inetd` 发起的。一个例子是 `Ssh`。

你怀疑 IP 为 `trouble.example.org` 的员工准备离开公司。他有些心存不满，并一心想要损害公司。你想保护你的数据不被盗取。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```
