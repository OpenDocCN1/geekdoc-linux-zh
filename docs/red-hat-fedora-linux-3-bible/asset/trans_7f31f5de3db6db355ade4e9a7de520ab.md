

... 系统中，你可能拥有比此处展示的多达数十个运行级别脚本。（稍后，我将描述这些文件如何链接到特定的运行级别目录中。）

### 表 12-5：/etc/init.d 中包含的运行级别脚本

| 运行级别脚本 | 它的作用是什么？ |
| :--- | :--- |
| apmd | 控制高级电源管理（Advanced Power Management）守护进程，该进程监视电池状态，并且可以安全地挂起或关闭支持此功能的全部或部分计算机。 |
| atd | 启动或停止 at 守护进程，以接收、排队并运行通过 `at` 或 `batch` 命令提交的任务。（anacron 运行级别脚本会运行那些因计算机关机而未执行的 at 和 batch 任务。） |
| autofs | 启动和停止自动挂载守护进程，用于自动挂载文件系统（例如，当插入 CD 时可以自动挂载）。 |
| crond | 启动或停止 cron 守护进程，以定期运行例行命令。 |
| cups-lpd | 控制处理打印请求打印队列的打印机守护进程。 |
| dhcpcd | 启动或停止 dhcpcd 守护进程，该守护进程自动为局域网（LAN）中的计算机分配 IP 地址。 |
| gpm | 控制 gpm 守护进程，该守护进程允许鼠标与控制台及基于文本的应用程序交互。 |
| halt | 终止所有进程，写出记账记录，移除交换空间，卸载所有文件系统，并根据命令的调用方式关闭或重启机器。 |
| httpd | 启动 httpd 守护进程，使您的计算机能够充当 HTTP 服务器（即提供网页服务）。 |
| iptables | 启动 iptables 防火墙守护进程，管理为计算机设置的任何 iptables 风格的防火墙规则。 |
| keytable | 加载预定义的键盘映射。 |
| killall | 在关闭或重启之前，关闭任何可能仍在运行的子系统。 |
| kudzu | 在启动时检测和配置新硬件。 |
| netfs | 挂载或卸载网络（NFS、SMB 和 NCPI）文件系统。 |
| network | 启动或停止所有配置的网络接口，并初始化 TCP/IP 和 IPX 协议。 |
| nfs | 启动或停止与 NFS 相关的守护进程（`rpc.nfsd`、`rpc.mountd`、`rpc.statd`、`rpc.rquotad`）并导出共享文件系统。 |
| pcmcia | 加载或卸载模块、驱动程序和程序（包括 `cardmgr` 守护进程），以支持笔记本电脑中的 PCMCIA 卡（以太网适配器、调制解调器、存储卡等）。 |
| portmap | 启动或停止 `portmap` 守护进程，管理使用远程过程调用（RPC）机制的协议和程序。 |
| random | 加载或保存机器随机数生成器当前状态的随机种子，以确保更具随机性的随机性。 |
| route | 启动或停止 `route` 守护进程，该守护进程控制通过路由器信息协议（RIP）进行动态路由表更新。 |
| rwiod | 启动或停止 `rwiod` 守护进程，该守护进程使网络上的其他人能够获取所有当前登录用户的列表。 |
| sendmail | 控制 `sendmail` 守护进程，该守护进程处理传入和传出的 SMTP（简单邮件传输协议）邮件消息。 |
| single | 终止所有正在运行的进程并进入运行级别 1（单用户模式）。 |
| smbd | 启动或停止 `smbd` 和 `nmbd` 守护进程，以允许访问 Samba 文件和打印服务。 |
| snmpd | 启动或停止 `snmpd`（简单网络管理协议）守护进程，该守护进程使他人能够查看机器配置信息。 |
| squid | 启动或停止 `squid` 服务，该服务使网络上的客户端能够使用代理服务。 |
| syslog | 启动或停止 `klogd` 和 `syslogd` 守护进程，分别处理来自内核和其他进程的日志事件。 |
| xfs | 启动或停止 `xfs`，即 X Window 字体服务器守护进程。 |
| xinetd | 设置机器的主机名，建立网络路由，并控制 `xinetd`（网络服务守护进程），该守护进程监听指向该机器的传入 TCP/IP 连接。 |
| ypbind | 绑定到 NIS（网络信息服务）主服务器（如果配置了 NIS），并启动或停止 `ypbind` 进程，该进程与主服务器通信。

每个表示您希望启动或停止的服务的脚本都链接到每个运行级别目录中的一个文件。对于每个运行级别，以 K 开头的脚本停止服务，而以 S 开头的脚本启动服务。

文件名中 K 或 S 后面的两个数字提供了一种机制来选择程序运行的优先级。例如，S12syslog 在 S90crond 之前运行。然而，虽然人类很容易看出 5 小于 10，但文件 S110my_daemon 在 85gpm 之前运行。这是因为 ASCII 排序序列对文件进行排序，这意味着仅比较一个位置上的字符。因此，在级别 3 中，以字符 110 开头的脚本在 10netword 和 15netfx 之间执行。

`/etc/rcX.d` 目录（其中 X 替换为运行级别编号）中的所有程序都是符号链接，通常指向 `/etc/init.d` 中的文件。`/etc/rcX.d` 目录包括以下内容：

- `/etc/rc0.d`：运行级别 0 目录
- `/etc/rc1.d`：运行级别 1 目录
- `/etc/rc2.d`：运行级别 2 目录
- `/etc/rc3.d`：运行级别 3 目录
- `/etc/rc4.d`：运行级别 4 目录
- `/etc/rc5.d`：运行级别 5 目录
- `/etc/rc6.d`：运行级别 6 目录

通过这种方式，`/etc/rc0.d/K05atd`、`/etc/rc1.d/K05atd`、`/etc/rc2.d/K05atd`、`/etc/rc3.d/S95atd`、`/etc/rc4.d/S95atd`、`/etc/rc5.d/S95atd` 和 `/etc/rc6.d/K05atd` 都是指向 `/etc/init.d` (atd) 的符号链接。使用这种简单且一致的机制，您可以自定义启动时启动哪些程序。

## 理解启动脚本的作用

尽管存在所有复杂的 rcX、S 和 K，但每个启动脚本的形式其实相当简单。因为它们都是纯文本，您可以只需用文本编辑器打开一个来看看它做了什么。在大多数情况下，运行级别脚本可以使用 start 选项、stop 选项以及可能的 restart 选项来运行。例如，以下行是 smb 脚本内容的一部分，该脚本定义了当脚本使用不同的选项来启动或停止 Samba 文件和打印服务时发生的情况：

```bash
#!/bin/sh

# chkconfig: - 91 35
# description: Starts and stops the Samba smbd and nmbd daemons \n used to provide SMB network services.

start() {
    KIND="$SMB"
    echo -n "Starting $KIND services: "
    daemon smbd $NMBOPTIONS
    RETVAL=$?
    echo
    KIND="NMB"
    echo -n "Starting $KIND services: "
    daemon nmbd $NMBOPTIONS
    RETVAL2=$?
    echo
    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && touch /var/lock/subsys/smb || \
        RETVAL=1
    return $RETVAL

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

restart() {
    stop
    start
}
```

为了说明此脚本的本质作用，我跳过了脚本的开头和结尾部分（其中检查网络是否已启动并运行以及设置一些值）。以下是当 smb 使用 start 或 stop 运行时执行的操作：

- **start** — 当使用 start 选项运行脚本时，脚本的这一部分启动 smbd 和 nmbd 服务器。
- **stop** — 当使用 stop 选项运行时，/etc/init.d/smb 脚本停止 smbd 和 nmbd 服务器。

restart 选项先以 stop 选项运行脚本，然后以 start 选项运行。如果您想自行启动 smb 服务，请输入以下命令（作为 root 用户）：

```bash
# service smb start
```

