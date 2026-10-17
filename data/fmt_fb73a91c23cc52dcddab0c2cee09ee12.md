
私钥密码。

`-verify` `filename`

使用公钥验证签名。输出为“Verification OK”或“Verification Failure”。

`-mac` `filename`

mac签名。

通过 `-mac` 传递选项。

`key:string`

以字符串形式指定 MAC 密钥（如果密钥包含打印字符）。字符串长度必须符合算法的任何限制。

`hexkey:string`

以十六进制格式指定 MAC 密钥（每字节两个十六进制位）。密钥长度必须符合算法的任何限制。

`-rand` `file(s)`

包含随机数据的文件或文件，用于初始化随机数生成器，或一个 EGD 套接（见 `RAND_egd(3)`）。多个文件可以使用依赖于系统的字符分隔。MS-Windows、VMS 使用 `;` 分隔，其他系统使用 `:` 分隔。

`-non-fips-allow`

在 FIPS 模式下允许使用非 FIPS 算法。

`-fips-fingerprint`

使用特定密钥计算 HMAC。

`file...`

要摘要的文件或文件。如果没有指定任何文件，则使用标准输入。

## 示例

创建文件的十六进制编码消息摘要：`openssl dgst -md5 -hex file.txt`

使用 SHA-256 签名文件并输出二进制文件：`openssl dgst -sha256 - sign privatekey.pem -out signature.sign file.txt`

验证签名：`openssl dgst -sha256 -verify publickey.pem \ - signature signature.sign \ file.txt`

# 注意

所有新应用程序的摘要选择是 SHA1。然而，其他摘要仍被广泛使用。

## 名称

`du` - 估计文件空间占用情况

# 语法概要

```
du [OPTION]... [FILE]... du [OPTION]... --files0-from=F
```

### 描述

汇总一组 `FILE` 的磁盘使用情况，对于目录则进行递归处理。

长选项的强制性参数对于短选项也是强制性的。

+   `-0`, `--null`

    以 NUL 结束每行输出，而不是换行符

- `-a`, `--all`

    为所有文件写入计数，而不仅仅是目录

- `--apparent-size`

    打印表义大小，而不是磁盘占用情况；虽然表义大小通常较小，但它可能比（“稀疏”）文件中的空洞、内部碎片、间接块等要大

- `-B,--block-size=SIZE`

    在打印大小前按 `SIZE` 缩放大小；例如，‘BM’ 以 1,048,576 字节为单位打印大小；见下文的 `SIZE` 格式

- `-b,--bytes`

    等同于 ‘apparent-size --block-size=1’

- `-c,--total`

    生成总计

- `-D`, `--dereference-args`

    仅对命令行中列出的符号链接进行解引用

- `-d,--max-depth=N`

    仅当目录（或文件，配合 `--all`）位于命令行下方 `N` 级以下时，打印其总计；`--max-depth=0` 等同于 `--summarize`

- `--files0=F`

    汇总 `F` 中指定的 NUL 终止的文件名的磁盘使用情况；如果 `F` 为 `-`，则从标准输入读取名称

- `-H`

    等同于 `--dereference-args (-D)`

- `-h`, `--human-readable`

    以人类可读的格式打印大小（例如 1K 234M 2G）

- `--inodes`

    列出 inode 使用信息而不是块使用情况

- `-k`

    同于 `--block-size=1K`

- `-L`, `--dereference`

    解引用所有的符号链接

- `-l`, `--count`

    如果是硬链接，则多次计数大小

- `-m`

    同于 `--block-size=1M`

- `-P`, `--no-dereference`

    不跟随任何符号链接（这是默认设置）

+   `-S`, `--separate-dirs`

    对于目录，不包含子目录的大小

+   `-si`

    类似 `-h`，但使用 1000 的幂次而不是 1024

+   `-s`, `--summarize`

    仅为每个参数显示总计

+   `-t`, `--threshold=SIZE`

    如果是正数，则排除小于 `SIZE` 的条目；如果是负数，则排除大于 `SIZE` 的条目

+   `-time`

    显示目录或任何子目录中任何文件的最后修改时间

+   `-time=WORD`

    用 `WORD` 显示时间而不是修改时间：`atime`（访问）、`use`、`ctime` 或 `status`（状态）

+   `-time-style=STYLE`

    使用 `STYLE` 显示时间，`STYLE` 可以是：`full-iso`, `long-iso`, `iso`, 或 `+FORMAT`；

    `FORMAT` 的解释方式类似于 ‘`date`’ 

+   `-X`, `--exclude-from=FILE`

    排除匹配 `FILE` 中任何模式的文件

+   `-exclude=PATTERN`

    排除匹配 `PATTERN` 的文件

+   `-x`, `--one-file-system`

    跳过不同文件系统上的目录

+   `-help`

    显示此帮助并退出

+   `-version`

    输出版本信息并退出

显示的值以第一个可用 `SIZE -block-size` 为单位，并由 `DU_BLOCK_SIZE`、`BLOCK_SIZE` 和 `BLOCKSIZE` 环境变量决定。否则，单位默认为 1024 字节（如果设置了 `POSIXLY_CORRECT` 则为 512）。

`SIZE` 参数是一个整数和一个可选单位（例如：`10K` 是 `10*1024`）。单位有 `K,M,G,T,P,E,Z,Y`（1024 的幂次）或 `KB,MB,...`（1000 的幂次）。

# 模式

`PATTERN` 是一个 shell 模式（不是正则表达式）。模式 `?` 匹配任何字符，而 `*` 匹配任何字符串（由零、一个或多个字符组成）。例如，`*.o` 将匹配任何以 `.o` 结尾的文件。因此，命令

```
du --exclude='*.o'
```

将跳过所有以 `.o` 结尾的文件和子目录（包括文件 `.o` 本身）。

### 作者

由 Torbjorn Granlund, David MacKenzie, Paul Eggert 和 Jim Meyerering 编写。

# 报告

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 反馈 `du` 翻译错误。

# 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和重新发行它。在法律允许范围内不提供任何保证。

# 另请

完整文档见：<http://www.gnu.org/software/coreutils/du> 或通过本地可用：info ‘(coreutils) du invocation’

## 名称

`dumpiso` - 倾储 IEEE 1394 同步通道数据包

# 语法概要

```
dumppiso [ options ] [ FILE ]
```

### 描述

`dumpiso` 监听选定的通道范围并将所有接收的数据包转储到文件 `FILE`，如果没有给出，则转储到标准输出。在转储过程中，接收到的数据包当前数量写入标准错误，并在每个数据包更新时更新。

它使用简单的文件格式用于 `dumpiso` 监听选定的通道范围并将所有接收的数据包转储到文件 `FILE`，如果没有给出，则转储到标准输出。在转储过程中，接收到的数据包当前数量写入标准错误，并在每个数据包更新时更新。它使用简单的文件格式 `isodump(5)`。

### 选项

`-c`, `--channels=CHANNELS`

    设置监听的通道。`CHANNELS` 可以是单个数字，或者是 `X-Y` 形式的范围。`-p`, `--port=PORT`

    选择接收端口。端口范围为 0 到 63。`-h`, `--help`

    显示帮助并退出。这种格式见 `isodump(1)`。

# 错误

无。

# 另请

`sendiso(1)`, `isodump(5)`

### 作者

Andreas Bombe <a@debian.org>

## 名称

`dvcont` - 向 DV 发送命令

# 语法概要

```
dvcont <command1> [ <command2> ]
```

### 描述

`dvcont` 是一个通过火线电发送命令的命令行工具。以下是命令：`dev <number>`

    选择使用的设备号。（`dvcont` 会尝试自动检测相机。）`play`

    让相机播放。如果已经在播放，则切换慢动作。`reverse`
