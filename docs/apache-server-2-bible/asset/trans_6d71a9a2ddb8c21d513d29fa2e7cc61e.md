

# AddDefaultCharset

AddDefaultCharset 应设置为最适合您本地需求的字符集。如果您不知道该使用哪种字符集，可以保留默认设置，查明应该使用的字符集，之后再修改默认值。

## 启动和停止 Apache

在您自定义了 httpd.conf 之后，就可以运行服务器了。对于本节，假设您采纳了我在上一章中的建议（即将 --prefix 设置为 /usr/local/apache）。如果您没有采纳我的建议，请确保在以下讨论中，将所有对 /usr/local/apache 的引用替换为适合您的路径。

### 启动 Apache

运行 /usr/local/apache/bin/apachectl start 命令以启动 Apache Web 服务器。如果 apachectl 报告语法错误，您应该修复 httpd.conf 文件中的错误并重试。

此外，请检查 %ErrorLog% 日志文件（即 /usr/local/apache/logs/error_log）以查找错误消息（如果有）。如果您在日志文件中看到错误，需要先修复它们。最常见的错误包括：

- 未以 root 用户身份运行服务器。您必须以 root 用户身份启动 Apache。Apache 启动后，会生成子进程，这些子进程将使用 User 和 Group 指令指定的 UID 和 GID。大多数人对这个问题感到困惑，试图使用 User 指令中指定的用户账户来启动服务器。
- Apache 抱怨无法“绑定”到某个地址。要么另一个进程已经占用了您配置 Apache 使用的端口，要么您是以普通用户身份运行 httpd 但试图使用 1024 以下的端口（例如默认端口 80）。
- 缺少日志文件路径。请确保 %ErrorLog% 和 %CustomLog% 路径存在，并且除了 Apache 服务器外，任何人都不可写。
- 配置拼写错误。每次修改 httpd.conf 配置文件时，运行 /usr/local/apache/apachectl configtest 以验证配置文件中没有语法错误。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_80_0.png)

**提示**

检查服务器是否正在运行的最快方法是尝试运行此命令：

```
ps auxx | grep httpd
```

该命令使用 ps 实用程序列出所有处于进程队列中的进程，然后将此输出管道传输到 grep 程序。grep 在输出中搜索与关键字 **httpd** 匹配的行，然后显示每个匹配的行。如果您看到一行包含 *root* 字样，那就是您的主要 Apache 服务器进程。请注意，当服务器启动时，它会创建多个子进程来处理请求。如果您以 root 用户身份启动 Apache，父进程将继续以 *root* 身份运行，而子进程则按照 *httpd.conf* 文件中的指示切换为用户。如果您在 Linux 上运行 Apache，可以创建 Listing 3-2 中显示的脚本，并将其保存在 */etc/rc.d/init.d/* 目录中。此脚本允许您在系统重启时自动启动和停止 Apache。

# 清单 3-2：httpd 脚本

```
#!/bin/sh
#
# httpd  此 shell 脚本用于启动和停止 Apache 服务器
# 它接受 'start' 或 'stop' 参数，相应地
# 启动和停止服务器进程。
#
# 注意：您可能需要更改脚本中使用的路径信息，
# 以反映您系统的配置。

APACHECTL=/usr/local/apache/bin/apachectl

[ -f $APACHECTL ] || exit 0

# 查看脚本是如何被调用的。
case "$1" in
    start)
        # 启动守护进程。
        echo -n "Starting httpd: "
        $APACHECTL start
        touch /var/lock/subsys/httpd
        echo
        ;;
    stop)
        # 停止守护进程。
        echo -n "Shutting down httpd: "
        $APACHECTL stop
        echo "done"
        rm -f /var/lock/subsys/httpd
        ;;
    *)
        echo "Usage: httpd {start|stop}"
        exit 1
esac
exit 0
```

> **提示**
>
> 要在系统启动时自动启动 Apache，只需运行一次此命令：
>
> `ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/S99httpd`
>
> 该命令在 `/etc/rc.d/rc3.d`（运行级别 3）目录中创建一个名为 `S99httpd` 的特殊链接，指向 `/etc/rc.d/init.d/httpd` 脚本。当系统启动时，该脚本将以 `start` 参数执行，从而自动启动 Apache。

### 重启 Apache

要重启 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl restart` 命令。

您也可以如下使用 `kill` 命令：

```
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

当使用 `apachectl restart` 或通过 `kill` 使用 `HUP` 信号重启时，父 Apache 进程（以 root 用户运行）会终止其所有子进程，读取配置文件，并根据需要重启新一代的子进程。

> **注意**
>
> 这种重启方式对于当时由仍存活的子进程提供服务的 Web 客户端来说是突然的。因此，您可能需要考虑使用 `apachectl` 的 `graceful` 选项代替 `restart`，以及在 `kill` 命令中使用 `WINCH` 代替 `HUP` 信号。在这两种情况下，父 Apache 进程都会通知其子进程完成当前请求，然后终止，以便它可以重新读取配置文件并重启一批新的子进程。在繁忙的站点上，这可能需要一些时间。

### 停止 Apache

您可以在系统重启时自动停止 Apache，或在任何时间手动停止它。以下部分将讨论这两种停止 Apache 的方法。

## 自动停止 Apache

要在系统重启时自动终止 Apache，请运行一次此命令：

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

该命令确保在系统关闭时，以 `stop` 参数运行 `httpd` 脚本。

## 手动停止 Apache 服务器

要停止 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl stop` 命令。

Apache 服务器还为您方便地查找根 Web 服务器进程的 PID。该 PID 写入分配给 `PidFile` 指令的文件中。这是主 `httpd` 进程的 PID。不要尝试手动逐个终止子进程，因为父进程会在需要时重新创建它们。停止 Apache 服务器的另一种方法是运行：

```
kill `cat /usr/local/apache/logs/httpd.pid`
```

该命令使用 `-TERM` 信号（即 -15）运行 `kill` 命令，针对由 `cat /usr/local/apache/logs/httpd.pid`（即 `cat %PidFile%`）命令返回的进程 ID。

# 测试 Apache

在启动 Apache 服务器后，请使用合适的主机名通过 Web 浏览器访问它。例如，如果您在服务器本身上运行 Web 浏览器，则使用 `http://localhost/` 访问服务器。但是，如果您想从远程主机访问服务器，请使用服务器的完全限定主机名。例如，要访问名为 `apache.pcn1td.com` 的服务器，请使用 `http://apache.pcn1td.com`。如果您将 `Port` 指令设置为非标准端口（即 80 以外的端口），请记得在 URL 中包含 `:port`。例如，`http://localhost:8080` 将访问 8080 端口上的 Apache 服务器。

如果您没有对默认的 `htdocs` 目录进行任何更改，您将看到如图 3-4 所示的页面。该页面随 Apache 发行版一起提供，需要替换为您自己的内容。

最后，您需要确保日志文件正确更新。要检查您的日志文件，请输入 `log` 目录并运行以下命令：

```
tail -f `path_to_access_log`
```

该命令中的 `tail` 部分是一个 Unix 实用程序，允许查看正在增长的文件（当指定 -f 选项时）。请确保将 `path_to_access_log` 更改为访问日志的完全限定路径名。现在，使用 Web 浏览器访问该站点；如果您已经在该站点上，只需重新加载当前在浏览器上的页面。您应该看到屏幕上添加了条目。多按几次重新加载按钮，以确保访问文件适当更新。如果您看到更新的记录，您的访问日志文件正在正常工作。按 Ctrl+C 退出 `tail` 命令会话。如果您没有看到文件中的任何新记录，应该检查日志文件及其所在目录的权限设置。

