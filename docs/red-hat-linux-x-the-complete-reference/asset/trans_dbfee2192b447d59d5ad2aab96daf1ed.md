
## How chkconfig Works

chkconfig 工具通过在 /etc/rc.d 目录中的适当运行级别目录中创建启动和关闭链接来工作。例如，当 chkconfig 在运行级别 5 添加 httpd 服务时，它会在 /etc/rc.d/rc5.d 目录中创建一个链接，指向 /etc/rc.d/init.d 目录中的启动脚本 httpd。当它从运行级别 3 关闭 Web 服务时，它会在 /etc/rc.d/rc3.d 目录中创建一个关闭链接，使用 /etc/rc.d/init.d 目录中的脚本 httpd，以确保 Web 服务不会启动。在下面的示例中，用户在运行级别 5 打开 Web 服务（httpd），在 rc5.d 中创建启动链接 S85httpd，然后在运行级别 3 关闭 Web 服务，在 rc3.d 中创建关闭链接 K15httpd。

```
chkconfig --level 5 httpd on
ls /etc/rc.d/rc5.d/*httpd
    /etc/rc.d/rc5.d/S85httpd

chkconfig --level 3 httpd off
ls /etc/rc.d/rc3.d/*httpd
    /etc/rc.d/rc3.d/K15httpd
```

## Service Scripts: /etc/init.d

大多数使用 RPM Red Hat 软件包的服务器软件将自动安装启动脚本，并在适当的 rcN.d 目录中创建所需的链接，其中 N 为运行级别编号。启动脚本也可以用于在系统启动时希望运行的任何程序。要使此类程序自动启动，首先在 /etc/rc.d/init.d 目录中为其创建启动脚本，然后在 /etc/rc.d/rc3.d 和 /etc/rc.d/rc5.d 目录中创建指向该脚本的符号链接。关闭链接（K）还应放置在用于运行级别 6（重启）的 rc6.d 目录中。

## Service Script Functions

在后面的章节中展示了 Red Hat 系统上 httpd 使用的启动脚本的简化版本。你可以在 /etc/rc.d/init.d/httpd 示例的 case 语句下看到不同的选项：start、stop、status、restart 和 reload。如果未提供选项（*），则会显示脚本的使用语法。httpd 脚本首先执行一个脚本来定义这些启动脚本中使用的函数。带有 httpd 的 daemon 函数实际执行 /usr/sbin/httpd 服务器程序。

```
echo -n "Starting httpd: "
daemon httpd
echo
touch /var/lock/subsys/httpd
```

killproc 函数关闭守护进程。然后删除锁文件和进程 ID 文件（httpd.pid）：

```
killproc httpd
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
```

daemon、killproc 和 status 函数是 shell 脚本，定义在 functions 脚本中，该脚本也位于 init.d 目录中。functions 脚本在每个启动脚本开始时执行以激活这些函数。这些函数的列表在表 20-4 中提供。

```
. /etc/rc.d/init.d/functions
```

表 20-4：Init Script Functions

| Init Script Function | Description |
|---|---|
| daemon [+/-nicelevel] program [arguments] [&] | 启动守护进程，如果它尚未运行。 |
| killproc program [signal] | 向程序发送信号；默认情况下发送 SIGTERM，如果进程未停止，则发送 SIGKILL。它还会删除任何 PID 文件，如果可以的话。 |
| pidofproc program | 由另一个函数使用，用于确定程序的 PID。 |
| status program | 显示状态信息。 |

## Service Script Tags

启动脚本的开头包含用于配置服务器的标签。这些标签以初始 # 符号开头，用于向系统提供有关服务的运行时信息。标签在表 20-5 中列出，并附带启动函数。你输入一个前面带有 # 符号的标签，标签名称后跟冒号，然后是标签参数。例如，processname 标签指定正在执行的程序的名称，在此示例中为 httpd：

表 20-5：System V init Script Tags

| Init Script Tags | Description |
|---|---|
| # chkconfig: startlevellist startpriority endpriority | 必需。指定此服务的默认启动级别以及启动和结束优先级。 |
| # description [ln]: description of service | 必需。服务的描述，可使用字符续行。对任何新增行使用初始 #。使用 ln 选项，可以指定描述所写的语言。 |
| # autoreload: true | 可选。如果此行存在，守护进程会检查其配置文件，并在它们更改时自动重新加载。 |
| # processname: program | 可选，允许多个条目。脚本中启动的程序或守护进程的名称。 |
| # config: configuration-file | 可选，允许多个条目。指定服务器使用的配置文件。 |
| # pidfile: pid-file | 可选，允许多个条目。指定 PID 文件。 |
| # probe: true | 可选，用于代替 autoreload、processname、config 和 pidfile 条目，以自动探测并启动服务。 |

```
# processname: httpd
```

如果你的脚本启动多个守护进程，你应该为每个守护进程提供一个 processname 条目。例如，Samba 服务同时启动 smbd 和 nmbd 守护进程。

```
# processname: nmbd
```

标签部分的结束由空行表示。此行之后，任何以 # 开头的行都将被视为注释。chkconfig 行列出了服务应启动的默认运行级别，以及启动和停止优先级。以下条目列出运行级别 3、4 和 5，启动优先级为 85，停止为 15：

```
# chkconfig: 345 85 15
```

对于 description，你输入服务的简短说明，使用 \ 符号在换行前使用多行。

```
# description: Apache Web server
```

使用 config 标签指定服务器可能使用的配置文件。对于 Apache Web 服务器，可能有三个配置文件：

```
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

pidfile 条目指示服务器的进程 ID 所在的文件。

## Service Script Example

作为示例，这里展示了 Web 服务器启动脚本 /etc/rc.d/init.d/httpd 的简化版本。大多数脚本要复杂得多，特别是当确定服务器启动时可能需要的任何参数或变量时。此脚本与 Web 服务器守护进程 httpd 的名称相同：

```
#!/bin/sh
#
# Startup script for the Apache Web Server
#
# chkconfig: 35 85 15
# description: Apache is a World Wide Web server. \
# It is used to serve HTML files and CGI.
# processname: httpd
# pidfile: /var/run/httpd.pid
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
# Source function library.
. /etc/rc.d/init.d/functions

# See how we were called.
case "$1" in
start)
    echo -n "Starting httpd: "
    daemon httpd
    echo
    touch /var/lock/subsys/httpd
;;
stop)
    killproc httpd
    echo
    rm -f /var/lock/subsys/httpd
    rm -f /var/run/httpd.pid
;;
status)
    status httpd
;;
restart)
    $0 stop
    $0 start
;;
reload)
    echo -n "Reloading httpd: "
    killproc httpd -HUP
    echo
;;
*)
    echo "Usage: $0 {start|stop|restart}"
    exit 1
esac
exit 0
```

## Installing Service Scripts

用于 Internet 服务器的 RPM 打包版本包含该服务器的启动脚本。安装 RPM 软件包会将脚本安装到 /etc/rc.d/init.d 目录，并在运行级别目录中创建适当的链接，例如 /etc/rc.d/rc3.d。如果相反，你决定使用源代码文件创建服务器，则可以手动安装启动脚本。如果不存在启动脚本，首先复制 httpd 脚本——重命名它，然后编辑副本以将所有对 httpd 的引用替换为服务器守护进程程序的名称。然后将脚本副本放置在 /etc/rc.d/init.d 目录中，并在 /etc/rc.d/rc3.d 目录中为其创建符号链接。或者你也可以使用 redhat-config-services 在 /etc/rc.d/rc3.d 目录中创建链接。选择 File | Refresh Services。现在启动系统时，新服务器会自动启动，同时运行并等待请求。
