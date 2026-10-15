
这是一个服务器（`tftpd`）接受命令行参数（`/tftpboot`，即 TFTP 目录的位置）的示例。这是通过将参数添加到 `server_args` 关键字来处理的。注意，此示例将对该服务的访问时间限制在上午 1 点到晚上 11 点，这可能是因为每天从晚上 11 点到上午 1 点有一个计划维护时段。

### 从 `/etc/rc.d` 启动网络服务

虽然大多数核心 Linux 网络服务是从 `inetd` 启动的，但越来越多的守护程序被配置为在系统启动时独立启动。这使应用程序开发人员能够更紧密地控制其服务的执行，并允许他们生成某些守护程序的额外实例，有时甚至在收到请求之前就进行。这对于高吞吐量和高开销的服务（如 `WWW`、`Sendmail`、`SSH` 等）特别有用。

然而，将所有的启动脚本维护在文件系统中的中心位置非常重要，Linux 使用 `/etc/rc.d` 目录作为此用途的默认位置。在此目录内，有一些以类似方式命名的子目录：

```bash
[ramon]$ cd /etc/rc.d
[ramon]$ ls -1d rc*.d
```

```
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc0.d
drwxr-xr-x   2 root     root       4096 Oct 21 13:42 rc1.d
drwxr-xr-x   2 root     root       4096 Oct 22 15:40 rc2.d
drwxr-xr-x   2 root     root       4096 Oct 22 15:40 rc3.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc4.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc5.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc6.d
drwxr-xr-x   2 root     root       4096 Oct 21 13:41 rcS.d
```

这些目录中的每一个都包含在系统进入特定运行级别（0–6 和 S）时要执行的脚本。表 4.1 展示了每个运行级别的含义。系统的 `init` 进程（总是第一个被执行的进程）调用 `/etc/inittab` 文件中找到的操作，进而，当系统进入每个运行级别时，调用 `/etc/rc.d` 中相应的文件。

#### 表 4.1 Linux 运行级别及其含义

| 运行级别 | 含义 |
| :--- | :--- |
| 0 | 停止系统（关机） |
| 1 | 无网络的多用户模式 |
| 2 | 有网络的多用户模式 |
| 3 | 有网络且带 `xdm`（X 显示管理器）的多用户模式 |
| 4 | 保留（Linux 未使用） |
| 5 | 保留（Linux 未使用） |
| 6 | 系统重启（重新启动） |
| S | 单用户模式 |

每个目录都包含启动脚本（文件名以 S 开头）和终止脚本（文件名以 K 开头），如列表 4.4 所示。

### 从 `/etc/rc.d` 启动网络服务

**列表 4.4 `/etc/rc.d/rc3.d` 目录的部分内容**

```
[ramon]$ cd rc3.d
[ramon]$ ls -l
total 0
lrwxrwxrwx 1 root root   8 Oct 21 13:45 K20rwhod -> ../rwhod
lrwxrwxrwx 1 root root  11 Oct 21 13:45 K20sendmail -> ../sendmail
lrwxrwxrwx 1 root root  13 Oct 21 13:45 K22wwdial.dod -> ../wwdial.dod
lrwxrwxrwx 1 root root  12 Oct 21 13:45 K23nfs-server -> ../nfs-server
lrwxrwxrwx 1 root root   9 Oct 21 13:45 K23pcfsd -> ../pcfsd
lrwxrwxrwx 1 root root   9 Oct 21 13:44 K24autoofs -> ../autoofs
lrwxrwxrwx 1 root root  11 Oct 21 13:45 K24ypclient -> ../ypclient
lrwxrwxrwx 1 root root   9 Oct 21 13:41 K30random -> ../random
lrwxrwxrwx 1 root root   9 Oct 21 13:41 K35routed -> ../routed
lrwxrwxrwx 1 root root   9 Oct 21 13:42 K35syslog -> ../syslog
lrwxrwxrwx 1 root root   6 Oct 21 13:41 K36nfs -> ../nfs
lrwxrwxrwx 1 root root   8 Oct 21 13:41 K38route -> ../route
lrwxrwxrwx 1 root root  11 Oct 21 13:45 K40dhclient -> ../dhclient
lrwxrwxrwx 1 root root  10 Oct 21 13:41 K40network -> ../network
lrwxrwxrwx 1 root root   8 Oct 21 13:41 K45dummy -> ../dummy
lrwxrwxrwx 1 root root  17 Oct 21 13:45 K45irda -> /sbin/init.d/irda
lrwxrwxrwx 1 root root  11 Oct 21 13:45 K51firewall -> ../firewall
lrwxrwxrwx 1 root root  10 Oct 21 13:41 K99kernel -> ../kernel
lrwxrwxrwx 1 root root   8 Oct 21 13:45 S20rwhod -> ../rwhod
lrwxrwxrwx 1 root root  11 Oct 21 13:45 S20sendmail -> ../sendmail
lrwxrwxrwx 1 root root   7 Oct 22 14:54 S20sshd -> ../sshd
lrwxrwxrwx 1 root root   7 Oct 21 13:41 S21cron -> ../cron
lrwxrwxrwx 1 root root   8 Oct 21 13:45 S21smfs -> ../smfs
lrwxrwxrwx 1 root root  13 Oct 21 13:45 S22wwdial.dod -> ../wwdial.dod
lrwxrwxrwx 1 root root   6 Oct 21 13:41 S30xdm -> ../xdm
lrwxrwxrwx 1 root root  11 Oct 21 13:45 S99firewall_final -> ../firewall
```

请注意，启动脚本和终止脚本实际上都是指向同一脚本的符号链接，该脚本位于 `/etc/rc.d` 目录中（在 SuSE 的情况下）或位于 `/etc/rc.d/init.d` 目录中（在 Red Hat 和其他 Linux 发行版的情况下）。当系统启动时，S 脚本以 `start` 作为命令行参数被调用。当系统关闭时，K 脚本取而代之，以 `stop` 作为命令行参数被调用。脚本首字母后的两个数字决定了脚本执行的顺序。例如，`S20a` 脚本在 `S21cron` 脚本之前执行。

虽然根据 `/etc/rc.d` 目录的大小判断，启动了大量守护进程，但实际上，大多数脚本会在启动服务之前检查特定配置是否存在。这意味着，除非你明确要求服务器提供特定服务（例如 `rwhod`），否则脚本不会启动该守护进程。如清单 4.5 所示的 `S20rwhod` 脚本首先检查 `/etc/rc.config` 文件，并且只有当它检测到环境变量 `$START_RWHOD` 被设置为 `yes` 时，才会启动 `rwhod` 守护进程。

#### 清单 4.5 `S20rwhod` 启动脚本
