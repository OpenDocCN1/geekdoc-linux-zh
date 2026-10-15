
## Gated 选项

- `-c coresize` 指定 `gated` 可能生成的核心转储大小的上限。通常用于当系统默认值小到无法使用时增加它。
- `-f filesize` 指定由 `gdc` 启动的 `gated` 可以产生的最大文件。
- `-m datasize` 指定由 `gdc` 启动的 `gated` 数据段大小的上限。
- `-s stacksize` 指定由 `gdc` 启动的 `gated` 栈的最大。

在命令行上可以指定以下操作：

- `checkconf /etc/gated.conf` 检查语法错误。
- `checknew /etc/gated.conf+` 检查语法错误。
- `newconf` 用 `/etc/gated.conf-` 替换 `/etc/gated.conf`。
- `backout` 将旧配置文件 (`/etc/gated.conf-`) 移回位置作为当前活跃的 `gated`。同时将当前的 `/etc/gated.conf` 轮转到 `/etc/gated.conf+`
- `BACKOUT` 与 `gated`（上述）相同，但将覆盖现有的 `/etc/gated.conf+`
- `modeconf` 将所有配置文件设置为模式 `664`，`owner=root`
- `modeconf` 将所有配置文件设置为模式 `664`，所有者=`root`。

## 命令

- `checkconf /etc/gated.conf` 检查语法错误。
- `checknew /etc/gated.conf+` 检查语法错误。
- `newconf` 用 `/etc/gated.conf-` 替换 `/etc/gated.conf`。
- `backout` 将旧配置文件 (`/etc/gated.conf-`) 移回位置作为当前活跃的 `gated`。同时将当前的 `/etc/gated.conf` 轮转到 `/etc/gated.conf+`
- `BACKOUT` 与 `gated`（上述）相同，但将覆盖现有的 `/etc/gated.conf+`
- `modeconf` 将所有配置文件设置为模式 `664`，`owner=root`。

## 守护进程

### imapd

- `-d` 调试模式。此选项违反了协议并可能产生安全漏洞。请谨慎使用。
- `-F<format>` 以指定的格式显示信息。格式包括：
  `%u` 用户名
  `%U` 用户数字
  `%g` (主) 组名
  `%G` (主) 组数字
  `%I` 按名称列出所有组
  `%L` 按数字列出所有组
  `%p` 运行进程的进程 ID
  `%c` 命令名
  `%C` 命令和参数
- `-v` 详细输出。
- `-f<config-file>` 使用指定的配置文件而不是默认文件。目前没用，因为不涉及任何配置文件。

`/usr/etc/imimap` 支持 IMAP4 远程邮件访问协议，通常在端口 `143` 上。示例：此守护进程通常由 `inetd` 调用。要启动 `imapd`：

```
imap stream tcp nowait root /usr/sbin/tcpd imapd
```

`inetd` 是守护进程的母体。它不直接提供任何用户服务，但它调用提供服务的其他守护进程。`inetd` 的创建是因为许多守护进程偶尔需要。然而，为了能够使用，守护进程必须监控端口以服务请求。为了进行监控，它们会占用系统资源。如果你配置了许多服务，这将是一个巨大的负担。`inetd` 通过监控其他守护进程的端口并在需要时调用它们来缓解这个问题。`inetd` 应该在启动时由 `/etc/rc.local` 启动。

示例：要调用 `inetd`，请创建一个包含以下行的脚本：

```
inetd &
```

- `-d` 以调试模式调用 `inetd`。
- `-q queuelength` 指定 socket 监听队列的长度（默认`128`）。

### klogd

```
klogd [-c n] [-d] [-f fname] [-il] [-n] [-o] [-p] [-s] [-k fname] [-v]
```

`klogd` 是内核日志守护进程。它拦截并记录 Linux 内核消息。

示例：此守护进程通常由 `init` 调用，可能带有如下行（`&` 它在后台运行）：

```
klogd &
```

- `-c n` 指定控制台消息的默认日志级别。
- `-d` 调试模式。
- `-f file` 将日志记录到指定的文件而非 `syslog`。
- `-i, -l` 向当前执行的 `klogd` 守护进程发送信号。
- `-n` 不自动后台运行。
- `-o` 一次性模式。读取并记录内核消息缓冲区中的所有消息，然后退出。
- `-p` 疯狂模式。每当在内核消息流中发现 `Oops` 字符串时，加载内核模块符号信息。
- `-s` 使用系统调用接口访问内核消息缓冲区。
- `-k file` 使用指定的文件作为内核符号信息的源。
- `-v` 显示版本信息并退出。

## Commands

### lpd [-l] [port#]

`lpd` 是线路打印机守护进程。它处理池化文件的操作和任何实际打印。它从 `printcap` 获取打印机信息。原始调用只监听请求；它会派生子进程来处理收到的任何请求。

示例：此守护进程通常由 `rc` 脚本调用。要启动带日志的 `lpd`，请在脚本中放置如下行的行：

```
lpd -l &
```

- `-l` 开启请求的日志记录。
- `port#` 允许用户在命令行上指定互联网端口号，而不是让进程从 `getsbyname` 获取端口号。

```
/usr/bin/rpc.mountd [-f exports-file] [ -d facility ] [ -P port ] [-Dhnprv ] [ --debug facility ] [ --exports-file=file ] [ -help ] [ --allow-non-root ] [ --re-export ] [ -version ]
```

`mount` 是 NFS 挂载守护进程。在导出文件系统之前，它会检查 `/etc/exports` 权限。如果请求被批准，它会为请求的目录创建一个文件句柄并在 `/etc/rmtab` 中添加条目。卸载时，会删除 `/etc/rmtab` 中的条目。

示例：此守护进程通常在启动时通过脚本调用，行如下：

```
mountd &
```

要从 `inetd` 启动 `mountd`，请向 `/etc/inetd.conf` 添加以下两行：

```
mount-1/2 dgram rpc/udp wait root /usr/bin/rpc.mountd rpc.mountd
mount-1/2 stream rpc/tcp wait root /usr/bin/rpc.mountd rpc.mountd
```

- `-f --exports-file` 指定除默认 `/etc/exports` 之外的导出文件。
- `-d --debug` 开启每个事务到标准误差的详细日志。
- `-F --foreground` 在前台运行 `mountd`。
- `-h` 或 `--help` 显示帮助信息并退出。
- `-n` 或 `--allow-non-root` 允许来自非保留 IP 端口的挂载请求。
- `-P portnum` 或 `--port portnum` 指定 `inetd` 监听的端口。通常端口号在 `/etc/` 中指定。
- `-p` 或 `--promiscuous` 告诉 `mountd` 服务网络上的任何主机。
- `-r` 或 `--re-export` 允许重新导出导入的 NFS 或 SMB 文件系统。
- `-v` 或 `--version` 显示版本信息并退出。

### named

```
named [-d debuglevel] [-p port#] [-(b|c) config_file] [-l-fq-r] [-u user_name] [-g group_name] [-t directory] [-w directory] [config_file]
```

`Named` 是互联网域名服务器。它将主机名解析为 IP 地址。`Named` 从 `/etc/named.conf` 获取配置信息。

示例：此守护进程通常由 `inetd` 调用。带某些调试信息启动 `named`：

```
named -d 1 &
```

## ROOT

- `-d debuglevel` 指定调试信息的级别。
- `-p port#` 告诉 `named` 使用指定的远程端口号。
- `-(b|c) config_file` 指定备用配置文件（默认为 `/etc/named.conf`）。
- `-f` 告诉 `named` 在前台运行。
- `-q` 如果 `NAMED` 编译时定义了 `QRYLOG`，则跟踪所有入站查询。
- `-r` 递归仅允许从本地（主或次）区域进行名称解析。

## Commands

- `-u user_name` 告诉 `named` 在初始化后作为指定用户运行。
- `-g group_name` 告诉 `named` 在初始化后作为指定组运行。
- `-t directory` 告诉 `named` 在处理任何命令行参数后切换到指定目录的 `root`。
- `-w directory` 为服务器指定工作目录。
