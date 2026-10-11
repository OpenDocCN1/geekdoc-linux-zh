
OS 检测确认目标运行的是 Linux 内核 `2.6.32`。这些信息结合服务版本，对目标系统的安全态提供了一个非常全面的视角。

# 第五部分：学习 Linux 技术

> 注意
> 如果你熟悉 `nmap`，你就知道 TCP SYN 扫描是 `nmap` 使用的默认扫描方式。TCP SYN 扫描在以隐蔽性方式探测远程系统方面表现出色。由于你是为了审计目的而扫描自己的系统，因此使用更“重重量级”的 `nmap` 工具进行扫描是有意义的。如果你仍然想使用 TCP SYN 扫描，命令是 `nmap -s ip_address`。

Host-A 上目前运行的服务并不十分“有趣”。因此在接下来的示例中，使用 `systemctl` 命令在 Host-A 上启动了另一个服务——`ssh`（参见第 15 章）。这应该为 `nmap` 工具提供一个更有趣的查找目标。

``` 
# systemctl start sshd.service

# systemctl status sshd.service

sshd.service - OpenSSH server daemon

Loaded: loaded (/lib/system/system/sshd.service; disabled)

Active: active (running)

Thu, 22 Mar 2015 10:57:24 -0400; 12 ago

Main PID: 1750 (sshd)

CGroup: name=systemd:/system/sshd.service

  1750 /usr/sbin/sshd -D#
```

此外，Host-A 的防火墙阻止了来自 Host-B 的 `nmap` 扫描，如果看到防火墙关闭时 `nmap` 扫描可以报告什么将会很有趣。以下是显示 Host-A 上禁用防火墙的示例：

``` 
# systemctl stop iptables.service

iptables.service - IPv4 firewall with iptables

Loaded: loaded (/lib/system/system/iptables.service; enabled)

Active: inactive (dead)

Thu, 22 Mar 2015 11:21:28 -0400; 8s ago

Process: 186 ExecStart=/usr/libexec/iptables.init stop

  (code=exited, status=0/SUCCESS)

Process: 6656 ExecStart=/usr/libexec/iptables.init start

  (code=exited, status=0/SUCCESS)

CGroup: name=systemd:/system/iptables.service
```

随着新服务的运行和 Host-A 防火墙的降低，`nmap` 扫描应该能发现一些东西。接下来，再次从 Host-B 运行 `nmap` 扫描。这次，`nmap` 工具使用了运行在开放端口 `22` `ssh` 服务。请注意，当 Host-A 防火墙关闭时，两次 `nmap` 扫描都获取了多得的信息。这确实证明了你的 Linux 服务器防火墙的重要性。

# 第 25 章：网络上的 Linux 安全防护

``` 
$ nmap -sT 10.140.67.23

Starting Nmap 5.21 ( http://nmap.org ) at 2012-03-22 06:22 HADT

nmap scan report for 10.140.67.23

Host is up (0.016s latency).

Not shown: 999 closed ports
```

| PORT | STATE | SERVICE |
| :--- | :--- | :--- |
| 22/tcp | | ssh |

Nmap done: 1 IP address (host up) scanned in 0.40 seconds
$ sudo nmap -sU 10.140.67.23 ************
[sudo] password for johndoe:
Starting Nmap 5.21 ( http://nmap.org ) at 2012-03-22 06:22 HADT
nmap scan report for 10.140.67.23
Host is up (0.0072s latency).
Not shown: 997 closed ports
```

| PORT | STATE | SERVICE |
| :--- | :--- | :--- |
| 68/udp | open|filtered | dhcp |
| 631/udp | open|filtered | ipp |

Nmap done: 1 IP address (host up) scanned in 10.83 seconds

为了进行彻底的审计，务必包含 UDP 扫描。此外，还有额外的 `nmap` 扫描可能对你的组织有所益。请查看 `nmap` 工具网站以获取更多建议。

> 警告
> 如果你一直在跟着操作并降低了服务器的防火墙以执行这些 `nmap` 扫描，请务必再次调高！

## 控制网络服务的访问

你仍然需要对你的 Linux 服务器应该提供的那些服务实施控制。完全禁用不使用的服务是可以的，但对于需要的服务，你必须设置访问控制。对于包含 Wrapper 支持的 Linux 系统，这种必要的访问控制是通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件实现的。如果支持 Wrapper，网络服务将使用 `libwrap`。要检查是否存在 `libwrap`，你可以对网络守护进程运行 `ldd` 命令。接下来的示例显示 `ssh` 守护进程使用了 Wrappers。如果你的 Linux 系统的 `sshd` 不使用 Wrappers，则不会显示任何输出。

``` 
$ ldd /usr/sbin/sshd | grep libwrap
```

当请求包含 Wrapper 的网络服务时，系统会扫描 `hosts.allow` 和 `hosts.deny` 文件，并检查是否有匹配请求远程系统地址的条目。当远程系统请求访问支持 Wrapper 服务时，会发生以下步骤：

1. 检查 `hosts.allow` 文件。
   - 如果远程系统的地址在列表中：
     - 允许访问。
     - 不进行 TCP Wrapper 检查。
   - 如果远程系统的地址不在列表中，则在 `hosts.deny` 文件上继续 TCP Wrapper 检查。
2. 检查 `hosts.deny` 文件。
   - 如果远程系统的地址在列表中，则拒绝访问。
   - 如果远程系统的地址不在列表中，则允许访问。

`hosts.deny` 文件的评估顺序很重要。例如，你不能在 `hosts.deny` 文件中拒绝一个已经在 `hosts.allow` 文件中被授予访问权限的主机。列出每一个可能尝试连接到你计算机的地址是没有意义的。`hosts.allow` 和 `hosts.deny` 文件允许你指定整个地址集和组。你可以使用通配符来指定所有可能的地址。此外，你还可以限制这些文件中的条目，使其仅适用于特定服务。考虑以下一个典型的 `hosts.allow` 和 `hosts.deny` 组合示例。

``` 
# cat /etc/hosts.allow

# hosts.allow 此文件描述了允许

# 使用本地 INET 的主机名

# allowed to use the local INET, as

# decided by /usr/sbin/tcpd.

sshd:192.168.1.

vsftpd: all
```

``` 
# cat /etc/hosts.deny

# hosts.deny 此文件描述了禁止

# 使用本地 INET 的主机名

# denied to use the local INET, as

# decided by /usr/sbin/tcpd.

all: all
```

在 `hosts` 文件中，以 `#` 字符开头的行是注释，会被忽略。其他行由逗号分隔的服务名称组成，后面跟着一个冒号（`:`）和一个逗号分隔的客户端列表。在这种语文中，客户端是指任何尝试访问系统的计算机。例如，上面的示例是相当严格的配置。该行：

``` 
sshd:
```

``` 
vsftpd:
```
