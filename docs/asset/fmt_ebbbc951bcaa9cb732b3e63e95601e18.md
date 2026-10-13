
# 系统启动脚本与运行级别

`/etc/rc.d/init.d` 目录中的启动脚本可以在每次启动系统时自动执行。在谨慎访问这些脚本（如你的网络接口和打印机守护进程等核心程序）时，这些 `init` 脚本是通过每个可能的运行级别的子目录中的链接访问的。在 `/etc/rc.d` 目录中有一组格式为 `rcN.d` 的子目录，其中 `N` 是指代运行级别的数字。`rc` 脚本检测系统启动时的运行级别，然后只执行运行级别子目录中指定的启动脚本。最常用的两个运行级别是 3（多用户登录）和 5（图形登录）。当你启动系统时，如果你执行的是命令行登录，`rc` 脚本会执行 `rc3.d` 中的脚本；如果你使用的是图形登录，则执行 `rc5.d` 中的脚本。`rc3.d` 和 `rc5.d` 目录包含 `/etc/rc.d/init.d` 中某些启动脚本的符号链接。`/etc/rc.d/init.d` 目录中的脚本实际上通过 `rc3.d` 或 `rc5.d` 中的符号链接调用。`/etc/rc.d/httpd` 的符号链接为 `S85httpd`。链接前缀 `S` 代表“启动”，对应的 `init.d` 脚本带有启动选项。数字表示启动脚本的执行顺序，数字越小越先。如果你将链接名称改为 `K...`，脚本将在 `rc0.d` 和 `rc6.d` 目录中调用。运行级别 0 停止系统，运行级别 6 重启。你可以使用 `runlevel` 命令查看当前运行的运行级别。运行级别列表所示：

| 运行级别 (Runlevel) | rc 目录 | 说明 |
|---|---|---|
| 0 | rc0.d | 停机（关闭）系统 |
| 1 | rc1.d | 单用户模式（无网络，功能受限） |
| 2 | rc2.d | 无 NFS 支持的多用户模式（功能受限） |
| 3 | rc3.d | 多用户模式（完全功能） |
| 5 | rc5.d | 带有图形登录的多用户模式（完全功能） |
| 6 | rc6.d | 重启系统 |

大多数使用 RPM 软件包的服务器软件会自动安装启动脚本并在相应的 `rc.d` 目录中创建所需的链接。，启动脚本也可用于系统启动时运行的任何程序。要让此类程序自动启动，你首先要在 `/etc/rc.d/init.d` 中为其创建一个启动脚本，并在 `rc3.d` 和 `rc5.d` 目录中创建指向该脚本的符号链接。停止链接 (`K`) 也应该被放在用于运行级别 6 的 `rc6.d` 目录中。

如果你的脚本启动了多个守护进程，你应该为每个守护进程准备一个 `processname` 条目。例如，Samba 服务启动了 smdb 和 nmdb 两个守护进程。

```
# processname: smdb
# processname: nmdb
```

标签部分的结束由一个空行指示。在该行之后，任何以 `#` 开头的行都被视为注释。`chconfig` 行将列出服务应该启动的运行级别，以及启动和停止优先级。以下条目列出了运行级别 3、4 和 5，启动优先级为 85，停止优先级为 15。

```
# chconfig: 35 85 15
```

使用 `description` 字段可以输入服务的简短描述，在换行符前使用 `\` 符号来使用一个 `pidfile`，该文件是存储服务进程标识符（PID）的文件。通过 `config` 标签，你可以指定服务可能使用的配置文件。以 Apache Web 服务器为例，可能会有三个配置文件：

```
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

## Apache 启动脚本示例

这里显示了一个 Web 服务器启动脚本的简化版本。大多数脚本要复杂得多，特别是在确定服务器启动时可能需要的任何参数或变量时。它与 Web 服务器拥有相同的守护进程 `httpd`。

`/etc/rc.d/init.d/httpd`

```
#!/bin/sh
#
# Apache Web Server 的启动脚本
# chconfig: 35 85 15
description: Apache 是一个全球万网服务器。它用于提供 \
# HTML 文件和 CGI。
# processname: httpd
# pidfile: /var/run/httpd.pid
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

```
# 加载函数库。
 /etc/rc.d/init.d/functions
```

```
# 查看 $1 是如何调用的。
case "$1" in
  start)
    echo -n "Starting httpd:"
    daemon httpd
    echo
    touch /var/lock/subsys/httpd
    ;;
```

```
stop)
    killproc httpd
```

```
echo -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
;;
status)
  status httpd
  ;
restart)
  $0 stop
  $0 start
  ;
reload)
  echo -n "Reloading: "
  killproc httpd -HUP
  echo
  ;
*)
  echo "Usage: $0 {start|stop|restart|reload|status}"
  exit 1
esac
exit 0
```

Internet 服务器的 RPM 软件包包含了服务器的 init 脚本。安装 RPM 包会将脚本安装在 `/etc/rc.d/init.d` 目录下，并在运行级别目录中创建适当的链接，例如 `/etc/rc.d/rc3.d`。如果需要，从你的源代码文件安装服务器，你仍然可以手动安装该 init 脚本。如果不存在启动脚本，你首先复制 `httpd-script-init`，然后编辑副本以将所有对 `httpd` 的引用替换为服务器守护进程的名称。然后，将脚本副本放置在 `/etc/rc.d/init.d` 目录下，并在 `/etc/rc.d/rc3.d` 目录对其创建一个符号链接。你可以使用 System V Init Editor，从菜单中选择“Re-scan”（重新扫描），点击“Available”列表中的条目，点击“Add”（添加）按钮，然后选择“Run”（运行）选项。

RPM 软件包的版本包含了服务器的 init 脚本。安装 RPM 包会将脚本安装在 `/etc/rc.d/init.d` 目录下，并在运行级别目录中创建适当的链接，例如 `/etc/rc.d/rc3.d`。如果需要，从你的源代码文件安装服务器，你仍然可以手动安装该 init 脚本。如果不存在启动脚本，你首先复制 `httpd-script-init`，然后编辑副本，将所有对 `httpd` 的引用替换为服务器守护进程的名称。然后，将脚本副本放置在 `/etc/rc.d/init.d` 目录下，并在 `/etc/rc.d/rc3.d` 目录对其创建一个符号链接。你可以使用 System V Init Editor，从菜单中选择“Re-scan”（重新扫描），点击“Available”列表中的条目，点击“Add”（添加）按钮，然后选择“Run”（运行）选项。当你启动系统时，新的服务器会自动启动，并发等待请求。

## 扩展服务守护 xinetd

如果你的系统只处理某个特定服务的请求，你就不需要一直运行该服务。扩展服务守护 `xinetd` 仅在远程用户访问服务时启动它们。扩展服务守护（`xinetd`）持续检查远程用户对特定服务的请求；当收到请求时，它会启动相应的守护进程。

`xinetd` 程序设计为 `inetd` 的替代品，提供了安全增强、日志支持甚至用户通知。例如，使用 `xinetd` 可以在用户无法访问服务时向他们发送横幅。`xinetd` 的安全功能可以防止拒绝服务攻击、限制并发连接数或限制连接速率。`xinetd` 还整合了 TCP，无需调用 `tcpd` 守护进程即可提供 TCP 安全。

此外，你不需要服务 `/etc/services` 文件列出的服务。`xinetd` 可以配置为启动任何种目的特殊服务器。Red Hat Linux 7.0 及以上版本使用 `xinetd`。许多旧版本的 Linux 系统可能仍在使用 `inetd`。

你可以使用 `/etc/rc.d/init.d` 目录下的启动脚本来启动、停止和重启 `xinetd`，如下：

```
# /etc/rc.d/init.d/xinetd stop
# /etc/rc.d/init.d/xinetd start
# /etc/rc.d/init.d/xinetd restart
```
