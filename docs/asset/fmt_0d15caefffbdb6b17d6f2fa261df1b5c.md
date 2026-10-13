
# 828 第四部分 + 红帽 Linux (Red Hat) 网络与服务器设置

## 表 21-7
### httpd 命令行参数

| 参数 | 说明 |
| --- | --- |
| `-c` 指令 | 读取配置文件并处理该指令。这可能会覆盖配置文件中该指令的定义。 |
| `-C` 指令 | 先处理指令，然后读取配置文件。该指令可能会更改配置文件的评估，但也可能被配置文件中的另一个定义覆盖。 |
| `-d` 目录 | 使用目录作为 `ServerRoot` 指令，指定模块、配置和日志文件目录的位置。 |
| `-D` 参数 | 定义用于 `IfDirective` 内部条件评估的参数。 |
| `-f` 文件 | 使用文件作为 `ServerConfigFile`，而不是默认的 `/etc/httpd/conf/httpd.conf`。 |
| `-h` | 显示可能的命令行参数列表。 |
| `-l` | 列出编译时链接到可执行文件中的模块：编译入的模块：`http_core.c` `mod_so.c` |
| `-L` | 打印可以在配置文件中使用的指令详细列表，并附带简短描述以及包含每个指令的模块。 |
| `-S` | 列出虚拟主机的配置设置。 |
| `-t` | 对配置文件进行语法检查。结果将为：`Syntax OK` 或（例如）：`Syntax error on line 118 of /etc/httpd/conf/httpd.conf:ServerType must be either 'inetd' or 'standalone'` |
| `-T` | 与 `-t` 相同，不同之处于不检查 `DocumentRoot` 的值。 |
| `-v` | 打印版本信息：`Server version: Apache/1.3.12 (Unix)(Red Hat/Linux)` `Server built: Aug 7 2000 06:20:48` |
| `-V` | 列出版本信息以及编译期间定义的任何值：`Server version: Apache/1.3.12 (Unix)(Red Hat/Linux)` `Server built: Apr 7 2000 06:20:48` `Server's Module Magic Number: 19990320:7` `Server compiled with...` `- D EAPI` `- D HAVE_MMAP` `- D HAVE_SHMGET` `- D USE_SHMGET_SCOREBOARD` `- D USE_MMAP_FILES` `- D USE_FCNTL_SERIALIZED_ACCEPT` `- D HTTPD_ROOT="/usr"` `- D SUEXEC_BIN_="/usr/sbin/suexec"` `- D DEFAULT_PID_LOG="/var/log/httpd.pid"` `- D DEFAULT_SCOREBOARD="/var/log/httpd.scoreboard"` `- D DEFAULT_LOCKFILE="/var/log/httpd.lock"` `- D DEFAULT_XFERLOG="/var/log/httpd/access_log"` `- D DEFAULT_ERRORLOG="/var/log/httpd/error_log"` `- D TYPES_CONFIG_FILE="/etc/httpd/conf/mime.types"` `- D SERVER_CONFIG_FILE="/etc/httpd/conf/httpd.conf"` `- D ACCESS_CONFIG_FILE="/etc/httpd/conf/access.conf"` `- D RESOURCE_CONFIG_FILE="/etc/httpd/conf/srm.conf"` |
| `-X` | 仅启动单个主守护进程，不会产生其他 `httpd` 进程。这应该仅用于测试目的。 |

## 监控服务器活动

Apache 提供了两种独特的内置方法来检查 Web 服务器的性能。`server-info` 处理器可以配置为显示 Web 服务器配置的详细摘要。`server-status` 处理器可以配置为显示有关服务器进程的信息。你可以通过分别向 `/etc/httpd/conf/httpd.conf` 文件中添加以下行来激活这些服务：

```
```
