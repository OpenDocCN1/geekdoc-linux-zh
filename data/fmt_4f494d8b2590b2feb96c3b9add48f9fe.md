
## 运行级别服务脚本

| `atd` | 启动或停止 at 守护进程，以接收、队列化并运行通过 `at` 或 `batch` 命令提交的作业脚本。（过时的运行级别脚本会运行那些因电脑关机而未运行的 at 和 batch 任务。） |

| `autofs` | 启动和停止自动挂载守护进程，用于自动挂载文件系统（例如，插入 CD 时可以自动挂载）。 |

| `crond` | 启动或停止 cron 守护进程，以定期运行例行命令。 |

| `gpm` | 控制 gpm 守护进程，允许鼠标与控制台和基于文本的应用程序交互。 |

| `halt` | 终止所有进程，写入统计记录，移除交换空间、所有文件系统，并关闭或重启机器（取决于如何调用该命令）。 |

| `httpd` | 启动 http 守护进程，允许你的计算机充当 HTTP 服务器（即提供 Web 页面）。 |

| `keytable` | 加载预定义的键盘映射。 |

| `killall` | 在关闭或重启之前关闭任何仍在运行的子系统。 |

| `kudzu` | 在启动时检测并配置硬件。 |

| `linuxconf` | 加载任何自定义的 linux 策略或模块，以及一些默认模块（配合 `linuxconf` 配置工具使用）。 |

| `lpd` | 控制 lpd 打印机守护进程，处理打印请求的暂存。 |

| `netfs` | 挂载或卸载网络（NFS、SMB 和 NCP）文件系统。 |

| `network` | 启动或停止所有配置的网络接口，并初始化 TCP/IP 和 IPX 协议。 |

| `nfs` | 启动或停止 NFS 相关的守护进程（`rpc.nfsd`, `rpc.mountd`, `rpc.statd` 和 `rcp.quotad`）并导出共享文件系统。 |

| `pcmcia` | 加载或卸载模块、驱动程序和程序（包括 cardmgr 守护进程），以支持笔记本电脑中的 PCIA 卡（以太网适配器、调制解调器、内存卡等）。 |

| `portmap` | 启动或停止 portmap 守护进程，管理利用远程过程调用（RPC）机制的程序和协议。 |

| `random` | 加载或保存随机生成器种子的当前状态以确保更高的随机性。 |

| `reconfig` | 在某些启动情况下（例如来自 LILO 启动提示符的重配置请求）运行 anaconda 重配置屏幕。 |

| `routed` | 启动或停止 routed 守护进程，通过路由信息协议（RIP）控制动态路由更新。 |

| `rstatd` | 启动或停止 `rpc.rstatd` 守护进程，允许网络上的其他机器探测其性能统计数据。 |

| `rusersd` | 启动或停止 `rpc.rusersd` 守护进程，允许网络上的其他人定位机器上的用户。 |

| `rwhod` | 启动或停止 rwhod 守护进程，允许网络上的其他人获取所有登录用户的列表。 |

| `sendmail` | 控制 sendmail 守护进程，处理入站和出站 SMTP（简单邮件传输协议）邮件。 |

| `single` | 终止所有正在运行的进程并进入级别 1（单用户模式）。 |

| `snmpd` | 启动或停止 snmpd（简单网络管理协议）守护进程，允许其他人查看机器配置信息。 |

| `syslog` | 启动或停止 klog 和 syslog 守护进程，分别处理来自内核和其他进程的日志事件。 |

| `xfs` | 启动或停止 xfs，即 X Window 服务器守护进程。 |

| `xinetd` | 设置主机名，建立网络路由，并控制 xinetd（网络服务守护进程），该守护进程监听指向机器的 TCP/IP 连接。 |

| `ybind` | 绑定到 NIS（网络信息服务）主服务器（如果配置了 NIS），并启动或停止与主服务器通信的 ybind 进程。 |

每个代表你想要启动或停止的服务的脚本都链接到每个运行级别目录中的一个文件上。对于每个级别，以 `K` 开头的脚本会停止服务，而以 `S` 开头的脚本会启动服务。

更多额外内容请访问 `www.unitded.com`

文件名中 `K` 或 `S` 之后的两个数字提供了一种选择程序运行优先级的机制。例如，`S30syslog` 在 `S40cron` 之前运行。然而，人类可以很容易看出 85 小于 110，但文件 `S110_daemon` 会在 `S85bpm` 之前运行。这是因为“ASCII 排序顺序对文件进行排序，这意味着只需比较一个位置字符与另一个字符”。因此，在运行级别 3 中，以字符 `S110` 开头的脚本会在 `S15netfs` 之前执行。

`/etc/rc.d` 目录下的所有程序（X 被替换为运行级别数字）都是符号链接，通常指向 `/etc/init.d` 中的文件。`/etc/rc.d` 目录包含：

- `/etc/rc0.d`: 运行级别 0 目录
- `/etc/rc1.d`: 运行级别 1 目录
- `/etc/rc2.d`: 运行级别 2 目录
- `/etc/rc3.d`: 运行级别 3 目录
- `/etc/rc4.d`: 运行级别 4 目录
- `/etc/rc5.d`: 运行级别 5 目录
- `/etc/rc6.d`: 运行级别 6 目录

## 12 章 自动化系统任务

为了说明此脚本实际上做了什么，我跳过了脚本的开头（即检查网络是否启动并运行）并设置了一些值。这里是 `nfs` 在带启动或停止参数运行时执行的操作：

```bash
#!/bin/sh
# nfs 此脚本负责启动和停止。
# chkconfig: 60 description: NFS 是一种用于共享的流行协议。

case "$1" in
start)
  # 启动守护进程。
  action "Starting NFS services: " /usr/sbin/exportfs -r
  echo
  echo -n "Starting NFS quotas: "
  daemon rpc.quotad
  echo
  echo -n "Starting NFS mount: "
  daemon rpc.mountd $RPCMODTOP
  echo
  echo -n "Starting NFS daemon: "
  daemon rpc.nfsd $RPCSCOUNT
  echo
  touch /var/lock/subsys
  ;)
stop)
  # 停止守护进程。
  action "Shutting down NFS services: " /usr/sbin/exportfs -au
  echo
  echo -n "Shutting down NFS mount: "
  killproc rpc.mountd
  echo
  echo -n "Shutting down NFS daemon: "
  killproc rpc.nfsd
  echo
  echo -n "Shutting down NFS quotas: "
  killproc rpc.quotad
  echo
  rm -f /var/lock/subsys/nfs
  ;)
*)
# Usage: nfs {start|stop|status|reload}
  exit 1
esac

exit 0
```

- 首先，脚本运行 `exportfs -r` 命令，使我们通过 `/etc/exports` 文件设置的任何文件系统供他人共享。接下来它启动 `rpc.quotad` 守护进程，为远程文件系统的使用设置配额。然后，运行 `rpc.mountd` 守护进程以监听并处理对共享文件系统的请求。在此之后，运行 `rpc.nfsd` 守护进程以启动一组守护进程（默认为八个），用于管理远程挂载点。最后，创建一个锁文件以指示服务正在运行。
- 当使用 `stop` 选项运行运行时，`nfs` 会停止共享其导出的系统（`exportfs -au`）。然后，它会杀死守护进程（`rpc.mountd` 和 `nfsd`）。最后，它会停止配额守护进程（`rpc.quotad`）并移除锁文件。

如果你想启动 `nfs` 服务，可以输入以下命令（作为 root 用户）：

```
# /etc/init.d/nfs start
Starting NFS services [ok]
Starting NFS quotas [ok]
Starting NFS mountd [ok]
Starting NFS daemon [ok]
```

要停止服务，你可以输入以下命令：

```
# /etc/init.d/nfs stop
Starting NFS services [ok]
Starting NFS mountd [ok]
Starting NFS daemon [ok]
Starting NFS quotas [ok]
```

`nfs` 运行级别脚本与其他运行级别脚本不同之处在于，它支持除 `start` 和 `stop` 之外的多个选项。例如，你可以使用以下选项运行 `nfs`：`status`（查看守护进程正在运行）、`restart`（停止并重启 nfs 服务）、`reload`（从 `/etc/exports` 载入任何新文件系统）和 `probe`（探测 nfs 资源的状态）。

## 修改运行级别脚本行为
