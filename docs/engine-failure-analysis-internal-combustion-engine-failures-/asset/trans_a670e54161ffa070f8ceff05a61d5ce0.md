

## 命令

- **使用此选项**：`format format`
  - 将文件传输类型设置为指定格式。选项为 `ascii` 和 `binary`。

- `get remote filename [ local filename ]`
  - 获取远程文件，并可选地使用指定的本地文件名将其存储在本地。

- `glob`
  - 切换 `mdelete`、`mget` 和 `mput` 的文件名扩展功能。默认状态为开启。

- `hash`
  - 切换 1024 字节数据块传输时显示哈希符号。

- `help [ command ]`
  - 显示所有命令的列表，或显示指定命令的帮助信息。

- `idle [ seconds ]`
  - 将远程服务器的不活动计时器设置为 *seconds* 秒。

- `lcd [ directory ]`
  - 将本地系统的工作目录更改为指定目录；如果未指定目录，则更改为用户的主目录。

- `ls [ remote directory ] [ local filename ]`
  - 显示指定目录的内容，并可选地将其保存到本地文件。

- `mdelete filename`
  - 删除远程机器上的 *filename*。

- `mget filename`
  - 获取远程机器上由文件名指定的多个文件，除非 `glob` 被关闭，否则可以使用文件名扩展。

- `mkdir directory`
  - 在远程机器上创建目录。

- `mode mode`
  - 将文件传输模式设置为指定模式。默认为 `stream`。

- `mtime filename`
  - 显示远程机器上该文件名的最后修改时间。

- `mput filename`
  - 在远程机器上放置由文件名指定的多个文件，除非 `glob` 被关闭，否则可以使用文件名扩展。

- `newer remote filename [ local filename ]`
  - 仅当远程文件的修改时间比本地文件新时，才获取该远程文件。

- `open hostname [ port ]`
  - 连接到主机名。可选使用指定端口。

- `prompt`
  - 切换交互式提示。

- `put local filename [ remote filename ]`
  - 将本地文件存储在远程机器上，可选使用远程文件名。

- `pwd`
  - 显示远程机器当前工作目录的名称。

- `quit`
  - 关闭 FTP 会话并退出 **ftp** 实用程序。

- `rget remote filename [ local filename ]`
  - 如果远程文件大于本地文件，则恢复 *remote filename* 的中断下载。

- `remotehelp [ command ]`
  - 请求远程 FTP 服务器的帮助。

- `remotestatus [ filename ]`
  - 显示远程机器的状态。可选显示指定文件名的状态。

- `rename [ old filename ] [ new filename ]`
  - 将远程机器上的旧文件名重命名为新文件名。

- `reset`
  - 清除响应队列。

- `restart marker`
  - 在指定的 *marker*（文件内的字节偏移量）处重新开始 **get** 或 **put** 操作。

- `rmdir directory`
  - 删除远程机器上的指定目录。

- `runique`
  - 切换远程机器上使用唯一文件名存储文件。

- `send local filename [ remote filename ]`
  - 将本地文件存储在远程机器上，可选使用远程文件名。

- `sendport`
  - 切换使用端口命令，这可以防止在执行多个文件传输时出现延迟。

- `size filename`
  - 显示远程机器上指定文件名的大小。

- `status`
  - 显示 **ftp** 实用程序的当前状态。

- `struct [ structure ]`
  - 将文件传输结构设置为 *structure*。默认结构为 *stream*。

- `sunique`
  - 切换远程机器上使用唯一文件名存储文件。

- `system`
  - 显示远程机器上运行的操作系统类型。

- `trace`
  - 切换数据包跟踪。

- `type [ mode ]`
  - 将文件传输类型设置为指定模式。默认为 ASCII。

- `umask [ mask ]`
  - 显示远程系统上的当前 **umask**。可选将远程 **umask** 设置为指定掩码。

- `user [ password [ account ] ]`
  - 登录到远程系统。可选指定密码和账户。

- `verbose`
  - 切换详细模式。

## ifconfig

`ifconfig [ interface ] [ option ] [ address ]`

显示网络接口的信息。此实用程序也可用于配置网络接口。它在启动脚本中用于在启动系统时配置网络硬件。对于用户而言，**ifconfig** 在不带选项调用时最有用。它提供了一种快速查看当前网络接口设置（包括 IP 地址和子网掩码）的方法。此处列出了基本 *ifconfig* 用法中可用的选项。中级和高级功能还有更多可用选项。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `broadcast address` | 设置此接口的广播地址 |
| `down` | 禁用接口 |
| `io_addr address` | 指定接口设备的 I/O 地址 |
| `irq address` | 指定接口设备的 IRQ 线路 |
| `media type \| port` | 指定设备使用的物理端口或介质类型（如果设备允许进行此类更改） |
| `mem_start addr` | 设置此设备使用的共享内存的起始地址 |
| `mtu n` | 设置接口的最大传输单元 (MTU) |
| `netmask address` | 指定此接口的子网掩码地址 |
| `txqueuelen length` | 设置设备的发送队列长度 |
| `up` | 启用接口 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `ifconfig eth0` | 显示指定网络接口（eth0）的当前配置。 |
| `ifconfig` | 显示所有活动网络接口的当前配置。 |

![](img/e85417bb52fc523c6fc7b3b77b124ecb_642_0.png)

## lynx

`lynx [ option ] [ path | URL ]`

启动文本模式 Web 浏览器，并可选显示指定的路径或 URL。一旦启动 lynx，您可以使用命令（参见本节中的命令表）来控制浏览器。此处列出了基本 lynx 用法中可用的选项。中级和高级功能还有更多可用选项。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| **--accept_all_cookies** | 接受所有 Cookie。 |
| **--anonymous** | 应用匿名账户的限制。 |
| **--assume_charset=***字符集* | 对于未指定字符集的文档，使用指定的字符集。 |
| **--assume_local_charset**=*字符集* | 对于本地文档，使用指定的字符集。 |
| **--assume_unrec_charset**=*字符集* | 对于未识别的字符集，使用指定的字符集。 |
| **--auth=***登录名***:**密码** | 对于受密码保护的文档，使用指定的登录名和密码。 |
| **\-book** | 启动 lynx 时显示书签页面。 |
| **\-cache=***n* | 在内存中缓存 *n* 个文档。默认为 10。 |
| **\-case** | 启用区分大小写的字符串搜索。 |
| **\-cfg=***文件名* | 指定除默认以外的配置文件。 |
| **\-color** | 如果可用，则使用彩色模式。 |
| **\-cookies** | 切换处理 Set-Cookie 头。 |
| **\-cookie_file=***文件名* | 将 Cookie 存储在指定的文件名中。 |
| **\-core** | 切换强制核心转储。 |
| **\-dont_wrap_pre** | 禁止 `<pre>` 标签内文本的换行。 |
| **\-editor=***编辑器* | 使用指定的编辑器进行外部编辑。 |
| **\-emacskeys** | 启用类似 emacs 的按键移动。 |
| **\-enable_scrollback** | 切换与通信程序回滚按键的兼容性。 |
| **\-error_file=***文件名* | 将错误写入指定的文件名。 |
| **\-force_html** | 强制将第一个文档解释为 HTML。 |

