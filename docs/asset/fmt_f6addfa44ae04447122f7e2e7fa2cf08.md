
### 列表 618 - 使用 pth-winexe 通过哈希传递

根据列表 618 中的输出，命令成功执行，提供了目标上的 shell，并使用了捕获的哈希值作为凭据。

在幕后，我们提供的 NTLM 哈希值的格式在身份验证过程中被更改为 NetNTLM 版本 1 或 2[580] 格式。我们可以使用中间人攻击或中毒攻击捕获这些哈希值，然后要么破解它们，[581] 要么中继它们。[582]

例如，像 Internet Explorer 和 Windows Defender 这样的某些应用程序使用 Web 代理自动发现协议（Web Proxy Auto-Discovery Protocol，WPAD）[583] 来检测代理设置。如果我们位于本地网络中，我们可以使用像 `Responder.py` 这样的工具来毒化这些请求并强制 NetNTLM 身份验证，[584] 该工具创建一个专门用于利用此安全问题的恶意 WPAD 服务器。由于中毒对其他用户具有高度干扰性，因此永远不应在实验室中使用 `Responder.py` 等工具。

[569] HashKiller, 2019, https://hashkiller.co.uk/
[570] Wikipedia, 2019, https://en.wikipedia.org/wiki/Security_Accounts_Manager
[571] Wikipedia, 2019, https://en.wikipedia.org/wiki/LM_hash
[572] Wikipedia, 2019, https://en.wikipedia.org/wiki/Data_Encryption_Standard
[573] Wikipedia, 2019, https://en.wikipedia.org/wiki/NTLM
[574] Wikipedia, 2019, https://en.wikipedia.org/wiki/MD4
[575] Dimitris Siamarls, 2017, https://blog.3cr.de/mimikatz-deep-dive-on-lsadmuplsx-patch-and-inject.html
[576] Wikipedia, 2019, https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service
[577] Foofus.Net, 2008, http://foofus.net/goons/fffzgig/fgdump/downloads.htm
[578] Amplia Security, 2018, https://www.ampliasecurity.com/research/windows-credentials-editor/
[579] byt3bl33d3r, 2015, https://github.com/byt3bl33d3r/ptk-toolkit
[580] Wikipedia, 2019, https://en.wikipedia.org/wiki/NT_LAN_Manager#NTLMv1
[581] Rob Brown, 2018, https://mark0zer0day.com/pasc-the-hash/crack-map-exec/2018/03/04/da-from-outside-the-domain.html
[582] by3b33d3r, 2017, https://by3b33d3r.github.io/practical-guide-to-ntlm-relaying-in-2017-aka-getting-a-foothold-in-under-5-minutes.html
[583] Wikipedia, 2019, https://en.wikipedia.org/wiki/Web_Proxy_Auto-Discovery_Protocol
[584] SpiderLabs, 2019, https://github.com/SpiderLabs/Responder

### 19.4.2.1 练习

- 1. 使用 `Mimikatz` 从 Windows 客户端中提取管理员用户的密码哈希。
- 2. 复用该密码哈希，从你的 Kali 系统发起“传递哈希”（pass-the-hash）攻击，并在你的 Windows 客户端上获取代码执行权限。

#### 19.4.3 密码破解

在密码分析学中，密码破解是指根据存储的哈希值恢复明文口令的过程。

从高层次来看，密码破解的过程相当直接。一旦我们确定了目标认证过程中所使用的哈希机制，就可以遍历词表中的每个单词并生成相应的消息摘要。如果计算出的哈希值与从目标系统获取的哈希值相匹配，我们就获得了匹配的明文密码。这通常都是借助专门的密码破解程序完成的。

> 如果认证过程中涉及盐值（salt）且我们不知道该盐值的具体内容，破解可能会变得极其复杂甚至不可能，因为我们需要使用各种盐值反复对每个潜在的明文密码进行哈希运算。尽管如此，根据我们的经验，我们几乎总能捕获到密码哈希以及盐值，无论是来自包含每记录中这两个唯一值的数据库，还是来自使用单一盐值对所有哈希值进行处理的配置文件或二进制文件。当这两个值都已知时，密码破解的复杂度会降低。

一旦我们获取了目标系统的密码哈希，就可以开始一个后台运行的密码破解会话，同时继续我们的评估。如果任何密码被破解，我们可以尝试将这些密码用于其他系统，以增加对目标网络的控制权。与其他渗透测试过程一样，这是一个迭代过程，随着我们扩大控制范围，我们会将数据反馈到早期步骤中。

为了演示密码破解，我们将再次使用 `John the Ripper`，因为它支持数十种密码格式，并且功能强大、灵活。

以纯暴力破解模式运行 `john`（尝试密码中所有可能的字符组合）非常简单，只需在命令行上传入包含我们密码哈希的文件名以及哈希格式即可。

在列表 619 中，我们攻击使用 `mimikatz` 转储的 NT 哈希（`--format=NT`）。

```
kali@kali:~$ cat hash.txt

WDAGUtilityAccount:0c509cca8bcd12a26acf0d1e508cb028

Offsec:2892d26cdf84d7a70e2eb3f9f05c425e

kali@kali:~$ sudo john hash.txt --format=NT

Using default input encoding: UTF-8
```

![](img/ec25e59d75726b7041242a56d3376832_586_0.png)

```
Rules/masks using ISO-8859-1

Loaded 2 password hashes with no different salts (NT [MD4 128/128 AVX 4x3])

Press 'q' or Ctrl-C to abort, almost any other key for status
```

*列表 619 - 使用 John the Ripper 进行暴力破解*

在上述输出中，JTR（John the Ripper）正确识别了哈希类型并开始对其进行破解。然而，像这样的暴力攻击基于系统速度可能需要很长时间。作为替代方案，我们可以使用 `--wordlist` 参数并提供词表的路径，这会缩短处理时间，但承诺的密码恢复率较低：

```
kali@kali:~$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt --format=NT
```

*列表 620 - 使用 John the Ripper 进行字典破解*

如果仍有密码未被破解，我们接下来可以尝试应用 JTR 的密码变形规则，使用 `--rules` 参数。

```
kali@kali:~$ john --rules --wordlist=/usr/share/wordlists/rockyou.txt hash.txt --format=NT
```

*列表 621 - 使用密码变形规则进行破解*

为了使用 JTR 破解基于 Linux 的哈希，我们需要首先使用 `unshadow` 工具将受攻破系统中的 `passwd` 和 `shadow` 文件合并。

```
kali@kali:~$ unshadow passwd-file.txt shadow-file.txt

victim:$6$f0S.xfbT$5c5vh3Zrk.88SbCWdUnirjgcgcYwCC/xT5Ec|SuJtrvqFk04pSWHaGxZojNy.vAqMGr8BN0b0P3pW1ybmx20IT/:1003:1003:::/:home/victim:/bin/bash

kali@kali:~$ unshadow passwd-file.txt shadow-file.txt > unshadowed.txt
```

*列表 622 - 准备 Linux 密码哈希以供破解*

现在我们可以运行 `john`，传入词表和未加盐的文本文件作为参数：
