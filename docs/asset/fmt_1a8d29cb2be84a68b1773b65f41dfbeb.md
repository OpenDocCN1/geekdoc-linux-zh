
```
Bootparam [Low Risk]: 0
BootparamDom [Low Risk]: 0
Finger [Low Risk]: 0
Rusers Output [Low Risk]: 0
Finger Output [Low Risk]: 0
SNMP Public Information [Low Risk]: 0
Old Sendmail Version [Low Risk]: 0
Verify Account Information About Users with Sendmail [Low Risk]: 1
Expand Account Information About Users with Sendmail [Low Risk]: 1
```

可以通过 `sendmail` 验证用户账户并获取信息。你可能需要禁用 `sendmail` 中的 `VRFY` 命令。

```
NNT Daemon [Low Risk]: 0
Trace Routing of Packets [Low Risk]: 1
```

你可以看到数据包如何从你的主机（源主机）发送到目标主机。这为黑客提供了关于你主机的路由和跳数信息。

```
Open/Close Connection Flood [Low Risk]: 0
Old INND Version [Low Risk]: 0
Kerberos User List Vulnerable [Low Risk]: 0
Kerberos Brute Force Vulnerable [Low Risk]: 0
RWH0 Daemon Overflow [Low Risk]: 0
SMTP Timer Abort: 0
Netbios Tests Disabled: 0
Unable to Bind to Ident: 0
Unable to Listen on Ident: 0
Additional Module Output: 0

--------- End of Report ---------
```

其余风险扫描项显示为零，意味着 `ISS` 没有发现那些漏洞。但这并不意味着其他扫描器不会发现有关你主机的信息。

列表 9-4 展示了一份扫描报告，提供了在之前扫描中发现的风险的详细信息。它还提供了针对发现的风险的可能解决方案。

## 列表 9-4：分析报告

```
Internet Security Scanner (C)1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.

Analysis Report

Report of Vulnerabilities

Summary Information

Hosts Scanned: 1
Hosts with Active Services: 1
Hosts with No Services: 0
Start Time: Tue Jul 7 15:40:21 1998
End Time: Tue Jul 7 15:44:12 1998
Total Time: 3 minutes 51 seconds
Scan Completed Normally

Information by Vulnerability

X Check [High Risk]

Open X Displays allows an intruder to capture keystrokes and to execute commands remotely

Use key-based protection scheme, such as xauth.

Was found on the following hosts:
IP Address: 127.0.0.1 Hostname: Could not resolve hostname

Rsh Vulnerable in hosts.equiv [High Risk]

Allows an intruder to log in remotely without a password

Remove the entry containing '+' in the file /etc/hosts.equiv. CERT Advisories: CA-91:12, CA-92:03, CA-92:14

Was found on the following hosts:
IP Address: 127.0.0.1 Hostname: Could not resolve hostname

Files Obtained [Medium Risk]

The files were obtained through various vulnerabilities on the
```

机器，并允许管理员快速检查这些关键文件中的配置错误。

修正获取这些文件的漏洞。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

通过 `rsh` 获取的文件已保存到 `'./127.0.0.1.rsh.files'`

通过 `FTP` 获取的文件已保存到 `./127.0.0.1.anonftp.files`

## 匿名 FTP [低风险]

此机器上启用了匿名 `FTP`。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

## Netstat [低风险]

`Netstat` 会向入侵者提供有关连接、开放端口和受信任主机的信息。

通过将其从 `/etc/inetd.conf` 中注释掉并重启 `inetd` 来禁用 `netstat` 守护进程。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

## Sysstat [低风险]

`Sysstat` 会向入侵者提供在线用户和受信任主机等信息。

通过将其从 `/etc/inetd.conf` 中注释掉并重启 `inetd` 来禁用 `sysstat` 守护进程。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

## 验证关于使用 Sendmail 的用户的账户信息 [低风险]

`VRFY` 允许入侵者确定系统中是否存在特定账户，这为对用户账户进行暴力破解攻击提供了重大帮助。

如果您正在运行 `Sendmail`，请在您的 `Sendmail` 配置文件中添加行 `"Opmvrfy"`，该文件通常位于 `/etc/sendmail.cf`。对于其他邮件服务器，请联系您的供应商以了解如何禁用 `verify` 命令。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

## 扩展关于使用 Sendmail 的用户的账户信息 [低风险]

`EXPN` 允许入侵者确定系统中是否存在特定账户，这为对用户账户进行暴力破解攻击提供了重大帮助。

如果您正在运行 `Sendmail`，请在您的 `Sendmail` 配置文件中添加行 `"O:noexpn"`，该文件通常位于 `/etc/sendmail.cf`。对于其他邮件服务器，请联系您的供应商以了解如何禁用 `verify` 命令。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

## 数据包路由追踪 [低风险]

`Traceroute` 允许您确定数据包在两个主机之间经过的路径。此信息允许他人确定网络拓扑结构以及网络上的路由器。

在以下主机上发现：

IP 地址：127.0.0.1 主机名：无法解析主机名

127.0.0.1

0

--------- 报告结束 ---------

清单 9-5 显示了受信任的主机——那些登录到您的系统时无需密码认证的主机。实际上，您的主机可能拥有与受信任主机相同类型的安全设置——起初这可能看起来很方便，但可能是一个真正的安全隐患。从安全角度来看，这次扫描的结果是好的，因为它显示没有受信任的主机。

清单 9-5：受信任的主机

```
Internet Security Scanner (C) 1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report
```

主机清单

摘要信息

扫描的主机数：1

具有活动服务的主机数：1

无服务的主机数：0

开始时间：1998 年 7 月 7 日 周二 15:40:21

结束时间：1998 年 7 月 7 日 周二 15:44:12

总耗时：3 分 51 秒

扫描正常完成

存活且活动但无主机名

IP 地址：127.0.0.1 主机名：无法解析主机名

被扫描主机信任的主机

未发现受信任的主机。

========= 报告结束 =========

清单 9-6 显示了一份服务报告，展示了在您的主机上发现了哪些服务。它还显示了哪些服务在您的主机上不可用。

清单 9-6：服务报告
