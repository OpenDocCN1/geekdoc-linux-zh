
列表 401 - 从我们的 OLE 对象接收到的 shell

# 13.3.1 练习

- 1. 使用 PowerShell 负载创建一个批处理文件并将其嵌入 Microsoft Word 文档中，向你的 Kali 系统发送反 shell。

# 13.3.4 规避受保护视图

此 Microsoft Word 文档在本地提供时非常有效，但当从 Internet 通过电子邮件或下载链接提供时，我们必须绕过名为“受保护视图”（Protected View）的保护层，该视图会禁用文档中的所有编辑和修改，并阻止宏或嵌入对象的执行。

为了模拟这种情况，我们将包含嵌入批处理文件的 Microsoft Word 文档复制到 Kali 机器并将其托管在 Apache 服务器上。然后，我们可以从服务器下载该文档并在受害者机器上打开它。此时，受保护视图已激活（如图 254 所示），我们无法执行批处理文件。

| 文件 工具 | MacroTest(受保护视图) - Word |
|---|---|
| 受保护视图 注意—来自 Internet 的内容可能包含病毒。除非你需要编辑，否则留在受保护视图中更安全。 | 启用编辑 |

图 254：受保护视图正在运行

虽然受害者可能会点击“启用编辑”并退出受保护视图，但这不太。理想情况下，我们更喜欢完全绕过受保护视图，实现这一点的一种直接方法是使用其他 Office 应用。

类似于 Microsoft Word，Microsoft Publisher 也与 Word 和 Excel 完全相同允许嵌入对象和最终代码执行，但它不会对 Internet 传输的文档启用保护视图。可以使用之前应用于 Word 的策略来绕过这些限制，但缺点是 Publisher 的使用频率低于 Word 或 Excel。尽管如此，如果你的指纹检测到 Publisher 被感染，这可能是一个可行且更好的向量。

# 13.3.4.1 练习

- 1. 通过模拟从 Internet 下载 Microsoft Word 文档来触发受保护视图保护。
- 2. 重用批处理文件并将其嵌入 Microsoft Publisher 文档中，向你的 Kali 系统接收反 shell。
- 3. 将文件移动到 Apache Web 服务器，以模拟从 Internet 下载 Publisher 文档并确认受保护视图。

### 13.4 总结

客户端攻击特别阴险，因为它们利用的是客户端软件（如浏览器）的漏洞，而不是利用服务器软件。这通常涉及某种形式的用户交互和欺骗，以便客户端软件执行恶意代码。

这些向量对攻击者特别有吸引力，因为它们不需要对受害者机器进行直接或可路由的访问。

> ³⁶² (Microsoft, 2019), https://support.microsoft.com/en-us/office/what-is-protected-view-30d77777-7774-4777-9777-7777 ( 文本)

# 攻击性安全

Kali Linux 2.0 渗透测试

利用程序是用低级语言编写的并需要编译，以源代码和二进制格式托管。源代码更容易检查，但在（没有专业技能和工具的情况下）检查起来很复杂，且运行更简单。

如果代码检查或编译太复杂，请使用带有干净快照的漏洞虚拟机或“沙箱”。

### 14.2 搜索利用程序

在渗透测试的信息收集和枚举阶段之后，我们可以对发现的软件进行漏洞交叉检查，尝试找到这些软件的发布利用程序。

# 14.2.1 在线利用资源

各种在线资源托管利用程序并免费向开放。在本节中，我们将介绍三个最流行的在线资源。这些资源通常会对提交的利用程序进行测试，并移除被认为伪造或恶意的代码。

# 14.2.1.1 利用程序数据库 (Exploit Database)

Exploit Database 是由 Offensive Security Maintain的项目。它是通过提交、邮件列表和公共资源收集的公开利用程序存档。

![](img/f99f528ca9845f4c256ce54e882b1345_438_0.png)

图 2.5：利用程序数据库

> 363 (Offensive Security, 2019), https://www.exploit-db.com/

> 364 (Offensive Security, 2019), https://www.offensive-security.com/

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

与其他在线资源相比，Exploit Database（漏洞利用数据库）偶尔会出于研究目的提供受影响软件版本的安装程序。当安装程序可用时，网站上会用一个图标标记，如图 255 的 A 列中显示的下载框图标所示。

Exploit Database 的更新通过 Twitter 馈 965 发布，同时也提供 RSS 馈送 966。

## 14.2.1.2 SecurityFocus 漏洞利用存档

SecurityFocus Exploit Archives 367 网站创建于 1999 年，专注于关注安全社区的几个关键领域。

- BugTraq：一个全公开披露的邮件列表，目的是讨论和发布安全漏洞。
- SecurityFocus 漏洞数据库：提供所有平台和服务的最新漏洞信息。
- SecurityFocus 邮件列表：基于主题的邮件列表允许全球范围内的研究人员讨论各种安全问题。

> 365 (Twitter, 2019), https://twitter.com/exploitdb
> 366 (Offensive Security, 2019), https://www.exploit-db.com/rss.xml
> 367 (SecurityFocus, 2019), https://www.securityfocus

## 漏洞

- Radiant CVE-2018-7261 多处 HTML 注入漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103080
- Drupal DRUPAL-SA-CORE-2018-001 多处安全漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103117
- Drupal DRUPAL-SA-CORE-2018-0011 多处访问绕过漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103115
- Cisco Unified Communications Manager CVE-2018-0124 远程代码执行漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103114
- Cisco Elasticast Services Controller Software CVE-2018-0121 身份验证绕过漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103113
- Juniper Jun 2-Web Interface CVE-2018-0001 远程代码执行漏洞
  2018-02-24
  http://www.securityfocus.com/bid/103062
- Apple iOS/watchOS/macOS/tvOS CVE-2018-4124 拒绝服务漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103068
- phpMyAdmin CVE-2018-7260 跨站脚本漏洞
  2018-02-21
  http://www.securityfocus.com/bid/103099
- ABB netCADOCS Web Application CVE-2018-5477 信息泄露漏洞
  2018-02-20
  http://www.securityfocus.com/bid/103093
- Linux Kernel /drivers/block/floppy.c 本地绕过漏洞
  2018-02-22
  http://www.securityfocus.com/bid/103088

搜索所有漏洞。

## 邮件列表

请勾选您想要订阅或取消订阅的列表。如果您已经订阅了 SecurityFocus 邮件列表，在订阅额外列表时，无需勾选这些列表。

邮箱地址：

确认地址：

| 订阅 | 取消订阅 |
| :--- | :--- |

您将收到来自每个列表的确认邮件。SecurityFocus 通过其 Twitter 馈 368 发布更新，同时也提供 RSS 馈送 369。

> 368 (Twitter, 2019), https://twitter.com/securityfocus?lang=en
> 369 (SecurityFocus, 2019), https://www.securityfocus.com/rss/index.html

## 14.2.1.3 Packet Storm

Packet Storm 70 建立于 1998 年。它提供安全新闻和漏洞的最新信息，以及安全供应商近期发布的工具。

### 渗透最新文件

| 全部 | 漏洞利用程序 | 白皮书 | 其他 |
| :--- | :--- | :--- | :--- |

### Hashcat 高级密码恢复

截至 2016 年 2 月，Hashcat 是一种高级的哈希工具，它利用了世界上最快的 GPU 引擎，专注于高迭代哈希、字典攻击等。

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

这些选项允许我们缩小搜索范围、更改格式、更新数据库等：

```
==Options

=======

-c, --case      [Term]

-e, --exact      [Term]

-h, --help        [Term]

-j, --json        [EDB-ID]

-o, --overflow   [EDB-ID]

-p, --path       [EDB-ID]

-t, --title      [Term]

-u, --update      [Term]

-w, --www         [Term]

-x, --execute     [EDB-ID]

--colour

--id

--nmap           [file.xml]

--exclude='term'
```

- 执行区分大小写的搜索（默认为不区分大小写）
- 在屏幕上执行精确匹配（默认为 []）
显示此屏幕。
- 以 JSON 格式显示结果。
- 镜像（别名复制）到当前工作目录
- 允许漏洞标题溢出列宽
- 显示漏洞的完整路径（并复制）
- 搜索漏洞标题（默认为标题）以及
- 检查是否安装了任何 exploitdb 软件包（更新或）
- 显示 Exploit-db 的 URL 而非本地路径。
- 使用 spider （别名复制）漏洞
- 禁用搜索结果中的高亮。
- 显示 E-ID 值而非本地路径。
- 检查 Nmap XML 输出中所有带有服务版本的的结果
- 使用 -v（详细）尝试更多组合
- 使用 " " 分隔大小写来移除结果，例如 --exclude='term|term|term|term'

列表 411：搜索选项帮助菜单

最后，菜单中的“Notes（备注）”搜索显示了实用的搜索提示：

=====
Notes

* 您可以使用任意数量的搜索词。
* 搜索词不区分大小写（默认情况下），顺序不重要。
* 如果您希望通过区分大小写的搜索来减少结果，请使用 '-c'。
* 如果您希望通过使用精确匹配过滤结果，请使用 '-e'。
* 在搜索数字（即版本）时使用 '-t' 排除文件路径。
* 在搜索数字时移除假正例（异常）--
* 在更新或显示帮助时，将识别搜索词。

列表 412：searchploit 帮助备注

例如，我们可以使用以下语法搜索针对操作系统上 SMB 服务的所有远程漏洞：

```
kali@~$ search exploit remote microsoft windows
```

| 漏洞标题 | 路径 |
| --- | --- |
| Microsoft DNS RPC Service - 'extractQ' | exploits/remote/16336.rb |
| Microsoft Windows - 'srv2.sys' SMB Cod | exploits/remote/40280.rb |
| Microsoft Windows - 'srv2.sys' SMB Neg | exploits/remote/14674.txt |
| Microsoft Windows - 'srv2.sys' SMB Neg | exploits/remote/16336.rb |
| Microsoft Windows - SMB Relay Code Ex | exploits/remote/13360.rb |
| Microsoft Windows - SmbRelay3 NTLM | exploits/remote/7125.txt |
| Microsoft Windows - Unauthenticated SMB | exploits/dos/41891.rb |
| Microsoft Windows 2000/XP | exploits/remote/20.txt |
| Microsoft Windows 2003 SP2 - 'ERRATIC' | exploits/windows/remote/41929.py |
| Microsoft Windows 95/Workgroups for XP | exploits/windows/remote/20371.py |
| Microsoft NT 4.8 SP2 / | exploits/windows/remote/31997.py |
| Microsoft Windows Server 2008 R2 (x86) | exploits/windows/remote/41887.py |
| Microsoft Windows Vista/7 - SMB2.0 | exploits/windows/dos/9594.txt |
| Microsoft Windows 7/8.1/2008 R2 (x)4 | exploits/windows/x86-64/remote/42031.py |
| Microsoft Windows 7/8.1/2012 R | exploits/windows/x86-64/remote/42315.py |
| Shellcode: No Result | |

列表 413：使用 search 列出可用的远程 SMB 脚本

Nmap 是最流行的枚举工具之一。该工具的一个强大功能是 Nmap 脚本引擎（NSE），正如其名称所示，它引入了使用脚本自动执行各种任务的能力。Nmap 脚本引擎带有各种用于枚举、暴力破解、检测以及利用的脚本。Nmap 脚本引擎提供的完整脚本列表可以在 `/usr/share/nmap/get`下找到。使用 grep 在 Nmap 脚本中搜索“exploit（利用）”一词会返回多个结果：

```
kali@~$ cd /usr/share/nmap/scripts

kali@~$ grep *.nse
```

- exploit-exec.nse: clamAV 服务器易受未经身份验证的命令执行影响。
- awstats-nse: Awstats 中的远程代码执行漏洞。
- axis-dir-traversal.nse: Apache 中的目录遍历漏洞。
- fileupload-nse: Web 应用中不安全表单。

列表 414：使用包含“exploit”单词的 NSE 脚本

我们可以通过运行带有 --help 后接脚本名称的 nmap 来列出脚本信息：

```
kali@~$ nmap --help exploit-exec.nse
```

- exploit-exec.nse: 易受未经身份验证的命令执行影响的 clamAV 服务器。
- awstats-nse: Awstats 中的远程代码执行漏洞。
- axis-dir-traversal.nse: Apache 中的目录遍历漏洞。
- fileupload-nse: Web 应用中不安全表单。

我们可以通过运行带有 --help 后接脚本名称的 nmap 来列出脚本信息：

```
kali@~$ nmap --help exploit-exec.nse
```

- exploit-exec.nse: 易受未经身份验证的命令执行影响的 clamAV 服务器。
- awstats-nse: Awstats 中的远程代码执行漏洞。
- axis-dir-traversal.nse: Apache 中的目录遍历漏洞。
- fileupload-nse: Web 应用中不安全表单。

这种未经身份验证的命令执行会影响 clamAV 服务器的漏洞。

参考：
* https://twitter.com/status/7406735078647698
* https://bugzilla.net/show_bug.cgi?id=1585

列表 415：使用 NSE 脚本获取信息

这提供了关于漏洞和外部资源的信息。

## 浏览器执行框架 (BeEF)

浏览器执行框架 (BeEF) 是一种专注于在 Web 浏览器中执行攻击的渗透测试工具。无需解释，它包含了大量的漏洞。

为了列出可用的漏洞，我们必须首先启动服务。这在 Kali Linux 中可以使用 `beef-xss` 命令完成：

```
kal@kali:~ sudo beef-xss
* 请等待 BeEF 服务启动。

* 在打开浏览器之前您可能需要刷新。

* UI: http://127.0.0.1:3000/ui/panel

* 钩子: <script src="http://127.0.0.1:3000/hook.js"></script>

* 示例: <script src="http://127.0.0.1:3000/hook.js"></script>
```
