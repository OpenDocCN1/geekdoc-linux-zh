
虚拟主机功能允许您在单个服务器上托管多个网站。当您有多个域名但只有一个 IP 地址时，这是一个非常实用的功能。

## 第 21 章：设置 Web 服务器 879

- `squirrelmail.conf` — 识别 SquirrelMail Web 邮件界面的位置，将其整合到您的 Apache Web 服务器中。要查看 SquirrelMail 登录界面，请在浏览器窗口中输入 `http://localhost/webmail`。（安装 `squirrelmail` 软件包。）

- `ssl.conf` — 配置 SSL 支持，使 Apache 知道如何处理通过安全连接请求的页面。（安装 `mod_ssl` 包。）

- `subversion.conf` — 加载 `mod_dav_svn` 和 `mod_auth_svn` 模块，以便通过 Apache 访问 Subversion 仓库。通过取消此文件中中的行的注释，你可以将 `/home/svnroot` 设置为存放授权文件的根目录。（安装 `mod_dav_svn` 包。）

- `webalizer.conf` — 允许您识别谁可以访问您网站的 `webalizer` 统计数据。（安装 `webalizer` 软件包。）

- `wordtrans.conf` — 识别 WordTrans 翻译窗口的位置，将其整合到您的 Apache Web 服务器中。要查看 WordTrans 登录界面，请在浏览器窗口中输入 `http://localhost/wordtrans`。（安装 `mod_auth_pgql` 包。）

这些配置文件在 `httpd` 启动时读取。这些文件中的信息本可以添加到 `httpd.conf` 中。然而，将文件放在这里是为了让不同的软件包添加它们的配置设置，而无需 RPM 软件包采用某种自动化方法将其配置信息添加到 `httpd.conf` 文件中。

# 启动和停止服务器

启动和停止 Apache 服务器的过程与许多守护进程相同。你可以使用 `chkconfig` 命令设置 `httpd` 服务在启动时启动。

> **交叉引用：** 请参见第 12 章，获取有关控制和停止守护进程及服务器进程的 shell 内部工作的详细信息。

`/init/httpd` 脚本接受任何命令行参数。如果使用 `start` 参数调用（由 root 执行），`httpd` 脚本将以用户 `apache`（由 `User` 和 `Group` 指令指定）运行一个守护进程（等于 `StartServers` 指令指定的数量）。这些进程负责响应传入的 HTTP 请求。如果使用 `stop` 调用，由于所有 `httpd` 进程都将被终止，服务器将关闭。

如果命令行参数为 `restart`，脚本将按顺序执行 `stop` 和 `start` 进程。使用 `reload` 作为参数将向主 `httpd` 守护进程发送挂起信号 `-HUP`，使其重新读取其配置文件并重启所有其他 `httpd` 守护进程。该 shell 脚本还支持 `status` 参数，它将报告守护进程是否正在运行，如果正在运行，将报告运行进程的 PID。所有其他命令行参数都将导致错误并打印用法信息。

Apache 的实际二进制文件 `/usr/sbin/httpd` 支持多个命令行参数，尽管通常使用默认值。可能的命令行参数列在表 21-7 中。

# 表 21-7：httpd 的命令-参数

| 参数 |  |
| :--- | :--- |
| `-c directive` | 读取配置文件并处理该指令。这可能会覆盖配置文件的定义。 |
| `-C directive` | 处理该指令然后读取配置文件。该指令可能会更改配置文件的评估，但也可能被配置文件中的另一个定义覆盖。 |
| `-d directory` | 使用目录作为 `ServerRoot` 指令，指定模块、配置和日志目录的位置。 |
| `-D parameter` | 定义用于 `IfDefine` 指令中条件评估的参数。 |
| `-f file` | 使用文件作为 `Server` 指令，而不是默认的 `/etc/httpd/conf/httpd.conf`。 |
| `-h` | 显示可能的命令行参数列表。 |
| `-l` | 列出编译时链接到可执行文件的模块。 |
| `-L` | 打印可以在配置文件使用的指令的详细列表，并带有简短描述以及包含每个指令的模块。 |
| `-S` | 列出为虚拟主机配置的设置。 |
| `-t` | 对配置文件进行语法检查。结果将是：Syntax OK 或错误通知：Syntax error on line 118 of `/etc/httpd/conf/httpd.conf` |
| `-T` | 与 `-t` 相同，但不对 `DocumentRoot` 值进行检查。 |
| `-v` | 打印版本信息：Server version: Apache/2.2.11 (Unix) Server built: Mar 17 2009 09:15:10 |
| `-V` | 列出版本信息以及编译期间定义的任何值：Server version: Apache/2.2.11 (Unix) Server built: Mar 17 2009 09:15:10 Server's Module Magic Number: 20051125:21 Architecture: 32-bit Server compiled with... -D APACHE MPM_DIR="server/mpm/prefork" -D APR_HAS_SENFILE -D APR_HAS_MMAP |
| `-k option` | 在 start, stop, 使用 `-k` |

# 第四部分：Fedora 和 RHEL 网络和服务器设置

## 服务器状态

`server-status` 页面包含当前时间、服务器启动的时间戳以及各种状态（等待连接、正在启动、读取请求、优雅退出）。

`server-status` 页面底部按进程 ID (`PID`) 列出每个服务器并使用以下值指示其状态：
* Waiting for Connection, S Reading Request,

`server-status` 页面还可以自动更新。如果指定 URL `http://localhost/server-status/refresh=40`，浏览器中的 `server-status` 页面将每 40 秒更新一次。这使得窗口可以完全监控服务器活动。

## 服务器信息

`server-info` 页面包含版本信息、当前时间、服务器启动的时间戳以及服务器运行时间。`server-info` 页面通常非常详细，包含的信息比服务器版本信息多。

`server-status` 页面提供了有关服务器的详细信息。图 21-3 是此处的示例。

# 服务器状态

`server-status` 页面包含当前时间、服务器启动的时间戳以及各种状态（等待连接、正在启动、读取请求、优雅退出）。

`server-status` 页面底部按进程 ID (`PID`) 列出每个服务器并使用以下值指示其状态：
* Waiting for Connection, S Reading Request,

`server-status` 页面还可以自动更新。如果指定 URL `http://localhost/server-status/refresh=40`，浏览器中的 `server-status` 页面将每 40 秒更新一次。这使得窗口可以完全监控服务器活动。

## 服务器信息

`server-info` 页面包含版本信息、当前时间、服务器启动的时间戳以及服务器运行时间。`server-info` 页面通常非常详细，包含的信息比服务器版本信息多。

`server-status` 页面提供了有关服务器的详细信息。图 21-3 是此处的示例。

# server-info 和 server-status 的进一步安全

由于 `server-info` 和 `server-status` 都包含不应让网络上的任何人访问的隐私信息，您还有几种额外的方法可以保护这些信息。您可以将这些信息限制为本地主机；然而，在某些环境中这可能并不切实际。

# 884 第四部分：Fedora RHEL 网络与服务器设置

如果你允许其他机器或网络访问此类详细配置信息，请仅允许必要的机器访问，且最好仅限本地网络上的机器。请注意，如果落入别有用之手，`server-info` 和 `server-status` 页面显示可能会你的整台机器的安全更容易受到破坏。

更改用于引用上述两个页面的 URL 可能也有有益。这是“通过隐性实现安全”的一个示例，虽然不应依赖它，但它可以让未经授权的人员获取你的 Web 服务器配置信息变得困难一点（特别是当你无法将连接限制在本地网络时）。要实现这一点，只需更改以下行中 `Location` 指令的文件名：

```
/server.information.page
```

以及：

```
/server.status.page
```
