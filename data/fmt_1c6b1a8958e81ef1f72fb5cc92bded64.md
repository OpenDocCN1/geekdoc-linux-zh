
| 标识符 (Identification) | 标志 (Flags) | 分片偏移 (Fragment Offset) |

| +------------------------------------------------------ |

| 生存时间 (Time to Live) | 协议 (Protocol) | 头部校验和 (Header Checksum) |

| +------------------------------------------------------ |

| 源地址 (Source Address) |

| +------------------------------------------------------ |

| 目的地址 (Destination Address) |

| +------------------------------------------------------ |

| 选项 (Options) | 填充 (Padding) |

| +------------------------------------------------------ |

通常，IP 头部不包含选项（Options）字段，因此长度为 20 字节。当存在选项字段时，其实际长度由总长度（Total Length）字段表示，该字段包含整个数据包（头部和数据）的长度。详情请参见 RFC 791：http://www.faqs.org/rcfs/rfc791.html。

### TCP（传输控制协议）头部

数据包都封装在 IP 数据包的数据（Data）字段中，该字段紧随 IP 头部之后。以下是 TCP 部的布局。请注意头部顶部的数字每个代表一个字节。

| 0 1 2 3 |

| 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 |

| +------------------------------------------------------ |

| 源端口 (Source Port) | 目的端口 (Destination Port) |

| +------------------------------------------------------ |

| 序列号 (Sequence Number) |

| +------------------------------------------------------ |

| 确认序列号 (Acknowledgment Number) |

| +------------------------------------------------------ |

| 数据 (Data) | U A P R S F | 窗口 (Window) |

| 偏移 (Offset) | 预留 (Reserved) | C R S S Y I |

| | G K H T N N |

| +------------------------------------------------------ |

| 校验和 (Checksum) | 紧急指针 (Urgent Pointer) |

| +------------------------------------------------------ |

| 选项 (Options) | 填充 (Padding) |

| +------------------------------------------------------ |

| 数据 |

| +------------------------------------------------------ |

详情请参见 RFC 793：http://www.faqs.org/rcfs/rfc793.html。

### UDP（用户数据报协议）头部

与 TCP 类似，每个 UDP 数据包也封装在 IP 头部的数据字段中。以下是 UDP 部的布局。头部顶部的数字每个代表一个字节。

```
0        7 8      15 16    23 24    31
+--------------------------------+
|   源端口    | 目的端口    |
|      Port      |      Port       |
+--------------------------------+
|      长度      |    校验和    |
+--------------------------------+
           数据字节 . ..
```

详情请参阅 RFC 768：http://www.faqs.org/rfcs/rfc768.html。

# 在线资源

除了书中提到的各种在线资源外，本节还包含了额外资源的链接，这些资源有助于跟进安全领域的最新动态。

> 记得检查 http://www.hacknotes.com/ 以获取最新的安全资源。

# 黑客工具

下表列出了当今黑客最常用的黑客工具。表中所提到的大多数工具在本书的第一部分中均有使用，书中也提供了这些工具的下载地址。

| 名称 | 描述 | 位置 |
|---|---|---|
| Airsnort | 流行的 WEP 破解器 (802.11b) | http://airsnort.shmo.com/ |
| Adore | 后门程序 | http://www.team-teso-teso/releases.php |
| Amap | 识别远程应用程序 | http://www.thc.org/releases.php |
| Cheops | 基于 GUI 的工具，用于识别网络上主机的 TCP 流量信息 | http://www.marko.net/cheops/ |
| Desproxy | 通过 Web 探测隧道 TCP 流量的命令行工具 | http://desproxy.sourceforge.net/ |
| Dsniff | 一套网络嗅探工具 | http://monkey.org/-/dungsong/dsniff/ |
| Ethereal | 基于 GUI 的网络嗅器 | http://www.ethereal.com/ |
| Ettercap | 基于 ncurses 的网络嗅器 | http://ettercap.sourceforge.net/ |
| Fata-Jack | 对 802.11 网络执行拒绝服务攻击 | http://www.loud-fat-bloke.com/w80211.html |
| Firewalk | 一种类似于 tracer 的工具，用于确定网关访问控制列表 | http://www.packetfactory.net/projects/firewall/ |
| Fragoute | 拦截、修改和重写网络流量 | http://www.monkey.org/-/dungsong/fragoute/ |
| Hping2 | 命令行 TCP/IP 数据包组装器和分析器 | http://www.hping.org/ |

## 16 参考中心

| 名称 | 描述 | 位置 |
|---|---|---|
| Hunt | 执行 TCP 劫持 | http://lin.fsid.cvut.cz/-kra/index.html#HUNT |
| Hydra | 主动密码暴力破解器 | http://www.thc.org/releases.php |
| John | 被动密码破解器 | http://www.thc.org/releases.php |
| Kismet | 网络嗅器 | http://www.kismet.org/ |
| Loki | 密码嗅器 | http://www.loki.org/ |
| Nmap | 端口扫描器 | http://nmap.org/ |
| OpenSSL | SSL 和 TLS | http://www.openssl.org/ |
| Snmpwalk | SNMP 查询 | http://www.snmp.org/ |
| Snort | 入侵检测系统 | http://www.snort.org/ |
| Spike | Web 代理 | http://www.spike.org/ |
| Stunnel | 创建安全隧道 | http://www.stunnel.org/ |
| Tcpdump | 数据包嗅探器 | http://www.tcpdump.org/ |
| Tornkit | Rootkit 工具 | http://www.tornkit.org/ |
| 名称 | 描述 | 位置 |
|---|---|---|
| Wget | 命令行客户端 | http://wget.org/ |
| Airirc | 破解 802.11 | http://www.airirc.com/ |
| Vuln | 漏洞列表 | http://www.vulncheck.org/ |
| Wiresh-ng | 命令行工具 | http://www.wi.com/ |
