
```bash
/etc/rc.d/init.d/httpd status
```

这会打印以下内容：

```text
httpd (pid 8643 8642 6510 6102 6101 6100 6099 6323 6322 6098 6097 6096 6095 362 6094 6093) is running . . .
```

这表明 Web 服务器正在运行；事实上，当前有 16 个服务器实例正在运行。

### 提示

如果您对各个服务器配置文件进行大量修改，请使用 `reload` 选项。通过让系统简单地重新读取配置文件，而不是停止和启动服务器，这可以节省时间。

## 列表 12.2 `/etc/rc.d/init.d/httpd`

```bash
#!/bin/sh
#
# Startup script for the Apache Web Server
#
# chkconfig: 345 85 15
# description: Apache is a World Wide Web server.  It is used to serve 
#              HTML files and CGI.
# processname: httpd
# pidfile: /var/run/httpd.pid
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf

# Source function library.
. /etc/rc.d/init.d/functions

# See how we were called.
case "$1" in
start)
echo -n "Starting httpd: "
daemon httpd
echo
touch /var/lock/subsys/httpd
;;
stop)
echo -n "Shutting down httpd: "
killproc httpd
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
;;
status)
status httpd
;;
restart)
$0 stop
$0 start
;;
reload)
echo -n "Reloading httpd: "
killproc httpd -HUP
echo
;;
*)
echo "Usage: $0 {start|stop|restart|reload|status}"
exit 1
esac

exit 0
```

# 配置文件列表

以下是 Apache 版本 1.3.12 的服务器配置文件完整列表。如果您安装了不同版本的服务器，或者即使您安装了此版本，您可能会注意到您的配置文件与这里列出的配置之间存在一些差异。其中一些差异仅仅是我的系统与您的系统之间的差异。其他是我将参数设置为不同值的地方。

列表 12.3 显示了服务器配置文件。

## 列表 12.3 `conf/httpd.conf`

```text
##
## httpd.conf -- Apache HTTP server configuration file
##

# Based upon the NCSA server configuration files originally by Rob McCool.
# This is the main Apache server configuration file. It contains the
# configuration directives that give the server its instructions.
# See <URL:http://www.apache.org/docs/> for detailed information about
# the directives.
#
# Do NOT simply read the instructions in here without understanding
# what they do.  They're here only as hints or reminders.  If you are unsure
# consult the online docs. You have been warned.

# After this file is processed, the server will look for access and process
# /usr/conf/srm.conf and then /usr/access.conf
# unless you have overriden these with ResourceConfid and/or
# AccessConfid directives here.

# The configuration directives are grouped into three basic sections:
#
1. Directives that control the operation of the Apache server process as a
   whole (the 'global environment').
#
2. Directives that define the parameters of the 'main' or 'default' server,
   which responds to requests that aren't handled by a virtual host.
   These directives also provide default values for the settings
   of all virtual hosts.
#
3. Settings for virtual hosts, which allow Web requests to be sent to
   different IP addresses or hostnames and have them handled by the
   same Apache server process.

# Configuration and logfile names: If the filenames you specify for many
# of the server's control files begin with " / " (or "drive:/" for Win32), the
# server will use that explicit path.  If the filenames do *not* begin
# with " / ", the value of ServerRoot is prepended -- so "logs/foo.log"
# with ServerRoot set to "/usr/local/apache/" will be interpreted by the
# server as "/usr/local/apache/logs/foo.log".

### Section 1: Global Environment
# The directives in this section affect the overall operation of Apache,
# such as the number of concurrent requests it can handle or where it
# can find its configuration files.
#
```

## 列表 12.3

#

# `ServerType` 为 `inetd` 或 `standalone`。`Inetd` 模式仅支持 Unix 平台。

#

`ServerType standalone`

#

# `ServerRoot`：服务器配置、错误和日志文件所在的目录树根目录。

#

# 注意！如果您打算将其放置在 NFS（或其他网络）挂载的文件系统上，请阅读 `LockFile` 文档

#（位于 `<URL:http://www.apache.org/docs/mod/core.html#lockfile>`）；

# 这将为您省去许多麻烦。

#

# 请勿在目录路径末尾添加斜杠。

#

`ServerRoot "/etc/httpd"`

#

# `LockFile` 指令设置锁文件路径，该文件在使用 `USE_FCNTL_SERIALIZED_ACCEPT` 或

# `USE_FLOCK_SERIALIZED_ACCEPT` 编译 Apache 时使用。通常应保持该指令的默认值。

# 更改它的主要原因是日志目录通过 NFS 挂载，因为锁文件**必须存储在本地磁盘上**。

# 主服务器进程的 PID 会自动追加到文件名中。

#

`LockFile /var/lock/httpd.lock`

#

# `PidFile`：服务器启动时应记录其进程标识号的文件。

#

`PidFile /var/run/httpd.pid`

#
