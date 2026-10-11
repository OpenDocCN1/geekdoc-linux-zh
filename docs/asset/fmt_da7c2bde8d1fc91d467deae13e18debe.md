
要终止文件传输，请使用终端中断键（通常为 `<Ctrl>-c`）

- `-v` 详细操作。显示来自远程服务器的所有响应。
- `-n` 在建立初始连接时不尝试自动登录。如果没有此选项，`ftp` 将检查用户是否具有
- `-i` 在执行多次传输时禁用提示。
- `-d` 调试模式。
- `-g` 禁用通配符匹配（globbing）。
- `-host` 要连接的客户端机器。

`ftp` 程序是交互式的。以下命令在 "`ftp>`" 提示符下有效：

- `! [command [args]]` 在本地机器上执行交互式 shell。第一个参数被视为命令；后续参数被视为参数
- `$ account [passwd]` 为访问系统提供登录信息（帐户和密码）。
- `append local-file [remote-file]` 将本地文件追加到远程机器。
- `ascii` 将文件传输类型设置为 ASCII（默认模式）。
- `bell` 在每次传输完成后响铃声。
- `binary` 将文件传输类型设置为二进制。
- `bye` 关闭所有连接并退出。
- `case` 在传输到本地机器时将文件名转换为小写。
- `cd remote-directory` 切换到远程机器上的指定目录。
- `cdup` 切换到远程机器当前目录的父目录。
- `chmod mode file-name` 修改远程系统的文件权限。

## 命令

- `close` 关闭远程主机的 FTP 会话但不退出 FTP。
- `cr` 切换 ASCII 获取期间的回车符去除。默认是去除回车符以符合 Unix 标准。
- `delete remote-file` 删除远程机器上的指定文件。
- `debug [debug-value]` 指定调试级别。
- `dir [remote-directory] [local-file]` 显示指定远程目录的内容列表或指定文件的信息。如果指定了 `local-file` 参数，列出的文件将发送到那里。
- `disconnect` 等同于 `close`。
- `form format` 将文件传输格式设置为 `format`。
- `get remote-file [local-file]` 从远程机器传输指定文件到本地机器，用于 `mdelete`、`mget` 和 `mput`。
- `glob` 切换每个 1024 字节数据块打印哈希符号（`#`）。数据块大小为 1024 字节。
- `help [command]` 显示指定命令的帮助信息。
- `idle [seconds]` 将远程机器上的空闲计时设置为指定的秒数。
- `lcd [directory]` 切换本地机器上的目录。
- `is [remote-directory] [local-file]` 显示指定远程目录的内容列表或指定文件的信息
- `macdef macro-name` 定义宏。随后的行组成宏的内容；通过输入空行结束宏定义。

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_480_0.png)

## delete [remote-files]

删除远程机器上的指定文件。

- `mdir remote-files local-file`
类似于 `dir` 命令，不同之处可以指定多个远程文件。

- `mget remote-files`
从远程机器获取指定的文件。

- `mkdir directory-name`
在远程机器上创建一个目录。

- `mls remote-files local-file`
显示远程机器上的文件列表。可以指定多个远程文件，且本地文件参数（列表发送到的接收处）是强制性的。

## mode [mode-name]

指定文件传输模式。默认是"`stream`"（流）。

- `modtime file-name`
显示指定远程文件的最近修改时间。

- `mput local-files`
将每个指定的文件传输到远程机器。

- `newer file-name [local-file]`
如果文件的修改时间比本地机器上的副本新，则检索该文件。

- `nlist [remote-directory] [local-file]`
显示指定远程目录下的文件。如果指定了 `local-file`，此命令的输出将发送到该文件而不是屏幕。

- `nmap [inpattern] [outpattern]`
切换文件映射机制。如果指定了 `inpattern` 和 `outpattern`，文件在传输过程中将根据指定的模式自动重命名。

- `ntrans [inchars] [outchars]`
切换文件名字符翻译。如果指定了字符映射，文件传输期间文件名字符将按指定进行自动翻译。

- `open host [port]`
连接到指定的主机 FTP 服务器。

- `prompt`
切换多个文件传输期间的交互式提示。

## Commands

453

| `proxy ftp-command` | 在辅助控制连接上执行 ftp 命令。此命令允许同时连接到两个远程 ftp 服务器，以便在两个服务器之间传输文件。 |
| `put local-file [remote-file]` | 将本地文件传输到远程机器。 |
| `pwd` | 显示远程机器上的当前工作目录。 |
| `quit` | 等同于 `bye`。 |
| `quote arg1 arg2 ...` | 将指定的参数原封地发送到远程 FTP 服务器。 |
| `recv remote-file [local-file]` | 等同于 `get`。 |
| `reget remote-file [local-file]` | 与 `get` 类似，但如果本地文件存在且小于远程文件，则认为传输是不完全。传输将从明显的故障点继续。 |
| `remotehelp [command-name]` | 从远程 FTP 服务器获取指定命令的帮助。 |
| `remotatus [file-name]` | 显示远程机器或远程机器上指定文件的状态。 |
| `rename [from] [to]` | 按指定重命名远程机器上的文件。 |
| `reset` | 清空回复队列。 |
| `restart marker` | 在指定的标记处重启紧随其后的 `get` 或 `put` 操作。 |
| `rmdir directory-name` | 删除远程机器上的指定目录。 |

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_482_0.png)

454

Networking Applications

- `runique` 切换使用唯一文件名存储本地文件。如果传输的目标文件已存在且设置了唯一模式，则文件不会被覆盖。相反，将生成一个具有相同基础但带有"1"扩展名的新文件（或 "2", "3", ..., "99"）。

- `send local-file [remote-file]` 等同于 `put`。

- `sendport` 切换 `PORT` 命令的使用。

- `site arg1 arg2 ...` 将指定的参数作为 `SITE` 命令原封地发送到远程 FTP 服务器。

- `size file-name` 显示机器上指定文件的大小。

- `status` 显示 `ftp` 的当前状态

- `struct [struct-name]` 将文件传输结构设置为 `struct-name`。默认使用 "`stream`" 结构。

- `sunique` 切换在远程机器上使用唯一文件名存储文件（见上文的 `runique`）。

- `system` 显示远程主机的操作系统信息。

- `tenex` 设置文件传输类型，以便与 TENEX 机器进行通信。

- `trace` 切换数据包跟踪。

- `type [type-name]` 按指定设置文件传输类型。默认是网络 ASCII。

- `umask [newmask]` 按指定设置远程服务器上的默认 `umask`。

- `user user-name [password] [account]` 将你的用户信息发送到远程 FTP 服务器。

## Commands

455

| `verbose` | 切换详细模式。 |
| `? [command]` | 等同于 `help`。 |

## hostname [NAME]

显示或设置本地机器的主机名。
示例：要显示本地机器的主机名：

```
hostname
```
