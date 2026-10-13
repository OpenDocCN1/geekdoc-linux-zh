
- `D` `ERROR_LOG`=`"/var/log/httpd/error_log"`

- `D` `TYPES_CONFIG_FILE`=`"/etc/httpd/mime.types"`

- `D` `SERVER_CONFIG_FILE`=`"/etc/httpd/httpd.conf"`

- `D` `ACCESS_CONFIG_FILE`=`"/etc/httpd/access.conf"`

- `D` `RESOURCE_CONFIG_FILE`=`"/etc/httpd/conf/srvm.conf"`

Apache 在配置文件 `httpd.conf`（由 `SERVER_CONFIG_FILE` 变量定义）中查找设置。使用 `-f` 命令行标志覆盖配置文件的位置：

```
# httpd -f /etc/httpd/httpd.conf
```

> 注意：这些标志适用于 Apache 1.，并随 Apache 的后续发布而变化。请访问 www.apache.org 获取更新。

其他 httpd 运行时标志包括：

```
# httpd -h

Usage: httpd [-D name] [-d directory] [-f file]

[-C "directive"] [-c "directive"] [-v] [-h] [-l] [-S] [-T]
```

## 启动时启动 httpd

大多数用户希望 Apache 在系统启动时自动启动。每个 Linux 发行版都有不同的实现方法；某些 RPM 和 DEB 包可能会将 Apache 添加到启动脚本；其他则不会。在 Red Hat 6.2 系统上，除非与操作系统同时安装，否则 RPM 可能不会设置 Apache 启动。要启用启动功能，启动脚本通常位于 `/etc/rc.d`。假设 Apache 安装在 `/www/`，添加以下条目：

```
/www/apachectl start
```

## 设置 Apache

大部分 Apache 设置都是通过 `httpd.conf` 文件完成的。如果在配置期间 Apache 运行，必须采取某些步骤。这些步骤在后续章节中概述。

## 启动和停止 Apache

当用户更改服务器（例如修改 `httpd.conf`）时，应重启 Apache 使更改生效。Apache 自带了 `apachectl` 脚本可用于此目的。`apachectl` 的工作原理类似于发行版在 `/etc/rc.d/init.d` 目录中的脚本。指定 `start` 和 `restart` 来启动或停止 Apache 服务器。

## 手动启动 httpd

要使用 `apachectl`，提供脚本路径以便使用 `apachectl`。在不提供任何选项的情况下，`apachectl` 将显示如下帮助屏幕：第 46 页

```
usage: /usr/sbin/apachectl (start|stop|restart|fullstatus|status|graceful|
  configtest|help)
```

```
start           启动 httpd
stop            如果运行则通过发送 SIGHUP 停止 httpd
restart         重启 httpd 显示完整状态页面；需要 lynx 和 mod_status
fullstatus      显示短状态页面；需要 lynx 和 mod_status
status          如果不运行则通过发送 SIGUSR1 执行优雅重启
configtest      进行配置语法测试
help            显示此屏幕
```

## fullstatus

`fullstatus` 需要 `lynx` 和 `mod_status` 模块来提供服务器状态的详细描述。

`apachectl fullstatus` 命令的输出如下：

```
## apachectl fullstatus
Apache Server Status for localhost.localdomain

Server Version: Apache/1.3.14 (Unix) PHP/3.0
Server Built: Dec 4 2000 09:46:50
Current Time: Thursday, 28-Dec-2000 19:34:56
Restart Time: Thursday, 28-Dec-2000 19:34:18
Parent Generation: 0
Server uptime: 30 seconds
Total accesses: 1 - Total Traffic: 2 kB
CPU Usage: u0: s0 c0 - .0263% CPU load
.0263 requests/sec - 53 B/second -2048 B/request
正在处理的请求，4 个空闲服务器
```

> 评分板键："." 等待连接，"S" 正在启动，"R" 读取请求，"W" 发送响应，"K" 保持连接（读取），"D" DNS 查询，"L" 记录日志，"G" 优雅结束，" ." 无当前进程的空槽

| Srv PID | Acc CPU | MSS Req | Conn Shld | Client | Vhost Request |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0-0 | 9886 | 0/1 .001 | 38 | 88 | 0.0 | 0.00 | 127.0.0.1 | localhost.localdomain GET /server-status HTTP/1.0 |
| 1-0 | 9887 | 0/0 W | 0.00 | 38 | 119647253 | 0.0 | 0.00 | 127.0.0.1 | localhost.localdomain GET /server-status HTTP/1.0 |

## 安装与配置

### configtest

使用 `configtest` 在不重启服务器的情况下检查配置的正确性：

```
## apachectl configtest
Syntax [ OK ]
Checking configuration for httpd: [ ok ]
```

### graceful

使用 `graceful` 优雅地重启 Apache。当用户使用 `graceful` 重启时，Apache 将等待处理所有请求，避免 `apachectl stop` 带来的强制停中断。

## 安装与配置 49

默认索引有一个 Apache 官方文档的链接。在本章中，我们将一直引用本地副本，也可以在 apache.org 网站找到它。

不同的发行版执行不同的函数。默认安装类似于：

```
/etc/httpd/conf/
access.conf httpd.conf default mime.types
srm.conf.default access.conf default magic mime.types.default httpd.conf
magic.default srm.conf
```

这些是原始配置文件。过去，Apache 使用三文件配置风格，所有通用选项都在 `httpd.conf` 中。所有依赖资源的配置（如虚拟服务器、目录、文档根，以及在文件系统中指定的与 Apache 相关的所有指令和选项）都在 `srm.conf` 中。任何与这些资源访问相关的配置（例如 Apache 阻止访问某些目录以及开启身份验证）都进入 `access.conf`。三个配置文件非常令人困惑；所有的 Apache 配置都可以放在这些文件中的任意一个。

这种过时的配置文件方式完全是任意的。系统可以拥有长度为零的 `httpd.conf` 和 `srm.conf`，而所有配置都在 `access.conf` 中，系统将执行相同的功能。其主要原因是为了兼容 NCSA 1.3 Web 服务器。自 1.3.4 发布以来，配置文件归类已发生变化；现在默认只使用 `httpd.conf`。如果用户需要发行版包，应该检查 `httpd.conf` 文件中的配置。这些行被我们的默认安装注释掉了，在系统中需要查找这些行以确定 Apache 是否正在使用 `srm.conf` 和 `access.conf`：

```
#ResourceConfig/srm.conf
#AccessConfig/access.conf
```

从 1.3 版本开始，这些文件可以直接删除；但是，你可能想通过类似于以下的操作将其显式地设置为零：

```
ResourceConfig /dev/null
AccessConfig /dev/null
```
