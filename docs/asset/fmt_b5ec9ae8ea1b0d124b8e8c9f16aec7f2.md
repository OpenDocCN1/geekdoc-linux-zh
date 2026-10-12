
## 列表 626 show 命令的帮助标志位

列表 626 显示了 Metasploit 模块的类别。要激活一个模块，我们需要使用 `use` 配合模块名。所有模块都遵循通用的斜杠分隔分级语法（模块类型/操作系统、供应商、应用、操作或协议/模块），这使得探索和使用模块变得非常容易。我们将在下一节探索辅助模块（auxiliary modules），并深入研究利用模块（exploit modules）。

### 20.1.2 辅助模块

Metasploit 框架包含了数百个辅助模块，提供了如协议枚举、端口扫描、模糊测试（fuzzing）、嗅探（sniffing）等功能。辅助模块对于许多任务非常有用，包括信息收集（在 `gather/` 层级下）、各种服务的扫描和枚举（在 `scanner/` 层级下）等。

这里还有更多内容，但我们将演示两个辅助模块的策略和操作。要列出所有模块，可以运行 `show auxiliary` 命令。这将呈现所有辅助模块列表，如截断输出所示：

```bash
msf6 auxiliary(scanner/ports/tcp) > show auxiliary
```

Auxiliary
=========
| Name | Rank | Description |
...985 auxiliary/scanner/smb/impacket/docomeexec 2018-03-19 normal | No DCOM Exec
986 auxiliary/scanner/smb/impacket/secretsdump normal | No DCOM Exec
987 auxiliary/scanner/smb/impacket/wmiexec 2018-03-19 normal | No WMI Exec
988 auxiliary/scanner/smb/pipe/pipe_auditor normal | No SMB Session
989 auxiliary/scanner/smb/pipe/pipe_auditor normal | No SMB Session
990 auxiliary/scanner/smb/logged_users normal | No Authenticated In
991 auxiliary/scanner/smb/enum_g normal | No Group Enumeration
992 auxiliary/scanner/smb/enum_hashes normal | No Hash Discovery
993 auxiliary/scanner/smb/enumusers normal | No Enumeration
994 auxiliary/scanner/smb/smb_domain normal | No Domain Enumeration
995 auxiliary/scanner/smb/smb_login normal | No Login
996 auxiliary/scanner/smb/smb_lookups normal | No Enumeration
997 auxiliary/scanner/smb/ms17_01 normal | MS1701
998 auxiliary/scanner/smb/smb_cred normal | No Credential
999 auxiliary/scanner/smb/smb_version normal | Version Detection

# OffSec

使用 Kali Linux 进行渗透测试

制作于摩洛哥

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Kali-logo.png/200px-200px-Kali-logo.png)

在进入下一节之前，让我们再次简单回顾模块。如所述，模块用于在 Metasploit 中执行任务，如扫描或利用目标。该框架包含数千个模块，分为若干类别。

类别显示在启动屏幕摘要中，但我们也可以使用 `show -h` 命令查看它们。

```bash
msf6 > -h
[*] "show" 命令的有效参数为: all, encoders, nops, exploits, payloads, auxiliary, post, plugins, info, options
[*] 额外的模块特定参数为: missing, advanced, evasion, actions
msf6
```

## 列表 628 - 列出所有辅助模块

列表 628 显示了 Metasploit 模块的类别。要激活一个模块，我们需要使用 `use` 配合模块名。

```bash
msf6 > use 56
msf6 auxiliary(scanner/smb/smb_version) >
```

## 列表 629 - 激活 smb_version 模块

列表 629 显示我们已经激活了 `smb_version` 模块，如命令行提示符所示。

要获取当前激活模块的信息，我们可以输入 `info`。

```bash
msf6 auxiliary(scanner/smb/smb_version) > info
```

Name: SMB 版本检测

Module: auxiliary/scanner/smb/smb_version

License: Metploit Framework (BSD)

Rank: Normal

Provided by:

hdm <@hdm.io>

Spencer McIntyre

Christophe De France

Check supported:

No

Basic options:

Name Current Setting Required Description

RHOSTS yes 目标主机(s)，见 https://github.com/rapid7/4-metasploit-framework/wiki/Using-Metploit

THREADS 1 yes 线程数（每个主机最多一个）

Description:

指纹并显示 SMB 服务器的版本信息。

将报告协议和主机操作系统（如果可用）。操作系统检测需要远程服务器支持 SMB 协议版本1。

## 列表 630 - 显示 smb_version 模块的选项

```msf6 auxiliary(scanner/smb/smb_version) > show options
```

模块选项 (`auxiliary/scanner/smb/smb_version`):

Name Current Setting Required Description

# OffSec

使用 Kali Linux 进行渗透测试

| RHOSTS | yes | 目标主机(s)... |

| --- | --- | --- |

| THREADS 1 | yes | 并发线程数（每个主机最多一个） |

列表 631 - 显示 `smb_version` 模块的选项

列表 631 显示 `RHOSTS` 选项没有设置值，但它是模块所必需的。

要显示所有必需但尚未设置的选项，我们可以使用 `show missing` 命令。

我们可以使用 `set` 和 `unset` 从选项中添加或删除值。让我们将 `RHOSTS` 选项的值设置为 BRUTE2（注：此处原文表述为 set the value for the option RHOSTS to BRUTE2）。

```
msf6 auxiliary(scanner/smb_version) > set RHOSTS 192.168.50.202
RHOSTS => 192.168.50.202
```

列表 632 - 手动设置选项 `RHOSTS` 的值

与其手动设置，我们还可以利用数据库中的结果以自动化方式设置 `RHOSTS` 的值。例如，我们可以使用 `services` 命令将 `RHOSTS` 设置为所有开启了 445 端口的主，使用 `-p` 指定端口号，使用 `--hosts` 设置选项的结果。在此之前，我们将手动取消设置当前值。

```
msf6 auxiliary(scanner/smb_version) > unset RHOSTS
Unsetting RHOSTS....
```

```
msf6 auxiliary(scanner/smb_version) > services -p 445 --hosts
Services
=====
```

| host | port | proto | name | state | info |

| --- | --- | --- | --- | --- | --- |

| 192.168.50.202 | 445 | tcp | microsoft-ds | open | |

| RHOSTS => 192.168.50.202 | | | | | |

列表 633 - 通过数据库结果自动化地设置 `RHOSTS`
