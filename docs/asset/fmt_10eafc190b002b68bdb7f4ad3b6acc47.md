
- 3. 使用 `./sara` 命令运行该二进制文件。

使用 SARA 就像使用 SAINT 一样。

## VetesCan

VetesCan 是一个批量漏洞扫描器，你可以从 http://www.self-evident.com 下载。它包含了许多检查网络安全漏洞的程序。一旦你下载并解压源码分发包，从源码目录运行提供的脚本，扫描器就会被编译并构建。对主机进行扫描在同一目录下运行 `/vetescan hostname` 即可简单。

## 使用端口扫描器

黑客经常扫描网络以寻找开放端口。他们运行尝试连接端口的程序，并检测由哪个服务器管理这些端口。这些信息可以帮助黑客判断机器是否正在运行具有可被利用的安全漏洞的服务器软件。这被称为端口扫描。你可以使用端口扫描器在黑客之前发现你的网络中哪些端口是开放的。你可能希望确保只有你的组织所需的端口是开放的。例如，如果你只想让从互联网访问 Web (HTTP) 服务，则只开放 80 端口即可。在这里，我将讨论如何使用端口扫描器找出给定系统开放了哪些端口。

## 使用 nmap 进行指纹分析

`nmap` 实用程序是一种端口扫描器，可以扫描单个主机或主机网络上的端口。它可以扫描 TCP、UDP、ICMP 端口，还可以推测目标系统正在使用的操作系统。具体来说，`nmap` 支持以下扫描方式：

- 原生 TCP `connect()` 扫描
- TCP SYN（半开放）扫描
- TCP FIN, Xmas, 或 NULL（隐身）扫描
- TCP ftp 代理（弹射攻击）扫描
- 使用 IP 分片进行 SYN/FIN 扫描（绕过某些数据包过滤器）
- TCP ACK 和 Window 扫描
- UDP 原始 ICMP 端口不可达扫描
- ICMP 扫描（ping 扫描）
- * TCP Ping 扫描*
- 直接（非端口映射）RPC 扫描
- 通过 TCP/IP 指纹识别远程操作系统，以及
- 反向识别扫描

### 开始使用 nmap

你可以从 http://www.insecure.org 下载最新版本的 `nmap` 源码 tar 包，并按照以下方式编译和安装：

- 1. 以 root 身份，在 `/usr/src` 中使用 `tar xvzf nmap-version.tar.gz` 解压下载的源码，然后切换到新创建的子目录。
- 2. 运行 `./configure; make; make install` 来配置和安装 `nmap`。

![](img/6d176ba5e3d859ca2b04a3bba254354c_574_0.png)

> 我在 Linux 上编译最新版本的 `nmap` 时遇到困难，我从该站点下载了二进制 RPM 分发包并使用以下命令进行安装：`rpm -v http://www.insecure.org/dist/nmap-2.53-1386.rpm` 确保你更改版本号。

## 扫描端口并猜测操作系统

要扫描目标上的开放端口并猜测其操作系统，运行如下 `nmap` 程序：

```
/usr/bin/nmap
```

替换主机名。指定 `/32` 让 `nmap` 扫描目标主机。指定 `/24`，它扫描 C 网络。指定 `/16`，它扫描 B 网络。指定 `/8`，它扫描 A 网络。如果你不知道主机名，可以使用 IP 地址。例如：

```
```

## 部分：防火墙

在 192.168.1.1 上启动 `nmap` 显示的有趣端口如下：

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 21 | open | ftp |
| 22 | open | ssh |
| 25 | open | smtp |
| 80 | open | http |
| 111 | open | rpc |
| 113 | open | auth |
| 443 | open | https |
| 554 | open | rtsp |
| 635 | open | unknown |
| 2049 | open | nfs |
| 3306 | open | mysql |
| 5050 | open | zeus |
| 3137 | open | admin |

上述命令的输出显示了操作系统：

## 在主机上扫描 UDP

要扫描开放的 UDP 端口，运行带有 `-U` 的 `nmap`：

```
/usr/bin/nmap -U 192.168.1.100/32
```

## 使用 Portentry 监控连接

`Portentry` 是一种 TCP/IP 监控工具，属于 Abacus 套件。它允许你检测主机上的端口扫描（探测）。当 `Portentry` 检测到监控端口上的活动时，它可以报告并执行指定的操作，包括：

- 通过 syslog 记录日志。
- 将源自动添加到 `/etc/hosts.deny`。
- 禁止本地主机向扫描系统发送任何数据包。这是通过添加死路由实现的。
- 使用数据包过滤丢弃来自扫描系统的数据包。

### 开始使用 portsentry

一旦你下载并解压了源码，编辑 `portsentry.conf` 文件包含以下行：

```
TCP_PORTS="1,11,15,79,111,119,143,443,554,635,1080,2000,5742,6667,12345,12346,20034,31337,32771,32772,32773,32774,40421,49724,54320"
UDP_PORTS="1,7,9,69,161,162,153,635,640,641,700,32770,32771,32772,32773,32774,31337,31337,54321"
ADVANCED_PORTS_TCP="1023"
ADVANCED_PORTS_UDP="1023"
ADVANCED_EXCLUDE_UDP="520,138,137,67"
IGNORE_FILE="/usr/local/psionic/portsentry/portsentry.ignore"
HIST_FILE="/usr/local/psionic/portsentry/portsentry.history"
BLOCKED_FILE="/usr/local/psionic/portsentry/portsentry.blocked"
BLOCK_UDP="1"
BLOCK_ROUTE="/sbin/iptables -I input -s $TARGET -j DROP"
KILL_HOSTS_DENY="ALL: $TARGET"
KILL_RUN_CMD="/bin/echo Attack host: $TARGET port: $PORT >> /var/log/attacks.log"
SCAN_TRIGGER="0"
```

表 21-1 解释了此配置文件中的每个选项。

### 表 21-1: PORTSENTRY 配置选项

| 选项 | 含义 |
|---|---|
| TCP_PORTS | 一个用逗号分隔的列表，包含你想让 PortSentry 监听的 TCP 端口。列表不能包含任何空格，最多列出的端口数量为 64。此列表不用于高级隐形扫描检测。 |
| UDP_PORTS | 与上述相同，但针对 UDP 端口。此列表不用于高级隐形扫描检测。 |
| ADVANCED_PORTS_TCP | 高级监控从指定的端口开始，并监控该端口以下的所有端口。 |
| ADVANCED_PORTS_UDP | 与上述相同，但 UDP 除外。 |
| ADVANCED_EXCLUDE_UDP | 一个用逗号分隔的列表，包含你想从监控中排除的 TCP 端口。如 HTTPS (443) 或 AUTH (113) 等端口经常被误访问，因此你不应该监控它们。例如，如果有人误访问了 https://www.yourdomain.com 而不是 http://www.yourdomain.com，你是否想设置警报？很可能不想。 |
| IGNORE_FILE | 与上述相同，但 UDP 除外。一个文件的完整路径，列出 PortSentry 忽略的主机 IP 地址。 |
| BLOCKED_FILE | 一个文件的完整路径，列出 PortSentry 拒绝访问的主机 IP 地址。 |
| BLOCK_UDP | 此选项用于启用 (1) 或禁用 (0) 对所有 UDP 扫描的自动响应。 |
| BLOCK_TCP | 与上述相同，但针对 TCP。 |
| KILL_ROUTE | 设置为一个命令，用于禁用 PortSentry 系统与恶意实体（PortSentry 的目标主机）之间的通信。当检测到攻击时，将执行此命令。宏 `$TARGET$` 会替换为违规目标主机的 IP 地址，`$PORTS$` 会扩展为攻击者使用的端口。 |

# 第 21 章：防火墙安全工具 555

| 选项 | 含义 |
|---|---|
