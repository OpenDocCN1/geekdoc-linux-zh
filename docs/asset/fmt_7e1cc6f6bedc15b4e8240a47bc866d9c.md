
删除远程机器上的目录。

# 412

### ftp

`unique` 切换开关，切换是否以唯一名称在本地系统上存储文件。如果在执行 `get` 或 `mget` 命令时已存在一个名称与目标本地文件名相同的文件，则在名称后附加 `.1`。如果生成的名称与另一个现有文件匹配，则在原始名称后附加 `.2`。如果此过程持续到 `.99`，则打印错误信息并终止传输。报告生成的唯一文件名。`unique` 不影响从 shell 命令生成的本地文件。默认值为 off。

`send-local-file [remote-file]`

`put` 的同义词。

`sendport` 切换开关，切换是否使用 `PORT` 命令。默认情况下，`ftp` 在每次数据传输建立连接时尝试使用 `PORT` 命令。使用 `PORT` 命令可以防止执行多次文件传输时出现延迟。如果 `PORT` 命令失败，`ftp` 将使用默认端口。当你禁用 `PORT` 命令的使用时，则不会尝试为每次数据传输使用 `PORT` 命令。当连接到某些忽略 `PORT` 命令但错误指示其已接受的 FTP 实现时，此选项非常有用。

`status` 显示 `ftp` 的当前状态。

`struct [struct-name]`

将文件结构设置为 `struct-name`。唯一有效的 `struct-name` 是 `file`，它对应默认的文件结构。该实现仅支持 `file` 并要求指定。

`sunique` 切换开关，切换是否以唯一文件名在远程机器上存储文件。远程 FTP 服务器必须支持 `STOU` 命令才能成功完成。远程服务器报告唯一名称。默认值为 off。

`tenex` 将表示类型设置为与 TENEX 机器通信所需的类型。

`trace` 切换开关，切换数据包跟踪（未实现）。

`type [type-name]`

将表示类型设置为 `type-name`。有效的 `type-names` 包括用于网络 ASCII 的 `ascii`，用于图像的 `binary` 或 `image`，以及以 8 字节为单位的本地文件的 `tenex`（用于与 TENEX 机器通信）。如果你未指定类型，`ftp` 会打印当前类型。默认类型为网络 ASCII。

`user-name [password] [account]`

向远程 FTP 服务器标识你的身份。如果你未指定密码且服务器要求提供，`ftp` 将提示你输入（在禁用本地回显后）。如果你未指定 `account` 字段且 FTP 服务器要求提供，将会提示你输入。如果你指定了 `account` 字段，则向远程服务器转发 `account` 命令。

# 413

### ftp

在登录序列完成后，如果远程服务器未要求登录则执行此操作。除非在调用 `ftp` 时禁用了自动登录，否则此过程在首次连接到 FTP 服务器时自动完成。

`verbose` 切换开启详细模式。在详细模式下，将显示来自 FTP 服务器的所有响应。此外，如果开启了详细模式并在传输完成后，将报告有关传输效率的统计信息。默认情况下，如果 `ftp` 的命令来自终端，则开启详细模式，否则不开启。

`? [command]` `help` 的同义词。

你可以使用引号（`""`）引用带有嵌入空格的参数。

如果你未指定任何未被标记为可选的命令参数，`ftp` 将提示输入该参数。

# 中止文件传输

要中止文件传输，请使用终端中断键。发送传输将立即停止。接收传输通过向远程服务器发送 FTP 协议 `ABOR` 命令并丢弃任何后续接收的数据来停止。完成此操作的速度取决于远程服务器对 ABOR 处理的支持。如果远程服务器不支持 `ABOR` 命令，则在远程服务器完成请求的文件之前，`ftp` 不显示提示符。

当 `ftp` 完成任何本地处理并等待远程服务器的回复时，终端中断键序列将被忽略。这种情况下出现长延迟取决于远程服务器对 `ABOR` 处理的支持。

# 文件命名约定

作为 `ftp` 参数指定的本地文件按照以下规则处理：

- 1. 如果指定了文件名，则使用标准输入（读取）或标准输出（写入）。
- 2. 如果文件名的第一个字符是 `|`，将剩余部分解释为 shell 命令。`ftp` 然后通过 `popen(3)` 使用该参数派生 shell，并从该 shell 的标准输出读取（写入）。这种机制一个非常有用的例子是：

# 414

### ftp

如果 shell 命令包含空格字符，你必须引用参数；例如 `"dir | ls -lt"`。
- 3. 检查失败，如果启用了 glob，则根据 `sh(1)` 使用的规则扩展本地名称；如果 `ftp` 命令期望单个文件（例如 `put`），则仅使用 glob 操作生成的第一个文件名。
- 4. 对于未指定本地名的 `mget` 和 `get` 命令，本地文件名是远程文件名，你可以通过 `ntrans` 或 `nmap` 设置修改它。如果开启了 `unique`，则可以修改生成的文件名。
- 5. 对于未指定远程名的 `put` 和 `append` 命令，远程文件名是本地文件名，你可以通过 `ntrans` 或 `nmap` 设置修改它。如果开启了 `unique`，则远程服务器可以修改生成的文件名。

# 文件传输参数

来自 FTP 规范的以下参数影响文件传输。

## 表示类型

ASCII、EBCDIC、image 或指定字节大小的本地字节大小（用于 PDP-10 和 PDP-20）。网络 ASCII 和 EBCDIC 类型具有进一步的子类型，指定垂直控制（如换行符）透传（nonprint）、以 TELNET 格式提供（TELNET 格式控制），或以 ASA 格式提供（FORTRAN 回车控制）。`ftp` 支持网络 ASCII（仅限 nonprint 类型）和 image 类型，以及与 TENEX 机器通信的 8 字节本地字节大小。

## 文件结构

file（无记录结构）、record 或 page。`ftp` 仅支持默认值，即 file。

## 传输模式

stream、block 或 compressed。`ftp` 仅支持默认值，即 stream。

## 使用

参见 `large(5)` 关于 `ftp` 在遇到大于或等于 2 GB（2**31 字节）的文件的行为描述。

## 文件

`~/.netrc`

## 属性

查看 `attributes(5)` 可获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcs |
| CSI | 已启用 (Enabled) |

## 参见

`ls(1)`, `rcp(1)`, `sh(1)`, `tar(1)`, `ftppd(1M)`, `open(3S)`, `netrc(4)`, `attributes(5)`, `largefile(5)`

# function — 定义 Shell 函数的内置内置命令

# 语法

```ksh
function identifier { list ; }
identifier() { list ; }
```

## 描述

Korn Shell
`function` 定义了一个通过 `identifier` 引用的函数。函数体是花括号 (`{}`) 之间的命令列表。
或者，你可以通过省略 `function` 关键字并在 `identifier` 后面加上一对包含的括号来定义函数。

## 示例

下面的示例创建了一个名为 `status()` 的函数，它会返回当前工作目录的名字并列出它。

```
$ status() { cd *; pwd;ls; }
$
$ functions
function status
{
 cd *; pwd;ls; }
$
$ status /home
/home
TT_DB bill lost+found
$
```

# 416

# function

下面的示例创建了一个名为 `scp()` 的函数用于安全复制。它可以防止你覆盖已存在的文件。当你执行相同的命令时，第二个命令将不会执行，`scp()` 函数会显示错误信息。

```
$ scp
{
  if test ! -s "$2"
    then cp "$1" "$2"
    else echo "scp: cannot copy $1: $2 exists"
  fi
}
$ scp junk junkl
$ scp junk junkl
scp: cannot copy junk: junkl exists
$
```
