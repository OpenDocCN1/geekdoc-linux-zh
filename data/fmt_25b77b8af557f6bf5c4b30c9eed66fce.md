
cron 守护进程会在指定时间自动启动某些程序。cron 仅在运行级别 2 和 3 中启动。建议在始终运行的计算机上启用它。另一种选择或补充是 `AT` 守护进程。

```bash
MAX_DAYS_IN_TMP="0"
```

`cron.daily` 可以检查 `tmp` 目录中的旧文件。它将删除超过此处指定天数未被访问的所有文件。将其留空或设置为 0 可禁用此功能。

```bash
TMP_DIRS_TO_CLEAR="/tmp /var/tmp"
```

指定应从中删除旧文件的目录。

```bash
OWNER_TO_KEEP_IN_TMP="root"
```

指定不应删除其文件的用户，即使已超过设定的时间。

```bash
CLEAR_TMP_DIRS_AT_BOOTUP="no"
```

将其设置为 `yes`，以便在启动时从 `TMP_DIRS_TO_CLEAR` 中定义的临时目录中完全删除（`rm -rf`）所有文件和子目录。此功能会忽略 `OWNER_TO_KEEP_IN_TMP`——所有文件都将被删除，没有例外。

```bash
DELETE_OLD_CORE="no"
```

是否应删除旧的 `core` 文件？如果设置为 `no`，`cron.daily` 会在发现旧 `core` 文件时告知你。此功能要求将 `RUN_UPDATEDB` 设置为 `yes`，并且需要安装 `findutils-locate` 软件包。

```bash
MAX_DAYS_FOR_CORE="7"
```

`core` 文件的最大保留天数。

```bash
REINIT_MANDB="yes"
```

是否应由 `cron.daily` 重新创建手册页数据库（`mandb` 和 `whatis`）？

```bash
DELETE_OLD_CATMAN="yes"
```

是否应删除旧的预格式化手册页（位于 `/var/catman`）？

```bash
CATMAN_ATIME="7"
```

旧的预格式化手册页在删除前应保留多长时间（以天为单位）？

## locate

`locate` 数据库允许在系统上快速查找文件。它通常在系统启动后不久更新。

```bash
RUN_UPDATEDB="no"
```

`locate`（`locate`）的数据库是否应每天更新一次？可以使用以下变量对 `updatedb` 进行更详细的配置。

```bash
RUN_UPDATEDB_AS="nobody"
UPDATEDB_NETPATHS=""
UPDATEDB_PRUNEPATHS="/mnt /cdrom /tmp /usr/tmp /var/tmp
/var/spool /proc /media"
UPDATEDB_NETUSER=""
UPDATEDB_PRUNEFS=""
```

## 内核

内核。

```bash
INITRD_MODULES="aic7xxx"
```

指定启动期间要加载的内核模块名称，*例如*，以便访问硬盘。在系统安装或更新期间，此处会进行合理的设置。

## sysctl

内核级别的系统控制。

```bash
IP_DYNIP="no"
```

是否希望在启动时启用“动态 IP 补丁”？

```bash
IP_TCP_SYNCOOKIES="yes"
```

启用“SYN 洪水防护”？参见 `/usr/src/linux/Documentation/Configure.help`。

```bash
IP_FORWARD="no"
```

如果主机应在两个网络接口之间转发，请将此变量设置为 `yes`。这通常对路由器或“伪装”有用。脚本 `/etc/init.d/boot.proc` 通过 `/proc` 文件系统中的一个条目启用 IP 转发。

```bash
ENABLE_SYSRQ="no"
```

如果将其设置为 `yes`，即使系统崩溃（例如在内核调试期间），你也能对系统进行一些控制。更多信息请查阅 `/usr/src/linux/Documentation/sysrq.txt`。

```bash
DISABLE_ECN="yes"
```

如果你使用 2.4 内核连接 Internet 上的某些机器时遇到问题，而使用 2.2 时没有问题，这可能是由于有问题的防火墙丢弃了设置了 ECN（早期拥塞通知）标志的网络数据包。将其设置为 `yes`，以便在启动时禁用 ECN。

```bash
BOOT_SPLASH="yes"
```

设置为 `no` 可在启动时（内核加载后）关闭控制台 1 上的启动画面。

## devfs

`devfs` 文件系统。

```bash
USE_DEVFS="no"
```

## 网络和本地服务的启动与配置

### SuSEfirewall2

激活防火墙。参见 SuSE-firewall2 软件包中的 readme 文件。

### 新闻

访问 NNTP 服务器的设置。

```bash
ORGANIZATION=""
```

此处输入的文本将出现在从此机器发送的每篇新闻帖子中。

```bash
NNTP_SERVER="news"
```

新闻服务器的地址。如果你通过 UUCP 接收新闻并且它们存储在本地，请将此变量设置为 `localhost`。

### 代理

代理设置。

```bash
HTTP_PROXY=""
```

如果相应设置了此环境变量，某些程序（例如 `lynx`、`arena` 或 `wget`）会使用代理服务器。SuSEconfig 会将其设置到 `/etc/SuSEconfig/*` 中（参见 SDB 文章 `file:/usr/share/doc/sdb/de/html/lynx_proxy.html`）。示例："http://proxy.me:3128/"

```bash
FTP_PROXY=""
```

FTP 的代理。示例："http://proxy.provider.com:3128/"。

```bash
GOPHER_PROXY=""
```

Gopher 的代理。示例："http://proxy.provider.com:3128/"。

```bash
NO_PROXY="localhost"
```

从代理使用中排除域或子域。示例："www.me.de, do.main, localhost"。

### ssh

在启动“Secure Shell 守护进程”之前，请确保存在“主机密钥”。请查阅 `/usr/share/doc/packages/ssh` 中的文档和手册页。

```bash
SSHD_OPTS=""
```

`sshd` 的选项。

### ypbind

NIS 客户端的配置。附加信息：域名在 `/etc/defaultdomain` 中设置。使用 YaST2 配置期间，服务器名称将直接输入到 `/etc/yp.conf` 中。

```bash
YP_OPTIONS=""
```

NIS 的选项。

### 网络

网络配置的目录。

### network/config

```bash
DEFAULT_BROADCAST="+"
CHECK_FOR_MASTER="yes"
NO_ROUTING_INTERFACETYPES="lo dummy"
CHECK_DUPLICATE_IP="yes"
CHECK_CONNECTIONS="yes"
CLOSE_CONNECTIONS="false"
```

关闭路由时，可以关闭所有网络连接（并不总是有用）。如果 `CLOSE_CONNECTIONS` 设置为 `true`，`/etc/init.d/route` 将扫描 `/proc` 中的活动网络连接，并向相应进程发送 `term` 信号。

```bash
DEBUG="no"
USE_SYSLOG="yes"
MODIFY_RESOLV_CONF_DYNAMICALLY="yes"
FQHOSTNAME="earth.cosmos.com"
```

完全限定主机名，包含主机名和域名。

### network/dhcp

启动 DHCP 服务器（动态主机配置协议）。

```bash
DHCLIENT_SLEEP="1"
DHCLIENT_DEBUG="no"
DHCLIENT_MODIFY_RESOLV_CONF="yes"
DHCLIENT_MODIFY_NTP_CONF="no"
DHCLIENT_MODIFY_NIS_CONF="no"
DHCLIENT_SET_HOSTNAME="yes"
DHCLIENT_SET_DOMAINNAME="no"
DHCLIENT_KEEP_SEARCHLIST="no"
DHCLIENT_TIMEOUT="999999"
DHCLIENT_HOSTNAME_OPTION=""
DHCLIENT_CLIENT_ID=""
DHCLIENT_RELEASE_BEFORE_QUIT="yes"
```

### network/ifcfg-eth0

```bash
IPADDR="193.141.17.202"
```

第一块网卡的 IP 地址。

### network/ifcfg-lo

### plip

PLIP：通过并行接口的点对点连接

### sendmail

`sendmail` 变量；使用 YaST2 邮件模块进行配置

### dhcpd

DHCP 服务器。
