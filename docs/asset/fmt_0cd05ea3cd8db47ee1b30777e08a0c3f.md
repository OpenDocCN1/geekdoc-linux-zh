
- **决定是否进入交互式启动** —— 如果在启动时向引导加载程序传递了 `confirm` 选项，则所有服务器进程在启动前必须在系统控制台上进行确认。

- **杀死并启动运行级别脚本** —— 停止上一个的运行级别脚本，然后从当前级别启动 RHEL 脚本。

在 Fedora 和 RHEL 中，提供给网络用户和计算机大部分服务都是通过运行级别脚本启动的。

## 理解运行级别脚本

在启动时（或系统更改运行级别时）需要启动服务的软件软件包可以位于 `/etc/init.d` 目录。该脚本随后可以链接到相应的运行级别目录，并带有 `start` 或 `stop` 选项（用于启动或停止服务）。

表 12-5 ...

表 12-5 列出了在 `/etc/init.d` 软件包中找到许多典型的运行级别脚本并解释了它们的功能。根据你在系统中安装的 Fedora 或 RHEL 软件包，你可能拥有比这里看到的多多的运行级别脚本。（稍后，我将描述如何将这些文件链接到特定的运行级别目录。）

每个代表你想要启动服务的脚本都链接到每个运行级别目录中的一个文件。对于每个运行级别，以 `K` 开头的脚本会停止服务，而以 `S` 开头的脚本会启动服务。

文件名中 `K` 或 `S` 之前的两个数字提供了一种选择程序运行优先级顺序的机制。例如，`s12syslog` 的运行顺序在 `s85rpm` 之前，尽管你可以明显看出 85 小于 110。这是因为 ASCII 排序顺序对文件进行了排序，这简单意味着比较一个位置字符与另一个字符。因此，在运行级别 3 中，以字符 `S110` 开头的脚本会在 `S1network` 和 `S15nets` 之前执行。

`/etc/rcX.d` 目录（其中 `X` 被替换为运行级别数字）中的所有程序都是符号链接，通常指向 `/etc/init.d` 中的文件。这些目录包括：

- `/etc/rc0.d`: 运行级别 0 目录
- `/etc/rc1.d`: 运行级别 1 目录
- `/etc/rc2.d`: 运行级别 2 目录
- `/etc/rc3.d`: 运行级别 3 目录
- `/etc/rc4.d`: 运行级别 4 目录
- `/etc/rc5.d`: 运行级别 5 目录
- `/etc/rc6.d`: 运行级别 6

通过这种方式，`/etc/rc0.d/K0satd`、`/etc/rc1.d/K05atd`、`/etc/rc2.d/K05atd`、`/etc/rc3.d/S95atd`、`/etc/rc4.d/S95atd`、`/etc/rc5.d/S95atd` 以及 `/etc/rc6.d/D05atd` 都是指向 `/etc/init.d/at` 的符号链接。使用这种简单、一致的机制，你可以自定义启动时启动哪些程序。

表 12-5: `/etc/init.d` 中的运行级别脚本

# 第三部分：管理 Fedora RHEL

| 运行级别脚本 | 它的作用是什么？ |
|---|---|
| `smb` | 启动或停止 `smbd` 和 `nmbd` 守护进程，允许访问 Samba 文件和打印机服务。 |
| `snmpd` | 启动或停止 `snmpd`（简单网络管理协议）守护进程，允许其他查看机器配置信息。 |
| `spamassassin` | 启动或停止守护进程，自动检查电子邮件消息内容是否为垃圾邮件。 |
| `squid` | 启动或停止 `squid` 服务，为你网络上的客户端提供代理服务。 |
| `ssh` | 运行安全 shell 守护进程 (`sshd`)，它监听来自 `ssh` 客户端的远程登录或远程执行请求。 |
| `syslog` | 启动或停止 `klogd` 和 `syslog` 守护进程，分别处理来自内核和其他进程的日志记录事件。 |
| `vsftpd` | 运行非常安全的 FTP 服务器 (`vsftpd`)，为远程客户端提供 FTP 会话以进行下载和上传文件。 |
| `xfs` | 启动或停止 `xfs`，即 X Window 字体服务器。 |
| `xinetd` | 设置主机名、建立网络路由并控制 `xinetd`，`xinetd` 是监听进入机器的 TCP/IP 连接的网络服务守护进程。 |
| `yum` | 允许你使用 `yum` 工具运行软件的自动每日更新。 |
| `xfs` | 重新生成字体列表并启动和停止 X 字体服务器。 |

# 了解启动脚本

尽管 `rcXs`、`Ss` 和 `Ks` 看起来复杂，但每个启动脚本的形式都非常简单。由于它们是纯文本，你只需用文本编辑器打开它们即可查看其功能。在大多数情况下，运行级别脚本可以使用 `start` 选项或 `stop` 选项运行。例如，以下行是 `smbd` 脚本的内容，，它定义了使用不同的选项启动或停止 Samba 文件和打印机服务运行脚本时会发生什么：

```
#!/bin/sh
# chkconfig: - 91 35
# description: Starts and stops the Samba smbd daemon \
  used to provide SMB network services.
#
```

# 第 12 章：自动化系统任务 525

```
start() {
  KIND="SMB"
  echo -n "$Starting $KIND services: "
  daemon smbd $SMBDOPTIONS
  RETVAL=$?
  echo

  [$RETVAL -eq 0 -a $RETVAL2 -eq 0] && touch /var/lock/subsys/smb || \
  RETVAL=1
  return $RETVAL
}
```

```
stop() {
  KIND="SMB"
  echo -n "Shutting down $KIND services: "
  killproc smbd
  RETVAL=$?
  echo

  [$RETVAL -eq 0 -a $RETVAL2 -eq 0] && rm -f /var/lock/subsys/smb
  return $RETVAL
}
```

```
restart() {
  stop
  start
}
```

为了说明此脚本作用的本质，我略过了脚本开头和结尾的部分内容（这些检查了网络是否已运行并设置了某些值）。以下是 `smbd` 在带 `start` 或 `stop` 选项运行时所采取的操作：

- *start* — 当使用 `start` 选项运行脚本时，该脚本的这部分会启动 `smbd` 服务器。
- *stop* — 当带 `stop` 选项运行时，`/etc/init.d/smbd` 脚本会停止 `smbd` 服务器。

`restart` 选项先运行 `stop` 选项脚本，然后运行 `start` 选项。如果你想手动启动 `smbd` 服务，请输入以下命令（作为 root 用户）：

```
# service smb start
Starting SMB services:    [ OK ]
```

要停止服务，请输入以下命令：

# 第三部分：管理 Fedora RHEL

```
# service smb stop
Shutting down SMB services: [ OK ]
```

运行级别脚本与其他运行级别脚本的区别在于，它支持 `start` 和 `stop` 之外的几个选项。例如，此脚本具有某些选项（示例中未显示），允许你重新加载 `smb.conf` 配置文件（`reload`），并可以检查脚本状态（`status`）。

# 修改运行级别脚本行为

修改任何此类脚本的启动行为仅需用文本编辑器打开该文件即可。例如，`atd` 守护进程会对从 `at` 和 `batch` 命令提交的任务进行排队。通过 `batch` 提交的任务只有在系统负载不高于某个特定值时才会被执行，该值可以通过 `atd` 命令的命令行选项进行设置。

默认的 0.8 限制负载因子是基于这样一个假设：一台 CPU 利用率低于 80% 的单处理器机器可以处理批处理任务带来的额外负载。然而，如果你向机器中添加了另一个 CPU，0.8 只代表计算机处理能力的 40%。你可以安全地提高该限制，而不影响整体系统性能。

你可以将限制负载因子从 0.8 更改为 1.6，以适应增加的处理能力。要做到这一点，只需修改 `/etc/init.atd` 脚本（`start` 部分）中的以下行：

```
daemon /usr/sbin/atd
```

将其替换为此行，并使用 `-1` 参数指定新的最小系统负载值：

```
daemon /usr/sbin/atd -1 1.6
```

保存文件并退出编辑器后，你可以重启机器或仅运行以下三个命令中的任意一个开始使用新的批处理阈值：

```
# service atd reload
# service atd restart
# service atd status
```

> 注意：在更改任何配置之前，请务必对其进行备份。

`atd` 守护进程队列了从 `at` 和 `batch` 命令提交的任务。通过 `batch` 提交的任务只有在系统负载不高于特定值时才会被执行，该值可以通过 `atd` 命令的命令行选项进行设置。
