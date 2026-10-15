
| 目的地 | 网关 | 生成掩码 | 标志 | MSS 窗口 | irtt 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.1.0 | * | 255.255.255.0 | U | 40 | 0 | eth0 |
| 127.0.0.0 | * | 255.0.0.0 | U | 40 | 0 | lo |
| default | possum.holler | 0.0.0.0 | UG | 40 | 0 | eth0 |

浏览 `netstat` 的 man 手页可以传达该命令许多不同用途的思路，但对于目前的用途，只需要一或两个命令行选项，如表 31-1 所示。

# 表 31-1 NETSTAT 命令行选项

| 选项 | 描述 |
| :--- | :--- |
| `-r` | 显示内核路由表 |
| `-p` | 显示在每个端口上监听的进程的 PID 和进程名 |
| `-l` | 仅显示监听套接字 |

例如，要仅显示监听套接字：

```
$ netstat -l
Active Internet connections (only servers)
Proto Recv-Q Send-O Local Address Foreign Address State
tcp 0 0 *:http *:* LISTEN
tcp 0 0 *:ftp *:* LISTEN
tcp 0 0 *:ssh *:* LISTEN
tcp 0 0 *:https *:* LISTEN
Active UNIX domain sockets (only servers)
Proto RefCnt Flags Type State I-Node Path
unix 2 [ ACC ] STREAM LISTENING 1139 /tmp/.font-unix/fs7100
```

该命令的输出表明此主机上有五个服务器正在监听请求：一个 Web 服务器、一个 FTP 服务器、一个 shell 服务器、https 以及安全 Web 服务器。可以通过协议进行精细调整，例如，仅限域套接字（使用 `--unix` 参数）或仅限互联网（TCP）套接字（使用 `-inet` 参数）：

```
$ netstat --unix
Active UNIX domain sockets (only servers)
Proto RefCnt Flags Type State I-Node Path
unix 2 [ ACC ] STREAM LISTENING 1139 /tmp/.font-unix/fs7100

$ netstat --inet
Active Internet connections (only servers)
Proto Recv-Q Send-O Local Address Foreign Address State
tcp 0 0 *:http *:* LISTEN
tcp 0 0 *:ftp *:* LISTEN
tcp 0 0 *:ssh *:* LISTEN
tcp 0 0 *:https *:* LISTEN
```

# 使用 lsof

该工具的名字是 list open files（列出打开的文件）的缩写。在红帽系统中，这意味着“列出所有内容”。Linux 与类 Unix 操作系统的区别之一是，许多实体被处理为文件。`lsof` 的 man 手页列出了其中一些：打开的文件可能是普通文件、目录、块文件、可执行的文本、库、流或网络文件（套接字）。`lsof` 的语法至少和 `netstat` 一样晦，但只需要一小部分子集就可以跟踪正在运行的服务。同样，对于 `netstat`，这是为了限制你感兴趣的内容，而你使用的 `-i` 选项将列出所有的互联网文件。

```
# lsof -i:x11
COMMAND PID USER FD TYPE SIZE NODE NAME
9551 root 1u IPv4 26045 TCP *:x11 (LISTEN)
# lsof -i:https
COMMAND PID USER FD TYPE SIZE NODE NAME
httpd 750 root 16u TCP *:https (LISTEN)
```

此输出可以根据主机、服务端口或名称或协议（TCP UDP）进行过滤，例如：

```
# lsof -i:x11
COMMAND PID USER FD TYPE SIZE NODE NAME
9551 root 1u IPv4 26045 TCP *:x11 (LISTEN)
# lsof -i:https
COMMAND PID USER FD TYPE SIZE NODE NAME
httpd 750 root 16u IPv4 1116 TCP *:https (LISTEN)
```

`netstat` 和 `lsof` 构成了从多个角度检查内核工作的强大工具。例如，可以查看 `lsof` 文档中关于结合使用的讨论：`/usr/share/doc//lsof-4.51/000QUICKSTART`

# 使用 nmap

没有 `nmap` 的服务的讨论是不完整的。虽然通常在探测远程主机以发现其开放端口的范围内提到，但 `nmap` 也可以扫描自己的主机。一个简单的端口扫描如下：

```
$ nmap -sT 127.0.0.1
```

Starting nmap V. 2.54BETA2 ( .insecure.org/nmap )

Interesting ports on possum.holler.org (127.0.0.1):

(下方未列出的 1537 个扫描端口状态为：closed)

Port State Service

21/tcp open ftp

22/tcp open ssh

80/tcp open http

443/tcp open https

6000/tcp open X11

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds

...主机和服务。对于这一点，`nmap` 是理想的工具。取决于你配置防火墙的方式，上述描述的简单 ping 扫描可能不足以完成任务，但 `nmap` 具备处理这些情况的能力，我将在本章稍后部分讨论这些情况。

# 停止运行的服务

你应该意识到关于服务的两个通用问题，并且，为了延续我们在书中这一部分反复提到的一个主题，这两个中的任何一个都无法仅通过技术考虑来解决：

- 哪些服务应该在运行？
- 正在运行的服务应该允许哪些访问权限？

每个问题都可以进一步细分。第一个问题“哪些服务应该在运行”还涉及到更具实操意义的问题，即如何控制特定服务，即如何开启和关闭它。基本的答案是服务通过 `xinetd` 控制、通过 `/etc/init.d/` 中的初始化脚本控制，或者两者兼顾。

针对第二个问题的后续问题——即“允许访问正在运行的服务”——是如何控制对特定服务的访问。在这种情况下，答案是类似的：访问控制通常通过 `xinetd`、使用 TCP Wrappers 访问文件（`/etc/hosts.allow` 和 `/etc/hosts.deny`）或使用服务自身的访问设施来实现。

Red Hat Linux 使用 `inetd`，它是 `inetd` 的增强版本，添加了大量的灵活性，并可能包含对于多年来习惯了原生 `inetd` 和 TCP Wrappers 的用户来说熟悉的功能。幸运的是，`inetd` 运行的各种服务和守护进程所选择的安装默认值使得从 `inetd` 到 `xinetd` 的过渡并不算痛苦。某些服务从 `xinetd` 启动，而某些则不是。对于后者，`chkconfig` 及其伴侣 `redhat-config-services` 成了管理网络服务和其他系统守护进程的“黄金组合”。`chkconfig` 和 `redhat-config-services` 是运行级别编辑器（run level editors），这些是为略微复杂的系统初始化脚本设置提供接口的工具。`chkconfig` 是一个命令行工具，可以说是是两个程序中更强大的一个，而 `redhat-config-services` 提供了一个更简单、更愉悦的菜单驱动控制台界面。

# 使用 chkconfig

`chkconfig` 在基本用法（`chkconfig --list`）中，列出 `/etc/init.d` 中命名的每个服务，以及该服务在七个级别（0–6）中的每个级别是否启用（开启或关闭）。它还列出了由 `xinetd` 处理的每个服务以及该服务是开启还是关闭。以下是一个，显示了我一直作为示例的主机的当前状态。在该系统上，`sshd`、`httpd` 和 `ftp` 对其他主机可用：

```bash
#chkconfig --list
ntpd    0:off 1:off 2:off 3:off 4:off 5:off 6:off
atd     0:off 1:off 2:off 3:off 4:on  5:on  6:off
```

# 第 31 章：实现网络安全

| keytable | 0:off | 1:on | 2:on | 3:on | 4:on | 5:on | 6:off |
