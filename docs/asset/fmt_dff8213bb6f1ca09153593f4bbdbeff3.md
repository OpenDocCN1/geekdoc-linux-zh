
- 命名目录及其所有子目录将被索引。换句话说，如果有索引文件，将显示它；如果没有索引文件，服务器将创建一个动态索引。`Options` 指令规定了这一点。

- 命名目录及其所有子目录允许跟踪（即作为路径）符号链接以访问信息。`Options` 指令也规定了这一点。

- 目录容器指定的选项可以通过本地访问控制文件覆盖（由 `s.conf` 中的 `AccessFileName` 指定；使用 `AllowOverride` 指令指定）。

- 允许所有访问。

在早期阶段，默认设置应该足够。但如果你的服务器在互联网上，你可能想从 `Options` 指令行移除 `FollowSymLinks` 选项。这样做会导致潜在的安全风险。例如，如果你的 Web 网站中的某个目录没有索引页面，服务器将显示一个自动索引，显示该目录中的任何符号链接。这可能会导致敏感信息的泄露，甚至允许任何人运行位于疏于链接目录中的可执行文件。

列表 12-4 中的最后一个配置段禁用了名为 `/usr/local/apache/share/cgi-bin` 的特殊目录的所有选项和目录（`htaccess`）覆盖。这是存放分发 CGI 脚本的目录。因为 CGI 脚本的内容不需要被浏览或通过目录索引提供，所以没有必要对该目录允许任何目录控制；因此，默认设置是移除所有选项。

## 控制 Apache 服务器

`Apache1.3.r` 自带了一个非常实用的 shell 脚本 `apachectl`，它可以使用多种方式控制服务器。在本节中，我将详细讨论该脚本。

## 第12 章：Web 服务

然而，在控制 Apache 之前，你必须成为系统的超级用户，除非你已配置 Apache 运行在 1023 以上的端口。

请注意，如果你为 `httpd` 正确设置了 `inetd` 配置，无需执行任何操作即可启动或停止 Apache 服务器，因为 `inetd` 在收到对 HTTP 端口的访问请求时会运行它。

### 启动服务器

要启动服务器，只需按如下方式运行 `/apachectl` 脚本：

```bash
/path/to/your/apache/sbin/dir/apachectl
```

如果你希望服务器在系统重启后自动启动，你应该将上述行添加到 `/etc/rc.local` 或 `rc.d` 目录下的类似文件中。请使用列表 12-5 中的脚本分别在启动和重启时自动启动和关闭 Apache。

#### 列表 12-5：httpd.sh 脚本

```bash
#!/bin/sh

# httpd 此 shell 脚本用于启动和停止 Apache 服务器
# 它接受参数 'start' 或 'stop' 来分别启动和
# 停止服务器进程。
#
# 注意：你可能需要更改脚本中使用的路径信息
# 以反映你系统的配置。
#
[ -f /usr/local/apache/sbin/apachectl ] || exit 0

# 查看脚本是如何被调用的。
case "$1" in
  # 启动守护进程。
  echo -n "Starting httpd:"
  /usr/local/apache/sbin/apachectl
  touch /var/lock/subsys/httpd
  echo
  ;;
stop)
  # 停止守护进程。
  echo -n "Shutting down httpd:"
  /usr/local/apache/sbin/apachectl stop
  echo "done"
  rm -f /var/lock/subsys/httpd
  ;;
  *)
  echo "Usage: httpd {start|stop}"
  ;;
esac
exit 0
```

我将此脚本放在了 `/etc/rc.d/init.d/` 目录下，并创建了以下符号链接：

```
/etc/rc.d/rc3.d/S80httpd -> /etc/rc.d/init.d/httpd.sh
/etc/rc.d/rc3.d/K80httpd -> /etc/rc.d/init.d/httpd.sh
```

当系统启动时，它会自动加载 Apache 服务器。脚本会在系统关机和重启时停止 Apache 服务器。

### 停止服务器

要停止服务器，只需按如下方式运行 `apachectl` 脚本：

```
/path/to/your/apache/sbin/dir/apachectl stop
```

### 重启服务器

要重启服务器，只需按如下方式运行 `apachectl` 脚本：

```
/path/to/your/apache/sbin/dir/apachectl restart
```

要执行平滑重启，按如下方式运行 `apachectl` 脚本：

```
/path/to/your/apache/sbin/dir/apachectl graceful
```

对于好奇的读者来说，`restart` 命令向 Apache 发送 `SIGHUP` 信号，而 `graceful` 命令则发送 `SIGUSR1` 信号。由于后者是用户定义的（即由 Apache 开发人员定义），它对正在运行的服务器要友好得多。

#### 获取服务器的完整状态

在获取服务器的完整状态之前，你需要确保系统已安装了 Lynx 文本 Web 浏览器。你可以从以下 URL 获取这个巧妙的浏览器：`http://lynx.browser.org/`

一旦安装了 Lynx，你就可以按如下方式运行 `apachectl` 脚本来获取运行服务器的完整状态：

```
/path/to/your/apache/sbin/dir/apachectl fullstatus
```

## 第12 章：Web 服务

你将得到一个充满信息的页面，显示了各种服务器状态数据。将状态信息重定向到文件中可能是一个好主意，因为其内容很可能超过一个全屏。以下是将数据重定向到名为 `/tmp/status` 文件的方法：

```
/path/to/your/apache/sbin/dir/apachectl fullstatus > /tmp/status
```

#### 检查服务器配置文件

为了测试服务器配置文件的是否存在语法错误，你可以按如下方式运行 `apachectl` 脚本：

```
/path/to/your/apache/sbin/dir/apachectl configtest
```

#### 测试 Apache 服务器

运行你喜欢的 Web 浏览器，并将其指向运行你新配置的 Apache 服务器的网站。如果你在运行 Apache 的同一系统上运行 Web 浏览器，可以使用 URL：`http://localhost`。

然而在所有其他情况下，你需要指定精确的主机名（例如 `www.company.com`）。如果你没有对默认 `httpdocs` 目录进行任何更改，你将看到一个显示“It Works! 此页面是 Apache 发行版的一部分，需要用你自己的内容更改”的页面。

最后，你想确保日志文件已正确更新。要检查日志文件，请进入日志目录并运行以下命令：

```bash
tail -f [/path/to/access_log]
```

命令中的 `tail` 部分是一个允许查看不断增长的文件的实用程序（当指定了 `-f` 选项时）。现在，使用 Web 浏览器访问该站点，或者如果你已经在那里，请刷新你当前在浏览器中打开的页面。你应该看到浏览器中添加了一个条目。你应该看到浏览器中添加了一个条目。你应该看到浏览器中添加了一个条目。

# 第四部分：设置内网/互联网服务

允许任何人浏览目录内容。`AddHandler cgi-script .pl/cgi` 这一行告诉 Apache 将命名扩展名列表视为 CGI 程序扩展名（换句话说，每当 Apache 遇到请求具有其中一个命名扩展名的文件的 URL 时，它必须将其作为 CGI 程序执行）。

## 为你的用户启用 cgi-bin 访问

许多互联网服务提供商（ISP）提供带有用户账户的网站。这些网站通常有 URL，例如 `http://www.isp.net/~username`。

他们经常收到用户对 `cgi-bin` 访问的请求。“`cgi-bin` 访问”这一术语是一个通用术语，用于指 Web 服务器上的 CGI 功能。CGI 程序目录被别名为 `/cgi-bin/`，因此产生了这个术语。另一个变得非常流行的常用术语是“主页”（`home page`），它指的是用户 Web 目录的顶层索引页。

在本节中，我将讨论在 Apache Web 服务器上为用户提供 `cgi-bin` 访问的两种方法。你只需要实现其中一种方法。

使用 `DIRECTORY` 或 `DIRECTMATCH` 容器。当 `UserDir` 指令设置为一个目录名时，Apache 将其视为 Web 网站的顶层目录，例如：

```
ServerName www.yourcompany.com
UserDir public_html
```

现在，当 `www.yourcompany.com/~username` 的请求到达时，Apache 会找到指定的用户的家目录（通常通过检查 `/etc/passwd` 文件），然后附加 `UserDir` 指定的目录以创建顶层 Web 目录的路径。例如：

```
www.yourcompany.com/~joe
```
