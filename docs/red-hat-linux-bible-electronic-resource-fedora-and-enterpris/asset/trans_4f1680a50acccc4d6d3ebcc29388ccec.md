
*TCP* (*atcp*) 和 *隐蔽 UDP* (*sudp*) 和 *高级隐蔽 UDP* (*audp*)。仅运行一个 TCP 服务和一个 UDP 服务。因此，如果你取消注释隐蔽或高级隐蔽服务，请确保在相应的基本服务前添加注释。

激活新服务后，你需要执行以下命令：

```
# /etc/init.d/portsentry restart
```

新的 PortSentry 模式将立即生效。这些新模式在计算机重新启动时也将生效。

## Testing PortSentry

## 测试 PortSentry

你可以以不同方式测试端口是否得到正确保护。你想要做的是运行潜在入侵者会运行的程序，并查看是否会触发 PortSentry 的适当响应。例如，你可以使用端口扫描器查看你的端口在外部世界中如何显示。你也可以使用 `telnet` 等命令尝试触发特定端口，查看 PortSentry 是否能捕获它。

`nmap` 是扫描 TCP 和 UDP 端口的流行工具。你可以向 `nmap` 命令提供主机名或 IP 地址，它将扫描计算机上的约 1500 个端口，以查看哪些端口是开放的（并且可能提供可能被破解的服务）。

`nmap` 的 RPM 包也可用。你可以下载 `nmap-frontend` 包，其中包含一个名为 `xnmap` 的 `nmap` 简单图形界面。我建议你在运行 PortSentry 的系统以及 LAN 上的另一台系统（如果有的话）上安装这些包。然后在 PortSentry 系统上运行以下流程进行测试：

- 1. 如果 PortSentry 正在运行，请通过输入以下内容将其关闭：
  # /etc/init.d/portsentry stop

- 2. 输入以下 `nmap` 命令以查看本地系统上哪些端口是开放的：
  # nmap -sS -O 127.0.0.1
  # nmap -sU -O 127.0.0.1
  
  输出显示了计算机上当前为 TCP 和 UDP 协议提供服务的端口。

- 3. 如果有任何你不希望开放的服务，你应该使用 `chkconfig service off`（将 `service` 替换为服务名称）关闭这些服务，或通过编辑 `/etc/xinetd.d` 目录中代表该服务的配置文件并将 `disable = no` 改为 `disable = yes`，或更改防火墙设置。

- 4. 如果有你希望从计算机上提供的服务，请确保代表这些服务的端口号未被 PortSentry 监控。从 `/etc/portsentry/portsentry.conf` 文件中的 `TCP_PORTS` 和/或 `UDP_PORTS` 选项中删除端口号，否则 PortSentry 将报告该端口存在可能的隐蔽扫描。

- 5. 按如下方式重新启动 PortSentry：
  ```
  # /etc/init.d/portsentry start
  ```
- 6. 再次运行 nmap，如前所述。提供合法服务的端口以及被 PortSentry 监控的端口都应显示为开放。
- 7. 检查 /var/log/messages 文件，确保 PortSentry 没有尝试监控你正在提供服务的任何端口。

当你确定 PortSentry 已按你希望的方式设置好后，从网络上的另一台计算机运行 nmap 命令。这次，将 127.0.0.1 替换为 PortSentry 计算机的名称或 IP 地址。如果一切正常，远程计算机在你的 PortSentry 计算机上扫描的第一个端口应会阻止所有后续扫描。

## Tracking PortSentry intrusions

## 跟踪 PortSentry 入侵

除了对入侵者采取行动外，PortSentry 还使用 syslog 实用程序记录其活动。PortSentry 的启动、关闭和扫描检测活动记录到你的 /var/log/messages 文件中。以下是该文件中 PortSentry 输出的示例。

```
portsentry[13259]: adminalert: Psionic PortSentry 1.0 is starting.
portsentry[13260]: adminalert: Going into listen mode on TCP port: 1
portsentry[13260]: adminalert: Going into listen mode on TCP port: 11
...
portsentry[13260]: adminalert: PortSentry is active and listening.
portsentry[]: attackalert:Connect from host:10.0.0.4 to TCP port: 31337
portsentry[]: attackalert: Connect from host: 10.0.0.4 to TCP port: 11
portsentry[]: attackalert: Host: 10.0.0.4 is already blocked. Ignoring
...
portsentry[13371]: securityalert: Psionic PortSentry is shutting down
portsentry[13371]: adminalert: Psionic PortSentry is shutting down
```

输出的第一部分显示 PortSentry 正在启动。随着 PortSentry 开始监听每个端口，该端口会在单独的日志消息中被记录。下一条消息显示计算机正在被扫描。主机 10.0.0.4 的某人运行了 nmap 来扫描计算机上的端口。PortSentry 捕获了对端口 31337 的扫描并阻止了对其他端口的扫描尝试。

最后，一组消息显示 PortSentry 正在关闭。这是一个安全警报，因为除了你之外的人也可能关闭 PortSentry 以隐藏他们已入侵的事实。

> **NOTE:** If you have been running the LogSentry package (described earlier), these messages show up in the e-mail messages you receive each hour from Logcheck.

> **注意：** 如果你一直在运行 LogSentry 包（前面已描述），这些消息会出现在你每小时从 Logcheck 收到的电子邮件消息中。

## Restoring access

## 恢复访问

如果对你想要访问的计算机的访问被切断，有几件事可以检查以纠正该问题：

- **/etc/hosts.deny:** See if the computer's IP address was mistakenly added to this file. This would cause network services to be denied to the host at that IP address.
- **/etc/hosts.deny：** 查看计算机的 IP 地址是否被错误地添加到此文件中。这会导致该 IP 地址的主机被拒绝网络服务。
- **/var/portsentry/portsentry.blocked:** Check that an entry for the computer's IP address wasn't added to the portsentry.blocked.udp or portsentry.blocked.tcp files.
- **/var/portsentry/portsentry.blocked：** 检查计算机的 IP 地址条目是否未被添加到 portsentry.blocked.udp 或 portsentry.blocked.tcp 文件中。
- **route:** Run the /sbin/route command to see if messages from the computer are being rerouted to a dead host (probably the localhost).
- **route：** 运行 /sbin/route 命令查看来自计算机的消息是否被重定向到死主机（可能是本地主机）。
- **ipchains:** Run the ipchains -L command to see if a new firewall was created to block access from the computer. (If you had created an iptables rule instead, type iptables -L to see the new firewall entry.)
- **ipchains：** 运行 ipchains -L 命令查看是否创建了新的防火墙以阻止来自计算机的访问。（如果你改为创建了 iptables 规则，输入 iptables -L 以查看新的防火墙条目。）

> TIP: To make sure that access isn't cut off again, you can add the IP address of the remote computer to the /etc/portsentry/portsentry.ignore file. Future improper scans or requests for services won't cause the remote computer to be blocked.

> 提示：为确保访问不会再次被切断，你可以将远程计算机的 IP 地址添加到 /etc/portsentry/portsentry.ignore 文件中。未来的不当扫描或服务请求不会导致远程计算机被阻止。

## Summary

## 摘要

随着互联网的兴起，安全已成为几乎所有计算机用户都面临的关键问题。正确使用密码、安全配置网络服务以及监控日志文件是保持计算机安全的重要方法。

使用加密密钥可以帮助验证你所通信对象的真实性，并使传输的数据更安全。借助 LogSentry 和 PortSentry 等工具，你可以保护你的 Red Hat Linux 系统免受入侵。

## Part IV

## 第四部分

## Red Hat Linux Network and Server Setup

## Red Hat Linux 网络和服务器设置

- Chapter 15: Setting Up a Local Area Network
- Chapter 16: Connecting to the Internet
- Chapter 17: Setting Up a Print Server
- Chapter 18: Setting Up a File Server
- Chapter 19: Setting Up a Mail Server
- Chapter 20: Setting Up an FTP Server
- Chapter 21: Setting Up a Web Server
- Chapter 22: Setting Up a News Server
- Chapter 23: Setting Up Boot Servers: DHCP and NIS
- Chapter 24: Setting Up a MySQL Database Server
- Chapter 25: Making Servers Public with DNS
- Chapter 26: Using Linux Servers from a Mac

- 第 15 章：设置本地局域网
- 第 16 章：连接到互联网
- 第 17 章：设置打印服务器
- 第 18 章：设置文件服务器
- 第 19 章：设置邮件服务器
- 第 20 章：设置 FTP 服务器
- 第 21 章：设置 Web 服务器
- 第 22 章：设置新闻服务器
- 第 23 章：设置启动服务器：DHCP 和 NIS
- 第 24 章：设置 MySQL 数据库服务器
- 第 25 章：使用 DNS 使服务器公开
- 第 26 章：从 Mac 使用 Linux 服务器

## Chapter 15

## 第 15 章

### Setting Up a Local Area Network

### 设置本地局域网

- In This Chapter
- Understanding local area networks
- Setting up a wired Ethernet LAN
- Setting up a wireless LAN
- Troubleshooting your LAN

- 本章内容
- 了解局域网
- 设置有线以太网 LAN
- 设置无线 LAN
- 故障排除你的 LAN

在家中或小型企业中，Red Hat Linux 可以帮助你连接到其他 Linux、Windows 和 Macintosh 计算机，以便你可以共享计算设备（文件、打印机和设备）。添加互联网连接和多个 LAN 之间的路由（在第 16 章中描述），Red Hat Linux 可以作为大型企业网络计算的焦点。

本章帮助你设置自己的局域网（LAN）。这里描述的流程为在家庭或组织中共享计算资源提供了基础。特别是，本章描述了如何使用以太网卡、布线和协议连接计算机。然后它具体说明如何配置你的 Red Hat Linux 计算机以便与其他计算机通信。

### Understanding Local Area Networks

### 了解局域网

通过 LAN 连接组织中的计算机可以为你节省大量时间和金钱。即使在小型配置（少于五到六个用户）中投入网络硬件的资金，也可以免去购买多台打印机、备份介质和其他硬件的费用。添加一个共享的互联网连接，你就不再需要多个调制解调器和互联网账户。

有了 LAN，你就不再需要拿着磁盘上的文件跑到走廊去在朋友的打印机上打印。必须等待邮件室传递的信息可以瞬间发送给 LAN 上的任何人（或所有人）。

有了 LAN，你开始发挥 Red Hat Linux 的最大潜力——它作为网络服务器的能力。由于 Red Hat Linux 比其他计算系统更稳健、功能更丰富（尤其是考虑到价格），将其添加到你的 LAN 中可以提供一个焦点 to
