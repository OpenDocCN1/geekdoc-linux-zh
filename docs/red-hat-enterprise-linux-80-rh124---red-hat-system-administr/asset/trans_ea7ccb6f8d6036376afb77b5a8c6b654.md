

# journalctl - 日志服务与事件

```
dm-event.socket loaded active listening Device-mapper daemon FIFOs
lvm2-llmpold.socket loaded active listening LVM poll daemon socket
...output omitted...
systemd-udev-control.socket loaded active running udev Control Socket
systemd-udev-kernel.socket loaded active running udev Kernel Socket
```

LOAD = 反映单元定义是否已正确加载。
ACTIVE = 高级单元激活状态，即 SUB 的泛化。
SUB = 低级单元激活状态，其值取决于单元类型。

列出了 12 个单元。
要显示所有已安装的文件，请使用 'systemctl list-unit-files'。

- 4. 探索 chronyd 服务的状态。该服务用于网络同步（NTP）。

- 4.1. 显示 chronyd 服务的状态。注意任何活跃守护进程的进程 ID（PID）。

```
[student@server ~]$ systemctl status chronyd
chronyd.service - NTP client/server
Loaded: loaded (/usr/lib/system/system/chronyd.service; enabled; vendor preset preset: enabled)
Active: active (running) since Wed 2019-02-06 12:46:57 IST; 7 min ago
Docs: man-chronyd(8)
-chronyd.conf(5)
Process: 684 ExStartPost=/usr/libexec/chrony-helper update-daemon
(code=exited,status=SUCCESS)
Process: 673 ExStart=/usr/sbin/chronyd $OPTIONS (code=exited,status=0)
```

```
Main PID: 680 (chronyd)
Tasks: 1 (limit: 11406)
Memory: 1.5M
Group: /system.slice/chronyd.service
L-680 /usr/sbin/chronyd
```

```
jequi.lt.example.com.systemd[1]: Starting NTP client/server...
...output omitted...
jequi.lt.example.com.systemd[1]: Started NTP client/server.
servera.lab.example.com chronyd[680]: Source 172.25.254.254 offline
servera.lab.example.com chronyd[680]: Source 172.25.254.254 online
servera.lab.example.com chronyd[680]: Selected source 172.25.254.254
```

- 4.2. 确认列出的守护进程正在运行。在上面的命令中，与 chronyd 服务关联的进程 ID 是 680。该进程 ID 在你的系统上可能不同。

```
[student@server ~]$ ps -p 680
PID TTY TIME CMD
680 ? 00:00:00 chronyd
```

- 5. 探索 sshd 服务的状态。该服务用于系统之间安全的加密通信。

- 5.1. 确定 sshd 服务是否已在系统启动时启用。

```
[servera ~$]$ systemctl is-enabled sshd
enabled
```

- 5.2. 在不显示所有状态信息的情况下，确定 sshd 服务是否处于活跃。

```
[servera ~$]$ systemctl is-active sshd
active
```

- 5.3. 显示 sshd 服务的状态。

```
[servera ~$]$ systemctl status sshd
* sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
   Active: active (running since 2019-02-06 12:46:58 IST; 4h 21min ago)
   Docs: sshd(8)
      sshd.config(5)
   Main PID: 720 (sshd)
   Tasks: 1 (limit: 11406)
   Memory: 5.8M
   CGroup: /system.slice/sshd.service
      /usr/sbin/sshd -D -ciphers=aes256-gcm@openssh.com,sha256-poly1305@openssh.com,aes256-ctr,aes256-bc,aes128-gcm@openssh.com,aes128-ctr,aes128-bc -hmac=hmac-sha256-etm@openssh.com,hmac-sha256-sha
      gequi.init.example.com systemd[1]: Starting OpenSSH server daemon...
      server.la.example.com sshd[720]: Server listening on 0.0.0.0:port 22.
      server.la.example.com systemd[1]: Starting OpenSSH server daemon.
      server.la.example.com sshd[720]: Server listening on ::port 22.
      ...output_merged...
      server.la.example.com sshd[1380]: pam_unix(sshd:session): session opened for
      user by (uid=0)
```

按 Q 退出命令。

- 6. 列出所有单元服务中已启用或禁用的服务。

```
[servera ~$]$ systemctl list-unit-files --type=service
```

| UNIT FILE | STATE |
| :--- | :--- |
| arp-ethers.service | disabled |
| atd.service | enabled |
| audit.service | enabled |
| auth-rcpgss-module.service | static |
| autovt.service | enabled |
| blk-availability.service | disabled |

```
chrony-dnssrv.service    static
chrony-wait.service     disabled
chronyd.service         enabled
...output omitted...
```

按 **Q** 退出命令。

- 7. 退出 servera。

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation]$
```

# 完成

在工作站（workstation）上，运行 **lab services-identify finish** 脚本以完成本次练习。

```
[student@workstation ~]$ lab services-identify finish
```

引导性练习结束。

# 控制系统服务

# 目标

完成本节后，你应该能够控制系统守护进程和网络服务。

# 启动和停止服务

某些服务需要其他服务先运行，从而对其他服务产生依赖关系。服务并非在启动时加载，而是根据需要启动。在两种情况下，systemd systemctl 会根据依赖关系或需要启动 CUPS。例如，如果 CUPS 服务未运行且向目录放置了文件，系统将启动它。

要启动服务，首先验证其未在运行。使用 systemd systemctl。以下示例显示如何启动：

```
[root@host ~]$ systemctl start
```

要完全停止系统上的服务，禁用单元。禁用服务禁用依赖。

要停止运行的服务，使用 stop 命令。以下示例显示如何停止：

```
[root@host ~]$ systemctl stop
Warning: Stopping cups,但可以通过以下方式激活：
cups.path
cups.socket
```

# 重启和加载服务

某些服务无需重启即可加载配置。此过程被称为加载。加载服务不会更改进程 ID。要重启服务，使用 restart 命令。以下示例显示如何重启：

```
[root@host ~]$ systemctl restart
```

# 控制服务

第七章 | 控制服务与依赖关系

如果不确定服务是否具有加载配置的功能，请在命令中使用 reload-restart 参数。如果加载功能可用，命令将加载配置；否则，命令将重启服务。

```
[root@host ~]$ systemctl reload-restart
```

# 列出单元依赖

systemctl list-dependencies UNIT 显示了启动服务单元的依赖层次映射。要查看反依赖（依赖于指定单元的单元），请在命令中使用 --reverse 选项。

```
[root@host ~]$ systemctl list-dependencies sshd.service
sshd.service
• --system.slice
• --ssh-keygen.target
• --ssh-keygen@ecdsa.service
• --ssh-keygen@ed25519.service
• --ssh-keygen@rsa.service
• --sysinit.target
• --output omitted..

# 屏蔽与取消屏蔽

有时系统可能安装了多个相互冲突的服务。例如，有多种方法管理邮件服务器（例如 postfix 和 sendmail）。屏蔽服务可以防止管理员意外启动与其他冲突的服务。屏蔽会在配置目录中创建指向 /dev/null 文件的链接，从而防止服务启动。

```
[root@host ~]$ systemctl mask sendmail.service
Created symlink /etc/systemd/sendmail.service -> /dev/null.
```

