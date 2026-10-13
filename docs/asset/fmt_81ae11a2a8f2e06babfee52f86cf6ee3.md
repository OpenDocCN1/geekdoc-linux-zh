
### 实验 4

设置任何 xinetd 服务（如 Telnet）都需要多个步骤。您需要修改 xinetd Telnet 配置文件。以下步骤演示了三种不同的方法来限制对 IP 地址为 `192.168.122.150` 的所记录系统的访问。三种方法中的任何一种都是可以接受的。这些方法通过三种方式保护 Telnet：在 `/etc/xinetd.d/telnet` 配置文件中，通过 TCP Wrappers，或通过适当的防火墙命令。在“现实世界”场景中，您可能会在分层安全策略中使用这三种方法。您在 `server1.example.com` 系统上执行此实验。

- 1. 确保已安装 `telnet-server` RPM。备份当前版本的 `/etc/xinetd.d/telnet` 配置文件。
- 2. 激活 Telnet。使用 `chkconfig telnet on` 命令修改 `/etc/xinetd.d/telnet` 配置脚本。
- 3. 编辑 `/etc/xinetd.d/telnet` 配置文件。添加 `only_from = 192.168.122.150` 行，表示 `tester1.example.com` 系统。
- 4. 保存配置文件并使用 `service xinetd reload` 命令重新加载 xinetd 服务脚本。尝试从本地计算机访问 Telnet。会发生什么？
- 5. 尝试从 IP 地址为 `192.168.122.150` 的计算机访问 Telnet。会发生什么？再尝试从 LAN 上的另一台系统访问。
- 6. 恢复之前的 `/etc/xinetd.d/telnet` 配置文件。不要忘记使用 `service xinetd reload` 命令重新加载 xinetd 服务脚本。
- 7. 备份当前版本的 `/etc/hosts.deny` 文件。在文本编辑器中打开该文件。添加 `telnetd : ALL EXCEPT 192.168.122.150` 行。
- 8. 尝试从 IP 地址为 `192.168.122.50` 的计算机访问 Telnet。会发生什么？再尝试从 LAN 上的另一台计算机访问。
- 9. 恢复之前的 `/etc/hosts.deny` 文件。
- 10. 保存任何现有的 iptables 链。备份当前的 `/etc/sysconfig/iptables` 文件。
- 11. 使用 `iptables -F` 命令刷新当前防火墙规则。
- 12. 使用 `iptables -A INPUT ! -s 192.168.122.150 -p tcp --dport 23 -j DROP` 命令阻止除 `192.168.122.150` 之外的所有 IP 地址的 Telnet 端口 23。
- 13. 使用 `/etc/init.d/iptables restart` 命令激活防火墙。
- 14. 尝试从 IP 地址为 `192.168.122.150` 的计算机访问 Telnet 服务器。会发生什么？再尝试从 LAN 上的另一台计算机访问。
- 15. 恢复任何之前的防火墙规则；从备份中恢复 `/etc/sysconfig/iptables` 的原始版本。使用 `/etc/init.d/iptables restart` 命令重新加载防火墙。
- 16. 奖励：对端口 22 上的 SSH 服务重复这些命令。

### 实验 5

要确认 TCP Wrappers 可用于帮助保护 SSH 服务，请运行以下命令：

```
# ldd /usr/sbin/sshd | grep libwrap
```

输出中包含对 `libwrap.so.0` 库的引用，确认了与 TCP Wrappers 库的库链接。一般来说，最安全的做法是通过在 `/etc/hosts.deny` 文件中包含以下条目来拒绝所有服务的访问：

```
ALL : ALL
```

然后您可以在 `/etc/hosts.allow` 文件中使用如下行设置对 SSH 服务的访问：

```
sshd : 192.168.122.50
```

虽然在大多数情况下，使用所记录 IP 地址的完全限定域名（`server1.example.com`）也应该有效，但使用 IP 地址通常是合适的。通过 IP 地址进行的限制不依赖于对 DNS 服务器的连接。

当然，这不是限制 SSH 访问到一台系统的唯一方法。可以在 `/etc/hosts.deny` 文件中使用如下指令实现：

```
sshd : ALL EXCEPT 192.168.122.50
```

也可以使用 `iptables` 命令式防火墙等其他安全选项来设置此项。

### 实验 6

在此实验可以工作之前，您需要激活一个 SELinux 布尔值 `ftp_home_dir`。它在 SELinux 管理工具中列为“允许 ftp 在用户主目录中读写文件”。虽然此布尔设置在第 11 章中有所介绍，但 SELinux 的基本管理，包括布尔设置的激活，是第 4 章中介绍的 RHCSA 技能。因此，在确定了关键布尔值后，您应该能够按所述设置 vsFTP。

本实验的描述应引导您找到 `/etc/pam.d/vsftpd` 配置文件。该文件中的模型命令行是

```
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers

onerr=succeed
```

它指向 `/etc/vsftpd/ftpusers` 文件，即“拒绝”访问的用户列表。由于实验中的条件表明您需要一个（一个）允许访问的用户列表，因此在此文件中添加类似类型的第二行是合适的。为了验证此实验，我添加了以下行：

```
auth required pam_listfile.so item=user sense=allow file=/etc/vsftpd/testusers

onerr=succeed
```
