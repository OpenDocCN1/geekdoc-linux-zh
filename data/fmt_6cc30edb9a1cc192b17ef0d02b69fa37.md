
| httpd | Apache Web 服务器 |
| inet | 各种基础 TCP/IP 服务 |
| keytable | 加载键盘映射 |
| killall | 杀死运行的服务 |
| kudzu | 启动时检查硬件变化 |
| linuxconf | 允许 linuxconf 在启动和关机时执行特定操作的钩 |
| local | `/etc/rc.d/rc.local` 脚本，包含本地定义 |
| lpd | 提供远程打印机的 LP 服务 |
| named | DNS 服务器，提供主机名和 IP 地址查询 |
| netfs | 挂载网络文件系统 |
| network | 激活和禁用网络接口 |
| nfs | 网络文件系统 (NFS) 服务器，提供文件共享 |
| pcmia | 激活和禁用 PCMCIA 支持 |
| 脚本 | 描述 |
| :--- | :--- |
| portmap | 管理 RPC 连接，例如供 NFS 和 NIS 使用 |
| postgresql | 数据库管理系统 |
| random | 保存并恢复随机数生成器的状态，以产生更好的随机数 |
| reboot | 指向 halt 脚本的符号链接 |
| routed | RIP 客户端和服务器，自动更新路由 |
| rstatd | 提供性能指标的 RSTAT 服务器 |
| rd | RUSERS 服务器，帮助定位用户 |
| rwhod | RWHO 服务器，列出登录用户 |
| sendmail | 邮件服务器 |
| single | 将系统设置为单用户模式 |
| smb | Samba (SMB) 服务器，提供身份验证以及文件和打印共享 |
| sound | 保存并恢复混音器设置 |
| sshd | SSH 服务器，提供安全登录和远程命令执行 |
| syslog | 启动和停止系统日志 |
| xfs | X 窗口字体服务器 |

现在你已经熟悉了最常用的运行级别脚本，请完成练习 14.2 以学习更多。

## 练习 14.2

### 运行级别脚本

大多数 Linux 系统使用表 14.2 中未列出的额外脚本。要了解系统上安装的脚本，请检查 `/etc/rc.d/init.d` 目录并识别表 14.2 中未找到的任何脚本。检查这些脚本的内容以了解它们的作用。大多数脚本都包含解释其功能的注释。

大多数脚本接受控制其运行的参数。最常用的参数有：

- `start`，导致脚本启动关联的服务
- `stop`，导致脚本停止关联的服务
- `restart`，导致脚本重启关联的服务
- `reload`，导致脚本重新读取配置文件
- `status`，导致脚本报告关联服务的状态

`linuxconf` 程序使用这些脚本来启动和停止服务。你也可以手动调用它们来控制服务。例如，你可以通过执行命令关闭 Web 服务器（`httpd` 服务）：

```
/etc/rc.d/init.d/httpd stop
```

或者，你可以通过执行命令重启服务器：

```
/etc/rc.d/init/httpd restart
```

使用 `/etc/rc.d/init.d` 中的脚本而不是通过其他方式控制服务是非常重要的。例如，可以通过执行命令 `/usr/sbin/httpd` 来启动 Web 服务器。但是，如果你这样做，Linux 在你关闭服务器时将无法清理锁文件和进程标识文件。更糟糕的是，除非使用运行级别脚本，否则可能会无意中启动多个服务器实例。

### `/etc/rc.d/rc?.d` 中的符号链接

`/etc/rc.d/rc?.d` 中的符号链接名称如 `K05keytable` 和 `S40atd`。以 `K` 开头的链接在被 `/etc/rc.d/rc` 执行时会接收 `stop` 参数；以 `S` 开头的链接则接收 `start` 参数。通常情况下，与运行级别相关的目录会为每个已安装的服务包含一个 `K` 脚本或一个 `S` 脚本。

脚本名称中的两个数字数字被称为“优先级”，它指示了给定目录中脚本运行的顺序；例如，脚本 `K10ufs` 会在脚本 `K15gm` 之前运行。表 14.3 根据脚本执行时的运行级别总结了这些运行级别脚本。

### 表 14.3 按运行级别总结的常用运行级别脚本

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| K01linuxconf | | X | X | | | | |
| K05keytable | | X | X | | | | |
| K10ufs | | X | X | | | | |
| K15gpm | | X | X | | X | X | |
| K15httpd | | X | X | | X | X |
| K15sound | | X | X | X | | | X |
| K20nfs | | X | X | X | | | X |
| K20rstatd | | X | X | X | X | X | X |
| K20usersd | | X | X | X | X | X | X |
| K20rwhod | | X | X | X | X | X | X |
| K30sendmail | | X | X | | X | X | | |
| K35smb | | | | X | X | | |
| K45named | | X | X | X | | | X |
| K45sshd | | X | X | X | | | X |

### 表 14.3 按运行级别总结的常用运行级别脚本（续））

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| K50inet | | X | | | | X | |
| routed | | X | X | X | X | X | |
| K60atd | | X | X | X | | | X |
| K60crond | | X | X | | | | X |
| K61pd | | X | X | | | | X |
| K80random | | X | | | | | X |
| K85netfs | | X | X | | | | X |
| K89portmap | | X | X | X | | | X |
| K90killall | | X | | | | | X |
| K90mysql | | X | X | | | | X |
| K90network | | X | X | | | | X |
| K92apm | | X | X | X | X | X | |
| K96pcmcia | | X | | X | X | X | |
| K99syslog | | X | X | | | | X |
| S0halt | | X | | | | | |
| S000 | | X | | | | | |
| S00reboot | | | | | | | X |
| S05apmd | | | X | | | | |
| S10network | | | X | X | X | | |
| S11portmap | | | | X | X | | |
| S15netfs | | | | X | X | | |

### 表 14.3 按运行级别总结的常用运行级别脚本（续）

| Script | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| S20random | | X | | X | X | | |
| S30syslog | | | X | | | | |
| S40atd | | | | X | X | X | |
| S40crond | | | X | X | X | | |
| S45pcmcia | | | X | | | | |
| S50inet | | | | X | X | X | |
| S55named | | | | X | X | | |
| S55sshd | | | | X | X | X | |
| S601pd | | | X | X | X | | |
| S60nfs | | | | X | X | | |
| S75keytable | | | X | X | X | | |
| S85sound | | | X | X | X | | |
| S85gpm | | | X | | | | |
| S90mysql | | | | X | X | X | |
| S90xfs | | | X | | | | |
| S90xfs | | | | X | | | |
| S91linuxconf | | | X | X | X | | |
| S99local | | | X | | | | |
