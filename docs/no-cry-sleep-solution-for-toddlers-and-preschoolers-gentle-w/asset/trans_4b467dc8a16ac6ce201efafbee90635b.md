

| Init Script Function | 描述 |
|---|---|
| daemon [+/-nicelevel] program [arguments] [&] | 启动守护进程，如果它尚未运行。 |
| killproc program [signal] | 向程序发送信号；默认发送 SIGTERM，如果进程未停止，则发送 SIGKILL。它还会删除任何 PID 文件，如果可以的话。 |
| pidofproc program | 由另一个函数使用，用于确定程序的 PID。 |
| status program | 显示状态信息。 |

## TABLE 20-4 Init Script Functions

## Service Script Tags

启动脚本的开头包含用于配置服务器的标签。这些标签以初始 # 符号开头，用于向系统提供有关服务的运行时信息。这些标签列在表 20-5 中，并附有启动函数。你输入一个标签，前面带 # 符号，标签名称后跟冒号，然后是标签

| Init Script Tags | 描述 |
|---|---|
| # chkconfig: startlevel list startpriority endpriority | 必需。指定此服务的默认启动级别以及启动和结束优先级。 |
| # description [ln]: description of service | 必需。服务的描述，使用 \ 字符续行。对任何新增行使用初始 #。使用 ln 选项，可以指定描述所写的语言。 |
| # autoreload: true | 可选。如果存在此行，守护进程会检查其配置文件，并在它们更改时自动重新加载。 |
| # processname: program | 可选，允许多个条目。脚本中启动的程序或守护进程的名称。 |
| # config: configuration-file | 可选，允许多个条目。指定服务器使用的配置文件。 |
| # pidfile: pid-file | 可选，允许多个条目。指定 PID 文件。 |
| # probe: true | 可选，用于代替 autoreload、processname、config 和 pidfile 条目，以自动探测并启动服务。 |

## TABLE 20-5 System V Init Script Tags

arguments. 例如，processname 标签指定正在执行的程序的名称，在此示例中为 httpd：

```
# processname: httpd
```

如果你的脚本启动多个守护进程，则应为每个守护进程提供一个 processname 条目。例如，Samba 服务同时启动 smbd 和 nmbd 守护进程。

```
# processname: nmbd
```

标签部分的结尾由一个空行表示。在此行之后，以 # 开头的任何行都将被视为注释。chkconfig 行列出了服务应启动的默认运行级别，以及启动和停止优先级。以下条目列出运行级别 3、4 和 5，启动优先级为 85，停止为 15：

```
# chkconfig: 345 85 15
```

对于 description，你输入服务的简短说明，使用 \ 符号在换行前使用多行。

```
# description: Apache Web server
```

使用 config 标签，你指定服务器可能使用的配置文件。对于 Apache Web 服务器，可能有三个配置文件：

```
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

pidfile 条目指示保存服务器进程 ID 的文件。

## Service Script Example

作为示例，这里展示了 Web 服务器启动脚本 /etc.rc.d/init.d/httpd 的简化版本。大多数脚本要复杂得多，特别是当确定服务器启动时可能需要的任何参数或变量时。此脚本与 Web 服务器守护进程 httpd 的名称相同：

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
```

