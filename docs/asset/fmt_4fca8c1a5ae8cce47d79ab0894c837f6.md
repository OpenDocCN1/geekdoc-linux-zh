
- 2. 运行 `./configure; make; make install` 来配置并安装 `nmap`。

- 3. 使用 `sara` 运行二进制文件。

# VetesCan

`VetesCan` 是你可以从 `http://www.vetescan.com` 下载的端口扫描器。一旦下载并解压源码，运行以下：

# 使用 nmap 进行指纹分析

`nmap` 工具可以扫描单个主机或主机网络。具体来说，`nmap` 支持：

* TCP `connect()` 扫描

* TCP SYN（半开放）扫描

* TCP FIN, Xmas, NULL（隐身）扫描

* TCP 攻击

* SYN/FIN 扫描（绕过某些过滤器）

* TCP ACK 和窗口扫描

* UDP 原始 ICMP

* ICMP 不可用

* ICMP 扫描（ping 扫描）

* TCP Ping 扫描

* 直接映射 RPC 扫描

* 通过 TCP/IP 指纹识别远程操作系统

* 反向

## 扫描 TCP 端口并猜测操作系统

要扫描目标系统的开放 TCP 端口并同时猜测其使用的操作系统，请按如下运行 `nmap` 程序：

```
/usr/bin/nmap -sT -O hostname
```

将 `hostname` 替换为目标主机名。`/32` 告诉 `nmap` 只扫描网络上的主机。如果你指定 `/24`，它将扫描给定主机所在的类网络上的所有主机。如果你指定 `/16`，它扫描类 B 网络，`/8` 则扫描类 A 网络。

如果你不知道主机名，可以使用 IP 地址代替。例如：

```
/usr/bin/nmap -sT -O 192.168.1.100/32
```

此命令告诉 `nmap` 仅扫描 `192.168.1.100` 主机上的 TCP 端口 (`-sT`) 并推测其操作系统。前一个命令的输出显示所示：

Starting nmap V.2.53 by fyodor@insecure.org ( www.insecure.org/nmap/ )

Interesting ports on ns.domain (192.168.1.100):

(扫描的 1506 个端口未显示，均处于关闭状态):

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 21/tcp | open | ftp |
| 22/tcp | open | ssh |
| 25/tcp | open | smtp |
| 53/tcp | open | domain |
| 80/tcp | open | http |
| 111/tcp | open | sunprpc |
| 113/tcp | open | auth |
| 443/tcp | open | https |
| 444/tcp | open | snpp |
| 554/tcp | open | rtsp |
| 635/tcp | open | unknown |
| 2049/tcp | open | nfs |
| 3306/tcp | open | mysql |
| 5050/tcp | open | mmc |
| 8080/tcp | open | http-proxy |
| 9090/tcp | open | zeus-admin |
| 31337/tcp | filtered | Elite |

TCP 序列预测: Class:random positive increments

Difficulty=313002 (好运！)

远程操作系统推测: Linux 2.1.122 - 2.2.14

map run completed - 1 IP address (1 host up) scanned in 18 seconds

如你所见，它检测到了几个开放的 TCP 端口，并推测了响应 `192.168.1.100` 地址的机器操作系统。

## 在主机上扫描 UDP 端口

要扫描 UDP 端口，使用带有 `-sU` 选项的 `nmap`。例如：

```
/usr/bin/nmap -sU hostname/32
```

这里 `nmap` 扫描指定主机的 UDP 端口。

## 使用 Portentry 监控连接

`Portentry` 是一个 TCP/IP 端口监控工具，是 Abacus 项目套件的一部分。它允许你检测主机上的端口（探针）。你可以从 `http://www.psionic.com/abacus/portsentry` 下载 `PortSentry`。

# 第21章：防火墙安全工具

当 `PortSentry` 检测到受监控端口上有活动时，它可以报告该活动并执行安全操作，其中包括拒绝进一步访问你系统的尝试。通常，黑客会扫描连接到端口的服务的漏洞，然后攻击该服务。由于 `PortSentry` 可以检测到对多个监控端口的访问尝试，它可以剥夺黑客发起缓冲区溢出或其他类型攻击所需的时间。当它检测到端口扫描时，将采取以下操作：

- 通过 syslog 设施创建日志记录。

- 自动将故障源添加到 `/etc/hosts.deny` 文件中。

- 禁止本地主机向扫描系统发送任何数据包。这是通过为扫描系统添加死路由实现的。

- 使用数据包过滤规则配置本地主机丢弃来自扫描系统的所有数据包。

## 开始 PORTSENTRY

一旦你在子目录中下载并提取了源码，请编辑 `portsentry.conf` 文件以包含以下行：

```
TCP_PORTS="1,11,15,79,111,119,143,650,635,640,641,700,32770,32771,32772,32773,12345,12346,034,31337,32771,32772,32773,32774,40421,49724,54320"
UDP_PORTS="1,7,9,69,161,162,513,635,640,641,700,32770,32771,32772,32773,32774,337,54321"
ANCED_PORTS_TCP="1023"
ANCED_PORTS_UDP="1023"
ANCED_EXCLUDE_TCP="113,139"
ANCED_EXCLUDE_UDP="520,138,137,67"
IGNORE_FILE="/usr/local/psionic/portsentry.ignore"
HISTORY_FILE="/usr/local/psionic/portsentry.history"
OCKED_FILE="/usr/local/psionic/portsentry.blocked"
BLOCK_UDP="1"
BLOCK_TCP="1"
KILL_ROUTE="/sbin/iptables -i input -s $TARGET$ -j DROP -1"
KILL_HOSTS_DENY="$TARGET$"
KILL_RUN_CMD="/bin/echo Attack host: $TARGET$ port:$PORT >> /var/log/attacks.log"
SCAN_TRIGGER="0"
```

表 21-1 解释了每个选项。

## PORTSENTRY 配置

表 21-1 解释了该配置中的每个选项。

| 选项 | 含义 |
| :--- | :--- |
| TCP_PORTS | 监控的 TCP 端口列表（逗号分隔）。 |
| UDP_PORTS | 监控的 UDP 端口列表（逗号分隔）。 |
| ADVANCED_PORTS_TCP | 高级 TCP 端口。 |
| ADVANCED_PORTS_UDP | 高级 UDP 端口。 |
| ADVANCED_EXCLUDE_TCP | 排除的高级 TCP 端口。 |
| ADVANCED_EXCLUDE_UDP | 排除的高级 UDP 端口。 |
| IGNORE_FILE | 忽略文件路径。 |
| HISTORY_FILE | 历史文件路径。 |
| BLOCKED_FILE | 封锁文件路径。 |
| BLOCK_UDP | 是否阻止 UDP（1为是）。 |
| BLOCK_TCP | 是否阻止 TCP（1为是）。 |
| KILL_ROUTE | 用于阻止主的命令。 |
| KILL_HOSTS_DENY | 需要被拒绝的主机地址。 |
| KILL_RUN_CMD | 攻击日志记录的执行命令。 |
| SCAN_TRIGGER | 扫描触发设置（0为不触发）。 |

## 防火墙表 21-1: PORTSENTRY 配置

| 选项 | 含义 |
| :--- | :--- |
| TCP_PORTS | 监控的 TCP 端口列表（逗号分隔）。 |
| UDP_PORTS | 监控的 UDP 端口列表（逗号分隔）。 |
| ADVANCED_PORTS_TCP | 高级 TCP 端口。 |
| ADVANCED_PORTS_UDP | 高级 UDP 端口。 |
| ADVANCED_EXCLUDE_TCP | 排除的高级 TCP 端口。 |
| ADVANCED_EXCLUDE_UDP | 排除的高级 UDP 端口。 |
| IGNORE_FILE | 忽略文件路径。 |
