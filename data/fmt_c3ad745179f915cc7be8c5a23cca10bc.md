
# 第3章 网络

现有的宏定义、从主控制连接上的主机到从级控制连接主机的 `get` 和 `mqtt` 传输，以及从从级控制连接上的主机到主控制连接主机的 `put`、`mput` 和 `append` 传输文件。第三方文件取决于从级控制连接上的服务器对 FTP 协议 `PASV` 命令的支持。

### `put local-file [remote-file]`
将 `local-file` 拷贝到 `remote-file`。
如果未指定 `remote-file`，
`ftp` 将将 `local-file` 名称（根据任何
`trans` 或 `nmap` 设置处理）分配给 `remote-file` 名称。

### `prm`
将远程工作目录的名称写入标准输出。

### `quit`
`bye` 的同义词。

### `quote arguments`
将参数发送到服务器主机。详见 `ftppd(1M)`。

### `recv remote-file [local-file]`
`get` 的同义词。

### `remget remote-file [local-file]`
`remget` 的行为类似于 `get`，但如果 `local-file` 存在且
小于 `remote-file`，则假设 `local-file` 是
`remote-file` 的部分传输副本，并从明显的故障点
继续传输。此命令在会断开连接的网络上传输
大文件时非常有用。

### `rhelp [command-name]`
向服务器主机请求帮助。如果指定了 `command-name`，
将其提供给服务器。详见 `ftppd(1M)`。

### `rstatus [file-name]`
带参数时，显示远程机器的状态。如果指定了 `file-name`，
则显示远程机器上 `file-name` 的状态。

### `rename-from-remote-to`
将 `remote-from`（可以是文件或目录）重命名为
`remote-to`。

### `reset`
清除重试队列。此命令将与远程 FTP 服务器的
命令/响应序列进行重新同步。在远程服务器
违反 FTP 协议后，可能需要进行重新同步。

### `restart marker`
重启紧随其后的命令，或在指定的
标记 `marker` 处重启。在 UNIX 系统上，`marker` 通常是文件的字节偏移量。

### `rmdir remote-directory`
删除 `remote-directory`。`remote-directory` 必须是一个
空目录。

### `runique`
切换在本地系统上使用唯一文件名存储文件。
如果已存在与 `get` 或 `met` 命令的目标文件
同名的文件，则在名称后附加 `.1`。如果生成的名称
与另一个现有文件匹配，则在原始名称后附加 `.2`。
如果此过程持续到 `.99`，则会打印错误信息且
不进行传输。`ftp` 会报告唯一文件名。

## `ftp`

注意，`runique` 不影响从 shell 命令生成的本地文件（见下文）。其默认值为关闭。

### `send local-file [remote-file]`
`put` 的同义词。

### `sendport`
切换是否使用 `PORT` 命令。默认情况下，`ftp` 在为
每次数据传输建立连接时尝试使用 `PORT` 命令。
如果 `PORT` 命令失败，`ftp` 将使用默认数据端口。
当禁用 `PORT` 命令的使用时，`ftp` 不会尝试为
每次数据传输使用 `PORT` 命令。这对于某些忽略 `PORT` 命令但（错误地）指示其已接受的
FTP 实现很有用。详见 `ftppd(LM)`。关闭端点可能会导致命令执行延迟。

### `site arguments`
将参数原封不动地作为 `SITE` 命令发送到服务器主机。
详见 `ftppd(LM)`。

将 `remote-file` 复制到 `local-file`。如果未指定 `local-file`，`ftp` 使用指定的 `remote-file` 名称作为 `local-file` 名称，但受当前 `case`、`ntrans` 和 `nmap` 设置的影响。

```
glob
```
切换文件通配符。当启用文件匹配通配符时，`ftp` 会展开文件名和目录中的 `sh(*)`。这些字符包括 `*`、`?`、`[`、`]`、`~` 和 `()`。服务器会展开远程文件和目录名。`ftp` 命令的通配符始终会被展开。如果启用了通配，多文件命令 `mdelete`、`mdr`、`mget`、`mls` 和 `mput` 也会展开这些元字符。

```
hash
```
每传输 1024 字节切换一次哈希符号（`#`）。

```
help [command]
```
打印关于 `ftp` 命令 `ftp-command` 的信息消息。如果未指定 `ftp-command`，则打印所有 `ftp` 命令列表。

```
id [seconds]
```
将远程服务器上的空闲计时器设置为秒数。如果省略 `seconds`，`ftp` 将打印当前空闲计时器。

```
lcd [local-directory]
```
将本地工作目录设置为 `local-directory`。如果未指定 `local-directory`，则将本地工作目录设置为用户的家目录。

```
ls [remote-directory] [local-file]
```
将 `remote-directory` 列表写入 `local-file`。列表包含服务器选择包含的任何依赖于系统的信息；例如，大多数 UNIX 系统通过 `ls` 命令生成（另参见 `list`）。如果既未指定 `remote-directory` 也 `local-file`，则列出远程工作目录。如果启用了通配符，元字符将被展开。

```
macdef macro-name
```
定义一个宏。随后的行将存储为宏 `macro-name`；空行将终止宏输入模式。所有定义的宏限制为 16 个，总字符数为 4096 个。宏将一直保留到执行 `close` 命令。宏处理器将 `$` 和 `\` 解析为特殊字符。`$` 后跟一个数字（或多个数字）将被替换为宏调用命令行上的对应参数。

```
rm remote-file
```
删除 `remote-file`。`remote-file` 可以是一个空目录。禁用通配符。

```
delete remote-file.
```
删除 `remote-file`。`remote-file` 可以是一个空目录。

```
get remote-file [local-file]
```
将 `remote-file` 复制到 `local-file`。如果未指定 `local-file`，`ftp` 使用指定的 `remote-file` 名称作为 `local-file` 名称，但受当前 `case`、`ntrans` 和 `nmap` 设置的影响。
