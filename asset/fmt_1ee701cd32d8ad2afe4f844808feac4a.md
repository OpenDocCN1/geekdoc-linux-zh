
`-h` 选项打印服务器的用法信息（假设你以 root 身份运行该命令）：

```
# httpd -h
Usage: httpd [-D name] [-d directory] [-f file]
[-C "directive"] [-c "directive"]
[-k start|restart|graceful|stop]
[-v] [-V] [-h] [-l] [-L] [-t]
```

### 选项

- `-D name`：为 `<IfName>` 指令定义一个名称
- `-d directory`：指定替代初始 `ServerRoot`
- `-f file`：指定替代 `ServerConfigFile`
- `-C "directive"`：在读取配置文件之前处理指令
- `-c "directive"`：在读取配置文件之后处理指令错误
- `-e level`：显示指定级别的启动错误（参见 `LogLevel`）
- `-E file`：将启动错误记录到文件
- `-v`：显示版本号
- `-V`：显示编译设置
- `-h`：列出可用命令行选项（本页）
- `-L`：列出已编译的模块
- `-t -D DUMP_VHOSTS`：显示解析设置（目前仅支持 vost 设置）
- `-t`：对配置文件运行语法检查

其他选项包括 Apache 的静态模块，或服务器的特殊、内置独立部分，以及可以与模块一起使用的选项。这些选项被称为配置指令和命令，用于控制静态模块的工作方式。注意，Apache 包含了近 50 个动态模块，即在服务器运行时可以选择性加载和使用的服务器软件部分。

`-t` 选项用于检查你的配置文件。在重启服务器之前运行此检查是一个好主意，特别是当你更改了配置文件时。此类测试是非常重要的，因为配置文件错误可能导致你的服务器在尝试重启时关闭。

> 注意：
> 当你从源码编译并安装 Apache 且不使用 Fedora 的 Apache RPM 文件时，请以 root 身份从命令行手动启动服务器（例如在测试时）。你这样做的原因如下：
> - 独立服务器使用默认 HTTP 端口（80 端口），且只有超级用户可以绑定低于 1024 的互联网端口。
> - 只有所有 root 的进程可以按照 Apache 的 `User` 和 `Group` 指令更改其 UID 和 GID。如果你在另一个 UID 下启动服务器，它将以启动进程的用户权限运行。
> 注意，以下某些示例显示了如何以 root 身份启动服务器，你应仅在安装 Apache 后进行测试时这样做。如果你使用 Fedora RPM 文件安装 Apache，Fedora 会配置为以 apache 用户运行网络服务。

# 使用 `/etc/rc.d/init.d/httpd`

Fedora 使用 `/etc/rc.d/init.d` 目录中的脚本来控制各种服务的启动和关闭，包括 Apache Web 服务器。为 Apache 服务器安装的主脚本是 `/etc/rc.d/init.d/httpd`，尽管实际工作是由 Apache 自带的 `apachectl` shell 脚本完成的。

> 注意：
> `/etc/rc.d/init.d/httpd` 是 shell 脚本，而不是位于 `/usr/sbin` 的 Apache 服务器。也就是说，`/usr/sbin/httpd` 是可执行文件（服务器）；`/etc/rc.d/init.d/httpd` 是使用另一个脚本 `apachectl` 来控制服务器的 shell 脚本。参见第 15 章有关 `/etc/rc.d/init.d` 下某些服务脚本的描述以及如何使用脚本作为 httpd 管理服务。

你可以使用 `/etc/rc.d/init.d/httpd` 脚本以及以下选项控制 Web 服务器：

- `start`：系统使用此选项在启动期间启动 Web 服务器。作为 root，你也可以使用此脚本启动服务器。
- `stop`：系统使用此选项优雅停止服务器。你应该使用此脚本而不是 `kill` 命令来停止服务器。
- `reload`：你可以使用此选项向 `httpd` 服务器发送 HUP 信号，使其重新加载。
- `restart`：你可以使用此选项重启服务器。
- `condstart`：该选项类似于 `start`，但仅在服务器未运行时启动。
- `status`：该选项显示服务器是否运行。

在 Fedora 之后，你可以使用 `/etc/rc.d/init.d/httpd` 脚本和以下选项来控制 Web 服务器：

- `start` — 系统在启动时使用此选项启动 Web 服务器。你作为 root 也可以使用此脚本启动服务器。
- `stop` — 系统使用此选项优雅地停止服务器。你应该使用此脚本，而不是 `kill` 命令来停止服务器。
- `reload` — 你可以使用此选项向 httpd 服务器发送 HUP 信号，使其重新加载。
- `restart` — 你可以使用此选项重启服务器。
- `condstart` — 该选项类似于 start，但仅在服务器未运行时启动。
- `status` — 该选项显示服务器是否运行。

例如，要检查服务器的状态，请使用：

```
# /etc/rc.d/init.d/httpd status
```

这将输出：

```
httpd (running)
```

这表示 Apache 正在运行。

除了前面的选项，`httpd` 脚本还提供以下功能：

- `help`：打印脚本的可用选项列表。
- `configtest`：对服务器配置进行简单测试，如果配置正确则报告 OK。你也可以使用 httpd 的 `-t` 选项，例如：

```
# httpd -t
```

- `fullstatus`：显示详细的状态报告。
- `graceful`：类似于 `restart` 参数，但不会中断连接。

> 提示：
> 如果你正在对各种配置文件进行大量更改，请使用 `reload` 选项。这可以在启动服务器时通过让重新读取文件来节省时间。

# 使用 service 命令控制 Apache

与其直接调用 `/etc/rc.d/init.d/httpd` 脚本，你可以使用 Red Hat 的 `service` 命令来启动、停止和重启 Apache。`service` 命令配合脚本名称（位于 `/etc/rc.d/init.d` 下）和关键字使用：

```
# service <脚本名称> <选项>
```

例如，你可以使用 `service` 配合上一节讨论的任何选项，如下：

```
# service httpd restart
```

这会在 Apache 运行时将其重启，如果未运行则启动服务器。

# 使用 chkconfig 命令控制 Apache

`chkconfig` 命令为 Fedora 服务脚本提供了一个基于命令行的接口。该命令用于列出并控制特定系统状态（如启动、重启或关闭）和运行级别（如单用户模式、带多任务的网络或带有 X11 的图形登录）下的软件服务。

例如，要查看系统的当前设置，请查看系统初始化表 `/etc/initab` 中定义的 Fedora 默认运行级别，使用 `grep` 命令：

```
# grep id: /etc/initab
id:3:initdefault:
```

此示例显示该 Fedora 系统启动到不运行 X11 的文本登录。然后你可以使用 `chkconfig` 命令查看 Apache 在运行级别下的行为：

```
# chkconfig --list grep httpd
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

# 第21 章 Apache Web 服务器管理

在这里你可以看到 Apache 在运行级别（runlevels）3 和 5 中是关闭的（这是默认 Fedora 系统中唯一的实际运行级别，尽管你可以为 Apache 创建一个自定义的运行级别 4）。使用 `--level`、`httpd` 和 `control` 关键字可以设置 Apache 在启动到运行级别 3 时自动启动：

```
# chkconfig --level 3 httpd
```

你可以再次使用 `chkconfig` 来验证此设置：

```bash
# chkconfig --list | grep httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:off 6:off
```

要让 Apache 在系统使用 X 启动图形化登录时启动，请使用 `level`、`httpd` 和 `control` 关键字 `on`，但这次要指定运行级别 5，如下：

```bash
# chkconfig --level 5 httpd
```

再次，使用以下命令验证你的系统设置：

```bash
# chkconfig --list | grep httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

使用 `off` 关键字可以停止 Apache 在特定的运行级别启动。

# 使用 Red Hat 的 system-config-services 客户端控制 Apache
