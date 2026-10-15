
750 (Microsoft 文档, 2021), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig

751 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol

PWK - © 2023 OffSec Services Limited. 保留所有权利

制作于摩洛哥

# OffSec

## 使用 Kali Linux 进行渗透测试

要显示包含系统所有路由的路由表，我们可以使用 `route print`。

此命令的输出对于确定指向其他系统或网络的可能的攻击向量有用。

```
PS C:\Users\dave route print
route print
=====================================================
6...00 50 56 8a 80 16 ......vmnet3 Ethernet Adapter
1................................Software Loopback Interface 1
======================================================
```

### IPv4 路由表

活动路由：

| 网络目标地址 | 子网掩码 | 网关 | 接口 | 跃点量 |
| :--- | :--- | :--- | :--- | :--- |
| 0.0.0.0 | 0.0.0.0 | | 192.168.50.220 | 271 |
| 127.0.0.0 | 255.255.255 | 直连 (On-link) | 127.0.0.1 | 331 |
| 127.0.0.0 | 255.255.255 | 直连 (On-link) | 127.0.0.1 | 331 |
| 127.255.255 | 255.255.255 | 直连 (On-link) | 192.168.50.220 | 271 |
| 192.168.50.220 | 255.255.255 | 直连 (On-link) | 192.168.50.220 | 271 |
| 192.168.50.255 | 255.255.255 | 直连 (On-link) | 192.168.50.220 | 271 |
| 224.0.0.0 | 240.0.0 | 直连 (On-link) | 127.0.0.1 | 331 |
| 224.0.0.0 | 240.0.0 | 直连 (On-link) | 127.0.0.1 | 331 |
| 255.255.255 | 255.255.255 | 直连 (On-link) | 127.0.0.1 | 331 |
| 255.255.255 | 255.255.255 | 直连 (On-link) | 192.168.50.220 | 271 |

持久路由：

| 网络地址 | 子网掩码 | 网关 | 跃点量 |
| :--- | :--- | :--- | :--- |
| 0.0.0.0 | 0.0.0.0 | 192.168.50.224 | 默认 |

> 384 - CLIENTWK20 路由表

显示 384 显示没有任何已知网络的路由。然而，我们应该始终检查目标系统的路由表，以确保没有遗漏任何信息。列出所有活动连接可以使用 `netstat -a` 显示所有活动的 TCP 和 UDP 端口，使用 `-n` 禁用解析，使用 `-o` 显示每个连接的进程 ID。

```
PS C:\Users\dave netstat -ano
```

活动连接

| 协议 | 本地地址 | 外部地址 | 状态 | PID |
| :--- | :--- | :--- | :--- | :--- |
| TCP | 0.0.0.0:80 | 0.0.0.0 | 监听 (LISTENING) | 6824 |
| TCP | 0.0.0.0:135 | 0.0.0.0 | 监听 (LISTENING) | 960 |
| TCP | 0.0.0.0:443 | 0.0.0.0 | 监听 (LISTENING) | 6824 |
| TCP | 0.0.0.0:45 | 0.0.0.0 | 监听 (LISTENING) | 4 |
| TCP | 0.0.0.0:336 | 0.0.0.0 | 监听 (LISTENING) | 1752 |
| TCP | 0.0.0.0:3389 | 0.0.0.0 | 监听 (LISTENING) | 1084 |
| TCP | 0.0.0.0:5040 | 0.0.0.0 | 监听 (LISTENING) | 3288 |
| TCP | 192.168.50.220:139 | 0.0.0.0 | 监听 (LISTENING) | 4 |
| TCP | 192.168.50.223:3389 | 192.168.119.4:366 | 建立 (ESTABLISHED) | 1084 |
| TCP | 192.168.50.224:444 | 192.168.119.5:1082 | 建立 (ESTABLISHED) | 2044 |

> 385 - CLIENTWK220 的活动连接

显示 385 通常表示系统上运行着 Web 服务器。此外，3306 端口表明运行着 MySQL^754 服务器。

输出还显示了我们在 4444 端口上的 Netcat 连接，以及来自 192.168.119.4 的 3389 端口的 RDP 连接。我们不是当前连接到系统的唯一用户。我们利用 Mimikatz 提升权限并尝试提取用户凭据。

接下来，我们将检查已安装的应用程序。我们可以使用 `Get-ItemProperty`756 命令查询注册表^755，列出 Windows 注册表中 32 位和 64 应用程序。我们将输出通过到 `select displayname`，以仅显示应用程序名称。我们从 32 位应用程序和 64 位应用程序开始：

```
PS C:\Users\dave> Get-ItemProperty
HKLM:\SOFTWARE\Wo432\Microsoft\Windows\CurrentVersion\Uninstall\* | select displayname
Get-ItemProperty
HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | select displayname
displayname
KeePass Password Safe 2.51
Microsoft Edge
Microsoft Edge Update
Microsoft Edge WebView Runtime
Microsoft Visual C++ 2015-2019 Redistributable (x86) - 14.28.29913
Microsoft Visual C++ 2019 Additional Runtime - 14.28.29913
Microsoft Visual C++ 2019 Minimum Runtime - 14.28.29913
Microsoft Visual C++ 2015-2019 Redistributable (x64) - 14.28.29913
```

# OffSec

使用 Kali Linux 进行渗透测试

## 7-Zip 21.07 (x64)

XAMPP

VMware Tools

Microsoft Visual C++ 2019 X64 Additional Runtime - 14.28.29913

Microsoft Visual C++ 2019 X64 Minimum Runtime - 14.28.29913

列表 386 - CLIENTWK220 上已安装的应用程序

列表 386 显示，在标准 Windows 应用程序之后，CLIENTWK220 上安装了 KeepPass$^{757}$ 密码管理器、7-Zip$^{758}$ 和 XAMPP$^{759}$。

正如在“定位公开漏洞”模块中讨论的那样，在完成信息感知过程后，我们可以为识别出的应用程序搜索公开漏洞。我们还可以利用密码攻击来获取密码器的密码，从而可能获得其他密码，允许我们以特权用户身份登录。

然而，386 中的列表可能并不完整。例如，这可能是由于安装过程不完整或存在缺陷。因此，我们应该始终检查 `C:\` 下的 32 位和 64 位 Program Files 目录。此外，我们应该检查 Downloads 目录的内容以找到更多潜在程序。

虽然在目标系统上创建已安装应用程序列表很重要，但识别其中哪些程序正在运行也同样重要。为了这一点，我们将使用 `Get-Process`760 审查系统进程。

```
PS C:\Users\dave> Get-Process
Get-Process
```
