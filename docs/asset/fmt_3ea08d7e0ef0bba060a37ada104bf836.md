
之后，你可以通过提示符处的相应数字读取消息。同样，你可以使用 `d` 命令加上消息编号来删除消息，或在提示符处输入 `q` 命令退出邮件工具。

另一个可以在终端运行的流行用户代理是 `matt`，它在屏幕顶部显示常用功能列表，并允许你使用键盘上的光标键显示电子邮件。`matt` 工具的示例如图 14-5 所示。

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_657_0.png)

图 14-5 matt 用户代理

## 章节总结

- 网络是连接在一起并交换信息的计算机集合。
- 协议定义了在网络上传输的信息格式。互联网和大多数网络使用的协议是 TCP/IP。
- TCP/IP 网络上的每台计算机必须有一个有效的 IP 地址和子网掩码。
- `/etc/sysconfig/network-scripts` 目录包含 NIC 和 PPP 接口的配置。
- 网络接口的 TCP/IP 配置可以手动指定或通过 DHCP 或启动服务器自动指定。

**AND 操作** —— 通过比较二进制位从 IP 地址和子网掩码计算网络 ID 和主机 ID 的过程。
**广播 (broadcast)** —— 针对网络上所有计算机的 TCP/IP 通信。
**无类域路由 (CIDR) 表示法** —— 常用于表示 IP 地址及其子网掩码的符号。
**默认网关 (default gateway)** —— 网络上用于发送数据包到远程网络的路由器 IP 地址。
**域名系统 (DNS)** —— 用于主机名的分级命名空间。
**以太网 (Ethernet)** —— 如今网络中最常用的介质访问方法。
**完全限定域名 (FQDN)** —— 遵循 DNS 规范的主机。
**ftp 工具** —— 可从 FTP 服务器下载文件的工具。
**主机 ID (host ID)** —— IP 地址中表示主机的部分。
**主机名 (host name)** —— 分配给计算机的友好名称。
**hostname 命令** —— 用于显示和更改计算机主机名的命令。
**ifconfig 命令** —— 用于显示和修改网络接口 TCP/IP 配置信息的命令。
**网协议 (IP) 地址** —— 代表网络上计算机的一系列 8 位数字。
**互联网服务提供商 (ISP)** —— 提供互联网访问的公司。
**局域网 (LANs)** —— 计算机在物理上相互接近的网络。
**mail 工具** —— 常见的 Linux 用户代理。

# 第14 章 网络配置

数据包网络管理器 (ping) — 一个用于检查网络上 TCP/IP 连通性的命令。

数据（packets） — 由网络协议格式化的数据包。

协议（protocol） — 网络上计算机之间使用的通信规则集。

路由器（routers） — 能够将数据包从一个网络传输到另一个网络的设备。

安全 shell (ssh) — 一种用于在 Linux 计算机上运行远程程序的程序；它可以加密客户端与服务器之间的流量。

smbclient — 用于连接到 Windows 系统共享的程序。

smbmount 命令 — 用于将 Windows 计算机的目录挂载到 Linux 计算机挂载点的命令。

子网掩码（subnet mask） — 一系列8 位数字，用于确定 IP 地址的网络部分和主机部分。

子网划分（subnetting） — 将单个网络划分为若干个较小的网络以控制流量的过程。

telnet — 一种用于在 Linux 计算机上运行远程程序的程序。

令牌环（Token Ring） — 一种流行的介质访问方法。

信任访问（trusted access） — 一种配置，允许计算机在不提供密码的情况下访问给定的计算机。

单播（unicast） — 目标为单个计算机的 TCP/IP 通信。

广域网 (WANs) — 计算机在地理位置上相隔远的网络。

## 复习题

+ 1. 子网掩码用于区分 TCP/IP 地址中的主机部分和网络部分。对或错？
+ 2. 当作为匿名用户登录 FTP 服务器时，通常使用什么密码？
  a. 用户的普通网络密码
  b. 存储在 `/etc/ftp/pass-secrets` 中的密码
  c. FTP 服务器上用户账户的密码
  d. 用户的电子邮件地址
+ 3. 哪种网络服务允许你将来自网络上另一台 Linux 计算机的目录挂载到你计算机上的挂载点？
  a. NIS
  b. NFS
  c. SMB
  d. FTP
+ 4. `/etc/sysconfig/network-scripts` 目录包含有关 NIC、ISDN 和 PPP 连接配置信息的文件。对或错？
+ 5. 哪一个文件存储了用于解析主机名的 DNS 服务器的 TCP/IP 地址？
  a. `/etc/hosts`
  b. `/etc/host.conf`
  c. `/etc/resolve`
  d. `/etc/resolv.conf`
+ 6. 输入什么命令退出 FTP 程序？
  a. close
  b. exit
  c. bye
  d. done
+ 7. 为了通过将主机名解析为 IP 地址来测试 DNS 配置，可以使用哪些命令？（选择所有适用项）。
  a. `nslookup hostname`
  b. `dig hostname`
  c. `host hostname`
  d. `resolve hostname`
+ 8. 哪一个文件存储了主机名解析时将使用的方法以及这些方法的顺序？
  a. `/etc/nsswitch.conf`
  b. `/etc/resolve.conf`
  c. `/etc/hosts`
  d. `/etc/dns.conf`
+ 9. 将主机名解析为相应 TCP/IP 地址的两种方法是什么？（选择两个答案）。
  a. DHCP
  b. DNS
  c. `/etc/hosts`
  d. `/etc/resolv.conf`
+ 10. WAN 覆盖的地理范围大于 LAN。对或错？
+ 11. 使用哪些设备将信息从一个网络传输到另一个网络？
  a. 路由器 (routers)
  b. 局域网 (LANs)
  c. DNS 服务器 (DNS servers)
  d. DHCP 服务器 (DHCP servers)
+ 12. 使用什么命令可以查看计算机上的 TCP/IP 配置？
  a. `ifconfig`
  b. `insmod`
  c. `showip`
  d. `ipconfig`
+ 13. 用于上网通信的标准协议是什么？
  a. TCP/IP
  b. IPX
  c. DLC
  d. AppleTalk
+ 14. 哪种程序允许 Linux 计算机访问基于 Windows 的计算机上的共享？
  a. nis
  b. nfsmount
  c. smb
  d. `smbclient`
+ 15. 127.0.0.1 的 TCP/IP 地址也称为 ________。
  a. 本地地址 (local address)
  b. 查找地址 (lookup address)
  c. 本地主机 (local host)
  d. 回环地址 (loopback address)
+ 16. 在启动时配置计算机主机名的行可以在 `/etc/sysconfig/network` 中找到。对或错？
+ 17. 使用哪个命令激活别名为 eth0 的 NIC？
  a. `ifup`
  b. `ifup eth0`
  c. `ipup eth0`
  d. `ifdown eth0`

## 动手项目

+ 18. 在系统下次启动或网卡启动时，修改哪个文件来更改系统上第一个别名 NIC 的 TCP/IP 地址？
  - `/etc/sysconfig/network-scripts/ifcfg-eth1`
  - `/etc/sysconfig/network-scripts/ifcfg-eth0`
  - `/etc/sysconfig/network-scripts/ipcfg-eth0`
  - `/etc/sysconfig/network-scripts/ipcfg-eth1`
+ 19. 在计算机使用路由器之前，必须向其提供哪些配置信息？
  - 路由表 (routing table)
  - 子网掩码 (subnet mask)
  - 默认网关 (default gateway)
  - 默认路由器 (default router)
+ 20. 下列哪些程序可以检查 TCP/IP 配置和网络连通性？（选择所有适用项。）
  - `ifconfig`
  - `ipconfig`
  - `ping`
  - `netstat`

这些项目应按照给出的顺序完成。本章介绍的动手项目总共需要三小时完成。

# 项目 14-4

在本次实践项目中，你可以使用 `ftp` 实用在互联网上托管一个 FTP 服务器。

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。
- 2. 在命令提示符下，输入 `ftp ftp.kernel.org` 并按回车。
- 3. 在 `<tmp>`，输入命令 `pwd` 并按回车。
- 4. 接下来在 `<ftp>` 提示符下输入 `cd pub` 将服务器上的目录更改为 `/pub`。输入 `pwd` 并按回车验证此操作。
- 5. 在 `<ftp>`，输入 `dir` 并按回车。
- 6. 在 `<ftp>`，输入 `lcd /tmp` 并按回车将你的本地目录更改为 `/tmp`。
- 7. 在 `<tmp>`，输入 `get README` 并按回车，将 README 文件下载到本地计算机的 `/tmp` 目录。
- 8. 接下来在 `<ftp>` 提示符下输入 `bye` 并按回车退出 `ftp` 实用程序。
- 9. 在命令提示符下，输入 `ls -F /tmp` 并按回车。
- 10. 在命令提示符下，输入 `less /tmp/README` 并按回车。
- 11. 输入 `exit` 并按回车退出 shell。

# 项目 14-5

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。
- 2. 在命令提示符下，输入 `/etc/rc.d/init.d/sshd restart` 并按回车以确保 SSH 守护进程正在运行。
- 3. 在命令提示符下，输入 `ssh localhost` 并按回车。
- 4. 在命令提示符下，输入 `who` 并按回车。
- 5. 在命令提示符下，输入 `exit` 并按回车。
- 6. 在命令提示符下，输入 `who` 并按回车。
- 7. 如果 `IP_address` 是你伙伴计算机的地址，在命令提示符下输入 `ssh IP_address` 并按回车。
- 8. 在命令提示符下，输入 `ps -elf | grep Z`。
- 9. 在命令提示符下，输入 `ifconfig` 并按回车。
- 10. 在命令提示符下，输入 `exit` 并按回车。
- 11. 在命令提示符下，输入 `ifconfig` 并按回车。
- 12. 输入 `exit` 并按回车退出 shell。

# 项目 14-6

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。
- 2. 在命令提示符下，输入 `mutt` 并按回车查看你的邮件队列内容。
- 3. 使用光标键滚动消息列表到达列表顶部，按回车读取第一条消息的内容。完成后按 `i` 退出。
- 4. 按 `d` 删除第一条消息。
- 5. 按 `q` 退出 mutt 邮件用户代理程序。
- 6. 在命令提示符下，输入 `mail` 并按回车查看你的邮件队列内容。在 `&` 提示符下，输入 `1` 并按回车读取第一封邮件。按 `q` 关闭消息。
- 7. 在 `&` 提示符下，输入 `?` 并按回车查看 mail 实用程序中可常用命令。
- 8. 在 `&` 提示符下，输入 `f *` 并按回车列出所有消息。
- 9. 在 `&` 提示符下，输入 `d *` 并按回车删除所有消息。
- 10. 在 `&` 提示符下，输入 `f *` 并按回车列出所有消息。
- 11. 在 `&` 提示符下，输入 `q` 并按回车退出 mail 实用程序。
- 12. 在命令提示符下，输入 `exit` 并按回车退出 shell。

## 654 第 15 章 配置网络服务与安全

## 网络服务

回想第 1 章“Linux 简介”，Linux 为网络上的用户提供了各种服务。

## 识别网络服务

网络服务是运行在你计算机上的进程，为网络上的客户端计算机提供某种有价值的服务。它们通常由一系列守护进程表示，这些进程监听网络上的客户端请求。守护进程通过监听具有特定数字的数据包来识别应该响应哪些数据包。这个数字被称为端口，用于唯一标识特定的服务。

端口及其关联协议定义在 `/etc/services` 文件中。要查看 telnet 守护进程监听哪个端口，可以使用以下命令：

```bash
```
