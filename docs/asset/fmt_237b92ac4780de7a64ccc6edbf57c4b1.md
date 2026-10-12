
```
msf info ii40_command
Name: msf/windows/ii40: Buffer Overflow
Class: exploit
Rank: 1.7
Payload: cmd/meterpreter/reverse_tcp
Encoding: none
Platform: windows
Created: 18 Oct 2002
Provided By: 
Available Targets:
Windows XP
Windows 2000
Windows Vista
Available Options:
optional: SSL target address
required: target port
Payload Information:
cmd/meterpreter/reverse_tcp
Encoder: none
BadChars: meson tunnel hide reverse
Encoder Information:
Description: 利用用于执行代码的 HTTP DLL 中的缓冲区溢出。操作是 32 位的。此方法仅在带 SSL 调用服务器时有效。在执行负载后响应请求。该漏洞提供了一个可靠的基于绑定 shell。如果你使用 HTTP，服务器在执行漏洞后将崩溃。使用 NOP 滑块，否则数据会被过滤器误改。
```

`msfweb` 界面返回的信息比 `msfview` 更详细。特别是负载（payload）部分提供了 Web 界面中无法获取的漏洞详情。负载部分列出了负载可用的空间大小、负载生成阶段可用的坏字符数量以及关键信息。MSF 引擎密钥用于确定哪些负载可以与漏洞配合。NOP 部分详细说明了 NOP 滑块不能修改的寄存器，以及可选的关键信息。编码器部分包含了关于默认编码器的信息或关键信息，具体取决于编码器模块。

接下来，我们通过输入 `use ii40_command` 使用编码器来加载 IIS 4 漏洞。通过默认启用的 Tab 补全，用户可以输入 `ii4` 并按 Tab 键完成漏洞名称。选择一个编码器模块还会会在全局环境之上加载临时框架环境。临时环境继承全局环境中的任何变量，在发生命名冲突时，变量的优先级更高（图 12.21）。

# 图 12.21 选择利用程序

```
msf >
msf >
msf >
msf >
msf > use linux48_btr
msf > linux48_btr >
```

当选择一个利用程序时，`msfconsole` 界面会从主利用模式切换，可用命令列表将反映利用模式的选项。例如，`show` 命令显示有关模块的特定信息，而不是可用利用程序、编码器或 NOP 的列表。`help` 命令显示了利用模式的命令列表（见图 12.22）。

# 图 12.22 利用模式命令列表

```
Metasploit Framework Console Help
=
back        显示主控制台帮助
cd          返回主菜单
check       执行漏洞检查
exit        退出控制台
exploit     显示上下文利用程序帮助
help        显示当前利用程序或载荷信息
info        退出控制台
quit        执行漏洞检查
reload      重新加载利用程序和载荷
reusable   重新加载并利用，适用于测试员类型
set         设置临时环境变量
show        显示选项、高级选项、载荷或目标
unset       移除临时环境变量
use         按名称选择利用程序
version     显示控制台版本
```

我们看到了新的命令。`set` 和 `unset` 命令之所以可用，是因为我们正处于临时环境中。在利用程序模块特定的环境内，我们可以使用 `set` 来指定变量与值的关联，并可以使用 `unset` 来移除绑定（见图 12.24）。如图 12.23 所示，执行 `back` 命令后退出利用模式，临时环境被恢复到带有全局环境的主模式。

# 图 12.23 退出利用模式

```
MSFConsole
msf iis40_htr > back
msf > set
msfconsole: set: command not found
msf >
```

现在利用模式中可以使用新命令了，且 `show` 命令现在可以接受不同的参数：目标、载荷、选项和高级选项。如图 12.24 所示，`show targets` 命令列出了适用于 IIS 4.0.HTR 缓冲区溢出利用程序的可用目标。在 MSE 中，每个目标都指定了运行漏洞应用程序的不同远程平台。MSF 引擎根据目标平台构建攻击。选择错误的目标会导致利用程序无法工作并可能导致漏洞应用程序崩溃。由于我们知道远程目标运行的是 Windows NT 4 Service Pack 5，因此使用 `TARGET 2` 命令设置目标平台（见图 12.24）。注意，我们正在使用新的 `set` 命令将临时环境变量 `TARGET` 与一个值关联。我们通过运行不带参数的 `set` 来验证 `TARGET`。

# 图 12.24 设置目标平台

```
MSFConsole
msf iis40_htr > show targets
Supported Exploit Targets:
=============
0 Windows NT4 SP
1 Windows NT4 SP5
2 Windows NT4 SP5

msf iis40_htr > set TARGET 2
TARGET = 2
msf iis40_htr > set
```

选择目标后，我们必须向 MSE 引擎提供有关远程主机的额外信息。这些信息通过框架环境变量提供；可以通过 `show options` 命令获取所需的环境变量列表。`show options` 命令的结果表明，在运行利用程序之前必须设置 `RHOST` 和 `RPORT` 环境变量（见图 12.25）。要设置 `RHOST`，当目标机器 IP 地址为 192.168.46.131 时，用户输入命令 `set RHOST 192.168.46.131`。远程端口（RPORT）已经有一个与我们的目标一致的默认值。从我们运行 `set TARGET 2` 命令开始，目标已经设置为 Windows NT4 SP5。

# 图 12.25 设置利用程序选项

```
MSFConsole
msf iis40_ht > show options
Exploit Options
-----------------
Exploit:      Name        Description
optional    SSL         Use SSL
required    HOST        The target address
required    PORT        80          The target port
Target: Windows NT4 SP5
msf iis40_ht > _
```

记住，`set` 命令只修改当前所选利用程序的临时环境变量值。如果用户想对同一台机器尝试多次利用，`set` 命令是更好的选择。MSF 引擎的每个实例都会记住每个利用程序模块的临时环境。如果我们进入利用模式、退出再重新进入，之前定义的临时环境会被重新加载。

根据利用程序的不同，可能还有高级选项。这些变量也通过 `set` 命令设置（见图 12.26）。

# 图 12.26 高级选项

```
MSFConsole
msf iis40_ht > show options
Exploit Options
-----------------
Exploit:      Name        Description
optional    SSL         Use SSL
required    HOST        The target address
required    PORT        80          The target port
Target: Windows NT4 SP5
msf iis40_ht > _
```

接下来，为利用程序选择一个可以在目标平台上运行的载荷（payload）。假设载荷是攻击者在目标系统上执行的“任意代码”。MSF 与大多数公开的独立利用程序不同的一个点是它能够选择任意载荷，这允许用户选择最适合网络状况的载荷。在图 12.27 中，当我们运行 `show payloads` 命令时，框架会显示一个兼容的载荷列表。通过 `set PAYLOAD win32_bind` 指令，在利用程序配置中指定了一个 shell。

# 图 12.27 设置载荷
