
-   **original.ssl.conf** — 配置 SSL 支持，以便 Apache 知道如何提供通过安全连接（https）请求的页面。
-   **perl.conf** — 标识并加载 mod_perl 模块，以便您的网页可以包含 Perl 代码。
-   **php.conf** — 标识并加载 libphp4 模块，以便您的网页可以包含 PHP 脚本语言。还有一个 DirectoryIndex 设置，允许您添加到目录中的 index.php 文件作为目录索引提供。
-   **python.conf** — 标识并加载 mod_python 模块，以便网页可以包含用 Python 编写的 Apache 处理程序。
-   **squirrelmail.conf** — 标识 SquirrelMail 基于 Web 的邮件界面的位置，以便将其整合到您的 Apache Web 服务器中。要查看 SquirrelMail 登录屏幕，请在浏览器窗口中输入 **http://localhost/webmail**。
-   **subversion.conf** — 加载 mod_dav_svn 和 mod_authz_svn 模块，以便您可以通过 Apache 访问 Subversion 仓库。通过取消此文件中行的注释，您可以将 /home/svnroot 设置为存放授权文件的位置。
-   **wordtrans.conf** — 标识 WordTrans 语言翻译窗口的位置，以便将其整合到您的 Apache Web 服务器中。要查看 WordTrans 登录屏幕，请在浏览器窗口中输入 **http://localhost/wordtrans**。

这些配置文件在 httpd 服务器启动时被读取。这些文件中的信息本可以添加到 httpd.conf 中。然而，这些文件被放在这里，以便不同的软件包可以添加自己的配置设置，而无需编辑 httpd.conf 文件。

## 启动和停止服务器

启动和停止 Apache Web 服务器的流程与其他许多服务器进程并无不同。您可以使用 chkconfig 命令设置 httpd 服务在启动时自动启动。

> **交叉引用：** 有关控制启动和停止守护进程及服务器进程的 shell 脚本内部工作原理的详细信息，请参阅第 12 章。

/etc/init.d/httpd shell 脚本接受任意五个命令行参数。如果使用参数 start 调用它，httpd 脚本将运行一个主守护进程（由“root”拥有），该进程会生成其他守护进程（数量等于 StartServers 指令指定的数量），由用户 apache（来自 User 和 Group 指令）拥有。这些进程负责响应传入的 HTTP 请求。如果使用 stop 调用，服务器将被关闭，所有 httpd 进程都会被终止。

如果给出命令行参数 restart，脚本将简单地按顺序执行 stop 和 start 流程。使用 reload 作为参数会向主 httpd 守护进程发送挂断信号 (-HUP)，导致其重新读取配置文件并重启所有其他 `httpd` 守护进程。shell 脚本还支持 `status` 参数，它将报告守护进程是否正在运行，如果正在运行，则报告正在运行进程的 PIDs。所有其他命令行参数都会导致错误并打印用法消息。

Apache 的实际服务器守护进程 `/usr/sbin/httpd` 支持多个命令行参数，尽管通常使用默认值。可能的命令行参数列在表 21-7 中。

### 表 21-7：httpd 的命令行参数

| 参数 | 描述 |
| :--- | :--- |
| -c directive | 读取配置文件然后处理 *directive*。这可能会覆盖配置文件中对该指令的定义。 |
| -C directive | 先处理 *directive*，然后读取配置文件。该指令可能会改变配置文件的评估，但也可能被配置文件中的另一个定义覆盖。 |
| -d directory | 使用 *directory* 作为 `ServerRoot` 指令，指定模块、配置和日志文件目录的位置。 |
| -D parameter | 定义 *parameter* 以在 `IfDefine` 指令中用于条件评估。 |
| -f file | 使用 *file* 作为 `ServerConfigFile` 指令，而不是默认的 `/etc/httpd/conf/httpd.conf`。 |
| -h | 显示可能的命令行参数列表。 |
| -l | 列出编译时链接到可执行文件的模块。 |
| -L | 打印可在配置文件中使用的指令的详细列表，以及简短描述和包含每个指令的模块。 |
| -S | 列出虚拟主机的配置设置。 |
| -t | 对配置文件执行语法检查。结果将是：Syntax OK 或错误通知，例如：/etc/httpd/conf/httpd.conf 第 118 行的语法错误： |
| -T | 与 -t 相同，只是不会检查 `DocumentRoot` 值。 |
| -v | 打印版本信息：<br>服务器版本：Apache/2.0.40<br>服务器构建时间：Feb 11 2003 12:02:50 |
| -V | 列出版本信息和编译期间定义的所有值：<br>服务器版本：Apache/2.0.40<br>服务器构建时间：Feb 11 2003 12:02:50<br>服务器模块魔术数字：20020628:0<br>架构：32 位<br>服务器编译时使用...<br>-D APACHE_MPM_DIR="server/mpm/prefork"<br>-D APR_HAS_MMAP<br>-D APR_HAVE_IPV6<br>...<br>-D SERVER_CONFIG_FILE="conf/httpd.conf" |
| -X | 仅启动单个主守护进程，不会生成其他 httpd 进程。这应仅用于直接从命令行进行测试的目的。 |

## 监控服务器活动

Apache 提供了两种独特的内置方法来检查 Web 服务器的性能。server-status 处理程序可以配置为显示服务器进程的信息。server-info 处理程序可以配置为显示 Web 服务器配置的详细摘要。您可以通过分别向 /etc/httpd/conf/httpd.conf 文件添加以下行来激活这些服务：

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from handsonhistory.com
</Location>
```

```
<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from handsonhistory.com
</Location>
```

在此示例中，handsonhistory.com 域中的所有计算机都可以显示 server-info 和 server-status 页面。您可以将 handsonhistory.com 更改为您 Apache 服务器托管的任何域或主机的名称。

## 显示服务器信息

服务器信息（server-info）页面包含服务器版本信息和各种通用配置参数，并按模块划分其余数据。每个已加载的模块都会列出，并提供该模块支持的所有指令的信息，以及该模块中任何已定义指令的当前值。

服务器信息通常非常详细，包含的信息远多于图 21-3 中显示的内容，后者仅显示指向每个模块部分的链接和常规服务器设置部分。

![](img/27a85d56d393921ced6412ae6e8336bf_856_0.png)

**图 21-3：** server-info 页面显示服务器和模块信息。

## 显示服务器状态

server-status 页面内容包括服务器的版本信息、当前时间、服务器上次启动的时间戳以及服务器的运行时间。该页面还详细说明每个服务器进程的状态，可选择多种可能状态（等待连接、刚刚启动、读取请求、发送回复、等待读取请求直至达到 KeepAliveTimeout 定义的秒数、执行 DNS 查找、记录事务或优雅退出）。

server-status 页面底部按进程 ID（PID）列出每个服务器并指示其状态，使用相同的可能值。图 21-4 是该页面的示例。

![](img/27a85d56d393921ced6412ae6e8336bf_857_0.png)

**图 21-4：** Apache server-status 页面显示 Apache 的通用信息并报告各个服务器进程的活动。

server-status 页面还可以执行自动更新以提供更密切的服务器监控。如果指定 URL http://localhost/server-status?refresh=40，则浏览器中显示的 server-status 页面将每 40 秒更新一次。这使得浏览器窗口可以完全用于持续监控 Web 服务器的活动。

默认情况下，仅生成基本状态信息。如果您希望生成完整的状态信息，则需要通过取消注释以下代码中的最后一行来打开 ExtendedStatus 指令：

```
#
# ExtendedStatus: controls whether Apache will generate "full" status
# information (ExtendedStatus On) or basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.
#
#ExtendedStatus On
```
