
示例 `./nmap -sP 192.168.100.0/24`（列出网络上的主机）

示例 `./nmap -sS -sV 192.168.100.18`（扫描一个主机。此示例使用 TCP/SYN 扫描并尝试识别已安装的服务）

## onesixxtyone

### DESCRIPTION
`onesixxtyone` 利用了 SNMP 是一种无连接协议的特性，并以尽可能快的速度发送所有 SNMP 请求。然后，扫描器等待响应返回并对其进行记录，这种方式类似于 `Nmap` 的 ping 扫描。默认情况下，`onesixxtyone` 在发送数据包之间等待 10 毫秒，这对于 100MB 的交换式网络是足够的。用户可以通过 `-w` 命令行选项调整此值。如果设置为 0，扫描器将以内核接受的速度发送数据包，这可能会导致数据包丢失。

### USAGE
`onesixxtyone [options] <host> <community>`

#### OPTIONS
- `-c <communityfile>` 包含尝试的团体名的文件
- `-i <inputfile>` 目标主机文件
- `-o <outputfile>` 输出日志
- `-d` 调试模式，使用两次可获取更多信息
- `-w <n>` 在发送数据包之间等待 `n` 毫秒（1/1000 秒）（默认值 10）
- `-q` 静默模式，不将日志打印到标准输出，配合 `-l` 使用

### EXAMPLE
`onesixxtyone 192.168.100.51`

Kali Linux 2013 工具列表

## [12] 信息收集 - SSL 分析

- `sslcaudit`
- `ssldump`
- `sslh`
- `sslscan`
- `sslsniff`
- `sslstrip`
- `ssllyze`
- `stunnel4`
- `tlssled`

## sslcaudit

### DESCRIPTION
`sslcaudit` 项目的目标是开发一种实用程序，自动测试 SSL/TLS 客户端对 MITM 攻击的抵抗能力。它对于测试厚客户端、移动应用程序、设备或几乎任何通过 TCP 进行 SSL/TLS 通信的程序可能有用。

完整文档地址：`http://www.gremwell.com/sslcaudit_files/doc/sslcaudit-user-guide-1.0.pdf`

### USAGE
`sslcaudit [Options]`

```
EXAMPLE ./sslcaudit
EXAMPLE ./sslcaudit --server 62.213.200.252:443
EXAMPLE ./sslcaudit --server 62.213.200.252:443 \
  --user-cert test/certs/www.example.com-cert.pem
  --user-key test/certs/www.example.com-key.pem
```

## ssldump

### DESCRIPTION
`sldump` 是一个专门针对 SSLv3/TLS 的网络协议分析器。该工具的主要目的是识别所选网络接口上的 TCP 连接，并将其解释为 SSLv3/TLS 流量。它解码 SSLv3/TLS 流量记录并使用文本进行显示。在某些情况下，它还可以解密并显示应用程序数据流量。与 `tcpdump` 不同，此工具需要看到数据传输的双方，在使用网络分路器（taps）时可能会遇到问题。

更多信息：`http://www.rtfm.com/ssldump/sldump.html`

### USAGE
`sldump [ -vtaTnsAxxHVNdq ] [ -r dumpfile ] [ -i interface ] [ -k keyfile ] [ -p password ] [ expression ]`

### EXAMPLE
`sldump -i eth0 port 443`（监听接口 `eth0` 端口 `443` 流量）

`sldump -i le0 port 443 and host romeo`（监听 `le0` 端口 `443` 主机 `romeo`）

`sldump -Ad -k ~/server.pem -p foobar -i le0 host romeo`（解密到主机 `romeo` 的流量并使用密码 `foobar`）

`sldump -nr /var/tmp/www-ssl-client.cap`（显示名为 `www-ssl-client.cap` 的 `tcpdump` 捕获文件中找到的所有 SSL 记录消息）

### DESCRIPTION
`sslh` - SSL/SSH 复用器。`sslh` 接受指定端口上的连接，并根据对远程客户端发送的第一个数据包进行的测试对其进行进一步转发。

因此，`sslh` 充当协议解复用器或交换机。它的名称来源于其最初在同一端口上提供 SSH 和 HTTPS 服务。

### USAGE
`sslh [-t num ] [-p listening address] [-l target address for SSL] [-s target address for SSH] [-u username] [-P pidfile] [-v] [-i] [-V] [-f]`

### OPTIONS
`http://rpm.pbone.net/index.php/stat/45/idpl/20655622/numer/8/nazwa/sslh`

### EXAMPLE
n/a 配置脚本并启动/停止/重启脚本

## sslscan

### DESCRIPTION
`sslscan` 是一个快速扫描器。它连接到 SSL 端口，确定支持哪些协议，并以文本返回信息。

### USAGE
`sslscan [Options]`

#### OPTIONS
- `-l <target address>` SSL 的目标地址
- `-s <target address>` SSH 的目标地址
- `-u <username>` 用户名
- `-P <pidfile>` pid 文件
- `-v` 详细模式
- `-i` 接口
- `-V` 版本信息
- `-f` 强制模式

### EXAMPLE
`sslscan 192.168.1.1`

## sslsniff

### DESCRIPTION
`sslsniff` 是一个用于拦截和解密 SSL 流量的工具。它与其他工具配合捕获并分析流量。

### USAGE
`sslsniff [Options]`

### EXAMPLE
`sslsniff 192.168.1.1`

## sslstrip

### DESCRIPTION
`sslstrip` HTTP 剥离攻击。它将透明地劫持网络上的 HTTP 流量，监控 HTTPS 链接和重定向，然后将这些链接映射为类似的 HTTP 链接或图形相似的 HTTPS 链接。它还支持提供看起来像锁图标的 favicon、选择性记录和拒绝会话。首先，`arpspoof` 说服网络它们应该将流量发送给我们。

## sslyze

### 描述
快速且功能强大的 SSL 扫描器。`SSLyze` 是一个 Python 工具，可以通过连接到服务器来分析其 SSL 配置。它的设计目标是快速且全面，旨在帮助组织和测试人员识别影响其 SSL 服务器的配置错误。

更多信息：`https://github.com/ISECPPartners/sslyze/wiki`

主要功能包括：
- 兼容 SSL 2.0/3.0 以及 TLS 1.0/1.1/1.2
- 性能测试：会话恢复和 TLS 票证支持
- 安全测试：弱加密套件、不安全的重协商、CRIME 和 THC-SSL DoS 攻击
- 服务器证书验证
- 支持带 SMTP 和 XMPP 的 StartTLS，以及通过 HTTPS 代理进行流量隧道
- 为执行双向认证的服务器提供客户端证书支持
- 扫描结果可以写入 XML 文件以便进一步后续处理

```
USAGE python sslyze.py [options] www.target1.com www.target2.com:443
```

```
EXAMPLE python sslyze.py --regular www.isecpartners.com:443 www.google.com
```

Kali Linux 2013 工具列表

## stunnel4

### 描述
`stunnel` 程序设计用于在远程客户端与本地 `inetd` 可启动 或远程服务器之间作为 SSL 加密封装器。其概念是，通过在系统上运行不感知 SSL 的守护进程，你可以轻松地设置让它们通过安全的 SSL 通道与客户端通信。`stunnel` 可用于为常用的 `inetd` 守护进程（如 POP-2、POP-3 和 IMAP 服务器）添加 SSL 功能，用于如 NNTP、SMTP 和 HTTP 等独立守护进程，以及在不更改源代码的情况下通过网络套接字对 PPP 进行隧道传输。

### 用法
`stunnel [<filename>] | -fdn | -help | -version | -sockets`
