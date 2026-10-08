

# 406

# ftp

mget remote-files

展开远程机器上的 `remote-files`，并对产生的每个文件名执行 `get`。有关文件名展开的详情请参见 `glob`。根据 `case`、`ntrans` 和 `nmap` 设置处理生成的文件名。将文件传输到本地工作目录，您可以使用 `lcd directory` 更改目录；可以使用 `! mkdir directory` 创建新的本地目录。

mkdir directory-name

在远程机器上创建一个目录。

mls remote-files local-file

类似于 `ls1`，但您可以指定多个远程文件。如果开启了交互式提示，ftp 会提示您确认最后一个参数是用于接收 `mls` 输出的目标本地文件。

mode [mode-name]

将传输模式设置为 `mode-name`。唯一有效的 `mode-name` 是 `stream`，它对应默认的流式模式。此实现仅支持 `stream` 且必须指定。

mput local-files

展开作为参数提供的本地文件列表中的通配符，并对结果列表中的每个文件执行 `put`。根据 `ntrans` 和 `nmap` 设置处理生成的文件名。

nmap [inpattern]

设置或取消文件名映射机制。如果未指定任何参数，则取消文件名映射机制。如果指定了参数，则在执行未指定远程目标文件的 `mput` 和 `put` 命令时对远程文件名进行映射。

`nmap` 命令在连接到具有不同惯例或实践的非 UNIX 系统主机时非常有用。映射遵循由 `inpattern` 和 `outpattern` 设置的模式；`inpattern` 是输入文件名的模板（该文件名可能已经根据 `ntrans` 和 `case` 设置经过了处理）。通过在 `inpattern` 中包含序列 `$1`, `$2`, ..., `$9` 来实现变量模板化。使用 `\` 防止对 `$` 进行这种特殊处理。所有其他字符均被视为字面量，并用于确定 `nmap inpattern` 变量的值。

例如，给定 `inpattern` 为 `$1.$2` 且远程名为 `mydata.data`，则 `$1` 的值为 `mydata`，`$2` 的值为 `data`。

# 407

`outpattern` 决定了映射后的结果文件名。序列 `$1`, `$2`, ..., `$9` 被替换为 `inpattern` 模板产生的任何值。序列 `$0` 被替换为原始文件名。此外，如果 `seq1` 不是空字符串，则序列 `[seq1,seq2]` 被替换为 `seq2`。

例如，命令 `mmap $1,$2 $3 [$1], [$2]` 对于输入文件名 `myfile.data` 和 `myfile.old` 会产生输出文件名 `myfile.data`；对于输入文件名 `myfile.data` 会产生 `myfile.file`；对于输入文件名 `myfile` 会产生 `myfile.myfile`。您可以在 `outpattern` 中包含空格字符，如示例 `mmap $1 | sed "s*/*/"` ,.` 所示。

ntrans [outchars]

设置或取消文件名字符翻译机制。如果未指定任何参数，则取消文件名字符翻译机制。如果指定了参数，则在执行未指定远程文件名的 `mput` 和 `put` 命令时翻译远程文件名中的字符，并在执行未指定本地目标文件的 `mget` 和 `get` 命令时翻译本地文件名中的字符。

`ntrans` 命令在连接到具有不同文件命名惯例或实践的非 UNIX 系统远程主机时有用。文件名中匹配 `inchars` 中字符的字符将被替换为 `outchars` 中对应的字符。如果字符在 `inchars` 中的位置长于 `outchars` 的长度，则从文件名删除该字符。

在 ftp 上使用 `ntrans` 命令时只能翻译 16 个字符。如果需要转换整个字母表，请使用 `case`。

open host [port]

与指定的主机 FTP 服务器建立连接。您可以提供一个可选的端口号，在这种情况下，ftp 会连接该端口的 FTP 服务器。如果开启了自动登录选项（默认设置），ftp 会尝试自动为用户登录 FTP 服务器。

prompt

切换交互式提示的开启。交互式提示在处理多个文件期间发生，允许您选择性地检索或存储文件。默认情况下，提示是开启。如果您尝试关闭提示，任何 `anyget` 将传输所有文件，任何 `mdelete` 将删除所有文件。

proxy ftp-command

在次级控制连接上执行 FTP 命令。`proxy` 命令允许同时连接两个远程 FTP 服务器，以便在两个服务器之间传输文件。第一个 `proxy` 命令应该是 `open`，用于建立次级控制连接。输入命令 `proxy ?` 可查看在次级连接上可执行的其他 FTP 命令。

# 408

以下命令在带有 `proxy` 前缀时行为会有所不同：`open` 在自动登录过程中不定义新宏；`close` 不擦除现有的宏定义；`get` 和 `mget` 从主控制连接上的主机传输文件到次级控制连接上的主机；而 `put`、`mput` 和 `append` 从次级控制连接上的主机传输文件到主控制连接上的主机。

第三方文件传输取决于次级控制连接上的服务器对 `PASV` 命令的支持。

```
local-file [remote-file]
```

在远程机器上存储本地文件。如果未指定 `remote-file`，则使用经过任何 `ntrans` 或 `nmap` 设置后的本地文件名命名远程文件。文件传输使用当前的表示类型、文件结构和传输模式设置。

```
pwd
```

打印远程机器上当前工作目录的。

```
quit
```

`bye` 的同义词。

```
quote arg2..
```

将参数原封不动地发送到远程 FTP 服务器。预期返回单个 FTP 回复代码。（`remotehelp` 命令显示有效参数的列表。）仅当您是熟悉 FTP 协议的高级用户时使用 `quote`。

```
recv remote-file [local-file]
```

`get` 的同义词。

```
remotehelp [command-name]
```

向远程服务器请求帮助。如果指定了 `command-name`，也会提供给服务器。

```
rename from
```

重命名远程机器上名为 `from` 的文件为 `to`。

```
reset
```

清除队列。此命令与远程 FTP 服务器同步。当远程服务器违反 FTP 协议时，可能需要重置。

```
rmdir directory-name
```

删除远程机器上的一个目录。

# ftp 409

unique 在本地系统中以唯一文件名存储文件。如果 `get` 或 `mget` 命令的目标本地文件名已存在，则在名称上附加 `.1`。如果生成的名称与另一个现有文件匹配，则在原始名称上附加 `.2`。如果此过程持续到 `.99`，则打印错误消息并终止传输。报告生成的唯一文件名。`unique` 不影响从 shell 命令生成的文件。默认值为关闭。

send local-file [remote-file]

`put` 的同义词。

sendport 切换 `PORT` 命令的使用。默认情况下，ftp 在建立每次数据传输连接时尝试使用 `PORT` 命令。在执行多个文件传输时，使用 PORT 命令可以防止延迟。如果 PORT 命令失败，ftp 将使用默认数据端口。当您禁用 PORT 命令的使用时，将不会尝试为每次数据传输使用 PORT。此选项对于连接到某些错误指示已接受 PORT 命令的 FTP 实现有用。

status 显示 ftp 的当前状态。

struct [struct-name]

将文件结构设置为 `struct-name`。唯一有效的 `struct-name` 是 `file`，它对应默认的文件结构。此实现仅支持 `file` 且必须指定。

unique 在远程机器上以唯一文件名存储文件。远程服务器必须支持 `STOU` 命令才能成功完成。远程服务器报告唯一名称。默认值为关闭。

tenex 将表示类型设置为与 TENEX 机器通信所需的类型。切换数据包跟踪（未实现）。

type [type-name] 将表示类型设置为 `type-name`。有效的类型名称包括用于网络 ASCII 的 `ascii`、用于图像的 `binary` 或 `image`，以及用于本地按 8 字节大小与 TENEX 机器通信的 `tenex`。如果您未指定类型，ftp 会打印当前类型。默认类型为 `ascii`。

user-name [password] [account] 向远程 FTP 服务器识别身份。如果您未指定密码且服务器需要，ftp 会提示您输入（在禁用本地回显后）。如果您未指定账户字段且 FTP 服务器需要，则会提示您输入。如果您指定了账户，命令到远程服务器将完成登录序列而无需在登录时要求它。除非在调用 ftp 时禁用了自动登录，否则此过程在初始连接到 FTP 服务器时自动完成。

