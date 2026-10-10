
- `manual.conf` — 定义手册的位置（位于 `/www/manual`）。（安装 `manual` 包。）

- `mrtg.conf` — 定义 `mrtg` 的位置（位于 `/www/mrtg`）。（安装 `mrtg` 包。）

- `perl.conf` — 加载 `mod_perl` 模块。（安装 `perl` 包。）

- `php.conf` — 加载 `mod_php` 模块。（安装 `php` 包。）

- `python.conf` — 加载 `mod_python` 模块。（安装 `python` 包。）

这些配置文件在 `http` 服务器启动时会被读取。这些文件中的信息本可以添加到 `httpd.conf` 中。但是，将其放在这里是为了让不同的包添加其配置设置，而无需让 `RPM` 软件

## 启动和停止服务器

启动和停止 Web 服务器的程序与许多其他守护进程相同。你可以使用 `chkconfig` 命令在启动时启动 `httpd` 服务。

> 交叉引用：参见第 12 章，了解控制启动和停止守护进程及服务器进程的脚本的详细工作。

`/etc/init.d/httpd` 脚本接受若干命令行参数。如果使用 `start` 参数调用，`httpd` 将运行一个主守护进程（由 `root` 所有），该进程将创建其他守护进程（数量由 `StartServers` 指令指定），用户为 `apache` 用户（来自 `User` 和 `Group` 指令）。这些进程负责响应 HTTP 请求。使用 `stop` 参数，由于所有 `httpd` 进程被终止，服务器将关闭。

给定命令行参数 `restart`，脚本将按顺序执行停止和启动程序。使用 `reload` 作为参数将向主 `httpd` 守护进程发送挂断信号 `-HUP`，导致其重新读取配置文件并重启所有其他 `httpd` 守护进程。该脚本还支持 `status` 参数，它将报告守护进程是否正在运行，如果正在运行，则显示运行中的 `PID`。

## 第 21 节：设置 Web 服务器 871

进程。所有其他命令行参数都会导致错误并打印用法信息。

Apache 的实际二进制文件 `/usr/sbin/httpd` 支持多个命令行参数，尽管通常会使用默认值。可能的命令行参数如表 21-7 所示。

### 表 21-7：httpd 的命令行参数

| 参数 | 描述 |
| --- | --- |
| `-c` 指令 | 读取配置文件并处理该指令。这可能会覆盖配置文件中对该指令的定义。 |
| `-C` 指令 | 先处理该指令，然后读取配置文件。该指令可能会更改对配置文件的评估结果，但也可能被配置文件中的另一个定义覆盖。 |
| `-d` 目录 | 使用目录作为 `ServerRoot` 指令，指定模块、配置和日志文件的所在。 |
| `-D` 参数 | 定义用于 `IfDefine` 指令中条件评估的参数。 |
| `-f` 文件 | 使用该文件作为 `ServerConfigFile` 指令，而不是默认的 `/etc/httpd/httpd.conf`。 |
| `-h` | 显示可能的命令行参数列表。 |
| `-l` | 列出编译时链接到可执行文件的模块。 |
| `-L` | 打印配置文件中所使用的指令详细列表，并附带简短描述以及包含每个指令的模块。 |
| `-S` | 列出虚拟主机的配置设置。 |
| `-t` | 对配置文件进行语法检查。结果将为：`Syntax OK` 或错误通知，例如：`Syntax error on line 118 of /etc/httpd/conf/httpd.conf` |
| `-T` | 与 `-t` 相同，但不对 `DocumentRoot` 的值进行检查。 |
| `-v` | 打印版本信息：Server version: Apache/2.0.48 Server built: March 17 2004 11:23:11 |
| `-V` | 列出版本信息以及编译期间定义的任何值：\nServer version: Apache/2.2.0\nServer built: Feb 11 2006 18:10:38\nServer's Module Magic Number: 20051115:0\nArchitecture: 32-bit\nServer compiled with...\n-D APACHE_MPM_DIR="server/mpm/prefork"\n-D APR_HAS_MMAP\n-D APR_HAVE_IPV6 (IPV4-mapped addresses enabled)\n-D SERVER_CONFIG_FILE="httpd.conf" |
| `-X` | 仅启动单个主守护进程，不会产生其他 `httpd` 进程。这应该用于直接从命令行进行测试。 |

# 监控服务器活动

对于想要为了目的劫持计算机的人来说，Apache Web 服务器是一个非常有吸引力的目标。你可以使用许多技术来保护你的服务器（在第 14 节中介绍），从 `SELinux` 到使用证书控制脚本的运行。然而，这里描述的是监控你的 Apache Web 服务器性能和安全性的技术。仔细观察你的服务器通常可以在攻击发生得之前阻止它。

Apache 提供了两个独特的内置方法来检查 Web 服务器的性能和状态。`server-info` 处理器可以配置为显示服务器配置详细摘要。你可以通过向 `/etc/httpd/conf/httpd.conf` 文件中添加以下行来激活这些服务：

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from localhost
</Location>
```

```
<Location /server-info>
  SetHandler server-info
  Order deny, allow
  Deny from all
  Allow from localhost
</Location>
```

在此示例中，来自本地计算机的所有用户都可以显示 `server-info` 和 `server-status` 页面。你可以将 `localhost` 更改为 Apache 服务器托管的任何域名或主机。

## 显示服务器信息

服务器信息 `server-info` 页面包含服务器版本信息以及各种通用配置参数，并按模块划分其余数据。它会列出每个加载的模块，以及该模块支持的所有指令，以及该模块中任何定义指令的当前值。

服务器信息通常非常详细，包含的信息比图 21-3 显示的多多，图 21-3 仅显示指向每个模块部分的链接和通用服务器设置部分。

![](img/74f214fbb2938b570bec5f957507ac66_906_0.png)

## 服务器设置

Server Version: Apache/2.2.4 (Unix) DAY/2

Server Built: May 9 2007 06:26:12

图 21-3：server-info 页面显示服务器和模块信息。

## 显示服务器状态

`server-status` 页面的内容包括服务器版本信息、当前时间、服务器上次启动的时间戳以及服务器的运行时间。该页面还详细说明了每个服务器的状态。该页面还详细说明了每个服务器可能的状态（等待连接、正在启动、读取请求、发送响应、等待读取、执行查找、事务或优雅地退出）。

`server-status` 页面列出了每个服务器 `PID` 并指示其状态。`server-status` 页面还可以执行自动更新。如果指定了 `http://localhost/server-status?refresh=40`，则该页面将每 40 秒更新一次。这允许浏览器完全监控服务器。

![](img/74f214fbb2938b570bec5f957507ac66_907_0.png)

图 21-4：server-status 页面显示通用信息。

默认情况下，只生成基本状态。如果你想生成完整状态，需要通过取消注释以下一行来启用 `ExtendedStatus` 指令：

```
# ExtendedStatus: Off
```

# ExtendedStatus On

由于 `server-info` 和 `server-status` 页面包含不应让网络任何人访问的信息，有一些额外方法可以保护这些信息。你可以将其限制为本地主机；但在某些环境中这可能不可行。如果你必须允许其他机器或网络访问详细信息，请尽可能只允许本地网络上的机器。此外，请注意，如果落入坏手，服务器显示的信息可能会让机器更容易受到攻击。这是一种“模糊安全”，虽然不应依赖它，但可以增加获取信息的难度。

## 记录错误

错误日志包含服务器生成的描述各种错误状况的 {。`httpd.conf` 文件中的 `ErrorLog` 和 `LogLevel` 指令（在配置服务器章节中描述）可以修改文件名和记录量。默认文件为 `/etc/httpd/logs/error_log`（它是 `/var/log/httpd/error_log` 的链接）。以下是错误日志中的几行示例：
