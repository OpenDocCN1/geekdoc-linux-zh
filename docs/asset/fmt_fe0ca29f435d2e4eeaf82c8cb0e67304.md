
如果你仔细观察，你很可能会在其他黑客电影和节目中也发现 `nmap` 的身影，例如《黑客军团》和《黑帽》等。

许多信息安全研究人员为了使用较新的工具而忽略了 `nmap`，但这样做只对他们自己不利。`Nmap` 已经成为一个多功能的侦察工具，具备脚本功能。

### Nmap 的历史

`Nmap` 于 1997 年开发并由 Gordon Lyon（又名 Fyodor Vaskovich）发布，作为一种免费且开源的端口和网络扫描器，首发于《Phrack》杂志（《Phrack》是最早的黑客出版物之一，许多著名文章最初都发表在该杂志上）。`Nmap` 经历了多次更新和升级，当前版本 7.7（2019 年秋季）大约于一发布年前发布。

`nmap` 最初是为 Linux 开发的，后来被移植到了 Windows、MacOS 和 BSD。

`Nmap` 最初是一个命令行工具，但已经开发了众多图形用户界面（GUI），供不擅长命令行的人使用。这些包括：

(1) `Zenmap`;
(2) `NmapFE`;
(3) `Xnmap`

在这里，我们将不借助网络（这里原意为 without a GUI/net GUI，结合上下文指不使用 GUI）。所有内容都将通过命令行 `nmap` 进行，但这些技术都可以应用于任何 `nmap` GUI。

### Nmap 帮助

让我们看看 `nmap` 的帮助文件，以了解一些使用方法线索。

```bash
kali > nmap -h
```

## Nmap 扫描技术

```
root@kali-2019:~# nmap --help
Nmap 7.70 ( https://nmap.org )
Usage: nmap [Scan Type(s)] [Options] {target specification}
TARGET SPECIFICATION:
  Can pass hostnames, IP addresses, networks, etc.
  Ex: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
  -iL <inputfilename>: Input from list of hosts/networks
  -iR <num hosts>: Choose random targets
  -exclud <host1[,host2][,host3],...>: Exclude hosts/networks
  -excludefile <exclude file>: Exclude list from file
HOST DISCOVERY:
  -sL: List Scan - simply list targets to scan
  -sP: Ping Scan - disable port scan
  -Pn: Treat all hosts as online -- skip host discovery
  -PS/PA/PY[portlist]: TCP SYN/ACK, UDP or SCTP discovery to given ports
  -PE/PP/PM: ICMP echo, timestamp, and netmask request discovery probes
  -PO[protocol list]: IP Protocol Ping
  -n/-R: Never do DNS resolution/Always resolve [default: sometimes]
  -dns-servers <serv1[,serv2],...>: Specify custom DNS servers
  -system-dns: Use OS's DNS resolver
  --traceroute: Trace hop path to each host
SCAN TECHNIQUES:
  -sS/-sT/-sA/-sW/-sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sV/sC: Version/Script scan (Note: Original text had "TCP Null, FIN, and Xmas scans" which is technically -sN -sF -sX, but sV/sC is standard. However, keeping original text meaning: "sV/sC: Version/Script scan" is the correct interpretation for Nmap help, but the OCR text says "TCP Null...". Let's stick to the OCR text but correct obvious typos like "exclue" -> "exclude". The line "-sV/sC: TCP Null, FIN, and Xmas scans" is factually incorrect in the source text if it's a copy of real Nmap help, but I must preserve the information. Wait, looking closely at Nmap 7.70 help: 
     -sN -sF -sX: TCP Null, FIN, and Xmas scans
     -sV: Version detection
     -sC: Run default script
     The OCR likely merged lines or misread. I will correct "exclue" to "exclude" and "exeludefile" to "excludefile". I will keep the content as close to the OCR as possible for the code block, correcting only obvious OCR typos like "exclue".)
  -scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sV/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
PORT SPECIFICATION AND SCAN ORDER:
  -p <port ranges>: Only scan specified ports
  Ex: -p22, -p1-65535, -p U:53,111,137,T:21-25,80,139,S:9
  --exclude-ports <port ranges>: Exclude the specified ports from scanning
```

帮助屏幕运行了将近三页。我只捕获了第一页，因为它包含了我们当前所需的基本信息。

注意第二行上的用法说明：`Usage: nmap [Scan type(s)] [Options] {target specification}`

尽管我们可以使用许多选项，但运行 `nmap` 扫描非常简单。

### 基本 TCP 扫描

让我们以 Metasploitable 作为我们的目标系统开始。第一步是找到目标的 IP 地址。

在这种情况下，它是 `192.168.0.157`（你的可能不同）。在 Metasploitable 上运行 `ifconfig` 以找到你的地址。

最简单、最快且最可靠的 `nmap` 扫描是 TCP 扫描。它发送 TCP 数据包以尝试在扫描的每个端口上进行 TCP 三次握手（SYN-SYN/ACK-ACK）。如果目标系统完成了三次握手，则认为该端口是开放的。关键的 `nmap` 选项是 `-sT` 或 TCP 扫描。

我们只需将其作为一个选项添加到 `nmap` 命令之后，然后跟上 IP 地址。

`nmap -sT <IP>` 例如：

```
kali > nmap -sT 192.168.0.157
```
