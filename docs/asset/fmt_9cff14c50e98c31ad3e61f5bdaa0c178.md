
| `-R DIRNAME` or `--public-root DIRNAME` | 将 `DIRNAME` 设置为 WebNFS 使用的公共文件的关联目录。 |

| `-r` or `--re-export` | 允许远程挂载的文件系统被导出。这可以将一台机器转换为 NFS 或 Novel 服务器的倍增器。在重新导出回环 NFS 挂载时应小心，因为重新进入挂载点将导致 NFS 客户端和 NFS 服务器之间发生死锁。它可能导致重新导出 `/proc`，从而带来安全风险。 |

| `-v` or `--version` | 输出版本号。 |

`showmount`

`showmount [-adehv] [--all] [--directories] [--exports] [--help] [--version] [ HOST ]`

`showmount` 查询 `HOST` 上的挂载守护进程以获取其 NFS 服务器状态的信息。在不带选项的情况下，`showmount` 列出从该主机挂载的客户端集合。

# 网络管理：showmount

| 选项 | 说明 |
| :--- | :--- |
| `-a` or `--all` | 以 `HOST:DIR` 格式列出客户端主机名和挂载目录。 |
| `-d` or `--directories` | 仅列出某些客户端挂载的目录。 |
| `-e` or `--exports` | 显示 NFS 服务器的导出列表。 |
| `-h` or `--help` | 打印用法总结。 |
| `--no-headers` | 抑制输出中的标题头。 |
| `-v` or `--version` | 输出当前版本号。 |

# 网络信息

此节描述了提供给客户端服务的服务。

## apache

`apache OPTION ...`

`apache` 是 Web 服务器。通过超文本传输协议 `HTTP` 为 Web 浏览器提供超文本标记语言 `HTML` 文档。它可以独立运行，也可以通过 `inetd` 调用。

| 选项 | 说明 |
| :--- | :--- |
| `-C DIRECTIVE` | 在启动前处理配置 `DIRECTIVE`。 |
| `-c DIRECTIVE` | 与 `-C` 相同。 |
| `-d SERVERROOT` | 设置 `ServerRoot` 的初始值为 `SERVERROOT`。Web 浏览引用相对于此值。 |
| `-f FILE` | 在启动时执行文件 `FILE`。如果不以 `/` 开头，则相对于 `ServerRoot`。 |
| `-h` | 输出在指令有效处具有参数的列表。 |
| `-1` | 输出在指令有效处具有参数的列表。 |
| `-S` | 显示配置中的设置。 |
| `-V` | 输出 `apache` 的版本和编译参数。 |
| `-v` | 输出 `apache` 的版本。 |

# fingered 和 in.fingerd

`fingered [-wul] [-pl PATH]`

`fingered` 服务响应 `finger` 客户端。更多信息请见第五章“网络客户端”。

# identd 和 inetd

`identd [-i|-w|-b] OPTION ... { KERNFILE { KMEMFILE } }`

`identd` 是实现 RFC 1413 文档指定的 TCP/IP 用户标识协议的服务器。它通过查找特定的 TCP/IP 连接并返回拥有连接的用户名来运行。

`-i` 标志可以在 `/etc/inetd.conf` 使用 `nowait` 选项启动守护进程时使用。使用此模式会导致 `inetd` 为每个连接请求启动 `identd` 守护进程。

`-w` 标志可以在 `/etc/inetd.conf` 使用 `wait` 选项启动守护进程时使用。这是推荐的操作模式，因为它会在第一个连接请求时启动 `identd` 副本，后续请求无需像 `-i` 模式那样每次都解析 `KERNEL` 文件中的 `nlist`。

`-b` 标志可以让守护进程以独立模式运行。这是最不受欢迎的模式，因为服务器的错误或任何致命条件都会终止它且必须手动重启。除外，它与 `-w` 模式具有相同优势，只需解析 `nlist`。

`KERNELFILE` 默认为当前运行的内核文件。`KMEMFILE` 默认为当前运行内核的内存空间。

## 网络管理：identd 和 in.identdd

| 选项 | 说明 |
| :--- | :--- |
| `-e` | 始终返回 `UNKNOWN-ERROR` 以代替 `NO-USER` 或 `INVALID-ID:PORT` 错误。 |
| `-gGID` | 使用 `-b` 选项绑定到 TCP/IP 端口后，切换到组 ID *GID ID*。 |
| `-1` | 使用 `syslog` 进行日志记录。 |
| `-0` | 不向客户端公开操作系统类型。始终返回 `OTHER`。 |
| `-m` | 允许每个会话处理多个请求。每个请求每行指定，响应将每行返回一个。在连接端关闭其行尾之前，连接不会关闭。 |
| `-N` | 为守护进程即将返回用户名的用户，在每个目录中检查是否存在 `.ident` 文件。如果文件存在，则向客户端返回 `HIDDEN-USER` 而不是实际 ID。 |
| `-n` | 返回用户 ID 而不是用户名。 |
| `-pPORT` | 使用 `-b` 运行模式绑定到端口 `PORT`。`PORT`可以是名称或数字。默认端口为 `113`。 |
| `-t SECONDS` | 将超时时间设置为 `SECONDS`。与 `-w` 一起使用。 |
| `-uUUID` | 使用 `-b` 选项绑定到 TCP/IP 端口后，切换到用户 ID *UUID*。 |
| `-V` | 显示版本号并退出。 |

## rpc.rusersd

`rpc.rusersd` 是 `rusers` 客户端程序的服务器。它返回当前登录到系统的用户信息。更多信息请参阅 `rusers`（第 5 章）。

## rwhod

`rwhod [-b]`

`rwhod` 是使用 `rwho` 和运行时客户端程序维护数据库的服务器。它同时作为状态信息的生产者和消费者运行。作为信息的生产者，它定期查询系统状态，并构建在网络上广播的状态消息。作为信息的消费者，它监听来自其他 `rwho` 服务器的状态消息，对其进行验证，并将它们记录在位于 `/var/spool/rwho` 目录下的文件汇集中。更多信息请参阅第 5 章中的 `rwhod` 和 `runtime` 命令。

| 选项 | 说明 |
| :--- | :--- |
| `-a` | 使用所有类型的网络接口。这是默认设置。 |
| `-b` | 仅使用广播接口（如以太网）。 |
| `-p` | 仅使用点对点接口。 |

## 网络管理：ftppd 和 in.ftpd 235

## ugiddd 和 rpc.ugidd

`rpc.ugidd`

`ugidd` 处理 RPC 请求，将 UID 和 GID 数字映射到字符串名称。每当客户端和服务器不共享相同的密码词典文件（`passwd` word file）时，`nfsd` 服务器会调用它。

## 网络文件传输

本节描述了允许在网络主机之间复制文件的服务。

## ftppd 和 in.ftpd

`ftppd [-dDHIMS] [-T MAXTIMEOUT] [-u MASK]`

`ftppd` 服务来自 `ftp` 客户端的请求。更多信息请参阅第 5 章中的 `ftppd`。

| 选项 | 说明 |
| --- | --- |
| `-A` | 仅允许匿名 FTP 连接或 `/etc/ftpchroot` 中列出的账户。其他连接尝试将被拒绝。 |
| `-D` | `ftppd` 将分离并成为守护进程，在 FTP 端口上接受连接并派生子进程来处理它们。这比在 `inet` 中启动 `ftppd` 产生更低的开销，适用于繁忙服务器以减轻负载。 |
| `-d` | 使用 `LOG_FTP` 将调试信息写入 `syslog`。 |
| `-h` | 服务器将使用高端口范围（通常为 `40000..44999`）中的数据端口进行被动连接。 |
| `-1` | 每个成功或失败的 `FTP(1)` 会话都使用 `syslog` 的 `LOG_FTP` 进行记录。如果指定两次此选项，获取 `get`、存储 `put`、追加、删除、创建目录、删除目录和重命名操作及其文件名也将记录。 |
| `-M` | 启用多方法。它不再简单地使用账户的主目录 `~`，而是使用与客户端所连接的主机名匹配且位于其内部的目录。例如，如果一个主机有多个主机名，但客户端连接到 `host.net`，`ftppd` 将使用 `~/` 作为其主目录。 |
| `-S` | 如果 `/var/log/ftppd` 存在，则将所有匿名传输记录到其中。 |
| `-T MAXTIMEOUT` | 客户端可以请求不同的超时时间。可以使用 `T` 选项将允许的最大时间设置为 `MAXTIMEOUT` 秒。默认限制为两小时。 |
| `-t TIMEOUT` | 将活动超时时间设置为 `TIMEOUT`（默认为 15 分钟）。 |
| `-u MASK` | 将默认 `umask` 从 `027` 更改为 `MASK`。 |

![](img/f4d938df47df156cd8e912e7982f710f_260_0.png)

## tftpd 和 in.ftpd

`in.tftpd [-1] [-n] [DIRECTORY ...]`
