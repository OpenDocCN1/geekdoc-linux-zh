

链接到适当的运行级别目录，并被启动或停止（以启动或停止服务）。

表 12-5 列出了在 `/etc/init.d` 目录中常见的许多典型运行级别脚本，并解释了它们的功能。根据您在系统上安装的 Red Hat Linux 软件包不同，您可能拥有比此处列出的多数十个运行级别脚本。（稍后，我将描述这些文件是如何链接到特定运行级别目录的。）

### 表 12-5：/etc/init.d 中包含的运行级别脚本

| 运行级别脚本 | 功能描述 |
| :--- | :--- |
| apmd | 控制高级电源管理（APM）守护程序，该程序监控电池状态，并且可以安全地挂起或关闭支持该功能的全部或部分机器。 |
| atd | 启动或停止 at 守护程序，以接收、排队并运行通过 at 或 batch 命令提交的任务。（anacron 运行级别脚本会运行那些因计算机关机而未运行的 at 和 batch 任务。） |
| autofs | 启动和停止自动挂载守护程序，用于自动挂载文件系统（例如，插入 CD 时自动挂载）。 |
| crond | 启动或停止 cron 守护程序，用于定期运行例行命令。 |
| dhcpd | 启动或停止 dhcpd 守护程序，该程序自动为局域网（LAN）中的计算机分配 IP 地址。 |
| gpm | 控制 gpm 守护程序，允许鼠标与控制台和基于文本的应用程序进行交互。 |
| halt | 终止所有进程，写入记账记录，移除交换空间，卸载所有文件系统，并根据调用方式关闭或重启机器。 |
| httpd | 启动 httpd 守护程序，允许计算机充当 HTTP 服务器（即提供 Web 页面服务）。 |
| iptables | 启动 iptables 防火墙守护程序，管理为计算机设置的任何 iptables 风格的防火墙规则。 |
| keytable | 加载预定义的键盘映射。 |
| killall | 在关闭或重启之前，关闭可能仍在运行的任何子系统。 |
| kudzu | 在启动时检测和配置新硬件。 |
| lpd | 控制处理打印请求队列的 lpd 行打印机守护程序。 |
| netfs | 挂载或卸载网络（NFS、SMB 和 NCP）文件系统。 |
| network | 启动或停止所有配置的网络接口，并初始化 TCP/IP 和 IPX 协议。 |
| nfs | 启动或停止 NFS 相关的守护程序（rpc.nfsd、rpc.mountd、rpc.statd 和 rpc.rquotad），并导出共享文件系统。 |
| pcmcia | 加载或卸载模块、驱动程序和程序（包括 cardmgr 守护程序），以支持笔记本电脑中的 PCMCIA 卡（以太网适配器、调制解调器、存储卡等）。 |
| portmap | 启动或停止 portmap 守护程序，该程序管理使用远程过程调用（RPC）机制的程序和协议。 |
| random | 加载或保存机器随机数生成器的随机种子当前状态，以确保更随机的随机性。 |
| reconfig | 在特定的启动情况（如从 LILO 启动提示符发出的重新配置请求）下运行 anaconda 重新配置屏幕。 |
| routed | 启动或停止 routed 守护程序，通过路由信息协议（RIP）控制动态路由表更新。 |
| rstatd | 启动或停止 rpc.rstatd 守护程序，允许网络上的其他用户探测机器的性能统计信息。 |
| rusersed | 启动或停止 rpc.rusersed 守护程序，允许网络上的其他用户定位机器上的用户。 |
| rwhod | 启动或停止 rwhod 守护程序，允许网络上的其他用户获取所有当前登录用户的列表。 |
| sendmail | 控制 sendmail 守护程序，处理传入和传出的 SMTP（简单邮件传输协议）邮件消息。 |
| single | 终止所有正在运行的进程并进入运行级别 1（单用户模式）。 |
| smb | 启动或停止 smbd 和 nmbd 守护程序，允许访问 Samba 文件和打印服务。 |
| snmpd | 启动或停止 snmpd（简单网络管理协议）守护程序，允许其他用户查看机器配置信息。 |
| squid | 启动或停止 squid 服务，允许网络客户端使用代理服务。 |
| syslog | 启动或停止 klogd 和 syslogd 守护程序，分别处理来自内核和其他进程的日志事件。 |
| xfs | 启动或停止 xfs，即 X Window 字体服务器守护程序。 |
| xinetd | 设置机器的主机名，建立网络路由，并控制 xinetd（网络服务守护程序），它监听传入机器的 TCP/IP 连接。 |
| ypbind | 绑定到 NIS（网络信息服务器）主服务器（如果配置了 NIS），并启动或停止 ypbind 进程，该进程与主服务器通信。

每个代表您要启动或停止的服务的脚本都会链接到每个运行级别目录中的一个文件。对于每个运行级别，以 K 开头的脚本停止服务，而以 S 开头的脚本启动服务。

文件名中 K 或 S 后面的两位数字提供了一种选择程序运行优先级的机制。例如，S30syslog 在 S40crond 之前运行。然而，虽然人类可以很容易地看出 85 小于 110，但文件 S110my_daemon 却在 S85gpm 之前运行。这是因为“文件按 ASCII 排序顺序排列”，这简单地意味着逐个字符进行比较。因此，以 S110 开头的脚本在运行级别 3 中执行于 S10network 和 S15netfs 之间。

`/etc/rcX.d` 目录（其中 X 被替换为运行级别数字）中的所有程序都是符号链接，通常指向 `/etc/init.d` 中的文件。`/etc/rcX.d` 目录包括以下内容：

- `/etc/rc0.d`：运行级别 0 目录
- `/etc/rc1.d`：运行级别 1 目录
- `/etc/rc2.d`：运行级别 2 目录
- `/etc/rc3.d`：运行级别 3 目录
- `/etc/rc4.d`：运行级别 4 目录
- `/etc/rc5.d`：运行级别 5 目录
- `/etc/rc6.d`：运行级别 6 目录

以此方式，`/etc/rc0.d/K05atd`、`/etc/rc1.d/K05atd`、`/etc/rc2.d/K05atd`、`/etc/rc3.d/S95atd`、`/etc/rc4.d/S95atd`、`/etc/rc5.d/S95atd` 和 `/etc/rc6.d/K05atd` 都是指向 `/etc/init.d/atd` 的符号链接。使用这种简单且一致的机制，您可以自定义在启动时启动哪些程序。

### 理解启动脚本的作用

尽管有各种复杂的 rcXs、Ss 和 Ks，每个启动脚本的形式其实非常简单。因为它们都是纯文本，所以你可以用文本编辑器打开其中一个查看其内容。通常情况下，运行级别脚本可以以 start 选项、stop 选项以及可能的 restart 选项运行。例如，以下行是 smb 脚本内容的一部分，定义了当该脚本以不同选项运行时启动或停止 Samba 文件和打印服务时发生的情况：

```bash
#!/bin/sh
#
# chkconfig: - 91 35
# Description: Starts and stops the Samba smbd and nmbd daemons \
#             used to provide SMB network services.
#
.
.

start() {
    KIND="SMB"
    echo -n "Starting $KIND services: "
    daemon smbd $SMBDOPTIONS
    RETVAL=$?
    echo
    KIND="NMB"
    echo -n "Starting $KIND services: "
    daemon nmbd $NMBDOPTIONS
    RETVAL2=$?
    echo
    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && touch /var/lock/subsys/smb || \
    RETVAL=1
    return $RETVAL
}

stop() {
    KIND="SMB"
    echo -n "Shutting down $KIND services: "
    killproc smbd
    RETVAL=$?
    echo
    KIND="NMB"
    echo -n "Shutting down $KIND services: "
    killproc nmbd
    RETVAL2=$?
    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && rm -f /var/lock/subsys/smb
    echo ""
    return $RETVAL
}

restart() {
    stop
    start
}

case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        restart
        ;;
    *)
        echo "$Usage: $0 (start|stop|restart|status|condrestart)"
        exit 1
esac
exit $?
```

为了说明此脚本本质上做了什么，我跳过了脚本的开头部分（其中它检查网络是否已启动并设置了一些值）。以下是 **smb** 脚本以 **start** 或 **stop** 选项运行时所执行的操作：

- **start** — 当脚本以 **start** 选项运行时，脚本的这一部分会启动 **smbd** 和 **nmbd** 服务器。
- **stop** — 当以 **stop** 选项运行时，`/etc/init.d/smb` 脚本会停止 **smbd** 和 **nmbd** 服务器。

**restart** 选项先运行脚本的 **stop** 部分，然后运行 **start** 部分。如果你想自己启动 **smb** 服务，可以输入以下命令（作为 **root** 用户）：

```bash
# /etc/init.d/smb start
Starting SMB services:				[   OK   ]
```

