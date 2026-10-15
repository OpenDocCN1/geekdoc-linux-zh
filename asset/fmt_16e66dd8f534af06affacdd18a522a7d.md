
如果为 `true`，则本地识别 `flush`、`interrupt`、`quit`、`erase` 和 `kill` 字符（见 `set`），并将其转换为相应的 TELNET 控制序列 `ao`、`ip`、`brk`、`ec` 和 `el`（见 `send`）。此切换的初始值在“行行”模式下为 `true`，在“逐字符处理”模式下为 `false`。如果启用过 `LINEMODE`，则 `quit` 被发送为 `abort`，而 `of` 和 `susp` 被发送为 `eof` 和 `susp`（见 `send`）。

## telnet 1333

`netdata` 切换显示所有网络数据（十六进制格式）。初始值为 `false`。

`options` 切换显示某些内部 TELNET 协议处理（与 `telnet` 选项有关）。初始值为 `false`。

`outbinary` 启用或禁用输出上的二进制（BINARY）选项。

`prettdump` 当 `netdata` 切换启用时，如果启用了 `prettdump`，则以更易于用户阅读的格式格式化来自 `netdata` 命令的输出。在输出的每个字符之间插入空格。任何 TELNET 转义序列的开头都会带有一个星号（`*`），用以帮助定位。

`skiprc` 在打开连接时，跳过读取用户主目录下的 `.telnetrc` 文件。初始值为 `false`。

`termdata` 切换显示所有终端数据（十六进制格式）。初始值为 `false`。

`?` 显示所有合法的切换命令。

`status` 显示 `telnet` 的当前状态，包括你所连接的对端和当前模式。

`z` 挂起 `telnet`。此命令仅在你使用支持作业控制的 shell（如 `sh(1)`）时有效。

`[command]` 获取帮助。如果不带参数，打印帮助摘要。如果指定了命令，且不带参数，则打印该命令的帮助信息。

## Files

`$HOME/.telnetrc` 在启动 `telnet` 会话之前执行的命令。

`/etc/nlogin` 在系统关闭期间尝试登录的用户显示的显示消息。

## Attributes

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNWcsu |

## 1334

另见

`login(1)`, `sh(1)`, `stty(1)`, `hosts(4)`, `nlogin(4)`, `telnetrc(4)`, `attributes(5)`, `inet(7P)`

## Diagnostics

`NO LOGINS`: 系统将在 N 分钟后关闭

系统正在关闭过程中，已禁用登录。

## test — 评估条件

### Synopsis

```
/usr/bin/test [condition]
```
`[condition]`

`sh`, `ksh`

`test condition`

`[condition]`

## Description

参见 `if(1)`。

## tftp — 简单文件传输程序

### Synopsis

```
/usr/bin/tftp [host]
```

## Description

`tftp` 命令是用户使用接口访问互联网 TFTP（简单文件传输协议）的程序，它使用用户数据报协议（UDP）而不是 `tftp` 使用的传输控制协议（TCP）。当你没有远程系统的登录权限且想要传输公开读取的文件时，可以使用 `tftp`。因为 `tftp` 不验证用户，因此是不安全的。由于 TFTP 协议内部没有用户登录或验证，许多远程站点以各种方式限制文件访问。允许的文件访问方法取决于每个站点，因此无法在此处记录。

`tftp` 在需要时与远程系统通信，不会与远程主机建立交互式会话。

## 1335

你可以在命令行上指定远程主机，在这种情况下，`tfftp` 将 `host` 作为后续传输的默认主机（参见 `connect` 命令）。

注意 — 默认传输模式为 `ascii`。此默认值与预 SunOS 4.0 和预 4.3 BSD 系统不同，在传输可执行命令等非 ASCII 二进制文件时，必须采取显式操作。

## Usage

一旦 `tfftp` 运行，它会发出 `tfftp>` 提示并识别以下命令。

# Commands

```
connect host-name [port]
```

设置传输的主机（可选端口）。与 FTP 不同，TFTP 协议传输之间不维持连接；因此，`connect` 命令实际上并没有创建连接，而只是记录用于传输的主机。你不需要使用 `connect` 命令；可以在 `get` 或 `put` 命令中指定远程主机。

```
mode transfer-mode
```

设置传输模式；`transfer-mode` 可以是 `ascii` 也可以是 `binary`。默认值为 `ascii`。

```
put filename
put localfile remotefile
put filename1 filename2... filenameN remote-directory
```

将文件或一组文件传输到指定的远程文件或目录。目标可以是两种形式之一：如果已经指定了主机，则为远程主机上的文件名；或者使用如下格式的字符串来同时指定主机和文件名。

```
host:filename
```

如果你使用后一种格式，指定的主机将成为后续传输的默认主机。如果你使用 `remote-directory` 形式，则假设远程主机运行着 UNIX 系统。只有当文件已存在且公开写时才能写入文件（参见 `.tftpd(1)`）。

```
get filename
get remotename localname
get filename1 filename2... filenameN
```

从指定的远程源获取文件或一组文件。源可以是两种形式之一：如果已经指定了主机，则为远程主机上的文件名；或者使用如下格式的字符串来同时指定主机和文件名。

```
host:filename
```

如果你使用后一种格式，最后指定的主机将成为后续传输的默认主机。使用 `get` 命令从远程主机传输多个文件时，必须指定三个或更多文件。如果你指定两个文件，则第二个文件将用作本地文件。

- `quit` 退出 `ftftp`。文件结束也会退出。
- `verbose` 切换详细模式。
- `trace` 切换数据包跟踪。
- `status` 显示当前状态。
- `remxt` `retransmission-timeout` 设置每个包重传超时时间（秒）。
- `timeout` `total-transmission-timeout` 设置总传输超时时间。
- `ascii` `mode` 的缩写。
- `binary` `mode` 的缩写。
- `?` 打印帮助。

## 1361

## Attributes

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNWcsu |

## 1334

另见
`login(1)`, `sh(1)`, `stty(1)`, `hosts(4)`, `nlogin(4)`, `telnetrc(4)`, `attributes(5)`, `inet(7P)`

## Diagnostics

`NO LOGINS`: 系统将在 N 分钟后关闭
系统正在关闭过程中，已禁用登录。

## test — 评估条件

### Synopsis

```
/usr/bin/test [condition]
```
`[condition]`

`sh`, `ksh`

`test condition`

`[condition]`

## Description

参见 `if(1)`。

## tftp — 简单文件传输程序

### Synopsis

```
/usr/bin/tftp [host]
```

## Description

`tftp` 命令是用户使用接口访问互联网 TFTP（简单文件传输协议）的程序，它使用用户数据报协议（UDP）而不是 `tftp` 使用的传输控制协议（TCP）。当你没有远程系统的登录权限且想要传输公开读取的文件时，可以使用 `tftp`。因为 `tftp` 不验证用户，因此是不安全的。由于 TFTP 协议内部没有用户登录或验证，许多远程站点以各种方式限制文件访问。允许的文件访问方法取决于每个站点，因此无法在此处记录。`tftp` 在需要时与远程系统通信，不会与远程主机建立交互式会话。

## 1335

你可以在命令行上指定远程主机，在这种情况下，`tfftp` 将 `host` 作为后续传输的默认主机（参见 `connect` 命令）。

注意 — 默认传输模式为 `ascii`。此默认值与预 SunOS 4.0 和预 4.3 BSD 系统不同，在传输可执行命令等非 ASCII 二进制文件时，必须采取显式操作。

## Usage

一旦 `tfftp` 运行，它会发出 `tfftp>` 提示并识别以下命令。

# Commands

```
connect host-name [port]
```

设置传输的主机（可选端口）。与 FTP 不同，TFTP 协议传输之间不维持连接；因此，`connect` 命令实际上并没有创建连接，而只是记录用于传输的主机。你不需要使用 `connect` 命令；可以在 `get` 或 `put` 命令中指定远程主机。

```
mode transfer-mode
```

设置传输模式；`transfer-mode` 可以是 `ascii` 也可以是 `binary`。默认值为 `ascii`。

```
put filename
```
