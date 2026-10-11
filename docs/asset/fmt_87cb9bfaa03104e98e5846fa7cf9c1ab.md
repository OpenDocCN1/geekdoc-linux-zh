
```
ps ax | grep [httpd]
...
26492 ? 0:00 /etc/httpd/conf/httpd_1.conf
26493 ? 0:00 /etc/httpd/conf/httpd_2.conf
26494 ? 0:00 /etc/httpd/conf/httpd_1.conf
```

# 第 6 章：配置 Apache Web 服务器

## Apache 故障排除

在 Web 服务器重启期间，如果 Apache 在配置文件中发现它不喜欢的选项，它会在控制台报错。致命错误将导致 Web 服务器无法启动；非致命错误将允许 Apache 启动，尽管功能受限。在启动或重启 Apache 时请注意这些错误。当它找不到所需的文件或目录时，Apache 会报出类似下面的错误：

```
fopen: No such file or directory
```

```
httpd: could not open error log file /var/log/httpd/apache/error_log.log
```

如你所见，我上面写错了错误日志文件的文件名。这个错误阻止了 Apache 的启动。

```
httpd:[Mon Aug 2 11:01:30 1999] [error] Cannot resolve host name
host.some_domain.com -- ignoring!
Warning:DocumentRoot [/www/docs/host.some_domain.com] does not exist
```

然而，这是一个非致命错误。Apache 无法解析我写错的 `VirtualHost` 指令，因为我提供了一个虚假的主机。尽管如此，它能够处理默认 Web 服务器并正常启动其服务。其他错误会出现在服务器日志中——通常，这些是非致命错误，Web 服务器正在运行，但它们可以提醒你注意可能影响观众的问题。

故障排除 Apache 的方法有几种，无论错误是否致命。大多数情况下，错误信息会具体指明它不喜欢的行号或配置指令。在检查 Apache 时，你可以查看服务器是否已经启动、它在主进程下以什么进程 ID 运行，以及错误和访问日志显示了什么。

如果你不确定 Apache 是如何编译/配置的，可以在命令行执行 `httpd.apache -v` 来查找。以下是与 OpenLinux 2.3 绑定的 `httpd.apache` 的输出：

```
Server version: Apache/1.3.4 (Unix)
Server built: Aug 10 1999 19:17:10
Server's Module Magic Number: 19990108:0
Server compiled with....
-D HAVE_MMAP
-D HAVE_SHMGET
-D USE_SHMGET_SCOREBOARD
-D USE_MMAP_FILES
-D USE_FLOCK_SERIALIZED_ACCEPT
-D HTTP_ROOT="/usr/local/apache"
-D SUXEC_BIN="/usr/local/apache/sbin/suexec"
-D DEFAULT_PIDLOG="logs/httpd.pid"
-D DEFAULT_SCOREBOARD="logs/apache/runtime_status"
-D DEFAULT_LOCKFILE="logs/accept.lock"
-D DEFAULT_XFERLOG="logs/access_log"
-D DEFAULT_ERRORLOG="logs/error_log"
-D TYPES_CONFIG_FILE="conf/types"
-D SERVER_CONFIG_FILE="conf/httpd.conf"
-D ACCESS_CONFIG_FILE="conf/access.conf"
-D RESOURCE_CONFIG_FILE="conf/misc.conf"
```

## 检查 Apache 是否启动

因为 Apache 将其进程 ID 写入 `/var/run/httpd.pid`，检查 Apache 是否正在运行的一种简单方法是查看该文件是否存在。使用 `cat` 命令查看文件。这里是一个显示 Apache 在进程 ID 7078 下运行的示例。

```
cat /var/run/httpd.pid
```

如果它没有运行，你的输出将是这样：

```
cat /var/run/httpd.pid: No such file or directory
```

这种方法并非万无一失；在系统崩溃后，Apache 退出但不删除其 `httpd.pid`。为了获得更准确的结果，请使用 `ps ax` 命令：

```
ps ax | grep [httpd]
...
26492 ? 0:00 /etc/httpd/conf/httpd_1.conf
26493 ? 0:00 /etc/httpd/conf/httpd_2.conf
26494 ? 0:00 /etc/httpd/conf/httpd_1.conf
```

## 安全性考量

然后我启动了两个服务器：

```
httpd.apache -f /etc/httpd/conf/httpd_1.conf
httpd.apache -f /etc/httpd/conf/httpd_2.conf
```

我通过访问 `http://10.0.0.1` 和 `http://10.0.0.2` 验证了我的配置。显示 `10.0.0.1` 以 `user_1` 的身份运行，而 `10.0.0.2` 以 `user_2` 的身份运行。

如果你使用此配置，你可能需要修改 `/etc/rc.d/init.d` 脚本，或者将其替换为你自己的脚本。现有的 `httpd` 脚本设计为系统启动一个 `httpd` 进程，而不是多个。

然而，这在某种程度上浪费了系统资源。如果你配置了 200 个站点，会有数百个进程在运行。对于少量的虚拟域名和特定情况，这是一种为 Web 开发人员提供灵活性的强大方法，且不会为了灵活性而牺牲安全性。

Apache 还有另一个在资源利用上更好，并且能为 cgi 程序提供相同安全性的功能。该功能被称为 `suExec`。在 Linux 随带的版本中，`suExec` 功能是不可用的。为了使用此功能，你需要从源码重新编译 Apache。涵盖该过程涉及的所有步骤超出了本书的范畴。如果你管理着许多服务器并希望 cgi 程序以虚拟域名所有者的身份运行，请查看参考资料以获取 Apache 关于 `suexec` 功能文档的链接。
