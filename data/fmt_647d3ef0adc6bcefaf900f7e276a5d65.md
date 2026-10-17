
在很多情况下，你可能想让 `tcpdump` 命令运行一段时间，并在稍后的某个日期查看数据。在这种情况下，最好使用 `-c` 选项限制输出，并使用 `-w` 选项将数据放入文件中：

```
[root@localhost ~]# tcpdump -c 5000 -w output-tcpdump
```

该文件包含二进制数据。要读取其内容，请在 `tcpdump` 命令中使用 `-r` 选项：

```
[root@localhost ~]# tcpdump -r output-tcpdump
```

## 考试准备任务

## 复习所有关键主题

复习本章最重要的主题，这些主题在页面外边页用“关键主题”图标标记。表 15-3 列出了这些关键主题的参考以及它们所在的页码。

表 15-3 第 15 章的关键主题

| 关键主题元素 | 描述 | 页码 |
| --- | --- | --- |
| 段落 | `ping` 命令 | 301 |
| 段落 | `nmap` 命令 | 302 |
| 段落 | `netstat` 命令 | 307 |
| 段落 | `lsof` 命令 | 310 |
| 段落 | `nc` 命令 | 312 |
| 段落 | `tcpdump` 命令 | 313 |

## 定义关键术语

定义本章中的以下关键术语，并在词表中检查你的答案：

`sniffer` (嗅探器), `port scanner` (端口扫描器), `ping flood` (ping 洪水), `port` (端口), `socket` (套接字)

## 复习题

这些复习题的答案在附录 A 中。

- 1. `ping` 命令的哪个选项可以限制发送到远程系统的数据包数量？
- 2. 命令 `ping -f 192.168.1.1` 会向 192.168.1.1 机器发送 ______ 个包。
  a. 百个
  b. 无限制的
  c. 大量的
  d. 随机数量的
- 3. 使用 `nmap` 命令仅扫描开放的 UDP 端口，你会使用哪个选项？
  a. `-sP`
  b. `-sU`
  c. `-sT`
  d. `-sD`
- 4. `nmap` 命令的 ___ 选项尝试确定远程系统的操作系统类型。
- 5. `netstat` 命令的哪个选项显示路由表？
  a. `-r`
  b. `-n`
  c. `-t`
  d. 以上均不是
- 6. `netstat` 命令的 ___ 选项显示数值而非名称。
  a. `-r`
  b. `-n`
  c. `-t`
  d. 以上均不是
- 7. ___ 命令列出本地系统上的文件。
- 8. 网络通信的终点称为 ___。
- 9. 你可以使用 ___ 命令打开到远程系统的任意 TCP 或 UDP 连接。
  a. `netstat`
  b. `lsof`
  c. `ping`
  d. `nc`
- 10. `tcpdump` 命令的 ___ 选项限制特定接口上的可用包。

# 故障排除网络问题

这是三个专注于网络配置和故障排除的章节之一。本章的重点是用于配置和故障排除 Debian 和 Red Hat 系统的文件。各种故障排除工具将提供修复网络问题的技能。

本章涵盖：
- 理解不同的配置文件
- 能够使用网络工具
- 理解 `NetworkManager`

本章涵盖以下目标：
- 205.3 故障排除网络

## 我学会了吗？

“我学会了吗？”测试可以让你评估自己是读完了整个章节，还是直接跳到了“考试准备”部分。表 16-1 概述了本章的主要标题和“我学会了吗？”问题。你可以在附录 A 中找到答案。

表 16-1 我学会了吗？基础知识映射

| 基础知识 | 章节涵盖的问题 |
| --- | --- |
| 网络配置文件 | 1, 2 |
| 网络故障排除 | 3 |
| `NetworkManager` | 4 |

- 1. 以下哪个文件用于指定 DNS 服务器的位置？
  a. `/etc/hosts`
  b. `/etc/resolv.conf`
  c. `/etc/witch.conf`
  d. `/etc/dns`
- 2. 以下哪个命令设置本地主机名？
  a. `host test1`
  b. `host -n test1`
  c. `hostname test1`
  d. `hostname -n test1`
- 3. Debian 系统的主要日志文件是 `/var/log/____`。
- 4. ____ 命令是一个提供网络设备当前状态的 `NetworkManager` 工具。

# 第16 章：故障排除网络问题

**注意：** 本章涵盖的主题位于 LPIC-2 考试的 205.3 节。在该目标中包含了之前的章节涵盖的内容：
- `/bin/route`
- `/bin/ifconfig`
- `/bin/netstat`
- `/bin/ping`

在学习 LPIC-2 考试时，请理解这些命令在 205.1、205.2 和 205.3 节中的涵盖范围。

## 网络配置文件

网络排除的一部分是了解用于设置网络的配置文件。这可能是复杂的，因为这些文件取决于你的发行版。让事情变得复杂的是一种名为 `NetworkManager` 的新服务，它是本章末的主题。

## `/etc/resolv.conf` 文件

`/etc/resolv.conf` 无论你在哪个发行版上工作都应该是相同的。该文件的目的是定义客户端 DNS 设置。一个简单的 `/etc/resolv.conf` 文件包含 DNS 服务器的 IP 地址：

```
[root@localhost ~]# more /etc/resolv.conf

nameserver 192.168.1.1
```

你可以拥有三个 `nameserver` 作为 DNS 客户端可以使用的最大 DNS 服务器数量（两个是理想的）。DNS 服务器按照文件中列出的顺序进行查询。

`/etc/resolv.conf` 文件的另一个有用设置是 `search` 设置，它允许你使用相对名称进行 DNS 查询。例如，注意以下命令：

```
[root@localhost ~]# ping www

ping: unknown host www
```

没有名为 `www` 的机器。但是，假设你的大多数查询都是针对 `oneourcesource.com` 域的机器。你可以通过以下更改（加粗显示）修改 `/etc/resolv.conf` 文件，自动向相对主机名附加此域名：

```
[root@localhost ~]# more /etc/resolv.conf

nameserver 192.168.1.1

search oneourcesource.com

[root@localhost ~]# ping -c 1 www

PING www.oneourcesource.com (38.89.136.109) 56(84) bytes of data.

64 bytes from 38.89.136.109: icmp_seq=1 ttl=51 time=87.7 ms
```

```
--- oneourcesource.com ping statistics ---

1 packets transmitted, 1 received, 0% packet loss, time 102ms

rtt min/avg/max/mdev = 87.1/87.1/87.1/0.000 ms
```

你可以指定多个域进行搜索，但总共限制六个域，且整个搜索行限制为 256 个字符。

`resolver` 是执行 DNS 查询的软件。你可以使用 `/etc/resolv.conf` 文件的选项来更改解析器的行为。例如，要将超时（在查询下一个 DNS 服务器之前等待 DNS 服务器响应的时间）设置为 3 秒，请使用以下高亮条目：

```
[root@localhost ~]# more /etc/resolv.conf

nameserver 192.168.1.1

search oneourcesource.com

options timeout=3
```
