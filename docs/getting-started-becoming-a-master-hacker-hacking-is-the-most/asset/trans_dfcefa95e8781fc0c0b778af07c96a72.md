
……利用该模块，它会显示**所有**载荷，这是一个**非常**长的列表（超过 500 个）。

正如你在上面的截图中所见，`show payloads` 命令列出了所有与该利用模块兼容的载荷。

msf > show options
此命令在运行利用模块时也非常有用。它会显示运行该模块前需要设置的所有选项（变量）。这些选项包括 IP 地址、URI 路径、端口号等。

在大多数利用模块中，你会看到以下选项（变量）。

- RHOSTS - 这是远程主机或目标 IP（在 Metasploit 4 中为 RHOST）
- LHOST - 这是本地主机或攻击者 IP
- RPORT - 这是远程端口或目标端口
- LPORT - 这是本地端口或攻击者端口

所有这些都可以使用 SET 命令来设置，后面跟着变量名（例如 RHOST）和值，例如：msf5 > SET RHOST 192.168.1.101

较少使用的命令是“show targets”。每个利用模块都有一个它能工作的目标列表。通过使用“show targets”命令，我们可以获取这些目标的列表。在这种情况下，目标选择是自动的，但某些利用模块拥有多达 100 个不同的目标，成功往往取决于你选择了正确的那个。这些目标可以由目标操作系统、服务包、语言以及其他因素定义。

msf5 > show targets

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_319_0.png)

# msf5 > info

**info** 命令很简单。当你**在**选择模块之后输入它时，它会显示该模块的关键信息。

如果你往下滚动一点，你可以看到更多信息，包括需要设置的选项、载荷空间的大小、模块的描述以及关于它所利用漏洞的参考链接。

我通常在选定利用模块后运行此命令。它帮我在使用之前了解利用模块的关键特性。

```
msf5 > set
```

此命令用于设置你所选模块中的选项。例如，如果我们回顾上面的 **show options** 命令，我们可以看到许多必须设置的选项，例如 **URIPATH, SVRHOST** 和 **SVRPORT**。我们可以使用 set 命令设置这些变量中的任意一个，例如：msf5 > set SRVPORT 80

这将默认的 SVRPORT（服务器端口）从 8080 更改为 80。

```
msf5 > unset
```

正如你可能预期的那样，此命令**取消设置**之前已设置的选项。例如：msf5 > unset SRVPORT

如图所示，我们首先将 SRVPORT 变量设置为 80，然后取消设置它。随后它恢复为默认值 8080，这可以在我们再次输入 show options 时看到。

msf5 > exploit
一旦我们加载了利用模块并设置了所有必要的选项，最后的操作是“**exploit**”。这将利用代码发送到目标系统，如果成功，则安装载荷。

利用过程开始并以后台作业运行，在 4444 端口上有一个反向处理器。然后该利用模块在主机 0.0.0.0 的 80 端口上启动了一个 Web 服务器，并带有随机生成的 URL（F5pmyl9gCHVGw90）。我们可以通过使用 set 命令修改 URIPATH 变量来选择特定的 URL 并**设置**它。

```
msf5 > back
```

我们可以使用 back 命令将我们的操作过程“后退”一步。例如，如果你决定不想使用 adobe/flash/avm2 利用模块，可以输入“back”，它将移除已加载的利用模块。

```
msf5 > exit
```
exit 命令，正如你所预期的那样，会让我们退出 msfconsole，回到 BASH 命令 shell。

注意，在这种情况下，它停止了我们在该利用模块中创建的 web 服务器，并让我们返回到 BASH shell 中的 Kali 命令提示符。

# 查找合适模块的策略
作为 Metasploit 的新手，“search”命令可能是最实用的。当 Metasploit 还很小且较新时，找到你需要的正确模块相对容易。现在，随着拥有超过 3000 个模块，找到恰到好处的模块可能会耗时且困难。Rapid7 从第 4 版开始添加了搜索功能，它已成为节省时间和生命的工具。对于初学者想要有效地使用 Metasploit，理解搜索功能至关重要。

```
msf5 > search type:exploit platform:windows flash
匹配模块
===========
# 名称 披露日期 排名 检查 描述
0 exploit/multi/browser/flash_backing_text_uif 2015-07-00 优秀 否 Adobe Flash Player 背层文本 UIF
1 exploit/multi/browser/flash_heimisser_bof 2015-06-23 优秀 否 Adobe Flash Player NellyPlayer 音频解码缓冲区溢出
...
```

msf5 > search

虽然你可以使用搜索功能在模块名称中搜索关键词，但这种方法并不总是高效的，因为它通常会返回一个**非常**大的结果集。

为了使搜索更具体，你可以使用以下语法。

- platform - 这是该模块针对的操作系统
- type - 这是模块的类型。例如，type:exploit
- name 或 keyword - 模块的名称或其描述中的关键词

使用 search 的语法是关键字；后跟冒号；然后是值，例如：msf5 > search type:exploit
例如，如果你正在寻找一个用于在 Windows（平台）上利用 Adobe Flash（关键词）的模块（类型），你可以通过输入以下命令显示所有相关的利用模块：msf5 > search type:exploit platform:windows flash

如上所示，Metasploit 在其数据库中搜索了针对 **Windows** 平台的 **exploits** 且包含关键词“**flash**”的模块，并找到并显示了全部 30 个。

虽然这并不是一份详尽的 Metasploit 命令列表，但仅凭这些命令，你应该能够执行 Metasploit 中大多数功能。当课程中需要其他命令时，我会花几分钟介绍它，但目前你可能只需要这些。

# **Metasploit 目录结构**

```
root@kali-2019:~# cd /usr/share/metasploit-framework
root@kali-2019:/usr/share/metasploit-framework# ls -l
total 148
drwxr-xr-x  4 root root 4096 Jun 19 15:13 app
drwxr-xr-x  3 root root 4096 Jul 11 09:31 config
drwxr-xr-x 22 root root 4096 Jul 11 09:31 data
drwxr-xr-x  3 root root 4096 Jul 11 09:31 db
lrwxrwxrwx  1 root root   27 Jun 19 15:15 documentation -> ../doc/metasploit-framework
drwxr-xr-x  1 root root 1235 Jul  2 15:55 Gemfile
-rw-r--r--  1 root root 10153 Jul  5 03:18 Gemfile.lock
drwxr-xr-x 15 root root 4096 Jul 11 09:31 lib
-rw-r--r--  1 root root  8844 Jul  5 03:18 metasploit-framework.gemspec
drwxr-xr-x  9 root root 4096 Jun 19 15:14 modules
drwxr-xr-x  1 root root  1263 Jul  5 03:18 msfconsole
drwxr-xr-x  1 root root  2813 Jul  5 03:18 msf
drwxr-xr-x  1 root root  5326 Jul  5 03:18 msfdb
-rw-r--r--  1 root root   635 Jul  5 03:18 msf-json-rpc.ru
drwxr-xr-x  1 root root  2229 Jul  5 03:18 msfrpc
drwxr-xr-x  1 root root  9677 Jul  5 03:18 msfrpcd
drwxr-xr-x  1 root root   166 Jul  5 03:18 msfupdate
drwxr-xr-x  1 root root 13069 Jul  5 03:18 msfvenom
-rw-r--r--  1 root root   551 Jul  5 03:18 msf-ws.ru
drwxr-xr-x  2 root root 4096 Jul 11 09:31 plugins
drwxr-xr-x  1 root root  1299 Jul  2 15:55 Rakefile
drwxr-xr-x  1 root root   876 Jul  5 03:18 ruby
drwxr-xr-x  1 root root  1470 Jul  5 03:18 script-exploit
drwxr-xr-x  1 root root   141 Jul  5 03:18 script-password
drwxr-xr-x  1 root root   138 Jul  5 03:18 script-recon
drwxr-xr-x  6 root root 4096 Jun 19 15:14 scripts
drwxr-xr-x 11 root root 4096 Jun 19 15:14 tools
drwxr-xr-x  3 root root 4096 Jun 19 15:14 vendor
root@kali-2019:/usr/share/metasploit-framework#
```

当我刚开始使用 Metasploit 时，我发现它相当晦涩且难以解读。它就像一个黑盒。只有当我熟悉了交互式界面（msfconsole）背后的目录结构后，我才开始窥探这个黑盒内部，顿悟豁然开朗！我将尝试在这里点亮同样的明灯，希望它能帮助你更好地理解 Metasploit。

让我们开始通过打开终端并导航到 /usr/share/metasploit-framework 目录来查看 Metasploit 的内部。

```
kali > cd /usr/share/metasploit-framework kali > ls -l
```

现在，将目录更改为 modules 目录。

```
kali > cd modules
root@kali-2019:/usr/share/metasploit-framework# cd modules
root@kali-2019:/usr/share/metasploit-framework/modules# ls -l
total 28
drwxr-xr-x 22 root root 4096 Jul 11 09:31 auxiliary
drwxr-xr-x 12 root root 4096 Jun 19 15:14 encoders
drwxr-xr-x 3 root root 4096 Jun 19 15:14 evasion
drwxr-xr-x 21 root root 4096 Jul 11 09:31 exploits
drwxr-xr-x 11 root root 4096 Jun 19 15:14 nops
drwxr-xr-x 5 root root 4096 Jun 19 15:14 payloads
drwxr-xr-x 14 root root 4096 Jun 19 15:14 post
root@kali-2019:/usr/share/metasploit-framework/modules#
```

