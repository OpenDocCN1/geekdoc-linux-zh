
`fsck` 是多个文件系统检查器的前端。

## 常用选项

- `-A` 尝试检查已安装的文件系统。
- `-C` 在支持的系统中显示进度条。
- `-N` 不执行，显示将做什么。
- `-t` 让用户指定要检查的文件系统类型。

## 示例 1

```
fsck /dev/hda1
```

检查第一个 IDE 分区。

## 示例 2

```
fsck /dev/fd0
```

检查软磁盘。

# `grep`, `egrep`, `fgrep`

打印匹配模式的行。

## 语法概要

```
grep [[AB] NUM] [-CEFGVbchiLnqsvxyU] [-e PATTERN | -f FILE]
[extended-regexp] [--fixed-strings] [--basic-reg-exp] [--regexp=PATTERN]
[file=FILE] [--ignore-case] [--word-regexp] [--line-regexp] [--line-regexp]
[--no-messages] [--revert-match] [--version] [--help] [--byte-offset] [--line-number]
[with-filename] [--no-filename] [--quiet] [--silent] [--files-without-match]
[files-with-matches] [--count] [--before-context=NUM] [--after-context=NUM]
[--context] [--binary] [--unix-byte-offsets]
```

## 简述

`grep` 允许在文件中搜索模式（字符组合）。

## 常用选项

- `-a` 将二进制数据文件视为文本文件。
- `-i` 使 `grep` 忽略大小写。
- `-n` 为每个返回项打印行号。
- `-r` 搜索所有子目录及其文件。
- `-s` 不打印损坏或不存在的文件信息。
- `-U` 将所有文件视为二进制文件。
- `-w` 仅当输入为完整单词时返回。
- `-x` 仅当输入字符串被显式匹配时返回。

## 示例 1

`fgrep hello *`

在当前目录下搜索所有模式为 `hello` 的文件。

## 示例 2

`egrep 'smith*' test.txt`

在文件 `test.txt` 中搜索模式为 `smith*` 的。

# `gv`

一个 PostScript 和 PDF 查看器。

## 概要

```
gv [filename][--monochrome][--grayscale][--color][--safer] [-noquiet][--arguments <arguments>][--page <label>][-nocenter][--media <media>][-portrait][--landscape][--upsidedown][--seagreen][--scale n][--scalebase n][--swap][-noswap][--antialias][--noantalias][--dsc][--nodcs][--eof][--noeof][--pixmap][--nopixmap][--watch][--nowatch][-?][-h][--help][-v][--resize][--noresize][--geometry[<width><x height>[+][offset][+][yoffset]][-ad <resource file>][-style <resource file>][-spartan][<other toolkit options]]
```

## 简要描述

`gv` 允许用户在 X Window 界面中查看 postscript 和 PDF 文档。

## 选项

- `-center` 将文档在显示器居中。
- `-h` 显示帮助信息。
- `-monochrome` 以黑白显示文档。
- `-grayscale` 以灰度显示文档。
- `-color` 以彩色显示文档。
- `-scale n` 使用指定的整数 `n` 设置文档比例。
- `-portrait` 以竖向模式显示文档。
- `-landscape` 以横向模式显示文档。

## 示例 1

查看 postscript 文件 `example1.ps` 的内容，输入：

## 第 3 章

```
gv example1.ps
```

这会显示文件 `example1.ps`。

## 示例 2

要查看 `example1.ps` 的横向版本，输入：

```
gv example1.ps -landscape
```

# `gzip`, `gunzip`, `zcat`

压缩或扩展文件。

## 概要

- `gzip [-acdfhlLnNrtvV19] [-S suffix] [name...]`
- `gzip [-acdfhlLnNrtvV] [-S suffix] [name...]`
- `zcat [-fHV] [name...]`

## 简要描述

`gzip` 使用 Lempel-Ziv 编码 (`LZ77`) 压缩文件。原始文件被带有 `.gz` 扩展名的新压缩文件替换。新压缩文件保留与原始文件相同的权限模式、访问时间和修改时间。

`gunzip`（等同于 `gzip -d`）程序解压使用 `gzip`、`zip`、`compress -H` 或 `pack` 创建的文件。`gunzip` 接收一个压缩文件列表并将其替换为文件的未解压版本。`gunzip` 识别以下压缩扩展名：`.gz`, `.gz`, `.z`, `.zi`, `.Z`, `.tgz`, `.taz`。

`zcat` 命令（等同于 `gunzip -c`）从命令行或标准输入解压文件列表。所有未解压的数据都将写入标准输出。

## 常用选项 (`gzip`)

- `-d` 告诉 `gzip` 解压已经压缩的文件。
- `-h` 显示 `gzip` 的帮助文件。
- `-l` 列出指定文件的信息。
- `-q` `gzip` 不显示任何警告。
- `-r` 指定 `gzip` 应该也压缩任何子目录中的文件。
- `-t` 测试文件是否有错误。
- `-S suffix` 添加指定的后缀代替 `.gz`。

## 常用选项 (`gunzip`)

- `-c` 将输出写入到标准输出。
- `-h` 显示 `gunzip` 的帮助文件。
- `-l` 列出指定文件的压缩信息。
- `-v` 显示每个文件解压后的信息。

## 示例 1

要解压名为 `big_file.gz` 的文件，使用以下命令：

```
gunzip big_file.gz
```

这会将 `big_file.gz` 替换为未解压版本。

## 示例 2

要压缩当前目录下所有文件及其子目录下的所有文件，输入：

```bash
gzip -r .
```

# `hdparm`

获取/设置硬盘参数。

## 概要

```
hdparm [-a [succulent]] [-A [0|1]] [-c [chipset_mode]] [-C] [-d [0|1]] [-f]
[-g] [-i] [-k [0|1]] [-K [0|1]] [-m [sectcount]] [-p [0|1|2|3|4|5]]
[-P [sectcount]] [-q -r [0|1]] [-S [timeout]] [-T] [-u [0|1]]
[-v -W [0|1]] [-X [xformde]] [-y] [-Y] [-Z] device
```

## 简要描述

`hdparm` 为 root 用户提供了若干个硬盘 I/O 控制 (`ioctl`) 的命令行界面。`hdparm` 适用于原生 Linux IDE/ST-506 设备驱动以及 2.1.23 及以上的 Linux 内核。建议使用内核 2.0.10 或更高版本的新的 (E)IDE 驱动。

## 常用选项

- `-d` 禁用/启用驱动器的“using_dma”标志。
- `-f` 在退出时同步并刷新设备的缓冲区缓存。

## 第 3 章

- `-g` 显示驱动几何结构（柱、磁头、扇区）。
- `-i` 显示启动时从驱动获取的识别信息。
- `-I` 直接从驱动请求识别信息。
- `-k [0|1]` 直接从驱动请求识别信息。
- `-m [sectcount]` 设置扇区数量。
- `-p [0|1|2|3|4|5]` 设置模式。
- `-P [sectcount]` 设置扇区数量。
- `-q -r [0|1]` 设置模式。
- `-S [timeout]` 设置超时。
- `-T` 设置超时。
- `-u [0|1]` 设置标志。
- `-v -W [0|1]` 设置模式。
- `-X [xformde]` 设置转换。
- `-y [-Y] [-Z]` 设备选项。

## 示例 1

```bash
hdparm -d /dev/sda
```

## 示例 2

```bash
hdparm -i /dev/sda
```

## 示例1

`lastlog`

显示所有组的最后登录情况。

## 示例2

要查看用户 `bob_from_accounting` 上次登录的时间，输入：

```
lastlog -u bob_from_accounting
```

# `ln`

在文件之间创建链接。

## 概要
