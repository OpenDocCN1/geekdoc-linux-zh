
### chown

- `-a`, `--archive` 归档模式。
- `-b`, `--backup` 备份文件。
- `-d`, `--no-dereference` 不跟随符号链接。

示例：将 `bigfile` 的所有者更改为 `"rcowan"`，文件的组更改为 `"compsci"`。

```
chown rcowan:compsci bigfile
```

- `-c`, `--changes` ...
- `-f`, `--force` 强制删除目标文件。
- `-i`, `--interactive` 在删除前提示。
- `-l`, `--link` 创建硬链接。
- `-p`, `--preserve` 保留所有者、组和时间戳。
- `-P`, `--parents` 根据需要创建父目录。
- `-r`, `--recursive` 递归拷贝子目录。

### dd [OPTION]...

将文件从一种格式拷贝到另一种格式。默认情况下，从标准输入到标准输出。

示例：将 EBCDIC 源文件 (`file.mainframe`) 转换为 ASCII：

```
dd if=file.mainframe of=file.linux conv=ascii
```

- `if=FILE` | 读取 `FILE` 而不是标准输入。
- `of=FILE` | 写入 `FILE` 而不是标准输出。
- `ibs=BYTES` | 每次输入指定的字节数。
- `bs=BYTES` | 每次输出指定的字节数。
- `cbs=BYTES` | 输出 `cbs` 参数指定的字节数。
- `skip=BLOCKS` | 在开始前跳过输入文件中指定数量的块。
- `seek=BLOCKS` | 在开始前跳过输出文件中指定数量的块。
- `count=BLOCKS` | 仅从输入文件拷贝指定数量的字节然后停止。
- `conv=CONVERSION[,CONVERSION...]` 从另一种格式转换文件。`CONVERSION` 是以下之一：
  - `ascii` EBCDIC 转 ASCII。
  - `ebcdic` ASCII 转 EBCDIC。
  - `ibm` ASCII 转交替型 EBCDIC。
  - `block` 对于输入中的每行，输出 `cbs` 参数指定的精确字节数，必要时用空格填充。
  - `unblock` 将每个 `cbs` 大小的输入块末尾空格替换为换行符。
  - `lcase` 将大写字母转换为小写。
  - `ucase` 将小写字母转换为大写。
  - `swap` 交换每对输入字节。
  - `noerror` 遇到读取错误后继续。
  - `notr` 不截断输出文件。
  - `sync` 在每个输入块末尾填充零字节，使其大小等于 `ibs` 的大小。

### file [-vbczl] [-f filename] [-m magicfiles] file ...

`file` 程序测试命令行上列出的所有文件，尝试确定它们的类型。

示例：确定 `filelist` 中命名文件的类型：

```
file -f filelist
```

- `-v` 显示版本信息并退出。
- `-m` 指定用于确定文件类型的“魔数”的不同源。
- `-z` 尝试查看压缩文件的内容。
- `-b` 简要模式。
- `-c` 打印解析后的魔法文件。
- `-filename` 从 `filename` 读取要测试的文件列表。
- `-L` 跟随符号链接。

### install [OPTION]... SOURCE DEST

`install` 的工作与 `cp` 命令非常相似。它拷贝文件但还会尝试设置它们的权限、所有者和组。`DEST` 可以是文件或目录。它最常用于 Makefile 中将编译好的程序拷贝到目标目录。

示例：将可执行文件 `interest` 拷贝到 `/usr/bin` 目录并赋予读和执行权限，同时备份现有的 `interest` 副本：

## 命令

```
install -b -m 555 interest /usr/bin
```

- `-b`, `--backup` 为即将被覆盖的文件创建备份。
- `-c` 不执行任何操作。为了向后兼容而包含。
- `-d`, `--directory` 创建由 `DEST` 指定的目录。
- `-g GROUP`, `--group=GROUP` 将安装文件的组属性设置为由 `GROUP` 指定的组名。
- `-m MODE`, `--mode=MODE` 将安装文件的权限属性设置为由 `MODE` 指定的模式。
- `-o OWNER`, `--owner=OWNER` 将安装文件的所有者属性设置为 `OWNER` 的值。
- `-s`, `--strip` 从安装的二进制可执行文件中剥离符号表。
- `-S SUFFIX`, `--suffix=SUFFIX` 当因使用 `-b` 选项而生成备份文件时，在备份文件后附加 `SUFFIX`。
- `-V METHOD`, `--version-control=METHOD` 与 `"-b"` 选项配合使用。`METHOD` 参数是以下内容之一：[ 编号的 | l ] [ 存在的 | 无 ] [ 从不 | 简单 ]

### ln [选项]... 源 [目标]

在文件或目录之间建立链接。此链接可以是“硬”链接或“软”链接。硬链接实际上是现有文件的一个新名称。软链接是一种特殊类型的文件，指向原始文件的指针。对于大多数用途，这些链接的行为就像文件本身一样：

示例：创建一个链接到 `/tmp` 目录的符号链接：

```
ln -s -d /tmp junk
```

- `-b`, `--backup` 为即将被覆盖的文件创建备份。
- `-d`, `-F`, `--directory` 允许对目录创建硬链接（仅限超级用户）。
- `-f`, `--force` 强制删除之前已存在的目标文件。
- `-i`, `--interactive` 在删除现有的目标文件前提示用户。
- `-n`, `--no-dereference` 当 `DEST` 值本身是符号链接时，将 `DEST` 视为实际文件。也就是说，创建指向 `DEST` 的链接，而不是直接指向 `DEST` 已经链接的（第三个）文件。
- `-s`, `--symbolic` 创建符号链接而非硬链接。
- `-v`, `--verbose` 在链接之前打印每个文件的名称。
- `-S SUFFIX`, `--suffix=SUFFIX` 在使用 `-b` 选项生成备份文件时，在每个创建的备份文件后附加 `SUFFIX`。
- `-V METHOD`, `--version-control=METHOD` 与 `"b"` 选项配合使用。`METHOD` 参数是以下内容之一：[ 编号 | t | 存在的 | 无 | 从不 | 简单 ]

### lockfile |-sleeptime | -r retries | -l locktimeout | -suspend | -! | -ml | -mu | filename ...

`lockfile` 用于创建信号文件。信号文件用于判断另一个文件（例如系统邮箱）是否正在被使用。如果无法创建指定的 `lockfile`，它将等待（默认）8 秒后重试。默认情况下，这种重试将无限进行。参数可以指定在命令行的任意位置，仅适用于参数之后列出的文件。

示例：解锁你的系统邮箱：

```
lockfile -mu
```

## 命令

- `-!` 反转 `lockfile` 的返回值。
- `-h`, `-?` 帮助。
- `-SLEEPTIME` 待机时间指定每次重试之间等待的秒数。
- `-s` 在发生强制删除后睡眠 n 秒。
- `-r retries` 在指定的次数重试后停止。
- `-ml` 锁定你的系统邮箱。
- `-mu` 解锁你的系统邮箱。

### ls

`ls` 程序显示有关文件或目录的信息。默认按字母顺序呈现输出。

`ls` 可疑是 Unix 世界中使用频率最高的单一命令。我参考了它的提示。`ls` 默认按字母顺序呈现输出。

```
ls -
```
