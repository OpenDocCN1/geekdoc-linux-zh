
该文件，你可以使用 `chkconfig` 命令在 `/etc/rcX.d` 目录中创建适当的链接。

交叉参考：有关控制守护进程和服务器进程启动与停止的 Shell 脚本内部工作原理的详细信息，请参阅第 12 章。

`/etc/init.d/httpd` Shell 脚本接受五个命令行参数中的任意一个。如果以 `start` 作为参数调用，httpd 脚本将运行一个由“root”拥有的主守护进程，该主守护进程将派生其他由用户 apache（来自 `User` 和 `Group` 指令）拥有的守护进程（数量等于 `StartServers` 指令指定的数量）。这些进程负责响应传入的 HTTP 请求。如果以 `stop` 作为命令行参数调用，随着所有 httpd 进程被终止，服务器将被关闭。

如果给定的命令行参数为 `restart`，脚本将依次执行停止和启动程序。如果使用 `reload` 作为参数，则会向主 httpd 守护进程发送挂起信号（`-HUP`），导致其重新读取配置文件并重启所有其他 httpd 守护进程。Shell 脚本还支持 `status` 参数，它将报告守护进程是否正在运行，如果是，则显示正在运行的进程的 PID。所有其他命令行参数都会导致错误，并打印用法信息。

Apache 实际的服务器守护进程 `/usr/sbin/httpd` 支持多个命令行参数，尽管通常使用默认值。可能的命令行参数列表如表 21-7 所示。

### 表 21-7：httpd 的命令行参数

| 参数 | 描述 |
| :--- | :--- |
| -c directive | 读取配置文件，然后处理该指令。这可能覆盖配置文件中该指令的定义。 |
| -C directive | 处理该指令，然后读取配置文件。该指令可能会改变配置文件的评估，但也可能被配置文件中的另一个定义所覆盖。 |
| -d directory | 使用 `directory` 作为 `ServerRoot` 指令，指定模块、配置文件和日志文件目录所在的位置。 |
| -D parameter | 定义 `parameter` 用于 `IfDefine` 指令内的条件评估。 |
| -f file | 使用 `file` 作为 `ServerConfigFile` 指令，而不是默认的 `/etc/httpd/conf/httpd.conf`。 |
| -h | 显示可能的命令行参数列表。 |
| -l | 列出编译时链接到可执行文件的模块： |
| -L | 打印出可在配置文件中使用的指令的详细列表，包括简短描述以及包含每个指令的模块。 |
| -S | 列出虚拟主机的配置设置。 |
| -t | 对配置文件进行语法检查。结果将是：<br><br><i>语法正常</i><br><br>或者（例如）：<br><br><i>/etc/httpd/conf/httpd.conf 第 118 行存在语法错误：</i> |
| -T | 与 -t 相同，但不检查 DocumentRoot 值。 |
| -v | 打印版本信息：<br><br>Server version: Apache/1.3.12 (Unix) (Red Hat/Linux)<br>Server built:  Aug   7  2000  06:20:48 |
| -V | 列出版本信息以及编译期间定义的任何值：<br><br>Server version: Apache/1.3.12 (Unix) (Red Hat/Linux)<br>Server built:  Apr   7  2000  06:20:48<br><br>Server's Module Magic Number: 19990320:7<br><br>Server compiled with....<br>-D EAPI<br><br>-D HAVE_MMAP<br><br>-D HAVE_SHMGET<br><br>-D USE_SHMGET_SCOREBOARD<br><br>-D USE_MMAP_FILES<br><br>-D USE_FCNTL_SERIALIZED_ACCEPT<br><br>-D HTTPD_ROOT="/usr"<br><br>-D SUEXEC_BIN="/usr/sbin/suexec"<br><br>-D DEFAULT_PIDLOG="/var/httpd/httpd.pid"<br><br>-D DEFAULT_SCOREBOARD="/var/httpd/httpd.scoreboard"<br><br>-D DEFAULT_LOCKFILE="/var/httpd/httpd.lock"<br><br>-D DEFAULT_XFERLOG="/var/log/httpd/access_log"<br><br>-D DEFAULT_ERRORLOG="/var/log/httpd/error_log"<br><br>-D TYPES_CONFIG_FILE="/etc/httpd/conf/mime.types"<br><br>-D SERVER_CONFIG_FILE="/etc/httpd/conf/httpd.conf"<br><br>-D ACCESS_CONFIG_FILE="/etc/httpd/conf/access.conf"<br><br>-D RESOURCE_CONFIG_FILE="/etc/httpd/conf/srm.conf" |
| -X | 仅启动单个主守护进程，不派生其他 httpd 进程。这应仅用于测试目的。 |

### 监控服务器活动

Apache 提供了两种独特的内置方法来检查 Web 服务器的性能。可以配置 server-info 处理器来显示 Web 服务器配置的详细摘要。可以配置 server-status 处理器来显示关于服务器进程的信息。你可以通过分别向 `/etc/httpd/conf/httpd.conf` 文件添加以下行来激活这些服务：

```
<Location /server-info>
    SetHandler server-info
    order deny,allow
    deny from all
    allow from handsonhistory.com
</Location>

<Location /server-status>
    SetHandler server-status
    order deny,allow
    deny from all
    allow from handsonhistory.com
</Location>
```

在此示例中，handsonhistory.com 域中的所有计算机都可以显示 server-info 和 server-status 页面。你可以将 handsonhistory.com 更改为你的 Apache 服务器托管的任何域或主机的名称。

### 显示服务器信息

服务器信息（server-info）页面包含服务器版本信息以及各种通用配置参数，并按模块对剩余数据进行划分。列出了每个已加载的模块，包括关于该模块支持的所有指令的信息，以及该模块中任何已定义指令的当前值。

服务器信息通常非常详尽，包含比图 21-2 中显示的更多的信息，该图仅显示了到每个模块部分和通用服务器设置部分的链接。

![](img/1744bde8c889adfab3fc911e1687fecf_886_0.png)

**图 21-2**：server-info 页面显示服务器和模块信息。

### 显示服务器状态

server-status 页面的内容包括服务器版本信息、当前时间、服务器上次启动的时间戳以及服务器的运行时间。该页面还详细说明了每个服务器进程的状态，状态可从几种可能的状态中选择（等待连接、刚刚启动、读取请求、发送响应、在达到 KeepAliveTimeout 定义的秒数之前等待读取请求、执行 DNS 查找、记录事务或正常退出）。

server-status 页面底部按进程 ID（PID）列出每个服务器，并使用相同的可能的值来指示其状态。图 21-3 是该页面的一个示例。

![](img/1744bde8c889adfab3fc911e1687fecf_886_1.png)

**图 21-3**：Apache server-status 页面显示一般的 Apache 信息并报告单个服务器进程的活动。

server-status 页面还可以执行自动更新，以提供更紧密的服务器监控。如果指定了 URL `http://localhost/server-status?refresh=40`，则在浏览器中显示的 server-status 页面将每 40 秒更新一次。这使得一个浏览器窗口可以完全专门用于持续监控 Web 服务器的活动。

默认情况下，只生成基本状态信息。如果你希望生成完整的状态信息，你需要通过取消以下代码中最后一行的注释来打开 *ExtendedStatus* 指令：

```
#
# ExtendedStatus: 控制当调用 "server-status" 处理器时，Apache 是否生成 "完整" 状态
# 信息 (ExtendedStatus On) 或基本信息 (ExtendedStatus
# Off)。默认为 Off。
#
#ExtendedStatus On
```

### 进一步保护 server-info 和 server-status

由于 server-info 和 server-status 页面都包含不应让网络上的任何人都可访问的私有信息，因此有几种额外方法可以保护这些信息。你可以将该信息限制为仅本地主机可访问；然而，在某些环境中这可能并不实际。

如果你必须允许其他机器或网络访问如此详细的配置信息，请仅允许必要的机器，最好仅允许你本地网络上的那些机器。此外，要意识到，如果落入错误的人手中，server-info 和 server-status 页面显示的信息会使你的整个机器的安全性更容易被破坏。图 21-4 显示了应向没有访问 server-status 页面权限的主机显示的错误消息。

![](img/1744bde8c889adfab3fc911e1687fecf_887_0.png)

更改用于引用上述两个页面的 URL 也可能有益。这是“通过混淆实现安全”的一个例子，不应该依赖于此，但

