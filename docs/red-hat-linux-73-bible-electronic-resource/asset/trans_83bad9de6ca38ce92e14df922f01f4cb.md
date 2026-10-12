
## 设置服务器根目录

ServerRoot 指令指定了包含配置文件、日志文件目录链接以及模块目录链接的目录。可以使用 httpd 的 -d 命令行参数来指定替代的 ServerRoot 路径名称。

```
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
#
# NOTE! If you intend to place this on an NFS (or otherwise network)
# mounted filesystem then please read the LockFile documentation
# available at <URL:http://www.apache.org/docs/mod/core.html#lockfile>.
# You will save yourself a lot of trouble.
#
# Do NOT add a slash at the end of the directory path.
#
ServerRoot "/etc/httpd"
```

## 存储服务器的 PID、锁和 ScoreBoard 文件

Apache Web 服务器会跟踪正在运行的服务器进程的 PID。它还存储有关锁文件的信息。在某些系统上，还会创建一个 ScoreBoard 文件，用于存储内部服务器进程信息。您可以使用下面描述的条目来更改这些文件的位置：

```
#
# The LockFile directive sets the path to the lockfile used when Apache
# is compiled with either USE_PCTL_SERIALIZED_ACCEPT or
# USE_FLOCK_SERIALIZED_ACCEPT. This directive should normally be left
# at its default value. The main reason for changing it is if the logs
# directory is NFS mounted, since the lockfile MUST BE STORED ON A
# LOCAL DISK. The PID of the main server process is automatically
# appended to the filename.
#
LockFile /var/run/httpd.lock

#
# PidFile: The file in which the server should record its process
# identification number when it starts.
#
PidFile /var/run/httpd.pid

#
# ScoreBoardFile: File used to store internal server process
# information. Not all architectures require this. But if yours does
# (you'll know because this file will be created when you run Apache)
# then you *must* ensure that no two invocations of Apache share the
# same scoreboard file.
ScoreBoardFile logs/apache_runtime_status
```

LockFile 指令的默认值（在编译时指定）是 `/var/run` 目录下的 `httpd.lock` 文件。由于在编译时定义了 `USE_Fcntl_SERIALIZED_ACCEPT`（一种尝试获取文件锁的方法），因此需要锁文件，但通常没有理由更改其默认值。

Apache 使用 PidFile 来存储第一个（root 拥有的）主守护进程的进程 ID。此信息由 `/etc/init.d/httpd` 脚本在关闭服务器时使用，也由服务器状态处理器使用（如后文所述）。

Red Hat Linux 不需要使用 ScoreBoardFile，因为通常保存在该文件中的状态信息是存储在内存中的。

## 绕过 srm.conf 和 access.conf 文件

如下方的注释所述，Apache 过去会在 httpd.conf 之后处理 `srm.conf` 和 `access.conf` 文件。现在，所有信息都应放入 httpd.conf 文件中。如果您想跳过对这些文件的处理，可以取消下方 ResourceConfig 和 AccessConfig 指令的注释，并将它们更改为 /dev/null。

```
#
#
# In the standard configuration, the server will process httpd.conf
# (this file, specified by the -f command line option), srm.conf, and
# access.conf in that order.  The latter two files are now distributed
# empty, as it is recommended that all directives be kept in a single
# file for simplicity.  The commented-out values below are the built-in
# defaults.  You can have the server ignore these files altogether by
# using "/dev/null" (for Unix) or "nul" (for Win32) for the arguments
# to the directives.
#
#ResourceConfig conf/srm.conf
#AccessConfig conf/access.conf
```

## 配置超时值

您可以设置几个与超时值相关的值。其中一些值描述如下：

```
#
#
# Timeout: The number of seconds before receives and sends time out.
#
Timeout 300

#
# KeepAlive: Whether or not to allow persistent connections (more than
# one request per connection).  Set to "Off" to deactivate.
#
KeepAlive Off

#
# MaxKeepAliveRequests: The maximum number of requests to allow
# during a persistent connection. Set to 0 to allow unlimited amount.
# We recommend you leave this number high, for maximum performance.
#
MaxKeepAliveRequests 100

#
# KeepAliveTimeout: Number of seconds to wait for the next request from
# the same client on the same connection.
#
KeepAliveTimeout 15
```

Timeout 指令决定了 Apache 在接收 PUT 或 POST HTTP 请求方法的报文与发送确认之间、在发送响应的确认与接收传入请求之间保持连接打开的秒数。如果您发现机器上有过多打开的空闲连接，肯定可以将默认的 5 分钟（300 秒）降低。

KeepAlive 指令指示 Apache 在请求处理完毕后保持连接打开一段时间。这使来自同一客户端的后续请求能够更快地处理，因为不需要为每个请求创建新的连接（通常连接到不同的服务器进程）。

MaxKeepAliveRequests 指令设置了一个限制，规定了在一个打开的连接上可以处理的请求数量。默认值肯定合理，因为大多数连接在达到 MaxKeepAliveRequests 之前就会触发 KeepAliveTimeout。

KeepAliveTimeout 指令指定了在等待另一个请求时保持连接的秒数。您可能需要根据客户端浏览平均页面并从中选择链接所需的时间，将默认的 15 秒增加。

## 设置服务器进程数量

您可以让 Apache 动态改变服务器进程的数量。为此，请设置 MinSpareServers 和 MaxSpareServers 值，如下所述：

```
#
# Server-pool size regulation. Rather than making you guess how many
# server processes you need, Apache dynamically adapts to the load it
# sees --- that is, it tries to maintain enough server processes to
# handle the current load, plus a few spare servers to handle transient
# load spikes (e.g., multiple simultaneous requests from a single
# Netscape browser).
#
# It does this by periodically checking how many servers are waiting
# for a request. If there are fewer than MinSpareServers, it creates
# a new spare. If there are more than MaxSpareServers, some of the
# spares die off. The default values are probably OK for most sites.
#
MinSpareServers 5
MaxSpareServers 20
#
# Number of servers to start initially --- should be a reasonable
# ballpark figure.
#
StartServers 8
#
# Limit on total number of servers running, i.e., limit on the number
# of clients who can simultaneously connect --- if this limit is ever
# reached, clients will be LOCKED OUT, so it should NOT BE SET TOO LOW.
# It is intended mainly as a brake to keep a runaway server from taking
# the system with it as it spirals down...
#
MaxClients 150
#
# MaxRequestsPerChild: the number of requests each child process is
# allowed to process before the child dies.  The child will exit so
# as to avoid problems after prolonged use when Apache (and maybe the
# libraries it uses) leak memory or other resources.  On most systems,
# this isn't really needed, but a few (such as Solaris) do have notable
# leaks in the libraries.  For these platforms, set to something like
# 10000 or so; a setting of 0 means unlimited.
#
# NOTE: This value does not include keepalive requests after initial
# request per connection.  For example, if a child process handles
# an initial request and 10 subsequent "keepalive" requests, it
# would only count as 1 request towards this limit.
#
MaxRequestsPerChild 1000
```

在独立模式下（源自 *ServerType* 指令），Apache 将启动一个由 root 拥有的主守护进程，该进程绑定到相应的 Port，然后切换到非特权 User。随后，将启动更多的服务器（等效于 *StartServers* 指令的值）作为相同的非特权 User（在这种情况下是 Apache 用户）。

Apache 尝试根据当前负载智能地启动和杀死服务器。如果流量减少且空闲服务器过多，一些服务器将被杀死（降至 *MinSpareServers* 中注明的服务器数量）。同样，如果大量请求在短时间内到达且等待新连接的服务器过少，将启动更多服务器（至多 *MaxSpareServers* 中注明的服务器数量）。

使用上面指定的值，当守护进程启动时，将运行 8 个服务器进程等待连接（由 *StartServers* 定义）。随着更多请求的到达，Apache
