
```sh
#!/bin/sh

echo -n 'utility'

case "$1" in

start)

  /usr/local/bin/utility

  ;

stop)

  kill -9 'cat /var/run/utility.pid'

  ;

es)

  echo "Usage: basename $0 {start|stop}" >&2

  exit 64

  ;

esac

exit 0
```

此脚本为此文简称为 `utility` 的应用程序提供了停止和启动选项。

可以通过以下命令手动启动：

```sh
# /usr/local/etc/rc.d/utility.sh start
```

虽然并非所有第三方软件都需要 `rc.conf` 中的该行，但几乎每天都有新端口会被修改以接受此配置。检查安装的最终输出以获取有关特定程序的更多信息。某些第三方软件带有启动脚本，允许应用程序配合 `rc.d` 使用；尽管将在下一节中讨论。

### 11.5.1 扩展应用程序配置

现在 FreeBSD 内部通过 `rc.d` 配置应用程序启动已变得更加简单且功能更强大。使用 `rc.d` 部分中使用的键，可以将应用程序设置为在其他服务（例如 DNS）之后启动；允许通过 `rc.conf` 传递额外的标志，以代替启动脚本中的硬编码标志。一个基础脚本可能如下所示：

```sh
#!/bin/sh

# PROVIDE: utility

# REQUIRE: DAEMON

# KEYWORD: shutdown

# 不要在此处更改这些默认值

# 在 /etc/rc.conf 文件中设置它们

utility_enable=${utility_enable:-NO}

utility_flags=${utility_flags:-"}

utility_pidfile=${utility_pidfile:-/var/run/utility.pid}

./etc/rc.subr

name='utility'

rcvar='set_rcvar'

command="/usr/local/sbin/utility"

load_rc_config $name

pidfile="${utility_pidfile}"

start_cmd=$(echo "Starting ${name}..."; /usr/bin/nice -5 ${command} ${utility_flags} ${command_args})

run_rc="$1"
```

此脚本将确保提供的工具在守护进程之后启动。它还提供了一种设置和跟踪 PID（或进程 ID 文件）的方法。
该应用程序可以在 `/etc/rc.conf` 中放置以下行：

`utility_enable="YES"`

这种方法还允许更方便地操作命令行参数，包含了 `/etc/rc.subr` 提供的默认函数，并与 `recorder(8)` 工具兼容，还通过 `rc.conf` 文件提供了更简便的配置。

### 11.5.2 使用服务启动服务

其他服务（如 POP3 服务器守护进程、IMAP 等）可以使用 `inetd(8)` 启动。这涉及从端口集合安装服务实用程序，并在 `/etc/inetd.conf` 文件中添加配置行，或取消当前某个配置行的注释。关于 `inetd` 及其配置的操作将在本节中详细描述。

在某些情况下，使用 `cron(8)` 守护进程启动系统服务可能更合理。这种方法许多优点，因为 `cron` 以 crontab 所有者的身份运行这些进程。这允许普通用户启动和维护某些应用程序。

`cron` 工具提供了一个独特的功能 `@reboot`，可以用来代替时间规范。这将导致任务在 `cron(8)` 启动时运行（通常在系统初始化期间）。

### 11.6 配置 cron 工具

*由 Tom Rhodes 贡献。*

FreeBSD 中最有用的工具之一是 `cron(8)`。`cron` 工具允许您按特定间隔调度任务。`crontab` 文件是定义这些任务的地方。`crontab` 文件的格式如下：

```
minute hour day month command
```

字段代表：
- `minute` (0-59)
- `hour` (0-23)
- `day` (1-31)
- `month` (1-12)
- `dow` (0-6)
- `command` (要执行的命令)

对于希望从头开始创建自己的 crontab 而不使用模板的用户，可以使用 `crontab -e` 选项。这将调用选定的编辑器并打开一个空文件。当文件保存时，它将由 `crontab` 命令自动安装。

如果你以后想完全删除你的用户 crontab，请使用带有 `-r` 选项的 `crontab`。

## 11.7 在 FreeBSD 5.X 及更高版本中使用 rc

由 Tom Rhodes 贡献。

2002 年，FreeBSD 集成了用于系统初始化的 FreeBSD `rc.d` 系统。用户应该注意 `/etc/rc.d` 目录下列出的文件。其中许多基本服务文件可以通过 `start`、`stop` 和 `restart` 选项进行控制。

```
# /etc/rc.d restart
```

此程序适用于其他服务。当然，服务通常按照 `rc.conf(5)` 中的指定在启动时自动启动。例如，在启动时启用网络地址转换（NAT）守护只需在 `/etc/rc.conf` 中添加以下行：

```
natd_enable=YES
```

如果已经存在 `natd_enable="NO"`，只需将 NO 改为 YES。如文所述，rc 脚本将在下次重启时自动加载任何其他依赖服务。

由于 `rc.d` 系统主要用于在系统启动/关闭启动/停止服务，标准的 `start`、`stop` 和 `restart` 选项只有在设置了相应的 `/etc/rc.conf` 变量时才会执行操作。例如，上面的 `ssh restart` 命令只有在 `/etc/rc.conf` 中将 `ssh` 设置为 YES 时才会生效。要忽略 `/etc/rc.conf` 启动、停止或重启服务，应带有 `/force` 执行命令。例如，要忽略当前的 `/etc/rc.conf` 设置重启 `sshd`，请执行以下命令：

```
# /etc/rc.d/sshd forcerestart
```

通过运行 `rcvar` 运行相应的 `rc.d` 脚本，可以很容易检查服务是否在 `/etc/rc.conf` 中启用。然而，管理员可以通过运行以下命令来检查 `ssh` 是否确实在 `/etc/rc.conf` 中已启用：

```
# /etc/rc.d/sshd rcvar
# ssh
$sshd_enable=YES
```

> 注意：第二行 (# sshd) 是 `sshd` 命令的输出，而不是 root 控制台的输出。

要确定服务是否正在运行，可以使用 `status` 选项。例如，验证 `sshd` 是否实际上正在运行：

```
# /etc/rc.d/sshd status
sshd is running as pid 433.
```
