
找到任何 Telnet 数据包，无论是在主窗口中浏览还是使用过滤器。过滤源或目的端口为 23 的所有 TCP 数据包，点击 Filter 字段并输入 `tcp.port == 23` 然后按 Apply。虽然过滤语法看起来很直观，但有时你并不知道需要哪些单词。可以通过点击 Expression 按钮来构建过滤器。这将弹出图 7.12 所示的窗口。

# 图 7.12 Wireshark Filters

![](img/0eb7273a8d9e486628f6e18d37ab22c6_445_0.png)

在 Field name 字段中导航到 TCP，然后展开 TCP 子树并选择 `tcp.port`。在 Field name 字段中选中项后，在 Relation 字段中选择逻辑运算符，例如用于等于的 `===`。最后在 Value 字段中输入所需的值（在此例中为 `23`）。然后点击 OK。这将过滤器表达式放入 Filter 字段中。你必须点击 Apply 将过滤器应用到数据包显示。现在你应该只看到 Telnet 数据包列表。如果你选择任何一个 Telnet 数据包（Wireshark 会在 Info 列中标记它们）并右键点击，可以选择 Follow TCP Stream。一个独立的窗口将如图 7.13 所示出现，显示该对话中所有数据包的数据部分。

# 网络报告与故障排除 • 第7章

## 图 7.13 Wireshark 跟踪 TCP 流

![](img/0eb7273a8d9e486628f6e18d37ab22c6_446_0.png)

这里包含了“跟踪 TCP 流”（Follow TCP Stream）窗口的完整输出，让你直观了解 Telnet 登录的外。这说明了 Telnet 并没有采用任何加密，使其成为在可信网络上进行远程访问的一种不安全选择。

```
.%...!..!.."
%...
'.%...SFUTNTVER.SFUTLNTMODE....%....!...."
....]...DISPLAY.Knoppix:0.0....'....%....

欢迎使用 Microsoft Telnet 服务

login:

password:

...
..xterm.
...
..xterm.

============================================================

Welcome to Microsoft Telnet Server.

============================================================

C:\Documents and Settings\Eric>

Volume in drive C is C:OS

Volume Serial Number is 2037-12FA
```

![](img/0eb7273a8d9e486628f6e18d37ab22c6_446_1.png)

```
Directory of C:\Documents and Settings\Eric

12/08/2003 06:52 PM <DIR>
12/08/2003 06:52 PM <DIR>
05/02/2005 11:30 PM <DIR> My Documents
05/02/2005 11:30 PM <DIR> Favorites
12/08/2003 06:44 PM <DIR> Desktop
12/08/2003 06:44 PM <DIR> Start Menu
12/23/2003 12:15 AM <DIR> WINDOWS
02/16/2006 08:46 PM <DIR> housecall
06/13/2006 08:15 PM <DIR> SecurityScans
06/24/2006 06:43 PM <DIR> .ssh
09/19/2006 03:27 PM 600 PUTTY.RD
09/04/2006 04:22 PM <DIR> Tenable
1 File(S) 600 bytes
1 Dir(s) 2,719,571,968 bytes free

C:\Documents and Settings\Eric>
```

为了节省空间，我删除了一些空行，除此之外，这就是完整的流数据。你可以看到对话开头包含了 `DISPLAY:Knoppix`，这是我连接的系统。下一行是“Welcome to Microsoft Telnet Service”，表明目标主机是运行 Telnet 服务的 Microsoft 系统。系统提示输入登录 ID（我使用了 `eric`）和密码。登录完成后，我使用 `dir` 命令获取了远程机器的目录列表。

你会发现用户名和密码没有列在跟踪 TCP 流的输出中。因为 Telnet 是一种明文协议，使用的用户名和密码在数据部分是可见的。Telnet 会为你输入的每个字符发送一个数据包，用户 ID 为“eric”，其中一个数据包只包含“e”，另一个是“r”，另一个是“i”，最后是“c”。要在此数据包捕获（Packet Capture）窗口中查看，使用顶部面板选择一个 Telnet 数据包。在中间你可以查看各个数据包层的详情。底部是 Telnet。点击加号，它将展开并显示数据包的数据部分。图 7.14 显示第 179 号数据包的数据负载包含“e”，这是我开始输入登录 ID 的开头。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_447_0.png)

## 图 7.14 Wireshark 数据表

![](img/0eb7273a8d9e486628f6e18d37ab22c6_448_0.png)

```
Frame 179 (67 bytes, 67 captured)
Ethernet: Src=00:0c:2f:4b:09:6f; Dst=00:50:5e:e8:0f:b3
Internet Protocol4: Src=192.168.1.103; Dst=192.168.1.199
Transmission Control Protocol: Src port=56988; Dst port=22; Seq=89; Ack=130; Len=0
Data:
0000 00 01 0b 29 88 b3 00 03 a0 c9 56 7f 08 00 41 10
0010 05 03 15 17 41 00 00 02 54 55 56 48 48 08 00
0020 01 03 09 6c 99 17 00 03 71 01 08 48 48 08 00
0030 01 03 09 6c 00 01 44 00 00 01 08 48 00 65 00 19
0040 00 24 65
```

你也可以在查询中进行搜索以导航到“编辑 | 查找数据包”（Edit | Find Packet）。你可以选择通过过滤器标头、值或字符串进行搜索。如果你选择“字符串”（String）然后在提供的字段中输入任何 ASCII 字符串，它将搜索所有捕获数据包的数据部分。这可以帮助你快速定位感兴趣的对话，例如搜索一个 URL 来找到你想要检查的 HTTP 会话。

你会注意到，如果你搜索一个包含 Telnet 用户登录 ID "eric" 的字符串，你永远找不到它，因为它是一个字符一个字符发送的。如果你不知道 Telnet 是这样工作的，你可能会感到困惑，认为 Wireshark 没有捕获到你的 Telnet 会话。如你所见，分析数据并不是易事。

## 使用命令行嗅探器

有时你需要一个开销较小的嗅探器。命令行嗅探器对于运行它的系统来说负担更小。在只有控制台访问且无法使用图形界面（GUI）工具的情况下，使用命令行嗅探器或许可以让你看到寻找的流量。我将简要介绍几种命令行嗅探器的用法。其中一个需要 Wincap，另一个在 Windows 2000 或更高版本上不需要，最后一个是命令行形式。

### Windump

许多 Linux 系统默认安装了 `tcpdump`。由于 `tcpdump` 非常常用，它被移植到了 Windows 并称为 Windump。Windump 需要 Wincap 才能工作。没有安装文件；下载的是整个包。只需将其下载到选择的目录即可。Windump 的手册与 `tcpdump` 非常相似，位于 `www.winpcap.org/windump/docs/manual.html`。虽然选项多到无法详细解释，但这里有一些入门命令。`windump -i` 列出接口。你可以通过 `windump -i 2` 限制输出，仅显示来自接口 2 的流量。命令行语法相对直观，手册底部有一些实用的示例。在 Wireshark 示例中，我们处理的是 Telnet 会话。如果我们想查看源或目的端口为 23（Telnet）的来自主机 `lab203` 的流量，可以输入 `windump -i host lab203` 与 `lab203` 开启了 Telnet 会话，部分输出如图 7.15 所示。注意：我删除了时间戳以免导致换行。

## 图 7.15 Windump: listening on \Device\NPF
