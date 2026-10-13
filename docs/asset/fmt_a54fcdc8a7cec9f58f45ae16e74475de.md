
其中 `latest_apache.rpm` 是最新 Apache RPM 的名称。有关使用 RPM 安装包的更多信息，请参阅第 8 章。

Apache RPM 将文件安装在以下目录：

- `/etc/httpd/conf/` — 此目录包含 Apache 配置文件 `httpd.conf`。请查看本章后文关于配置 Apache 的部分以获取信息。
- `/etc/rc.d/` — 此目录下的树包含系统启动脚本。Apache RPM 为 Web 服务器安装了一个名为 `httpd` 的启动脚本。你可以使用该脚本从命令行启动和停止服务器，它会在计算机停止、启动或重启时自动启动和停止服务器。
- `/var/www` — RPM 在此位置安装默认服务器图标、通用网关接口 `CGI` 程序和 HTML 文件。如果你想将 Web 内容保存在其他地方，可以通过在服务器配置中进行适当的更改来实现。
- `/var/html/manual/` — 如果你安装了 `apache-manual` RPM。
- `/usr/share/man/` — 如果你安装了 `apache-manual` RPM。
- `/sbin/` — 如果你安装了 `apache-manual` RPM。
- `/bin/` — 如果你安装了 `apache-manual` RPM。
- `/var/log/httpd/` — 如果你安装了 `apache-manual` RPM。
- `/var/run/` — 如果你安装了 `apache-manual` RPM。
- `/etc/httpd/` — 如果你安装了 `apache-manual` RPM。
- `/var/www/` — 如果你安装了 `apache-manual` RPM。

![](img/446debe023486a07fde575245cf7a3ff_540_0.png)

- `/usr/local/apache2` — `cgi-bin`、`icons` 和 `hdocs` 子目录分别包含 CGI 程序、标准图标和默认 HTML 文档。
- `/usr/local/apache2/bin` — 可执行程序被放置在此目录中。
- `/usr/local/apache2/logs` — 服务器日志文件放置在此目录中。默认情况下，有两个日志文件——`access_log` 和 `error_log`——但你可以定义任意数量的自定义日志，其中包含各种信息（请参阅本章稍后的“日志（Logging）”部分）。由 Red Hat Linux 安装的 Apache 日志默认位置为 `/var/log/httpd`。

# Apache 快速上手指南

使用 Red Hat Linux 设置、测试 Web 页面并启动 Apache 可以通过几个步骤完成。首先，确保你的系统中已安装了 Apache，这可以在安装过程中选择它，或者安装 Red Hat 的 `httpd` 及其 RPM 文件（如果需要安装服务器软件，请参阅第 8 章）。

接下来，通过编辑你系统上 `/var/www/html` 目录下的 `index.html` 文件（以 root 身份）为你的系统设置一个页面。在开始之前，请对原始页面或 www 目录进行备份复制，以便在必要时将 Web 服务器恢复到默认状态。

使用 `service` 命令（再次以 root 身份）配合关键字 `httpd` 和 `start` 来启动 Apache，如下所示：

```bash
# service httpd start
```

你也可以使用 `/etc/rc.d/init.d/` 目录下的 `httpd` 脚本，如下所示：

```bash
# /etc/rc.d/init.d/httpd start
```

你可以通过运行喜欢的浏览器并在统一资源定位符（URL）中使用 `localhost`、你的系统主机名或其互联网协议（IP）地址来检查你的主页。例如，使用 `links` 文本浏览器，可以使用命令行：

```bash
# links http://localhost/
```

请注意，出于安全考虑，如果你的主机连接到互联网或公司内网，你不应该以 root 身份启动和运行 Apache。幸运的是，无论如何启动，Apache 都会设置为以 `apache` 用户和组身份运行（通过 `/etc/httpd/httpd.conf` 中的用户和组设置）。在这种安全的默认情况下，Apache 应该由用户名（定义在 `/etc/passwd` 中）启动和管理。在你对 Web 网站满意后，使用 `setup`（选择 Services）或 `ntsysv`（选择 `httpd`）命令来确保 Apache 正确启动。

# 启动和停止 Apache

此时，你已经使用默认配置安装了 Apache 服务器。Red Hat Linux 在 `/var/www/html` 目录下提供了一个名为 `index.html` 的默认主页作为测试。运行 Apache 的正确方法是设置 Red Hat 系统初始化，使其在启动、网络配置以及任何防火墙配置之后运行服务器。有关 Red Hat 引导的更多信息，请参阅第 7 章“管理服务（Managing Services）”。

是时候首次启动它了。以下章节将展示如何启动和停止 Apache，或者配置 Red Hat Linux 在启动时或不启动 Apache。

## 手动启动 Apache 服务器

你可以从基于文本的控制台命令行或 X 终端窗口启动 Apache。服务器守护进程 `httpd` 识别了你可以使用的几个命令行选项，用于设置某些默认值，例如指定 `httpd` 从何处读取配置指令。Apache `httpd` 可执行文件还理解其他选项，允许你选择性地使用配置文件的部分、指定不同的配置文件（可能用于测试）以及将启动错误输出到特定的日志。`-v` 选项导致 Apache 打印其开发版本并退出。`-V` 选项显示服务器编译时生效的所有设置。

`-h` 选项打印服务器的用法信息：

```bash
# httpd -h
Usage: httpd [-D name] [-d directory] [-f file]
[-C "directive"] [-c "directive"]
[-k start|stop]
```

# 使用 Red Hat 的 service 控制 Apache

与其直接调用 `/etc/rc.d/init.d/httpd` 脚本，你也可以使用 Red Hat 的 `service` 命令来启动、停止和重启 Apache。`service` 命令配合服务名称（列在 `/etc/rc.d/init.d` 下）以及可选关键字使用：

```bash
# service <name_of_script> <option>
```

例如，你可以像这样使用 `service` 配合 `httpd` 以及上一节讨论过的任何选项：

```bash
# service httpd restart
```

如果 Apache 正在运行，这会重启它；如果没有运行，则会启动服务器。

# 使用 Red Hat 的 chkconfig 命令控制 Apache

`chkconfig` 命令为 Red Hat 的服务脚本提供了基于命令行界面。该命令用于列出并控制在特定系统状态（如启动、重启或关机时）和运行级别（如单用户模式、带多任务的网络模式或带有 X 的图形化登录）下哪些服务将启动、重启和停止。

例如，要查看当前设置，可以使用 `grep` 命令查看系统初始化表 `/etc/inittab` 中定义的 Red Hat 默认运行级别：

```bash
# grep id /etc/inittab
id:3:initdefault:
```

此示例显示该 Red Hat Linux 系统将启动到基于文本的登录界面而不运行 X11。你可以使用 `chkconfig` 命令查看 Apache 在该运行级别下的行为：

```bash
# chkconfig --list | grep httpd
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

在这里你可以看到 Apache 在运行级别 3 和 5 下是关闭的（这是默认 Red Hat 系统中唯一的两个级别，尽管你可以为 Apache 创建自定义的运行级别 4）。使用 `level`、`httpd` 和控制关键字 `set` 配合 `on`，让 Apache 在启动到运行级别 3 时自动启动：

```bash
# chkconfig --level 3 httpd on
```

# 第 16 章 Apache Web 服务器管理

你可以再次使用 `chkconfig` 来验证此设置。

```bash
# chkconfig --list | grep httpd
httpd      0:off 1:off 2:off 3:on 4:off 5:off 6:off
```

为了让 Apache 在系统使用 X 启动到图形登录时也启动，再次使用 `level`、`httpd` 和当前关键字 `on`，但这次要指定运行级别 5，如下：

```bash
# chkconfig --level 5 httpd on
```
