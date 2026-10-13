
空格键。此外，你可以使用 KDE System V Init 编辑器 (`ksysv`) 来确定在哪些运行级别（`runlevel`）启动和停止哪些服务器和守护进程。

| 文件 | 说明 |
| :--- | :--- |
| `/etc/sysconfig` | Red Hat Linux 上存放系统配置文件和目录的目录。 |
| `/etc/rc.d` | 存放系统启动和关机文件的目录。 |
| `/etc/rc.d/rc.sysinit` | 系统的初始化文件。 |
| `/etc/rc.d/rc.local` | 自定义命令的初始化文件；你可以自由地编辑此文件以添加自己的启动命令；这是最后一个执行的启动文件。 |
| `/etc/rc.d/rc.modules` | 加载内核模块（Red Hat Linux 上默认未实现）。 |
| `/etc/rc.d/init.d` | 存放许多守护进程、服务器和脚本的目录，例如用于 Web 服务器的 `httpd` 以及启动网络连接的网络。 |
| `/etc/rc.d/num.d` | 不同运行级别的目录，`num` 表示运行级别。这些目录包含指向 `/etc/rc.d/init.d` 目录中脚本的链接。 |
| `/etc/rc.d/init.d/halt` | 每次关闭系统时执行的操作，如卸载文件系统；在其他发行版称为 `rc.halt`。 |
| `/etc/rc.d/init.d/cups` | 启动和停止 `cups` 守护进程。 |
| `/etc/rc.d/init.d/xinetd` | 启动或停止 `xinetd` 守护进程的操作。 |
| `/etc/rc.d/init.d/network` | 启动或停止网络连接的操作。 |
| `/etc/rc.d/init.d/httpd` | 启动或停止你的 Web 服务器守护进程 `httpd` 的操作。 |

表 24-6. 系统启动文件

# 第 24 章：基础系统管理

在 RedHat 中，配置和启动信息也存储在 `/etc/sysconfig` 目录中。在这里，你会找到包含系统变量定义的文件，这些变量用于配置键盘和鼠标等设备。这些条目是在安装期间配置设备时定义的。你还会找到网络定义以及启动和停止网络连接的脚本。这里显示了键盘文件的示例。

```
/etc/sysconfig/keyboard
KEYBOARD="pc"
KEYTABLE="us"
```

这些文件中的几个是由 Red Hat 管理工具生成的，例如 `redhat-config-mouse`、`redhat-config-board` 或 `redhat-config-network`。表 24-7 列出了若干常用工具以及它们控制的 `sysconfig` 文件。（有关 Red 管理工具的完整列表，请参阅第 4 章。）例如，`redhat-config-mouse` 将为鼠标设备名称、类型和某些功能生成配置变量，并将它们存放在 `/etc/sysconfig/mouse` 文件中，如下所示：

```
FULLNAME=Generic - 3 Button Mouse (PS/2)
MOUSETYPE="PS/2"
XMOUSETYPE="PS/2"
XEMU3="no"
DEVICE=/dev/mouse
```

其他文件（如 `hwconf`）将列出你所有的硬件设备，定义配置变量，如其类别（视频、CD-ROM、硬盘等）、它使用的总线（PCI、IDE 等）、它的设备名称（如 `hdd` 或 `st0`）、它使用的驱动程序以及设备描述。这里显示了一个 CD-ROM 条目：

```
class: CDROM
bus: IDE
detached: 0
device: hdd
driver: ignore
desc: TOSHIBA DVD-ROM-SD-M1402"
```

其中包含了几个目录，例如 `network-scripts`，它列出了若干网络连接的启动脚本——例如启动 PPP 连接的 `ifup-ppp`。

某些管理工具会使用多个一个 `sysconfig` 文件。`redhat-config-network` 将主机名和网关等网络配置信息放在 `/etc/sysconfig/network` 文件中。特定的以太网设备配置（包括你的 IP 地址和网络）放在 `/etc/sysconfig/network-scripts` 目录中相应的以太网设备配置文件中。例如，`eth0` 以太网设备使用的 IP 地址和掩码可以在 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中找到。本地主机设置位于 `/etc/sysconfig/network-scripts/ifcfg-lo` 中。

某些管理工具（如 `authconfig-gtk`）会为所选的服务进一步配置文件。`authconfig-gtk` 工具会配置 `/etc/sysconfig/authconfig`，以及用于 Kerberos 认证的 `/etc/krb5.conf`、用于 NIS 支持的 `/etc/yp.conf` 和用于 LDAP 认证的 `/etc/ldap/ldap`。

## 系统日志：`/var/log` 和 `syslog`

系统上执行任务的各种系统日志存储在 `/var/log` 目录中。在这里，你可以找到邮件、新闻以及所有其他系统操作的日志 `/var/log/messages` 文件是未被其他日志涵盖的所有系统任务日志。这通常包括启动任务，如加载驱动程序和挂载文件系统。如果某个卡的驱动在启动时安装失败，你可以在这里找到它的错误信息。登录信息也会记录在此文件中，显示谁尝试登录哪个账户。`/var/log/maillog` 文件记录邮件消息传输和新闻传输。

你可以使用 Red Hat 日志查看器（等等，这里的文本似乎重复了）。

| 工具 | 配置文件 | 说明 |
| :--- | :--- | :--- |
| `authconfig-gtk` | `/etc/sysconfig/authconfig` | 认证选项，例如启用 NIS、shadow 和 LDAP。 |
| `redhat-config-security` | `/etc/sysconfig/security` | 选择级别：高、中、无。 |
| `redhat-config-keyboard` | `/etc/sysconfig/keyboard` | 选择键盘类型。 |
| `redhat-config-mouse` | `/etc/sysconfig/mouse` | 选择鼠标类型。 |
| `redhat-config-network` | `/etc/sysconfig/network-scripts/ifcfg-eth0` | 设置你的网络设置。 |
| `redhat-config-date` | `/etc/sysconfig/clock` | 设置日期。 |
| `redhat-logviewer` | `/etc/sysconfig/redhat-logviewer` | 显示日志列表。 |

表 24-7. Red Hat 管理工具

# 第 24 章：基础系统管理

`log/messages`。要将日志记录到远程主机，你只需要在主机名前加上 `@` 符号。以下示例将所有内核消息保存到 `rabbit.trek.com`：

```
kern.* @rabbit.trek.com
```

对于用户，你只需要列出想要接收消息的用户登录即可。以下示例将关键新闻消息发送到用户 `chris` 和 `aleina` 的控制台：

```
news.=crit chris,aleina
```

你还可以将消息输出到命名管道（FIFO）。操作字段的管道项以 `|` 开头。以下示例将内核调试消息管道到命名管道 `/usr/adm/debug`：

```
kern.debug=/usr/adm/debug
```

| 设施 (Facilities) | 说明 (Description) |
| --- | --- |
| `auth-priv` | 安全/授权消息（私有） |
| `cron` | 守护进程（cron 和 at）消息 |
| `daemon` | 其他系统守护进程消息 |
| `kern` | 内核消息 |
| `lpr` | 打印机子系统消息 |
| `mail` | 邮件子系统消息 |
| `mark` | 仅内部使用 |
| `news` | Usenet 新闻子系统消息 |
| `syslog` | Syslog 内部消息 |
| `user` | 通用用户级消息 |
| `uucp` | UUCP 子系统消息 |
| `local0` 到 `local7` | 留作本地使用 |

表 24-8. Syslogd 设施、优先级和运算符

# 红帽 Linux 8：完全参考

| 设施 (Facilities) | 说明 (Description) |
| --- | --- |
| `debug` | 7, 调试消息，优先级最低 |
| `info` | 6, 信息性消息 |
| `notice` | 5, 通知，正常但重要的情况 |
| `warning` | 4, 警告 |
| `err` | 3, 错误消息 |
| `crit` | 2, 关键情况 |
| `alert` | 1, 警，必须立即采取行动 |
| `emerg` | 0, 紧急消息，系统不可用，优先级最高 |
| 运算符 (Operators) | 说明 (Description) |
