
第一个 `<Directory />` ... `</Directory>` 容器配置段非常严格；它只允许服务器跟随符号链接，并为从系统根目录开始的所有目录禁用基于目录的访问控制文件（`.htaccess`）。请保持此配置段不变。想法是既打开需要打开的东西，又锁定其他所有东西。例如，`<Directory "/usr/local/apache/htdocs">` ... `</Directory>` 配置段允许 `DocumentRoot` 目录的目录索引和 `FollowSymLinks` 功能。

你可能需要将目录 `/usr/local/apache/htdocs` 更改为你在 `httpd.conf` 文件中 `DocumentRoot` 指令中之前设置的参数。默认设置包括 `Options` 和 `AllowOverride` 等多个指令，告诉服务器以下内容：

- 指定的目录及其下的所有子目录可以被索引。换句话说，如果存在索引文件，则会显示它；如果没有索引文件，服务器会为该目录创建动态索引。`Options` 指令指定了这一点。
- 指定的目录及其下的所有子目录可以拥有服务器可以跟随的符号链接（即用作路径来访问信息）。`Options` 指令也指定了这一点。
- 目录容器中未指定的选项不能被本地访问控制文件（由 `srm.conf` 中的 `AccessFileName` 指令指定；默认是 `.htaccess`）覆盖。这是通过 `AllowOverride` 指令指定的。
- 允许所有人访问。

默认设置在此早期阶段应已足够。然而，如果你的服务器要放在互联网上，你可能希望从 `Options` 指令行中移除 `FollowSymLinks` 选项。保留此选项会造成潜在的安全风险。例如，如果你的网站中的某个目录没有索引页，服务器会显示一个自动索引，列出该目录中你可能拥有的任何符号链接。这可能导致敏感信息被显示，甚至可能允许任何人运行位于随意链接目录中的可执行文件。

`<Directory "/usr/local/apache/cgi-bin">` ... `</Directory>` 容器指定了 `/usr/local/apache/cgi-bin` 目录的选项：这是存放分发 CGI 脚本的目录。由于 CGI 脚本的内容不应被浏览或通过目录索引提供，因此无需在此目录上允许任何按目录的控制；因此，默认情况下会移除所有选项。

## 为独立服务器配置指令

默认 `httpd.conf` 文件中的以下指令仅对以独立模式运行的 Apache 有意义。

```
KeepAlive on | off
```

此指令启用或禁用 Apache 内置的 `KeepAlive` 功能。简单来说，`KeepAlive` 是一种允许服务器与客户端之间保持持久连接的功能。保持持久连接有助于加快内容传输速度，因为无需为每个请求建立新连接而浪费时间。保持默认设置不变，因为它是 HTTP 1.1 规范的一部分。

```
KeepAliveTimeout
```

此指令指定服务器在与客户端断开连接前等待后续连接的最长时间（以秒为单位）。保持默认设置不变。

### MaxClients 数量

此指令设置可支持的同时请求数量的限制。最大可能值为 256。如果你觉得需要处理超过 256 个同时连接，请编辑 `src/include/httpd.h` 头文件并将 `HARD_SERVER_LIMIT` 常量设置为所需限制。编译新服务器后，你将能够将此指令设置为所需限制。

### MaxKeepAliveRequests 数量

此指令指定每个 `KeepAlive` 连接要处理的请求的最大数量。保持默认设置不变。请注意，将值设置为 0 会禁用 `KeepAlive` 功能。

### MaxRequestsPerChild 数量

此指令设置子服务器进程在终止前将处理的请求数量的限制。如果你将值设置为 0，子服务器进程将永不终止。保持默认设置不变。

### MaxSpareServers 数量

此指令指定 Apache 将运行的备用（空闲）服务器的最大数量。你只有在运行 Apache 以托管非常繁忙的网站时才应尝试此指令。

此指令在 Apache 的 Windows 版本中无用。

### MinSpareServers 数量

此指令设置主服务器将保留的备用（空闲）服务器的最小数量。你只有在运行 Apache 以托管非常繁忙的网站时才应尝试此指令。Apache 可以自动调整负载，因此我建议你在此处不要使用很大的数字。

此指令在 Apache 的 Windows 版本中无用，因为它不使用服务器池来处理请求。

### Pidfile 路径/文件名

此指令用于指定存储主服务器 PID 信息的文件名。此文件可由脚本用来轻松确定主服务器的 PID。例如，如果 `PidFile` 设置如下：

```
PidFile /usr/local/apache/var/run/httpd.pid
```

我可以通过以下方式使用 `kill` 命令重启 Apache 服务器：

```
kill -HUP `cat /usr/local/apache/var/run/httpd.pid`
```

无论你将此文件保存在哪个目录，都要确保只有主服务器进程对该目录具有写权限。这是一个重大的安全问题；允许其他用户或进程写入该目录可能会使未经授权的人接管你的主 Web 服务器进程 UID，通常是 root 账户。

### ScoreBoardFile 路径/文件名

此指令设置为主服务器用于与其子服务器进程通信的文件名。这仅在少数操作系统平台上需要。如果你必须使用 `ScoreBoardFile`，则将其放在 RAM 磁盘上可能会提高速度。请参阅你的操作系统手册。

### StartServers 数量

此指令设置 Apache 启动时将启动的子服务器进程的初始数量。Apache 可以自动调整负载，因此你无需更改默认值。

## 控制 Apache 服务器

Apache 1.3.x 附带一个名为 `apachectl` 的便捷 shell 脚本，可用于以多种方式控制服务器。本节详细讨论此脚本。然而，在你能够控制 Apache 之前，必须成为系统上的超级用户，除非你已配置 Apache 在 1023 之上的端口上运行。

如果你正确设置了 `httpd` 的 `inetd` 配置，则无需执行任何操作即可启动或停止 Apache 服务器，因为 `inetd` 在收到 HTTP 端口的访问请求时会运行它。

### 启动服务器

要启动服务器，请按如下方式运行 `apachectl` 脚本：

`/path/to/apache/bin/apachectl start`

如果你希望服务器在系统重启后自动启动，请将前一行添加到你的 `/etc/rc.local` 文件或 `r.c.d` 目录中的类似文件。我使用清单 12-1 中所示的脚本分别在启动和重启时自动启动和关闭 Apache。

### 清单 12-1 httpd.sh 脚本

```sh
#!/bin/sh
# httpd This shell script starts and stops the Apache server
# It takes an argument 'start' or 'stop' to start and
# stop the server process, respectively.
#
# Notes: You might have to change the path information
# used
# in the script to reflect your system's configuration.
#
[ -f /usr/local/apache/bin/apachectl ] || exit 0

# See how the script was called.
case "$1" in
start)
    # Start daemons.
    echo -n "Starting httpd:"
    /usr/local/apache/bin/apachectl start
    touch /var/lock/subsys/httpd
    echo
    ;;
stop)
    # Stop daemons.
    echo -n "Shutting down httpd:"
    /usr/local/apache/bin/apachectl stop
    echo "done"
    rm -f /var/lock/subsys/httpd
    ;;
*)
    echo "Usage: httpd {start|stop}"
    exit 1
esac
exit 0
```

我将此脚本放在 `/etc/rc.d/init.d` 目录中并创建了以下符号链接：

`/etc/rc.d/rc3.d/S80httpd -> /etc/rc.d/init.d/httpd.sh`

`/etc/rc.d/rc3.d/K80httpd -> /etc/rc.d/init.d/httpd.sh`

系统启动时，它会自动加载 Apache 服务器。该脚本也在系统关机或重启时停止 Apache 服务器。

### 停止服务器

要停止服务器，请按如下方式运行 `apachectl` 脚本：

`/path/to/apache/bin/apachectl stop`

### 重启服务器
