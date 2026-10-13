
要了解所做的更改，请将生成的`/etc/sysconfig/iptables`文件与备份进行比较。任何差异都基于您在防火墙配置工具中的操作。

> **考试提示** 如果您使用防火墙配置工具，可能希望避免直接编辑`/etc/sysconfig/iptables`文件。任何更改在下次使用该工具时都将被覆盖。第 10 章描述了如何使用防火墙配置工具设置自定义规则。

### 防火墙配置工具的受信任服务

无论选择哪个工具，两者都支持轻松配置防火墙以允许访问表 4-6 中描述的各种服务器。

将表 4-6 与表 4-5 进行比较时，您可能会注意到，虽然 TCP 和 UDP 协议经常为特定服务保留端口，但实际服务经常只使用其中一种协议。

### 控制台防火墙配置工具

您可以使用`system-config-firewall-tui`命令启动控制台防火墙配置工具；结果如图 4-5 所示。如图所示，防火墙默认启用；该选项可以取消选择。

### 表 4-6
常见 TCP/IP 端口

| Service | Description |
|---|---|
| Amanda Backup Client | 与高级马里兰自动网络磁盘归档器（AMANDA）相关联的客户端，与 UDP 端口 10080 相关联 |
| Bacula | 一个开源网络备份服务器；与 TCP 端口 9101、9102 和 9103 相关联 |
| Bacula client | Bacula 服务器的客户端；与 TCP 端口 9102 相关联 |
| DNS | 域名服务（DNS）服务器；与端口 53 相关联，使用 TCP 和 UDP 协议 |
| FTP | 文件传输协议（FTP）服务器，与 TCP 端口 21 相关联 |
| IMAP over SSL | IMAP 通过安全套接字层（SSL）通常使用 TCP 端口 993 |
| IPsec | 与用于互联网安全关联和密钥管理协议（ISAKMP）的 UDP 端口 500 相关联，以及 ESP 和 AH 传输层协议 |
| Mail (SMTP) | 简单邮件传输协议服务器，如 sendmail 或 Postfix，使用 TCP 端口 25 |
| Multicast DNS (mDNS) | 与 UDP 端口 5353 相关联，以支持 Linux 的零配置网络（zeroconf）实现，即 Avahi |
| NFS4 | NFS 版本 4 使用 TCP 端口 2049，等等 |
| Network Printing Client | 标准打印客户端使用基于互联网打印协议（IPP）的 UDP 端口 631 |
| Network Printing Server | 标准打印服务器客户端使用基于互联网打印协议（IPP）的 TCP 和 UDP 端口 631 |
| OpenVPN | 开源虚拟专用网络系统，使用 UDP 端口 1194 |
| POP-3 over SSL | POP-3 通过安全套接字层（SSL）通常使用 TCP 端口 995 |
| RADIUS | 远程身份验证拨入用户服务（RADIUS）协议使用 UDP 端口 1812 和 1813 |
| Red Hat Cluster Suite | Red Hat 多系统套件使用 TCP 端口 11111 和 21064，以及 UDP 端口 5404 和 5405 |
| Samba | Linux 在 Microsoft 网络上通信的协议使用 TCP 端口 139 和 445，以及 UDP 端口 137 和 138 |
| Samba Client | Linux 在 Microsoft 网络上客户端通信的协议使用 UDP 端口 137 和 138 |
| Secure WWW (HTTPS) | 与安全 Web 服务器的通信使用 TCP 端口 443 |
| SSH | SSH 服务器使用 TCP 端口 22 |
| TFTP | 与简单文件传输协议（TFTP）服务器的通信需要 TCP 端口 69 |
| TFTP Client | 奇怪的是，TFTP 客户端不需要开放端口；所有通信都通过 TFTP 服务器的开放 TCP 端口 69 进行 |
| Virtual Machine Management | 远程访问基于 KVM 的虚拟机使用 TCP 端口 16509 |
| Virtual Machine Management (TLS) | 远程访问基于 KVM 的虚拟机使用 TCP 端口 16509 可以配置传输层安全（TLS） |
| WWW (HTTP) | 众所周知的 Web 服务器使用 TCP 端口 80 |

## 图 4-5

`system-config-firewall`

控制台防火墙配置工具

![](img/9139201cfcaf4292284a0eed074928e5_226_0.png)

按需按下 TAB 键以高亮 Customize 选项并按 ENTER 继续。查看受信任服务的列表；虽然顺序略有不同，但它们与表 4-6 中显示的列表相匹配。如果您已在本地系统上配置了其中一项服务，您需要激活选项将其设为受信任服务。向下滚动直到看到 SSH。它默认应已启用。做出适当的选择并选择 Forward 继续。

在 Other Ports 窗口中，高亮 Add 并按 ENTER 打开图 4-6 所示的 Port and Protocol 屏幕。该图中的条目演示了如何在防火墙中以 TCP 协议打开 10000 到 10010 端口的方式。进行任何所需更改并选择 OK，或通过选择 Cancel 取消。

返回到 Other Ports 窗口后，您可以配置额外的端口。如有需要，您可以单击 Forward 进入 Trusted Interfaces 窗口，然后配置 Masquerading、Port Forwarding 和 ICMP 过滤，但这些细节更密切地关联于第 10 章讨论的 RHCE 考试目标。

相反，选择 Close 并按 ENTER 返回图 4-5 所示的屏幕。您可以再次重复 Customize 过程，选择 Cancel 以禁用更改，或选择 OK 以实施它们。在实施更改之前，您会收到如图 4-7 所示的警告。

## 图 4-6
为防火墙配置其他端口

![](img/9139201cfcaf4292284a0eed074928e5_227_0.png)

## 图 4-7
在实施新的防火墙之前

![](img/9139201cfcaf4292284a0eed074928e5_228_0.png)

## GUI 防火墙配置工具

如果安装了`system-config-firewall`软件包，您可以使用`system-config-firewall`命令在基于 GUI 的命令行中启动 GUI 防火墙配置工具。或者，在 GNOME 桌面环境中，单击 System | Firewall。结果如图 4-8 所示。如图所示，防火墙默认是启用的，但可以通过按下 Disable 按钮来禁用。

GUI 防火墙配置工具具有与对应的基于控制台的工具相同的服务列表，只是顺序略有不同。

如有需要，您还可以配置自定义访问端口；单击 Other Ports 并单击 Add 以打开图 4-9 所示的 Port and Protocol 窗口。请注意窗口如何根据`/etc/services`文件的内容提示端口。

与基于控制台的工具一样，GUI 防火墙配置工具的其他功能更密切地关联于 RHCE 考试。有关更多信息，请参阅第 10 章。

## 图 4-8
GUI 防火墙配置工具

![](img/9139201cfcaf4292284a0eed074928e5_229_0.png)

## 图 4-9
在 GUI 防火墙配置工具中添加自定义端口

![](img/9139201cfcaf4292284a0eed074928e5_229_1.png)

## 练习 4-3
### 调整防火墙设置

在本练习中，您将从命令行界面调整防火墙，并使用`nmap`和`telnet`命令查看结果。虽然在 Red Hat 考试中解决问题的具体方式并不重要，但在本次练习中，您将看到修改`/etc/sysconfig/iptables`配置文件时会发生什么。当然，可以使用防火墙配置工具执行相同的任务。这假设系统具有本章所述的默认防火墙。

- 1. 使用`nmap localhost`命令查看本地系统上的当前活动服务。使用`ifconfig eth0`命令记录本地系统的 IP 地址。如果本地系统是`server1.example.com`，则该 IP 地址应为`192.168.122.50`。
- 2. 备份当前防火墙配置文件`/etc/sysconfig/iptables`的副本。确保使用`cp`命令而不是`mv`命令。
- 3. 使用`/etc/sysconfig/iptables restart`命令确保防火墙当前正在运行。
- 4. 转到另一台系统。您可以通过不同的虚拟机进行操作，或使用`ssh`命令远程访问。如果`tester1.example.com`系统正在运行，您可以使用`ssh 192.168.122.150`命令登录该系统。
- 5. 使用`nmap`命令查看防火墙之外看到的内容；对于所提及的`server1.example.com`系统，正确的命令将是`nmap 192.168.122.50`；如果步骤 1 中找到的 IP 地址不同，请相应替换。
- 6. 返回原始系统。在文本编辑器中打开`/etc/sysconfig/iptables`文件。
- 7. 在文件中将 22 替换为 25，并保存更改。
- 8. 如步骤 3 所做，重新启动防火墙。
- 9. 如步骤 4 所做，返回`tester1.example.com`系统。
- 10. 重复步骤 5。您看到了什么？
- 11. 返回原始系统。如有需要，从备份中恢复`iptables`文件，并如步骤 3 所做重新启动防火墙。

## 认证目标 4.04
### 安全增强型 Linux 入门

Security-Enhanced Linux (SELinux) 由美国国家安全局开发，以提供强制访问控制级别。它超出了与文件权限和 ACL 相关的自主访问控制。本质上，如果发生安全漏洞，SELinux 会限制损害。例如，如果与 FTP 服务关联的系统账户被攻破，SELinux 会使利用该账户攻破其他服务变得更加困难。

### SELinux 的基本功能

SELinux 为每个文件分配不同的上下文，称为 subjects、objects 和 actions。在 SELinux 世界中，subject 是一个进程，例如正在执行的命令，或正在运行的应用程序，例如 Apache Web 服务器。object 是一个文件。action 是 subject 可以对 object 执行的操作。

例如，Apache Web 服务器进程可以获取诸如网页之类的对象并将其显示给全世界的客户端查看。只要对象文件具有适当的 SELinux 上下文，该操作在 RHEL 6 的 SELinux 实现中通常是允许的。

与 SELinux 关联的上下文是细粒度的。换句话说，如果黑客入侵并接管了您的 Web 服务器，SELinux 上下文会阻止该黑客利用此漏洞入侵其他服务。

要查看特定文件的上下文，请运行`ls -Z`命令。例如，查看图 4-10 中此命令的作用，它显示了我`/root`目录中的安全上下文。

如本章开头所述，RHCSA 考试中有四个目标与 SELinux 相关。您将在以下各节中探索如何实现这些目标。

### SELinux 状态

如 RHCSA 目标所述，您需要知道如何“为 SELinux 设置 enforcing /permissive 模式”。SELinux 有三种可用模式：enforcing、permissive 和 disabled。enforcing 和 disabled 模式不言自明。SELinux 在 permissive 模式下意味着任何被违反的 SELinux 规则都会被记录，但违规不会阻止任何操作。

如果您想更改 SELinux 的基本状态，请更改 SELINUX 指令。下次重新启动时，更改将应用于系统。

如果 SELinux 配置为 enforcing 模式，它以两种方式之一保护系统：在 targeted 模式或在 mls 模式下。默认是 targeted，它允许您以细粒度的方式自定义 SELinux 保护的内容。相比之下，MLS 更进一步，使用为国防部开发的 Bell-La Padula 模型。该模型，如`/etc/selinux/targeted/setrans.conf`文件所示，支持 c0 和 c3 层级之间的安全层级。虽然 c3 级别被列为“Top Secret”，但可用级别的范围一直延伸到 c1023。这种细粒度的保密级别尚未完全开发。如果您想探索 MLS，请安装`selinux-policy-mls` RPM。

## 图 4-10
不同文件的 SELinux 安全上下文

```
