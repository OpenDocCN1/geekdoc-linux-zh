
## Shell 归档

*Shell 归档*（或 *shar 文件*）是一组编码为单个 shell 脚本的文本文件或脚本。脚本中的数据在此以文件形式表示。二进制文件会通过 Linux 的 uuencode 命令转换为文本。Shell 归档是自解压的归档；当 shell 脚本执行时，归档中的文件会被解压。

Linux shar (*shell archive*) 命令是一个用于创建新 shell 归档的工具。要将名为 orders.txt 的文件保存为 shell 归档，请使用以下命令：

```bash
$ shar orders.txt > orders.shar
shar: Saving orders.txt (text)
```

要提取文件，请使用 Bash 运行该 shell 归档：

```bash
$ bash orders.shar
x - creating lock directory
x - extracting orders.txt (text)
```

要创建当前目录中所有文件的 shell 归档，请使用以下命令：

```bash
$ shar * > myproject.shar
```

在归档目录时，shar 命令会递归地归档其子目录。

shar 命令有大量开关（选项）。这些开关主要用于处理特殊情况。完整列表见本章的参考部分。

还有一个 unshar 命令。它并不完全是 shar 的反操作，该命令从保存的电子邮件消息中提取 shar 归档，然后使用 Bash 解压文件。

在互联网早期，Shell 归档是通过新闻组共享文件的流行方法。Shell 归档的效率并不高，但它们展示了 shell 脚本的一种不寻常的用法，并且所有 Linux 发行版都提供支持。

虽然 shell 脚本可能不会像我在大三操作系统课程中的 C 程序那样在屏幕上输出竖线并弹出磁盘，但它们调试起来同样困难。知道 Bash 具有调试功能会让查找和修复脚本变得更容易。借助版本控制、补丁和日志，你的工作可以与其他程序员分享，由脚本更新引起的问题也可以被快速定位。这些工具在下一章关于子 shell 的内容中将会派上用场。

## 参考部分

### tee 命令开关

- `--append`（或 `-a`）—将输出附加到现有文件的末尾。
- `--ignore-interrupts`（或 `-i`）—即使被 Linux 信号中断，仍保持 tee 运行。

### Linux Time 命令开关

- `--portability`（或 `-p`）—遵循 POSIX 标准。
- `--output`（或 `-o`）—将输出重定向到文件。
- `--append`（或 `-a`）—将结果附加到文件。
- `--verbose`（或 `-v`）—提供每个统计详情的详细说明。

### Bash Time 命令格式代码

- `$$`—字面量 `%`。
- `$[precision][.1]R`—实际时间；以秒为单位的经过时间。
- `$[precision][.1]U`—用户模式下消耗的 CPU 秒数。
- `$[precision][.1]S`—系统模式下消耗的 CPU 秒数。
- `$P`—CPU 使用率，计算方式为 `($U + $S) / $R`。

### Linux Time 命令格式代码

- `$$`—字面量 `%`。
- `%R`—实际时间；以时:分:秒格式表示的经过时间。
- `%e`—实际时间；以秒为单位的经过时间。
- `%S`—以 CPU 秒为单位的系统时间。
- `%U`—以 CPU 秒为单位的用户时间。
- `%P`—程序使用的 CPU 百分比。
- `%M`—程序的最大常驻集大小（以千字节为单位）。
- `%t`—程序的平均常驻集大小（以千字节为单位）。
- `%D`—未共享数据区的平均大小。
- `%p`—未共享堆栈的平均大小（以千字节为单位）。
- `%X`—共享文本区的平均大小。
- `%Z`—系统页的大小（以字节为单位）。
- `%F`—主要页面错误的数量。
- `%R`—次要页面错误的数量（页面之前已加载且仍由 Linux 缓存）。
- `%W`—进程被换出的次数。
- `%c`—时间片上下文切换的次数。
- `%w`—自愿上下文切换的次数。
- `%I`—文件系统输入的次数。
- `%O`—文件系统输出的次数。
- `%R`—接收套接字消息的次数。
- `%S`—发送套接字消息的次数。
- `%K`—接收信号的次数。
- `%C`—命令行。
- `%X`—退出状态。

## Shell 调试选项

- `-o errexit`—如果命令返回错误代码，终止 shell 脚本。
- `-o nounset`—如果引用未设置（或不存在）的变量，则以错误终止。
- `-o xtrace`—在执行每条命令前显示该命令。

### `shar` 命令开关

- `-quiet`（`-silent` 或 `-q`）—在创建归档时隐藏状态消息。
- `-intermix-type`（`-p`）—允许打包选项在命令行中单独应用，而不是应用于所有文件。
- `-stdin-file-list`（或 `-f`）—从标准输入读取要打包的文件列表。
- `-output-prefix=s`（或 `-o`）—生成的 *shar* 文件的名称（与 `-whole-size-limit` 一起使用时）。
- `-whole-size-limit=k`（或 `-l`）—将生成的 *shar* 文件的大小限制为指定的千字节数，但不拆分单个文件。
- `-split-size-limit=k`（或 `-k`）—将生成的 *shar* 文件的大小限制为指定的千字节数，并拆分单个文件。
- `-archive-name=name`（或 `-n`）—在头部添加归档名称行。
- `-submitter=email`（或 `-m`）—在头部添加 *submitted* by（提交者）行。
- `-net-header=s`—添加 *submitted* by（提交者）和 *archive* name（归档名称）头部。
- `-cut-mark`（或 `-c`）—添加 `cut here`（在此处裁剪）行，用于标记嵌入电子邮件正文中的归档的开头。
- `-mixed-uencode`（或 `-m`）—（默认）允许文本和 uencode 二进制文件。
- `-text-files`（或 `-T`）—强制将所有文件视为文本处理。
- `-uencode`（或 `-B`）—将所有文件视为要 uencode 的二进制数据。
- `-gzip`（或 `-z`）—使用 gzip 压缩所有数据并进行 uencode。
- `-level-for-gzip=l`（或 `-g`）—设置压缩级别（1–9）。
- `--compress`（或 `-Z`）—使用 Linux `compress` 命令压缩所有数据并进行 uuencode。
- `--bits-per-code=B`（或 `-b` `$B`）—设置 `compress` 压缩字大小（默认 12 位）。
- `--no-character-count`（或 `-w`）—抑制字符计数检查。
- `--no-md5-digest`（或 `-D`）—抑制 MD5 校验和。
- `--force-prefix`（或 `-P`）—在前缀字符后添加行。
- `--here-delimiter=d`（或 `-d` `$d`）—将 `here` 文件分隔符更改为 *d*。
- `--vanilla-operation`（或 `-V`）—创建一个可以使用最少数量 Linux 命令解压的归档。
- `--no-piping`（或 `-P`）—不在 `shar` 文件中使用管道。
- `--no-check-existing`（或 `-x`）—覆盖现有的 `shar` 文件。
- `--query-user`（或 `-X`）—在解压时，覆盖前提示用户。
- `--no-timestamp`（或 `-n`）—在解包时不固定修改时间戳。
- `--quiet-unshar`（或 `-Q`）—丢弃解包注释。
- `--basename`（或 `-f`）—解压时丢弃路径名，将所有文件存储在当前目录。
- `--no-i18n`—Shell 归档中不启用国际化。
- `--print-text-domain-dir`—显示 `shar` 用于不同语言消息的目录。

## 参数和子 Shell

**T**o serve as a flexible tool，脚本在被调用时必须通过限定（qualification）来提供额外信息，说明如何以及在何处执行其任务。与命令类似，脚本使用参数进行限定。开关和参数使脚本可复用，从而减少成本和时间。

### 位置参数

有三种方法可以使用参数扩展 Linux 脚本。第一种方法使用*位置参数*。脚本可以根据参数在命令行中出现的位置（或顺序）来引用它们。由于其他两种方法依赖于位置参数，因此首先讨论位置参数。

Bash 变量 $0 是脚本的路径名。它不一定是完整的路径名，而是执行脚本时用于指定脚本的路径。

```bash
$ printf "%s\n" "$0" `/bin/bash`
```

在这种情况下，Bash 会话是通过命令 `/bin/bash` 启动的。

当与 `basename` 命令结合使用时，脚本名称会从剩余的路径名中移除。

```bash
$ declare -rx SCRIPT=`basename $0`
$ printf "%s\n" "$SCRIPT"
bash
```

一个稍快的版本使用 Bash 的子字符串功能，避免运行外部程序。

```bash
$ declare -rx SCRIPT=${0%%*/}
$ printf "%s\n" "$SCRIPT"
bash
```
