
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

为了说明此脚本本质上做了什么，我跳过了脚本的开头部分（其中它检查网络是否已启动并设置了一些值）。以下是 `smb` 脚本以 `start` 或 `stop` 选项运行时所执行的操作：

- `start` — 当脚本以 `start` 选项运行时，脚本的这一部分会启动 `smbd` 和 `nmbd` 服务器。
- `stop` — 当以 `stop` 选项运行时，`/etc/init.d/smb` 脚本会停止 `smbd` 和 `nmbd` 服务器。

`restart` 选项先运行脚本的 `stop` 部分，然后运行 `start` 部分。如果你想自己启动 `smb` 服务，可以输入以下命令（作为 `root` 用户）：

```bash
# /etc/init.d/smb start
Starting SMB services:				[   OK   ]
```

正在启动 NMB 服务：                    [ OK ]

要停止该服务，您可以输入以下命令：

```
# /etc/init.d/smb stop
正在关闭 SMB 服务：              [ OK ]
正在关闭 NMB 服务：              [ OK ]
```

`smb` 运行级别脚本与其他运行级别脚本的不同之处在于，它支持除了 `start` 和 `stop` 之外的其他几个选项。例如，该脚本有一些选项（示例中未显示），允许您重新加载 `smb.conf` 配置文件（`reload`）以及检查服务的状态（`rhstatus`）。

## 更改运行级别脚本的行为

要修改任何此类脚本的启动行为，只需在文本编辑器中打开该文件即可。例如，`atd` 守护进程会排队处理从 `at` 和 `batch` 命令提交的任务。通过 `batch` 提交的任务仅当系统负载低于特定值时才会执行，该值可以通过 `atd` 命令的命令行选项进行设置。默认值 `0.8` 基于这样一个假设：CPU 利用率低于 80% 的单处理器机器能够处理批处理任务带来的额外负载。但是，如果您向机器添加了另一个 CPU，默认的阈值将过低，批处理任务将无法得到足够的限制。

您可以将系统负载阈值从 `0.8` 更改为 `1.6`，以适应增加的处理能力。要做到这一点，只需修改 `/etc/init.d/atd` 脚本中（在 `start` 部分）的以下行：

```
daemon /usr/sbin/atd
```

将其替换为以下行，使用 `-1` 参数来指定新的最小系统负载值：

```
daemon /usr/sbin/atd -1 1.6
```

保存文件并退出编辑器后，您可以重新引导机器，或者运行以下三个命令中的任意一个，开始使用新的批处理阈值：

```
/etc/init.d/atd reload
/etc/init.d/atd restart
/etc/init.d/atd stop ; /etc/rc.d/init.d/atd start
```

`注意：` 在更改运行级别脚本之前，请务必先对其进行备份。此外，在升级脚本来源的包之前，请记录您对运行级别脚本所做的更改。升级后，您需要再次进行这些更改。

如果您不习惯编辑启动脚本，而只是希望为脚本运行的守护进程进程添加选项，也许有一种方法可以直接输入这些更改，而无需直接编辑启动脚本。检查 `/etc/sysconfig` 目录，看看是否存在一个与要修改的脚本同名的文件。如果有，该文件通常提供可以设置的值，用于向启动脚本传递选项。`amd`、`arpwatch`、`dhcpd`、`kudzu`、`ntpd`、`samba`、`squid` 等都有 `sysconfig` 文件。

## 重组或移除运行级别脚本

有几种方法可以处理从系统启动目录中移除程序、将其添加到特定运行级别，或更改其执行时间。第一种方法是手动删除符号链接（以移除它）或重新编号它（以更改其执行顺序）。如果您希望阻止 `sendmail` 守护进程在运行级别 2 中启动（仅在其运行级别 3、4 和 5 中激活），您可以删除 `/etc/rc2.d/S80sendmail` 链接。但是，将链接重命名为不以 `S` 开头的名称（例如 `/etc/rc2.d/_S80sendmail`）可能更方便，以防您以后想要重新启用它。要更改其执行顺序，只需重命名文件并将数字 80 更改为更高或更低的数字即可。

`警告：` 您不应该删除实际的文件（在此情况下是 `/etc/init.d/sendmail`）。由于不会自动从 `/etc/init.d` 目录直接运行脚本，因此将脚本保留在此处不会造成任何伤害。`/etc/init.d` 中的脚本仅通过 `/etc/rcX.d` 目录中的链接进行访问。通过将脚本保留在 `init.d` 目录中，您以后可以通过将它们重新链接到适当的运行级别目录来随时添加它们。

另一种重组或移除运行级别脚本的方法是使用服务配置窗口。以 `root` 用户登录，并在终端窗口中输入以下内容：

```
# serviceconf &
```

图 12-1 显示了服务配置窗口的一个示例。

![](img/1744bde8c889adfab3fc911e1687fecf_493_0.png)

**图 12-1：** 在服务配置窗口中重组、添加和移除运行级别脚本。

服务配置窗口允许您为运行级别 3、4 和 5 重新配置服务。您当前正在运行和正在编辑的运行级别显示在屏幕顶部附近。可用于该运行级别的服务显示在框架中间，配置为在该级别启动的服务旁边带有对勾。您可以从此窗口执行以下操作：

- `添加` — 单击您希望在该运行级别自动启动的每个服务旁边的方框，使方框中出现对勾。
- `移除` — 单击您想要为特定运行级别移除的运行级别脚本，以移除对勾。
- `保存更改` — 单击窗口中的 `保存更改` 以保存您对运行级别脚本所做的任何更改。
- `启动、停止或重启` — 单击列表中的服务。选择 `操作`；然后选择 `启动服务`、`停止服务` 或 `重启服务`。选定的服务将立即启动、停止或重启。

一些管理员更喜欢使用基于文本的命令来管理运行级别脚本以及管理其他自动启动的系统服务。可以使用 `chkconfig` 命令来列出运行级别脚本启动的服务，以及 `xinetd` 守护进程启动的服务是开启还是关闭状态。要查看所有系统服务的列表及其开启或关闭状态的指示，请输入以下命令：

```
# chkconfig --list | less
```

然后您可以翻页查看这些服务。如果您想查看单个服务的状态，可以在列表选项的末尾添加该服务。例如，要查看 `nfs` 服务是否在每个运行级别启动，请输入以下内容：
