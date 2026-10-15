
```
ssh-hostkey:
3072 56:57:11:d3:b5:dc:f1:d3:50:88:b8:ab:93:e2:29 (RSA)
256 64:f1:d2:f5:cb:b0:43:e0:76:b4:c3:96:19:a2:ba:f0:44 (ECDSA)
256 67:46:b3:27:96:a9:e3:48:e20:b3:98:7a:32 (ED25519)
```

```
23/tcp closed telnet
25/tcp closed smtp
53/tcp closed domain
80/tcp open Apache http 2.4.1 ((Ubuntu))
http-server-header: Apache/2.4.1 (Ubuntu)
http_title: Under Construction
110/tcp closed pop3
111/tcp closed rpcbind
```

列表 65 - 使用 `nmap` 执行二十端口扫描，并将输出保存为 `greppable` 格式

20 个 `nmap` 结果是使用 `/usr/share/nmap/map-services` 文件生成的，该文件使用了三个空白分隔列的简单格式。第一列是服务名称，第二列包含数字和协议，第三列是“频率”。第三列之后的所有内容都会被忽略，通常用于注释（如 `#` 符号所示）。频率基于在互联网进行定期扫描期间发现该端口的频率³³

```
kali@kali:~# cat /usr/share/nmap/map-services
finger 79/udp 0.008956 # www -http | World Web HTTP
http 80/tcp 0.068090 # World Web HTTP
http 80/tcp 0.484143
http 80/udp 0.035767 # World Web HTTP
hosts2- 81/tcp 0.012086 # HOST2 Name Server
hosts2-ns 81/udp 0.001085 # HOST2 Name Server
```

列表 66 - 显示 TCP 端口 80 开放频率的 `nmaps` 文件

³ (`Nmap`, 2022), https://nmap.org/book/nmap-services.html

⁴ (`Nmap`, 2022), https://nmap.org/book/man-host-discovery.html

⁵ (`Nmap`, 2022), https://nmap.org/book/osdetect.html

# 使用 Kali Linux 进行 OffSec 渗透测试

（以及 TCP 窗口大小），这些细微差异创建了 `Nmap` 经常可以识别的指纹。

`Nmap` 将检查从目标机器接收的流量，并尝试将指纹与已知列表进行匹配。默认情况下，如果检索到的指纹非常准确，`Nmap` 将显示检测到的操作系统（OS）。由于我们想获取目标操作系统的大致信息，因此我们包含了 `osscan-guess` 选项，以便在结果不完全准确时强制 `Nmap` 猜测结果。

例如，让我们考虑一下这个简单的 `Nmap` 指纹扫描。

```
kali@kali~$ sudo nmap -O 192.168.0.54 --oscan-guess
...
Running (GUESSING): Windows Server 2008|2012|2016|Vista (88%)
OS CPE: cpe:microsoft:windows_server:2008:sp1
cpe:microsoft:windows_server:2008:r2 cpe:microsoft:windows_server:2012:r2
cpe:microsoft:windows_server:2016 cpe:microsoft:windows_7
cpe:microsoft:windows_vista:sp1:home_premium
Aggressive (GUESSING): Windows Server 2008 Vista or Windows Server 2008 R2 (88%), Microsoft Windows Server 2012 Windows Server 2012 R2 (88%), Microsoft Windows Server 2012 R2 (88%), Microsoft Windows Server 2016 (87%), Microsoft Windows 7 (86%), Microsoft Windows Vista Home Premium SP1 (85%), Windows 7 Professional (85%)\No exact OS matches for host (If you know what OS is running on, see
https://nmap.org/submit/)
...
```

> 列表 6 - 使用 `nmap` 进行操作系统指纹识别

响应表明，该目标的底层操作系统可能是 Windows 2008 R2、2012、2016、Vista 或 Windows 7。

> 注意，操作系统指纹识别并不总是 100% 准确，这通常是因为防火墙或代理等网络设备在通信中重写了数据包头。

一旦我们识别了底层操作系统，就可以通过 `-A` 参数检查服务横幅（banners）来进一步识别特定端口上运行的服务，该参数还会针对目标运行各种操作系统和服务服务的枚举脚本。

```
kali@kali~$ nmap -sT -A 192.168.0.54
nmap scan report for 192.168.0.54
Host is up (0.12s latency).
Not shown: 996 closed tcp ports (conf-used)
PORT STATE VERSION
21/tcp open ftp?
| fingerprint-strings:
| DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, NULL, RPCCheck,
SSLSession,TLSSessionReq, TLSServerCookie:
220-Filezilla Server 1.2.0
| Please visit https://filezilla-project.org/
GetRequest:
|220-Filezilla Server 1.2.0
| Please visit https://filezilla-project.org/
```

What are you trying to do? Go away.

Options, RTSRequest:

220-FileZilla Server 1.2.0

Please visit https://filezilla-project.org/

Wrong command.

Help:

220-FileZilla Server 1.2.0

Please visit https://filezilla-project.org/

The following commands are recognized.

USER TYPE SYST BTO RNFR REST QUEST

HELP XXMD MLQ MNQ EPSY XWWD NOUP OPTS DELETE

CDUP APPE STOR ALOE PTRWD FEAT CLNT CLMT

MODE XMRD PROT ADAT ABPR XPWD MDTM MLIS MLSD FEAT CLNT PASV

NLST EPRT PASS STUS PAT COST

Help ok.

```
ftp-stat:
| ssl-cert: Subject: commonName=filezilla-server self signed certificate
| Not valid before: 2022-02-01T15:37:24
| Not valid after: 2023-01-07T15:42:24
| ssl-date: randomness does not represent time
135/tcp open ms-rpc
139/tcp open netbios
445/tcp open microsoft-ds
Nmap done: 1 IP address (host) scanned in 55.6 seconds
```

> 列表 68 - 使用 `nmap` 进行横幅抓取和服务枚举

在这个示例中，我们使用 `-A` 参数运行带有额外选项的服务扫描。如果我们想运行普通的 `nmap` 扫描，只需使用 `-sV` 参数即可。横幅抓取（Banner grabbing）会显著影响使用的流量大小以及我们的扫描速度。我们应该始终留意在 `nmap` 中使用的选项以及它们如何影响我们的扫描。（img/33d6ea891e7464f1ad6442619ced490.png）
