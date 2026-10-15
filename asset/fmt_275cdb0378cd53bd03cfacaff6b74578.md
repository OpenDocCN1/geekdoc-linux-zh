
## 第 7 章 配置网络

| `-M` | 此选项使用 `"WinPopUp"` 向另一计算机发送消息。 | `cat message.txt SMB/CIFS client -M user` |

| `-A` | 这允许您指定一个文件，从文件中读取连接时使用的用户名和密码。 | `-A filename` |

| `-N` | 抑制正常的密码提示。 | `-N` |

| `-I` | 指定一个文件名，运行中的客户端的操作数据将记录到其中。 | `-I logfilename` |

| `-L` | 列出服务器上可用的服务。 | `-L host` |

| `-I` | IP 地址是要要连接的服务器地址。通常与 `-L` 使用。 | `-I 10.0.0.250` |

### 开关

| 开关 | 描述 | 示例 |
| --- | --- | --- |
| `-E` | 使客户端将消息写入标准错误流 (`stderr`) 而不是标准输出流。 | `-E` |
| `-c` | 用分号分隔的命令字符串，用于执行而非通过提示 `stdin`。使用 `-c` 会隐含 `-N`。 | `-c command string such as -c 'print'` |
| `-i` | 指定 `SMB/CIFS` 客户端在进行 `NetBIOS` 名称通信时使用的 `NetBIOS` 套接。 | `-i scope` |
| `-O` | 客户端套接上设置 `TCP` 选项。`SMB/CIFS.conf` 手列出了有效选项。 | `-O socket options` |
| `-p` | 该数字是连接服务器时使用的 `TCP` 端口号，而不是标准的 `TCP` 端口。 | `-p port` |
| `-R` | 域名解析顺序，带有 `"Imhosts","host","wins"` 和 `"bcast"` 选项。 | `-R Imhosts` |
| `-s` | 提供 `SMB/CIFS.conf` 文件的位置。 | `-s SMB/CIFS.conf` |
| `-T` | 可使用 `SMB/CIFS` 客户端创建 `SMB/CIFS` /CIFS 共享上所有文件的兼容备份。 | `//server/share "" -N -Tc backup.tar *` |

考试提示：不仅要了解开关，还要熟悉 Linux 中使用的所有命令的格式。

表 7-3 中的这些开关用于创建连接。连接后，用户将看到一个如下所示的新提示符：

```
SMB/CIFS :>
```

该提示符表示客户端已就绪，并等待执行用户命令。用户命令显示在表 7-3 中。

### 表 7-3

### SMB/CIFS 客户端命令

| 命令 | 描述 | 示例 |
|---|---|---|
| `?` | 用于提供有关命令的信息。 | `? [command]` |
| `!` | `!` 命令将在本地执行 `shell` 并运行指定的命令。 | `! [shell command]` |
| `cd` | 用于更改目录，如果没有请求特定目录，它将列出当前目录。 | `cd [directory name]` |
| `del` | 客户端将请求服务器尝试删除当前目录下所有匹配 `"mask"` 的文件。 | `del <mask>` |
| `dir` | 将检索并显示当前目录下匹配 `"mask"` 的文件列表。 | `dir <mask>` |
| `exit` | 退出 `SMB/CIFS` 客户端程序；这将终止所有连接。 | `exit` |
| `get` | 获取远程文件 `<name>` 并将其复制到本地文件 `[name]`。这是一次二进制传输。 | `get <remote file name> [local file name]` |
| `help` | 用于提供有关命令的信息。 | `help [command]` |
| `lcd` | 将本地机器上的当前工作目录更改指定的目录。 | `lcd [directory name]` |
| `lowercase` | 当小写切换为开启时，使用 `get` 和 `m` 命令将本地文件名转换为小写。 | `lowercase` |
| `ls` | 将检索并显示当前目录下匹配 `"mask"` 的文件列表。 | `ls <mask>` |
| `mask` | 此命令允许用户设置掩码，该掩码将在 `mget` 和 `mput` 命令的递归操作中使用。 | `mask <mask>` |
| `md` | 用于创建一个指定名称的新目录。 | `md <directory name>` |

| 命令 | 描述 | 示例 |
| --- | --- | --- |
| `mget` | 从服务器复制所有匹配 `mask` 的文件到运行中的客户端。 | `mget <mask>` |
| `mkdir` | 用于创建一个指定名称的新目录。 | `mkdir <directory name>` |
| `mput` | 从运行中的客户端复制所有匹配 `mask` 的文件到服务器。 | `mput <mask>` |
| `get` | 获取远程文件 `<name>` 并将其复制到本地文件 `[name]`。这是一次二进制传输。 | `get <remote file name> [local file name]` |
| `lcd` | 将本地机器上的当前工作目录更改指定的目录。 | `lcd [directory name]` |
| `lowercase` | 当小写切换为开启时，使用 `get` 和 `m` 命令将本地文件名转换为小写。 | `lowercase` |
| `ls` | 将检索并显示当前目录下匹配 `"mask"` 的文件列表。 | `ls <mask>` |
| `mask` | 此命令允许用户设置掩码，该掩码将在 `mget` 和 `mput` 命令的递归操作中使用。 | `mask <mask>` |
| `md` | 用于创建一个指定名称的新目录。 | `md <directory name>` |

## 第三部分 配置

### NIS 配置

更多信息见第 5 章。

`ypbind` 通常位于 `/usr/sbin`。其他二进制文件（`ypcat`, `ypassword`, `ypoll`）通常位于 `/usr/bin`。大多数 `ypbind` 版本都有一个配置文件 `etc.conf`。对于主机查找，您必须在 `etc.conf` 中添加 `"nis"`，或者可以如图 7-20 所示进行配置。

**图 7-20: 配置 NIS**

使用以下清单测试 `NIS`：

- 启动 `/usr/sbin/portmap`。
- 启动 `/usr/sbin/ypbind`。
- 使用命令 `rpcinfo -p localhost` 检查 `ypbind` 是否已向 `portmap` 注册。
- 运行 `rpcinfo -u localhost ypbind`。
- 命令 `ypcat` 提供整个密码数据库。

### NFS 配置

要验证 `NFS` 客户端软件是否可以在 `/proc` 文件系统上运行，请检查 `/proc/filesystems` 文件并确保其中包含 `NFS` 的行。如果没有，您将需要编译内置支持的内核。

有关升级的更多信息请见第 5 章。

## 配置互联网服务

### 3.6 配置基础互联网服务（例如 HTTP, POP, SMTP, SNMP, FTP）

### 3.15 配置访问权限（例如 登录 NIS, FTP, TFTP, SSH, Telnet）

互联网服务的配置是一个非常广泛的话题。客户端服务通常指的是广域网、电子邮件、新闻组和 `FTP` 客户端。配置这些服务需要了解你正在提供的是哪种服务的知识。

### Web 浏览器

`Web` 浏览器用于通过超文本传输协议（`HTTP`）使用超文本标记语言（`HTML`）查看 `Web` 页面。配置第三方 `Web` 浏览器或内置浏览器（如 `KDE Konqueror Web` 浏览器）不需要多少费力。这些程序使用网络配置中的设置。在系统分配了 `IP` 地址、默认路径（网关）和 `DNS` 之后，`Web` 浏览器将使用这些设置访问内网或互联网。然而，在某些环境中，这些设置可能是不够。例如，如果使用代理服务器来管理用户的互联网访问，你必须配置一个额外的设置来指定代理服务器的地址。

### POP 和 SMTP

`POP3` 和 `SMTP` 结合使用，为客户端提供发送和接收电子邮件的能力。`POP3`（或邮局协议 3）是用于从服务器下载电子邮件到客户端的标准接收协议的最新版本。`POP3` 系统会保留电子邮件，直到客户端连接；客户端连接后，邮件将下载到客户端的系统中。简单邮件传输协议（`SMTP`）用于发送和接收电子邮件。由于其局限性，`SMTP` 通常用于服务器到服务器的邮件传输以及客户端上传消息。

`IMAP` 标准是 `POP3` 的替代方案。它允许客户端从邮件服务器访问电子邮件，而在没有收到客户端指示之前，不会将其从服务器上删除。

`POP3` 和 `SMTP` 客户端的基本配置需要一些信息。你需要将以下信息插入到邮件客户端中。

- 用户名（User Name）
- 电子邮件账户名（E-mail account name）
- `POP3` 服务器名称（用于接收的邮件）
- 使用的 `POP3 TCP/IP` 端口；默认值为 `110`，通常会使用，但可以更改
- `SMTP` 服务器名称（用于发送的邮件）
- 使用的 `SMTP TCP/IP` 端口，默认值为 `25`，通常但可以更改
- 使用的身份验证方法
