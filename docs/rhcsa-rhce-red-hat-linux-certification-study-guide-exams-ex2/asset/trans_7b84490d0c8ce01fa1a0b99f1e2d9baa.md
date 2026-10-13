
## 自测题答案

### Linux 安全层

1. 对于系统上当前不需要的服务，最佳的安全选项是不安装该服务。

### 防火墙和网络地址转换

2. 根据给定的命令，来自 192.168.77.77 系统的任何连接尝试（包括使用 ping 命令发送的数据包）都会被拒绝。

3. 与基于 iptables 的防火墙关联的规则存储在 /etc/sysconfig/iptables 中。

4. 要在为少量用户提供 Internet 访问的同时设置小型办公室，您只需要一个专用 IP 地址。其他地址可以位于私有网络上。伪装使这成为可能。

5. 设置伪装的 iptables 命令开关是 -t nat。

### 扩展的 Internet 超级服务器

6. 单个 xinetd 服务的配置文件存储在 /etc/xinetd.d 目录中。

7. 有多种可接受的选项可重新读取与 xinetd 服务关联的配置文件。标准选项是 /etc/init.d/xinetd reload；service xinetd reload 命令在功能上等效。虽然可以用 restart 代替 reload，但这是一个较差的答案。“restart”会断开任何已连接的用户。

### TCP Wrappers

8. 您正在使用 xinetd 程序启动服务。要将 Telnet 访问限制为 192.168.170.0 网络上的客户端，您需要在 /etc/hosts.allow 中允许该网络访问，并在 /etc/hosts.deny 中将其拒绝给其他所有人。由于 /usr/sbin 在 root 用户路径中，您可以直接引用 telnetd 守护进程，并在 /etc/hosts.allow 中添加以下指令：

```
telnetd : 192.168.170.0/255.255.255.0
```

然后将以下内容添加到 /etc/hosts.deny：

```
telnetd : ALL
```

9. 如果您在 /etc/hosts.allow 中允许某项服务并在 /etc/hosts.deny 中禁止它，则该服务将被允许。

### 可插拔认证模块

10. 四种基本 PAM 类型是：auth、account、password 和 session。include 类型指的是不同文件中一个或多个其他 PAM 类型。

11. sufficient 控制标志如果模块成功则立即终止认证过程。

### 使用 GPG 安全文件等

12. 列出当前已加载公钥的命令是 `gpg2 --list-key`。`gpg --list-key` 命令也是可以接受的。

## 实验答案

### 实验 1

验证此实验应该很简单。如果它有效，您应该能够在 tester1.example.com 系统上使用以下命令进行确认：

```
$ gpg2 --list-keys
```

它应包含刚刚导入到该系统的 GPG2 公钥。当然，如果加密、文件传输和解密都成功，您还应该能够在本地文本编辑器中读取解密后的 56510-labs.txt 文件。

### 实验 2

这个实验在某种程度上是自解释的，因为它可以帮助您思考如何使系统更安全。如本章所述，它从最小安装开始。RHEL 6 的最小安装恰好包含 SSH 服务器，用于远程管理访问。

虽然 RHEL 6 大大减少了安装的标准服务数量，但大多数用户仍会发现一些不需要的服务。例如，有多少管理员实际上需要为安装在虚拟机上的 RHEL 6 系统提供 Bluetooth 服务？

### 实验 3

如果您想将 RHEL 计算机设置成安全的 Web 服务器，这是一个在第 14 章中描述的简单过程。但防火墙配置是本章涵盖的过程的一部分。为此，您需要设置防火墙以阻止除最基本端口之外的所有端口。这应包括 TCP/IP 端口 80 和 443，它们允许外部计算机访问本地常规和安全 Web 服务。开放端口还应包括端口 22，用于 SSH 通信。

设置此项的最简单方法是使用 Red Hat 防火墙配置工具，您可以使用 system-config-firewall 命令启动它。进入防火墙配置工具后，请执行以下步骤，这些步骤在基于 GUI 和基于控制台的工具版本之间略有不同。

- 1. 自定义防火墙。
- 2. 选择受信任服务窗口。 （如果您使用的是基于文本的工具，请单击自定义以打开防火墙配置 – 自定义窗口。）激活 WWW（HTTP）选项。这允许从本地计算机外部访问本地常规网站。同样激活安全 WWW（HTTPS）选项。确保 SSH 选项保持激活状态。
- 3. 确保应用任何更改并退出防火墙配置工具。
- 4. 输入以下命令以检查 resulting 防火墙：
- 5. 一旦您按照第 14 章所述配置了 Web 服务，用户将能够从远程系统访问常规和安全 Web 服务器。

```
# iptables -L
```

### 实验 4

设置任何 xinetd 服务（如 Telnet）都需要多个步骤。您需要修改 xinetd Telnet 配置文件。以下步骤演示了三种不同的方法来限制对 IP 地址为 192.168.122.150 的所记录系统的访问。三种方法中的任何一种都是可以接受的。这些方法通过三种方式保护 Telnet：在 /etc/xinetd.d/telnet 配置文件中，通过 TCP Wrappers，或通过适当的防火墙命令。在“现实世界”场景中，您可能会在分层安全策略中使用这三种方法。您在 server1.example.com 系统上执行此实验。

- 1. 确保已安装 telnet-server RPM。备份当前版本的 /etc/xinetd.d/telnet 配置文件。
- 2. 激活 Telnet。使用 chkconfig telnet on 命令修改 /etc/xinetd.d/telnet 配置脚本。
- 3. 编辑 /etc/xinetd.d/telnet 配置文件。添加 only_from = 192.168.122.150 行，表示 tester1.example.com 系统。
- 4. 保存配置文件并使用 service xinetd reload 命令重新加载 xinetd 服务脚本。尝试从本地计算机访问 Telnet。会发生什么？
- 5. 尝试从 IP 地址为 192.168.122.150 的计算机访问 Telnet。会发生什么？再尝试从 LAN 上的另一台系统访问。
- 6. 恢复之前的 /etc/xinetd.d/telnet 配置文件。不要忘记使用 service xinetd reload 命令重新加载 xinetd 服务脚本。
- 7. 备份当前版本的 /etc/hosts.deny 文件。在文本编辑器中打开该文件。添加 telnetd : ALL EXCEPT 192.168.122.150 行。
- 8. 尝试从 IP 地址为 192.168.122.50 的计算机访问 Telnet。会发生什么？再尝试从 LAN 上的另一台计算机访问。
- 9. 恢复之前的 /etc/hosts.deny 文件。
- 10. 保存任何现有的 iptables 链。备份当前的 /etc/sysconfig/iptables 文件。
- 11. 使用 iptables -F 命令刷新当前防火墙规则。
- 12. 使用 iptables -A INPUT ! -s 192.168.122.150 -p tcp --dport 23 -j DROP 命令阻止除 192.168.122.150 之外的所有 IP 地址的 Telnet 端口 23。
- 13. 使用 /etc/init.d/iptables restart 命令激活防火墙。
- 14. 尝试从 IP 地址为 192.168.122.150 的计算机访问 Telnet 服务器。会发生什么？再尝试从 LAN 上的另一台计算机访问。
- 15. 恢复任何之前的防火墙规则；从备份中恢复 /etc/sysconfig/iptables 的原始版本。使用 /etc/init.d/iptables restart 命令重新加载防火墙。
- 16. 奖励：对端口 22 上的 SSH 服务重复这些命令。

### 实验 5

要确认 TCP Wrappers 可用于帮助保护 SSH 服务，请运行以下命令：

```
# ldd /usr/sbin/sshd | grep libwrap
```

输出中包含对 libwrap.so.0 库的引用，确认了与 TCP Wrappers 库的库链接。一般来说，最安全的做法是通过在 /etc/hosts.deny 文件中包含以下条目来拒绝所有服务的访问：

```
ALL : ALL
```

然后您可以在 /etc/hosts.allow 文件中使用如下行设置对 SSH 服务的访问：

```
sshd : 192.168.122.50
```

虽然在大多数情况下，使用所记录 IP 地址的完全限定域名（server1.example.com）也应该有效，但使用 IP 地址通常是合适的。通过 IP 地址进行的限制不依赖于对 DNS 服务器的连接。

当然，这不是限制 SSH 访问到一台系统的唯一方法。可以在 /etc/hosts.deny 文件中使用如下指令实现：

```
sshd : ALL EXCEPT 192.168.122.50
```

也可以使用 iptables 命令式防火墙等其他安全选项来设置此项。

### 实验 6

在此实验可以工作之前，您需要激活一个 SELinux 布尔值 ftp_home_dir。它在 SELinux 管理工具中列为“允许 ftp 在用户主目录中读写文件”。虽然此布尔设置在第 11 章中有所介绍，但 SELinux 的基本管理，包括布尔设置的激活，是第 4 章中介绍的 RHCSA 技能。因此，在确定了关键布尔值后，您应该能够按所述设置 vsFTP。

本实验的描述应引导您找到 /etc/pam.d/vsftpd 配置文件。该文件中的模型命令行是

```
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers
onerr=succeed
```

它指向 /etc/vsftpd/ftpusers 文件，即“拒绝”访问的用户列表。由于实验中的条件表明您需要一个（一个）允许访问的用户列表，因此在此文件中添加类似类型的第二行是合适的。为了验证此实验，我添加了以下行：

```
auth required pam_listfile.so item=user sense=allow file=/etc/vsftpd/testusers
onerr=succeed
```

它允许 /etc/vsftpd/testusers 文件中列出的所有用户。onerr=succeed 指令意味着如果该行其他地方出现错误，vsFTP 服务器仍然可以工作。例如，如果 /etc/vsftpd 目录中没有 testusers 文件，则该行中的指令是宽容的，允许 auth 模块类型的条件成功。

作为一个实验，请在布尔值 ftp_home_dir 变量设置和未设置的情况下尝试此实验。这应该能展示 SELinux 的强大功能，并作为第 11 章的适当预览。
