
HTTP request sent; waiting for response

事实上，`psad` 已经切断了与攻击者 IP 地址的所有通信，持续整整一小时。DROP 规则被添加到三个阻塞链中，数据包从内置的 INPUT、OUTPUT 和 FORWARD 过滤链跳转到这些链中，针对攻击者 IP 地址提供了有效的 DROP：

```
[iptablesfw] # psad --fw-list
[+] Listing chains from IPT_AUTO_CHAIN keywords...
```

### Chain PSAD_BLOCK_INPUT (1次引用)

| pkts bytes target | prot in | out | source | destination |
|---|---|---|---|---|
| 0 0 DROP | all | * | * | 142.202.X.X | 0.0.0.0/0 |

### Chain PSAD_BLOCK_OUTPUT (1次引用)

| pkts bytes target | prot in | out | source | destination |
|---|---|---|---|---|
| 0 0 DROP | all | * | * | 0.0.0.0/0 | 142.202.X.X |

### Chain PSAD_BLOCK_FORWARD (1次引用)

| pkts bytes target | prot in | out | source | destination |
|---|---|---|---|---|
| 0 0 DROP | all | * | * | 0.0.0.0/0 | 142.202.X.X |
| 0 0 DROP | all | * | * | 142.202.X.X | 0.0.0.0/0 |

## DROP 与 REJECT 目标

在上述章节的数据包追踪中，包含字符串 `/Setup.php` 的数据包重传是 TCP 内置数据保障机制的体现，这发生在 DROP 拒绝将数据包转发到目标 TCP 栈之后。在超时后，TCP 会话会被并不优雅地关闭。然而，`fwsnort` 可以使用 `iptables REJECT` 目标代替 DROP 目标，这样攻击者的 TCP 栈在无法通过 `iptables` 防火墙转发恶意数据包的同时，还能接收到一个 RST 信号：

```
[iptablesfw#] --fwsnort --snort-sid 2281 --ipt-reset
+] Parsing Snort rules...
+] Found sid: 2281 in web-php.rules
Successful translation
```

```
[+] logfile: /var/log/fwsnort.log
+] iptables script: /etc/fwsnort/fwsnort
```

```
[iptablesfw#] /etc/fwsnort/fwsnort
+] Adding web-php rules
Rules: 4
```

现在，当我们通过 `psad --flush` 清除阻塞规则并再次对 Web 服务器发起攻击时，我们的 TCP 栈接收到了强制关闭会话的数据包：

```
[ext_scanner#] lynx http://71.157.X.X
Alert! Unexpected network error. Connection aborted.
Can't access 'http://71.157.X.X/Setup.php'
Alert! Unable to access document.
```

在 `iptables` 外部接口上截获的数据包追踪显示了发送回攻击者的 RST 数据包：

```
[iptablesfw#] tcpdump -i eth -n port 80
21:32:04.03557 142.202.X.59651 > 71.157.X.X.80: S 142921682:142921682(0)  440,0,324203167 0,nop,scale 2
21:39:24.03517 142.202.X.59651 > 71.157.X.X.80: S 138465123:138465123(0) ack 142931668 5792 460,timestamp 3247036978 324703167,nop,scale 2
21:39:24.073190 142.202.X.59651 > 71.157.X.X.80: ack 1460 nop,nop,time 3247030172 302706976
21:39:24.078422 142.202.X.59651 > 71.157.X.X.80: R 138465124:138465124(0) win 0
```

## 拦截传入 RST

在攻击示例中，TCP 连接客户端接收 RST 被本地 TCP 栈处理。但如果攻击者运行的是带有防火墙（如 `iptables`）的操作系统呢？回第三章，触发规则的数据包是已连接的一部分，因此本身设置了 ACK，而 RFC 793 规定响应数据包生成的任何 RST 都不会设置 ACK 位。只有当之前收到的数据包没有设置 ACK 位时，才会发送 RST。会话还会继续吗？

幸运的是，答案是否定的。虽然会话保持开启（因为 REJECT 目标仅将数据包发送回源地址），但违规包同时也被 `iptables` 丢弃。因此，这种场景类似于第 19 页的“结合 fwsnort 和响应”，其中使用的是 DROP 目标而不是 REJECT 目标。由于攻击者的操作系统是 Linux，我们可以调查在使用 `lynx` 客户端发送传入 RST 后的情况。我们在 `ext_scanner` 系统上添加了一条 `iptables` 规则来过滤所有传入的 RST 包：

```
[ext_scanner]$ iptables -I INPUT 1 -p tcp --tcp-flags RST,S 71.157.X.X -j DROP
[ext_scanner]$ lynx http://71.157.X.X
HTTP request sent; waiting for response
```

进程显示攻击者的 TCP 栈重传包含 `/Setup.php` 的数据包，这表明保护 Web 服务器的远程防火墙从未接收到 RST 包。由于每个重传的数据包包含相同的恶意字符串，每个数据包再次匹配了 `fwsnort` 的 REJECT 规则，因此每个数据包都会触发 `iptables` 的 RST。由于 RST 过滤规则在攻击者系统中仍然有效，攻击者的 TCP 栈从未看到这些 RST。下文显示了 RST 包（注意没有 RST 包包含 ACK）。

```
[iptablesfw]$ tcpdump -i eth0 -l -nn port 80
22:14:01.07639 142.202.X.X.37788 > 71.157.X.X.80: S 370393615:370393615(0) win 5840 ms 1460, sackock, timestamp 324783780 0,nop,scale 0
22:14:01.08079 142.202.X.X.37788 > 71.157.X.X.80: S 3669033680:3669033680(0) ack 0 370393615 win 5792 ms 1460, sackock,timestamp 2309208153 324783780,nop,scale 0
22:14:01.094582 142.202.X.X.37788 > 71.157.X.X.80: ack 1 1460 nop,timestamp 3247837789 2309208153
```

# 所有的 Metasploit 更新默认都通过带有自签名 SSL 证书的 SSL 进行。图 11-1 显示 Metasploit 客户端通过运行 `fswport` 和 `psad` 的 `iptables` 防火墙启动更新。

![](img/84e6ec42d170b9df6cf29b40151f3d15_226_0.png)

图 11-1：通过 `fswport` 和 `psad` 进行 Metasploit 更新

如你所示，客户端使用了 Metasploit 更新功能，但在 Metasploit 服务器返回更新之前，必须实例化一个有效的 SSL 会话。因此，在 SSL 握手期间，Metasploit 服务器会将其 SSL 证书返回给客户端。

Metasploit 的更新过程取决于 Metasploit 框架的版本。从 3.0 版本开始，Metasploit 使用 Ruby 编写，并使用 Subversion 源码控制系统⁴ 不仅管理漏洞数据库，还管理源代码文件。由于 Subversion 可以通过 SSL 与远程仓库通信，Metasploit 无需在内部构建此功能。相比之下，Metasploit 2.x 系列通过命令行中的 Perl 脚本 `msfupdate` 执行更新。

## Metasploit 3.0 更新

要下载并更新 Metasploit 3.0 框架，用户可以执行以下命令。（为了简洁，删除了部分输出，并假设已安装了 Subversion 控制命令 `svn`。）由于我们想查看 Metasploit 更新过程如何与更新服务器通信，因此我们使用 `tcpdump` 对 `iptables fswport` 系统进行追踪，然后在 `int_scanner` 系统上执行更新。（`tcpdump` 的 `-s 0` 命令行参数确保记录每个数据包的长度。）

```
[iptablesfsw] tcpdump -i eth -s 0 -1 -nn port 443 -w metasploit_update.pcap
[int_scanner] http://framework-markers.metasploit.com/msf/downloader/framework-3.0.tar.gz
[int_scanner] tar xf framework-3.0.tar.gz
[int_scanner] cd framework-3.0
[int_scanner] svn update
```

> ⁴Subversion (http://subversion.org) 是跟踪源码（甚至二进制文件）更改的极佳机制。http://www.cipherdyne.org 的所有项目都在 Subversion 仓库中进行跟踪，甚至用于编写本书的文件在编写过程中也通过 Subversion 进行了跟踪。

结合 `psad` 和 `fswport`

```
Error validating server certificate for 'https://metasploit.com:443':
 The certificate is not issued by a trusted authority. Use the fingerprint
to validate the certificate manually
Certificate information:
- Hostname: metasploit.com
- Valid: from Tue, 31 Jul 2008 15:39:57 GMT until Wed, 30 Jul 2008 15:39:57 GMT
- Issuer: The Metasploit Project, San Antonio, Texas, US
- Fingerprint: 05:aa:fd:bb:ea:cd:bd:00:69:d9:35:cf:75:83:3e:fc:(R),accept (temporarily) or accept (permanently)? t
u external/ruby-logon/extconf.rb
```

在 ? 处，你可以看到 Metasploit 使用自签名 SSL 证书，在 @ 处可以看到该证书的标识符和指纹信息，我们通过按下 t 来临时接受它。我们的本地漏洞数据库和所有源代码文件都与通过 Metasploit Subversion 仓库提供的最新版本同步，并且我们拥有 `metasploit_update.pcap` 文件，其中包含整个更新过程的数据包捕获。（你可以从 http://www.cipherdyne.org/LinuxFirewalls 下载此文件）

## Metasploit 2.6 更新

以下是你使用 `msfupdate` 脚本更新 Metasploit 2.6 框架时使用的命令。由于此过程也通过 SSL 进行，因此我们不需要收集另一个数据包追踪——我们只需要查看 SSL 证书如何在线路上传输的。在第 205 页“Metasploit 3.0 Updates”中获取的数据包追踪就足够了。

```
[scanner] wget http://www.metasploit.com/tools/framework-2.6.tar.gz
[scanner] tar xf framework-2.6.tar.gz
[scanner] cd framework-2.6
[scanner] ./msfupdate -u
```

```
+ -- = msfupdate v2.6 [revision 145]
[*] Calculating local file checksums. Please wait...
Update: /data/meterpreter/ext_server_sam.dll
Update: /data/msfpayload/template.exe
Update: /exploits/badlue_ext_overflow.pm
Update: /exploits/bomberclone_overflow_win32.pm
Continue?(y or no) > yes
[*] Starting online update of 34 file(s)...
0001/0034 00012000 bytes /.data/meterpreter/ext_server_sam.dll
0002/0034 0002200 bytes /.data/msfpayload/template.exe
0003/0034 0000c74 bytes /.exploits/badlue_ext_overflow.pm
0004/0034 0000c72 bytes /.exploits/bomberclone_overflow_win32.pm
[*] Regenerating local database
```

## Signature开发

在下面的部分，我们收集了一个 Metasploit 更新会话的数据包追踪，这允许我们看到 SSL 证书的样子。使用 Snort 准确检测 Metasploit 更新的第一步是使用你喜欢的嗅探器或解码器分析此数据包。我们的目标是开发这样一条 Snort 规则，因为 Metasploit 使用自签名 SSL 进行更新，由于证书是以明文形式传输的，因此使用 Wireshark 或 `tcpdump` 等工具提取数据包是非常简单的：

```
[iptablesfw]$ tcpdump -i eth -s 0 -1 -nn port 443 -w metasploit_update.pcap
22:52:30.17872 IP 216.75.243 > 192.168.1.20:443, length 148 (timestamp 15312381)
0000  ip4500 0a5d dc44 4000 02f6 ec08 d4ab
0010  001a 08b9 01b3 06cc 082f 44e2 44b7 a3a2
0020  0010 00a8 82e6 33d1 e221 088a f97
0030  d5e1 74f3 1601 0140 08e1 06d9 0145
0040  2c85 82f1 05e5 e0bd 023c 0973 04d7
0050  4182 65d7 40c7 55f6 59f8 0300 00
0060  66e7 1d36 63d3 78f8 c1d0 06d4 05f4 66
0070  80e7 42f6 3bfc 8af7 9d55 09c1 08d3
0080  0039 0316 0031 0614 08bf 0670 0060
0090  066a 0312 0666 3082 054a 0063 0201 0202
00a0  0101 000d 06b9 82e6 4486 27f8 0105
00b0  0010 8a1d 31b8 30d9 05c1 6064 0553
00c0  0731 1439 12d6 03c5 04f8 1305 3465
00d0  00f0 5316 648f 5620 04d5 6760 7371 7630
00e0  2050 726f 7265 6457 3114 3012 0654
00f0  01b3 04ba 6576 6656 6670 62d6 6673
0110  0120 3014 0650 53d1 03d3 6474 6173
0120  06f9 7420 7431 3124 3022 0629 2486 2486
```
