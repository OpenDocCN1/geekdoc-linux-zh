
一旦配置了 DHCP 服务器，配置 Solaris 客户端就非常简单了。在安装客户端时，系统会询问你是否希望安装 DHCP 支持。此时，你应该回答是。相应地，你不会像普通安装那样被要求输入静态 IP 地址，因为这将由 DHCP 服务器通过 `OFFER` 消息提供。

如果你想在已安装的客户端上支持 DHCP，将需要使用 `sys-unconfig` 命令，该命令可用于所有系统重新配置网络和系统设置，而无需手动编辑配置文件。`sys-unconfig` 命令会重启系统以执行此任务，因此用户在重新配置开始前将获得充分警告。再次，在配置期间你会被询问是否安装 DHCP 支持，你应该回答是。

配置完成后，客户端 `dhcpagent` 由 `ifconfig` 管理——尽管 `dhcpagent` 可以手动启动，但它通常是由 `ifconfig` 针对特定接口启动的。此过程允许最初获取租约，并在接口仍空闲时随后续租。

# 配置 Windows DHCP 客户端

为 Microsoft Windows 客户端设置支持很容易——只需在网络控制面板的 TCP/IP 部分选择 DHCP 支持选项，这在大多数 Windows 版本中都能找到。图 38-3 显示了 Windows 95 的 DHCP 客户端。一旦启用 DHCP 支持，就不需要输入任何静态 IP 地址信息。

# 练习 39-1：配置和取消配置 DHCP 服务

此练习要求你配置和取消配置 DHCP 服务。例如，为 `paulwatters.com` 域设置 DHCP 服务器，DNS 服务器为 `204.56.54.22`，租用时间为 14400 秒（4 小时），以下命令序列将：

- 识别本地 DNS 服务器的 IP 地址：

```
# grep nameserver /etc/resolv.conf
```

- 识别本地 DNS 域：

```
# cat /etc/defaultdomain
```

- 配置服务：

```
# dhcpconfig -D -r SUNWbinfiles -p /var/dhcp -l 14400 \
-d paulwatters.com -a 204.56.54.22 -h dns -y paulwatters.com
```

- 取消配置服务：

```
# dhcpconfig -U -f -x -h
```

# 第 38 章：DHCP

695

![](img/0ce985fd07a5af27ed793d64cf4b977d_722_0.png)

图 38-2 Microsoft Windows 的 DHCP 客户端

> 考试提示 你应该能够识别 `dhcpmgr` 的主要功能。

## 总结

在本章中，我们研究了如何使用 `dhcpconfig` 和 `dhcpmgr` 设置 DHCP 服务。我们涵盖了如何通过 `dhtadam` 手动编辑 `dhcptab`。此外，我们讨论了如何配置 Solaris 和 Windows DHCP 客户端。最后，我们回顾了需要时如何取消配置。

## 问题

1. 配置 DHCP 服务器的命令是？

A. `dhcpagent`

B. `dhcpd`

C. `dhcpconfig`

D. `dhcps`

2. DHCP 客户端命令是？

A. `dhcpconfig`

B. `dhcpd`

C. `dhclient`

D. `dhcps`

3. 配置 DHCP 服务时会被询问什么？

A. 时区

B. NIS 服务器

C. NIS 支持

D. DHCP 支持

4. 手动更新 `dhcptab` 的命令是？

A. `dhtadam`

B. `dhcpconfig`

C. `dhcpd`

D. `dhcpagent`

5. 哪种 IP 提供的地址最多？

A. `IPv4`

B. `IPv6`

C. `IPv8`

D. 以上都不是

6. Solaris 支持哪些 协议？

A. `IPv4` 和 `IPv6`

B. `IPv6` 和 `IPv8`

C. `IPv4` 和 `IPv8`

D. 以上都不是

7. DHCP 提供什么？

A. 静态 IP 地址

B. 每个接口多个 IP 地址

C. 租约 IP 地址

D. 防墙

8. BOOTP 和 DHCP 之间的关系是？

A. DHCP 是 BOOTP 的超集。

B. BOOTP 用于 Windows；DHCP 用于 Solaris。

C. BOOTP 用于 Linux；DHCP 用于 Solaris。

D. DHCP 是 BOOTP 的子集。

9. DHCP 集成了哪些其他协议？

A. LDAP

B. SNMP

C. BOOTP

D. 以上都是

10. 客户端寻找 IP 地址的广播消息是？

A. `DHCPACK`

B. `DHCPCPIND`

C. `DHCPDISCOVER`

D. `DHCP_TX`

11. 服务器提供 IP 地址的广播消息是？

A. `DHCPOFFER`

B. `DHCPCPERVE`

C. `DHCERVICE`

D. `DHCP_SRV`

12. 客户端结束 IP 地址的广播消息是？

A. `DHCPCPEND`

B. `DHCPFINISH`

C. `DHCPPRELEASE`

D. `DHCP_END`

13. 服务器无法按指定提供 IP 地址的广播消息是？

A. `DHCPCPFAIL`

B. `DHCPNACK`

C. `DHCPPOFF`

D. `DHCP_NO_CAN_DO`

14. 服务器确认租约发送的消息是？

A. `DHCPPOK`

# Sun 认证 Solaris 9.0 系统与网络管理员全合一考试指南

- B. `DHCPGOOD`
- C. `DHCPPACK`
- D. `DHCPBACK`
- 15. 客户端使用什么命令通过 DHCP 指定接口配置？

  - A. `dhcp`
  - B. `dhcpd`
  - C. `ifconfig`
  - D. `route`

## 答案

- 1. DHCP 服务器命令在 `dhcpd` 中。
- 2. DHCP 客户端命令是 `dhcpagent`。
- 3. 在配置 DHCP 服务时，系统不会提示 LDAP 服务器名称。
- 4. `dhtadm` 命令用于手动更新 `dhcptab` 的内容。
- 5. Solaris 同时支持 `IPv4` 和 `IPv6`。
- 6. Solaris 同时支持 `IPv4` 和 `IPv6`。
- 7. DHCP 提供租约 IP 地址。
- 8. DHCP 是 BOOTP 的超集。
- 9. DHCP 与 BOOTP 集成。
- 10. `DHCPDISCOVER` 是由寻找 IP 地址的客户端广播的。
- 11. `DHCPPOFFER` 是提供 IP 地址的服务器广播的。
- 12. `DHCPRELEASE` 是由完成 IP 地址使用的客户端广播的。
- 13. `DHCPNACK` 是无法提供指定 IP 地址的服务器广播的。
- 14. `DHCPPACK` 是服务器确认租约时发送的。
- 15. 客户端使用 `ifconfig` 命令通过 DHCP 指定接口配置。

# 网络时间协议

在本章中，你将：

- 学习网络时间协议 `NTP` 的特性
- 学习企业系统和网络如何使用 `NTP`
- 复习配置 `NTP` 服务器的步骤
- 复习配置 `NTP` 客户端的步骤
- 学习 `NTP` 支持的访问控制和身份验证方法

网络时间协议 `NTP` 为单个系统和系统网络上的准确时间和日期标准化和同步提供了一个框架。

时间可能相对于观察者，但保持准确且一致的时间为运行在本地服务器和跨网络上的应用程序提供了至关重要的参考。想象一个数据库应用程序，它在网上银行系统的临时数据库中记录银行余额。每个账户的最新余额在更新时，将始终插入 `accounts` 表的 `balance` 列，并使用两个主键来识别余额：`account_name` 和 `timestamp`。每当需要输入最新余额时，就会向 `accounts` 表插入一条带有 `account_name`、`balance` 和 `timestamp` 的新行。所有其他交易（如取款）都要求从系统中确定最新余额（出于安全考虑，不允许更新行）。如果系统没有一致地维护日期和时间，可能会导致根据分配的错误时间戳进行选择，而错过当前的真实银行余额。

这种差异显然使账户变得毫无用——对于 `account_name` `95639636`，`accounts` 表中已插入了两个余额。图 39-1 展示了这种场景：`$18,475.90` 是 2002 年 1 月 1 日 18:54:21 的余额；`$17,475.90` 是 2002 年 1 月 1 日 18:59:22 的余额。这组条目表明在第一笔交易一秒后发生了了 `$1,000` 的取款。如果系统时钟的精度未达到一秒以内，那么在运行未来的查询时，可能会报告 `$18,475.90` 的错误余额。

# Sun Celtic Solaris 9.0 系统与网络管理员全合一考试指南

702

| account_name | Balance | timestamp |
| :--- | :--- | :--- |
| 95639656 | 18475.90 | 01012002185421 |
| 95639656 | 17475.90 | 01012002185422 |

**图 39-1**

使用时间戳插入数据库记录需要准确的时间计时。
