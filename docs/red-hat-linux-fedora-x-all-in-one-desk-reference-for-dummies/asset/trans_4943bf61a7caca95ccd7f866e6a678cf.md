

# 探索安全工具 589

表 4-4 某些常用的计算机安全测试工具
| 类型 | 工具名称 |
|---|---|
| 端口扫描器 | nmap, Strobe |
| 漏洞扫描器 | Nessus Security Scanner, SAINT, SARA, Whisker (CGI 扫描器), ISS Internet Scanner, CyberCop Scanner, Vetescan, Retina Network Security Scanner |
| 网络实用工具 | Netcat, hping2, Firewall, Cheops, ntop, ping, ngrep, AirSnort (802.11 WEP 加密破解工具) |
| 主机安全工具 | Tripwire, itself |
| 数据包扫描器 | tcpdump, dsniff, sniffit |
| 入侵检测系统 (IDS) | Snort, Abacus process, scanlog, NFR, LIDS |
| 密码检查工具 | John the Riper, LC4 |
| 日志分析与监控工具 | logcolorise, tcpstats, flog, logcheck, LogWatch, Swatch |

## Nmap

Nmap（network mapper 的缩写）是一种端口扫描工具。它可以快速扫描大型网络，并确定网络上有哪些可用主机、它们提供哪些服务、运行什么种操作系统（以及操作系统版本）、使用了什么种类型的数据包过滤器或过滤器，以及数十种其他特征。Fedora Core 自带了 nmap。你可以在 www.insecure.org/nmap 了解更多关于 nmap 的信息。

如果你想尝试使用 nmap 扫描本地网络，只需使用类似下方的命令（将 IP 范围替换为适合你的的地址）：

```
nmap -sS 192.168.0.2-10
```

以下是该命令的典型输出：

```
Starting nmap 3.50 (http://www.insecure.org/nmap/ ) at 2004-04-14 21:01 EDT
Interesting ports on 192.168.0.2:
(下方未显示的 1654 个扫描端口状态为:closed)
POW STATE SERVICE
135/tcp open msrpc
139/tcp open netbios-ssn
445/tcp open microsoft-ds
1025/tcp open NFS-iis
5000/tcp open UPnP
Device type: general purpose
Running: Microsoft Windows 95/98/ME/NT/2K/XP
OS details: Microsoft Windows Millennium Edition (Me), Windows 2000 Professional or Advanced Server, or Windows XP
```

Interesting ports on 192.168.0.6:
(下方未显示的 1654 个扫描端口状态为: closed)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
111/tcp open rpcbind
32771/tcp open sometimes-rpc5
Device type: general purpose
Running: Linux 2.4.32-s5
OS details: Linux 2.5.25-2.5.70 or Gentoo 1.2 Linux 2.4.19 ric-77
uptime 5.015 days (since Wed Apr 10 20:41:00 2004)
<< finished>>
map result completed 9 IP addresses (3 hosts up) in 167.19 seconds

```

如你所见，nmap 显示了开放端口的名称，并对操作系统名称和版本号进行了猜测。

## Nessus

Nessus Security Scanner 是一种模块化审计工具，它使用 Nessus 脚本语言中的插件来测试各种网络漏洞。Nessus 使用客户端-服务器软件架构，包含一个名为 nessus 的服务器和一个名为 nessus 的客户端。

在尝试安装 Nessus 之前，你必须先安装 sharutils RPM 包。该包包含了 unicode 支持。

