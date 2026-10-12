

此脚本中的创建流程。只需添加一个 `mkdir` 命令来创建默认的 public_html 目录（如果你将其分配给 UserDir 指令），用作 Web 目录。添加 chmod 和 chown 命令，以授予 Web 服务器用户读取和执行该公共目录下文件和目录的权限。

你需要配置的最后一组指令用于设置网站中文件、目录和脚本等项目的访问权限。你需要修改的第一个指令具有如下语法：

```
<Directory "path"> . . . </Directory>
```

`<Directory>` 和 `</Directory>` 用于包裹一组指令。所包裹指令的作用范围仅限于指定的目录路径（包括子目录）；但是，你只能使用允许在目录上下文中使用的指令。指定的目录可以是目录的完整路径，也可以是通配符字符串。

第一个 `<Directory /> . . . </Directory>` 容器配置段限制非常严格；它使服务器仅跟随符号链接，并禁用从系统根目录开始的所有目录基于目录的访问控制文件（htaccess）。请保持此配置段不变。其理念是开放需要开放的内容，并锁定其他所有内容。例如，`<Directory "/usr/local/apache/htdocs"> . . . </Directory>` 配置段允许 DocumentRoot 目录进行目录索引并启用 FollowSymLinks 功能。

你可能需要将目录 /usr/local/apache/htdocs 更改为之前设置为 httpd.conf 文件中 DocumentRoot 指令参数的值。包含 Options 和 AllowOverride 等多个指令的默认设置告诉服务器以下内容：

- 指定的目录及其下所有子目录可以被索引。
- 换句话说，如果存在索引文件，它将显示；如果没有索引文件，服务器会为目录创建一个动态索引。Options 指令指定了这一点。
- 指定的目录及其下所有子目录可以拥有服务器可以跟随（即用作路径）以访问信息的符号链接。Options 指令也指定了这一点。
- 目录容器中指定的任何选项都不能被本地访问控制文件覆盖（由 *srm.conf* 中的 AccessFileName 指令指定；默认为 `.htaccess`）。这是使用 AllowOverride 指令指定的。
- 允许所有人访问。

在此早期阶段，默认设置应该足够了。然而，如果你的服务器将接入 Internet，你可能希望从 Options 指令行中移除 FollowSymLinks 选项。保留此选项会带来潜在的安全风险。例如，如果你网站中的某个目录没有索引页，服务器将显示一个自动索引，该索引会显示该目录中可能存在的任何符号链接。这可能导致敏感信息显示出来，甚至可能允许任何人运行位于随意链接目录中的可执行文件。

```
<Directory "/usr/local/apache/cgi-bin"> . . . </Directory>
```

`<Directory "/usr/local/apache/cgi-bin">` 容器指定了 /usr/local/apache/cgi-bin 目录的选项。这是存放分发 CGI 脚本的目录。由于 CGI 脚本的内容不应被浏览或通过目录索引提供访问，因此无需允许对该目录进行任何基于目录的控制；因此，默认是移除所有选项。

## 为独立服务器配置指令

默认 *httpd.conf* 文件中的以下指令仅在 Apache 以独立模式运行时才有意义。

### KeepAlive on | off

此指令启用或禁用内置于 Apache 的 KeepAlive 功能。简单来说，KeepAlive 是一种允许服务器和客户端之间保持持久连接的功能。拥有持久连接有助于加快内容传递速度，因为无需为每个请求花费时间建立新连接。请保持默认设置不变，因为它是 HTTP 1.1 规范的一部分。

### KeepAliveTimeout

此指令指定服务器在断开与客户端连接之前等待后续连接的最大时间（以秒为单位）。请保持默认设置不变。

### MaxClients _number_

此指令设置可以同时支持的最大请求数限制。最大可能值为 256。如果你认为需要处理超过 256 个并发连接，请编辑 `src/include/httpd.h` 头文件并将 HARD_SERVER_LIMIT 常量设置所需的限制。编译新的服务器后，你将能够将此指令设置为所需的限制。

### MaxKeepAliveRequests _number_

此指令指定每个 KeepAlive 连接要处理的最大请求数。请保持默认设置不变。注意，将值设置为 0 会禁用 KeepAlive 功能。

### MaxRequestsPerChild _number_

此指令设置子服务器进程在终止之前将处理的请求数限制。如果你将值设置为 0，子服务器进程将永远不会终止。请保持默认设置不变。

### MaxSpareServers _number_

此指令指定 Apache 将保留的最大备用（空闲）服务器数量。只有在你运行 Apache 来托管非常繁忙的 Web 网站时，才尝试使用此指令。Apache 可以自动调整负载，所以我建议不要在此使用较大的数值。此指令对 Windows 版本的 Apache 毫无用处，因为它不使用服务器池来处理请求。

### PidFile _path/filename_

此指令用于指定一个用于存储主服务器 PID 信息的文件名。脚本可以使用此文件轻松确定主服务器的 PID。例如，如果 PidFile 设置如下，

```
PidFile /usr/local/apache/var/run/httpd.pid
```

我可以使用 kill 命令通过以下方式重启 Apache 服务器：

```
kill -HUP `cat /usr/local/apache/var/run/httpd.pid`
```

无论你将在哪个目录中保存此文件，请确保只有主服务器进程在该目录中具有写访问权限。这是一个主要的安全问题；允许其他用户或进程写入此目录可能会让未经授权的人接管你的主 Web 服务器进程 UID，这通常是 root 账户。

### ScoreBoardFile path/filename

此指令设置为一个文件名，主服务器使用该文件与其子服务器进程进行通信。不建议使用此指令。

### StartServers number

此指令设置 Apache 在启动时启动的初始子服务器进程数。Apache 可以自动调整负载，因此你不需要更改默认值。

## 控制 Apache 服务器

可以使用 apachectl 脚本以多种方式控制服务器。本节详细讨论此脚本。但是，在控制 Apache 之前，你必须成为系统超级用户，除非你已配置 Apache 在 1023 以上的端口上运行。

如果你正确设置了 httpd 的 inetd 配置，则无需执行任何操作来启动或停止 Apache 服务器，因为当 inetd 收到 HTTP 端口的访问请求时，它会运行该服务。

### 启动服务器

要启动服务器，请按如下方式运行 apachectl 脚本：

```
/path/to/apache/bin/apachectl start
```

如果你希望服务器在系统重启后自动启动，请将上一行添加到你的 `/etc/rc.local` 文件或 `rc.d` 目录中的类似文件中。我使用清单 12-1 中显示的脚本在启动和重启时分别自动启动和关闭 Apache。

### 清单 12-1 httpd.sh 脚本

```sh
#!/bin/sh
#
# httpd  此 shell 脚本启动和停止
# Apache 服务器。
# 它接受 'start' 或 'stop' 参数，分别用于
# 启动和停止服务器进程。
#
# 注意：你可能需要更改脚本中使用的
# 路径信息，以反映你系统的配置。
#
[ -f /usr/local/apache/bin/apachectl ] || exit 0

# 查看脚本是如何被调用的。
case "$1" in
start)
    # 启动守护进程。
    echo -n "Starting httpd:"
    /usr/local/apache/bin/apachectl start
    touch /var/lock/subsys/httpd
    echo
    ;
stop)
    # 停止守护进程。
    echo -n "Shutting down httpd:"
    /usr/local/apache/bin/apachectl stop

    echo "done"
```

