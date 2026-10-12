
此目录中存储的图像用于在该目录中未找到 DirectoryIndex 指定的文件时显示动态目录列表。 除非您更改了图标目录的路径，否则应保持别名不变。 别名定义之后跟随的目录容器设置此图标目录的权限。 我不喜欢它通过将 Options 设置为 Indexes 来允许目录浏览（即动态目录索引）的想法，因此我建议您将 Options Indexes 改为 Options -Indexes。

## ScriptAlias

ScriptAlias 指令用于设置常用的 CGI 脚本别名目录 `/cgi-bin/`，使其指向 `/usr/local/apache/cgi-bin/`（即 `ServerRoot/cgi-bin/`）。 如果您计划从主服务器使用 CGI 脚本，请保留它，否则删除此指令。 或者，如果您想将 CGI 脚本目录移动到其他位置，请更改指令中给出的物理路径以匹配您的路径。

![](img/9eb7e89292d2f85707b4d49102c865b7_332_0.png)

> 切勿将 CGI 脚本路径设置为文档根目录内的目录（即 `DocumentRoot/somepath`），因为将 CGI 脚本保留在文档根目录下会使其面临各种潜在的安全问题。 将您的 CGI 脚本路径和 DocumentRoot 设置在同一级别。 例如，如果您将 DocumentRoot 设置为 `/a/b/c/htdocs`，则将 ScriptAlias 设置为指向 `/a/b/c/cgi-bin`，而不是 `/a/b/c/htdocs/cgi-bin` 或 `/a/b/c/htdocs/d/cgi-bin` 等。

接下来，`<Directory ...>` 容器对 ScriptAlias 目录施加限制，以确保不允许目录级选项。 在这里，Options 指令被设置为 None（这意味着 ScriptAlias 的内容不可浏览），ScriptAlias 目录内的符号链接不会被跟随，等等。

## Other directives

其余指令对于启动运行并不重要，因此我现在将忽略它们。 它们包括 IndexOptions、AddIconByEncoding、AddIconByType、AddIcon、DefaultIcon、ReadmeName、HeaderName、IndexIgnore、AddEncoding、AddLanguage、AddCharset、BrowserMatch、AddType。

然而，如果需要，您可能需要考虑更改的这两项其他指令是 LanguagePriority 和 AddDefaultCharset。

默认情况下，LanguagePriority 指令将默认语言设置为 en（英语），这可能不适合世界上的每个人。 因此，如果得到支持，您可能希望将默认语言更改为您自己的母语（支持许多语言，但并非全部）。 AddDefaultCharset 也应设置为最适合您本地需求的字符集。 如果您不知道应使用什么字符集，可以保留默认值，稍后再查明所需字符集并进行更改。

现在保存 httpd.conf 中的配置更改。

## Starting and Stopping the Server

在您自定义了 httpd.conf 后，您就可以运行服务器了。 我假设您已将 Apache 安装在 /usr/local/apache 目录中。 如果您未将 Apache 安装在此目录中，请确保在以下讨论中将 /usr/local/apache 的所有引用替换为您适当的目录。

## Starting Apache

运行 `/usr/local/apache/bin/apachectl start` 命令以启动 Apache Web 服务器。 如果 apachectl 抱怨一个或多个语法错误，您应该修复 httpd.conf 文件中的错误并重试。

同时检查 ErrorLog 日志文件（即 `/usr/local/apache/logs/error_log`）是否有错误消息（如果有）。 如果您在日志文件中看到错误，则需要先修复它们。 一些最常见的错误是：

- **未以 root 用户身份运行服务器。** 您必须以 root 用户身份启动 Apache。 一旦 Apache 启动，它将生成子进程，这些子进程将使用 User 和 Group 指令中指定的 UID 和 GID。 大多数人对这个问题感到困惑，并尝试使用 User 指令中指定的用户帐户启动服务器。
- **端口设置不正确。** 如果 Apache 抱怨无法“绑定”到地址，则要么另一个进程已在使用您配置 Apache 使用的端口，要么您以普通用户身份运行 httpd，但尝试使用 1024 以下的端口（如默认端口 80）。
- **缺少日志文件路径。** 确保 ErrorLog 和 CustomLog 路径都存在，并且只有 Apache 服务器可以写入。
- **配置拼写错误。** 只要您更改 httpd.conf 配置文件，您就可以运行 `/usr/local/apache/apachectl configtest` 来验证配置文件的语法是否正确。

检查服务器是否正在运行的最快方法是尝试以下命令：

```
ps auxw | grep httpd
```

此命令使用 ps 实用程序列出进程队列中的所有进程，然后将此输出通过管道传输到 grep 程序，后者搜索输出中与关键字 httpd 匹配的行并显示每条匹配行。 如果您看到一行中包含单词 root，则该行就是您的主 Apache 服务器进程。 请注意，服务器启动时，会创建多个子进程来处理请求。 如果您以 root 用户身份启动 Apache，父进程将继续以 root 身份运行，而子进程将更改为 httpd.conf 文件中指定的用户。

您可以创建如清单 12-1 所示的脚本并将其保存在 /etc/rc.d/init.d/ 目录中。

## Listing 12-1 The httpd script

```
#!/bin/sh
#
# httpd  This shell script starts and stops the Apache server
# It takes an argument 'start' or 'stop'
# to respectively start and stop the
# server process.
#
# Notes: You might have to change the
# path information used
# in the script to reflect your
# system's configuration.
#
```

## Listing 12-1 Continued

```
APACHECTL=/usr/local/apache/bin/apachectl

[ -f $APACHECTL ] || exit 0

# See how the script was called.
case "$1" in
    start)
        # Start daemons.
        echo -n "Starting httpd: "
        $APACHECTL start
        touch /var/lock/subsys/httpd
        echo
        ;;
    stop)
        # Stop daemons.
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

要使 Apache 在重新启动后自动启动，只需运行以下命令一次：

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/S99httpd
```

此命令在 /etc/rc.d/rc3.d（运行级别 3）目录中创建一个名为 S99httpd 的特殊链接，该链接指向 /etc/rc.d/init.d/httpd 脚本。 当系统启动时，此脚本将使用 start 参数执行，Apache 将自动启动。

要在系统重新启动时自动终止 Apache，请运行以下命令一次：

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

这可确保在系统关闭时使用 stop 参数运行 httpd 脚本。

## Stopping a standalone Apache server

要停止 Apache 服务器，请运行 /usr/local/apache/bin/apachectl stop 命令。 Apache 还使您方便地找到 root Web 服务器进程的 PID（进程 ID）。 PID 被写入分配给 PidFile 指令的文件中。 此 PID 用于主 httpd 进程。 请勿尝试手动杀死子进程——父进程会根据需要重新创建它们。

停止 Apache 服务器的另一种方法是运行以下命令：

```
kill -TERM `cat /usr/local/apache/logs/httpd.pid`
```

此命令使用 kill 命令并使用 -TERM 信号（即 -9）针对 cat /usr/local/apache/logs/httpd.pid（即 cat PidFile）命令返回的进程 ID。

## Restarting a standalone Apache server

要停止 Apache 服务器，请运行 /usr/local/apache/bin/apachectl restart 命令。

您可以使用 kill 命令，如下所示：

```
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

使用 apachectl restart 重新启动或使用 kill 命令配合 HUP 信号时，以 root 用户身份运行的父 Apache 进程会杀死所有子进程，读取配置文件，并根据需要重新启动新一代子进程。 这种类型的重启对当时由存活的子进程提供服务的 Web 客户端来说是突然的，因此您可能希望考虑使用 apachectl 的 graceful 而不是 restart 选项，并使用 kill 命令配合 WINCH 信号而不是 HUP 信号。

![](img/9eb7e89292d2f85707b4d49102c865b7_336_0.png)

这在繁忙的网站上可能需要一些时间。
