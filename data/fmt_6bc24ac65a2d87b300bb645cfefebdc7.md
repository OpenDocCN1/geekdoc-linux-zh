
### 57. 在配置 Linux 服务器以在主要 Windows 环境中共享文件和打印机时，您希望客户端无需访问且无许可成本。为了完成此目的，您将运行哪个服务/守护程序？（选择两项。）

- A. `nfsd`
- B. `smbd`
- C. `tarantella`
- D. `wu-ftpd`
- E. `nmbd`

### 58. 你需要在局域网环境中跨网络进行安装。你赶时间，文件存在于服务器 `/shared` 目录中，并且你希望尽可能少地对服务器进行修改。你应该编辑哪个文件来实现这一目标？

- A. `/etc/dfs/dfstab`
- B. `/etc/exports`
- C. `/etc/exportfs`
- D. `/etc/nfs/exports`
- E. `/proc/sys/nfs/shares`

### 59. 在配置新的 Apache 服务器时，你需要确定内容在系统上的存放位置。你阅读了 `httpd.conf` 文件，并发现一个指令指定了默认放置 HTML 内容的位置。以下哪项是该指令的名称？

- A. `RootDoc`
- B. `DocRoot`
- C. `ContentRoot`
- D. `DocumentRoot`
- E. `DocPath`

### 60. 你在使用电子商务用途的其中一个 Apache 服务器上进行了几处重要更改，需要重新读取配置文件。你可以使用哪条命令在不终止当前会话的情况下完成此操作？

- A. `/etc/rc.d/init.d/httpd restart`
- B. `service httpd restart`
- C. `apachectl graceful`
- D. `killall -1 httpd`

### 61. 使用哪条命令可以让你的 `sendmail` 守护进程重新读取用户名到电子邮件地址的映射列表，而无需重启 `sendmail` 守护进程？请在下方空白处填写：

`sendmail -q` 

### 62. 用户抱怨他们的电子邮件未能投递到其他域，但内部电子邮件运行正常。哪条命令可以显示未投递远程邮件的队列目录状态？请在空白处仅填写命令名称：

`mailq`

### 63. 包含用户电子邮件的目录的完整路径是什么？请在空白处填写完整路径和位置名称：

`/var/spool/mail`

### 64. 从提供商租用了一个 C 类 IP 段后，你决定需要建立六个网络，并且每个网络上的主机数量尽可能多。以下哪一项代表你应该选择的子网掩码？

- A. `255.255.255.128`
- B. `255.255.255.224`
- C. `255.255.255.0`
- D. `255.255.255.240`
- E. `255.255.255.248`

### 65. 在配置好一组新的 Samba 配置参数后，你用 `cron` 安排了重启 `smbd` 和 `nmbd` 守护进程，然后回家过周末。在 `cron` 作业本应运行时左右，你收到呼叫，称文件和打印机共享服务不可用。在离开之前，你应该使用哪条命令来检查你的 `smb.conf` 文件？请在下方空白处仅填写命令名称：

`testparm`

### 66. 你需要从一个远程主机向另一个主机传输一些敏感文件。你希望通过一条命令完成此操作，并将目录及所有文件传输到目标主机。请在空白处仅填写实现此目的所需命令名称及必要选项：

`rsync -av`

### 67. 用于为 Samba 服务器设置兼容 Windows 名称的参数名称是什么？请在空白处填写确切字符，为你的主机设置名称为 `boomer`：

`netbios name = boomer`

### 68. 你被要求为特定用户提供 Telnet 服务。在你的系统上，你刚刚执行了以下命令：

`chkconfig telnet on`

对哪个文件进行了什么更改？（选择最佳答案。）

- A. 在 `runlevel` 目录中创建了指向 `telnet` 的链接。
- B. 添加了一行 `telnet:on:/etc/services`。
- C. 在 `rc.sysinit` 脚本中添加了一行。
- D. `/etc/xinetd.d/telnet` 中的一行现在显示为 `disable = no`。

### 69. 你遇到一个文件，其内容包含以下条目：

```
zone "" in {
    type hint;
    file "root.hint";
};
```

包含这种语法文件的完整路径和文件名是什么？

- A. `/etc/named.boot`
- B. `/etc/named.dns`
- C. `/etc/named.conf`
- D. `/etc/named.db`

### 70. 你刚刚接到了来自 ISP 的电话，他们警告你，如果你不禁用所有垃圾邮件中继，你的租用线路将被关闭。如果你使用的是 `Sendmail`，应在哪个文件中做出此更改？

- A. `/etc/aliases`
- B. `/etc/sendmail.cf`
- C. `/etc/sendmail.conf`
- D. `~/forward`

### 71. 在尝试挂载远程服务器的 NFS 共享失败后，你想调查系统是否启用了正确的服务和端口。请在空白处仅填写名称和选项以实现此目的：

`netstat -an | grep nfs`

### 72. 在找到一个设置了特殊位 4（SUID）的受 root 限制的命令后，你开始寻找系统中所有设置了任何特殊位并在控制台上显示出来的文件。请在空白处填写确切的命令、选项和参数以实现此目的：

`find / -perm -4000`

### 73. 你怀疑本地工作站上的防火墙软件配置错误，因为它刚刚允许本应被拒绝的数据包通过。请在下方空白处填写确切的命令，该命令显示默认 iptables 表的规则集：

`iptables -L`

### 74. 在生病的旧服务器上加班工作时，你发现一名普通朝九晚五的用户已登录并正忙于列出你 Linux 服务器上的文件。你不想永久删除该用户或影响她的密码，但你想让她再次登录前联系你。

在你杀死用户的 shell 进程之前，你可以做什么来实现这一点？

- A. 运行 `passwd -l`。
- B. 运行 `usermod -L`。
- C. 在 `/etc/passwd` 的密码字段中放入 `*`。
- D. 运行 `touch /etc/nologin`。
- E. 运行 `passwd -d`。

### 75. 在阅读了一本杂志文章后，你决定在所有系统上禁用 Telnet。检查后，你发现 Telnet 在大多数 Linux 系统上默认是 `disabled`。请在空白处填写正确的单词来描述这种情况：

### 76. 每天早上，你运行一个报告，显示标准 Linux 系统上最新的用户认证活动。输出类似于以下内容：

```
root pts/2 192.168.1.103 Thu Jun 17 14:39 still logged in
root pts/1 192.168.1.103 Thu Jun 17 13:28 - 14:39 (01:10)
root pts/1 0     Thu Jun 17 13:27 - 13:27 (00:00)
root pts/1 192.168.1.103 Thu Jun 15 16:49 - 17:07 (00:18)
root pts/1 192.168.1.103 Tue Jun 15 16:12 - 16:49 (00:37)
```

你运行以显示此输出的命令读取的是哪个日志文件？

- A. `/var/log/boot.log`
- B. `/var/log/secure`
- C. `/var/log/wtmp`
- D. `/var/log/lastlog`

### 77. 要通过 SSH 登录远程服务器，该服务器上 `/etc/ssh/id_dsa.pub` 文件的权限至少应该是多少？

- A. `640`
- B. `644`
- C. `440`
- D. `400`
