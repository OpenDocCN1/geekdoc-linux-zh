
`mail [-s subject] [-c address,...] [-b address,...]`

`mail -f [mailbox]`

`mail [user]`

### 重要标志选项
- `-b address,...`: 指定密抄副本列表。
- `-c address,...`: 指定副本地址。
- `-f [mailbox]`: 从指定的邮箱读取。
- `-s subject`: 指定消息的主题。
- `-u user`: 打开用户的邮箱进行读取。

注意 完成编写消息时，使用 `Ctrl+D` 或在空行输入 `.` 。

## `mailq`
### 描述
显示输出队列的内容。

### 语法
`mailq`

### 重要标志和选项
无

## `mailto`
### 描述
向一个或多个接收者发送电子邮件。如果命令行上没有指定接收者，将提示用户输入接收者。如果没有标准输入，将提示用户输入消息内容。

### 语法
`mailto [-a character-set] [-c address,...] [-s subject] [recipient ...]`

### 重要标志和选项
- `-a character-set`: 指定另一种字符集，例如 `ISO-8859-8`。默认是 `US-ASCII`。
- `-c address,...`: 指定副本地址。
- `-s subject`: 指定消息的主题。

## `man`
### 描述
显示指定命令的帮助页。

### 语法
`command`

### 重要标志和选项
`command`: 指定要显示帮助页的命令。

## `mattrib`
### 描述
更改 MS-DOS 文件系统（如 DOS 软盘）上的属性。这类似于 DOS `ATTRIB` 命令。

### 语法
`mattrib [-a|+a] [-h|+h] [-r|+r] [-s|+s] mdsfile [mdosfile ...]`

### 重要标志和选项
- `+a|-a`: 设置或取消归档位。
- `+h|-h`: 设置或取消隐藏位。
- `+r|-r`: 设置或取消只读位。
- `+s|-s`: 设置或取消系统位。

# `mcopy`

- `+r|-r`: 设置或取消只读位。
- `+s|-s`: 设置或取消系统位。

#### 注意事项

在选项前使用 `+` 来设置标志位，使用 `-` 来取消标志位。

# `mbadblocks`

### 描述

测试 DOS 软盘的坏块。如果发现任何坏块，它们将在磁盘的 FAT 中被标记。
`mbadblocks` 驱动器:

### 语法

无

### 重要标志和选项

# `mcd`

### 描述

更改 MS-DOS 文件系统（如软盘）上的目录。如果未提供参数，则将显示当前设备和目录。类似于 DOS 的 `CD` 命令。

### 语法

```
mcd [msdosdirectory]
```

### 重要标志和选项

无

# `mcopy`

### 描述

在 Unix 和 MS-DOS 文件系统（如软盘）之间双向复制文件。可以将多个文件复制到单个目录中，该目录是最后一个参数。如果使用 DOS 驱动器标识符作为（如 `:`），则表示这是一个 DOS 文件；否则假设为 Unix 文件系统。如果参数中只有一个 DOS 文件，则该文件将被复制到当前目录。类似于 DOS 的 `COPY` 命令。

```
mcopy [-tnm] sourcefile targetfile

mcopy [-tnm] sourcefile [sourcefile ...] targetdirectory

mcopy [-tnm] MSDOSourcefile
```

### 重要标志和选项
- `-m`: 复制时保留修改时间。
- `-n`: 覆盖 Unix 文件时不询问确认。
- `-t`: 复制时在 Unix 文本文件和 DOS 文本文件之间转换文本文件。

### 语法

无

# `mdel`

### 描述

删除 MS-DOS 软盘上的文件。类似于 DOS 的 `DEL` 命令。

### 语法

```
mdel mdsdosfile [msdosfile ...]
```

### 重要标志和选项

无

# `mdeltree`

### 描述

删除一个或多个 MS-DOS 目录。类似于 DOS 的 `DELTREE` 命令。

### 语法

```
mdeltree mdsdosdirectory [msdosdirectory ...]
```

### 重要标志和选项

无

# `mdir`

### 描述

显示 MS-DOS 文件系统（如软盘）上目录的内容。如果指定了特定文件，则只列出这些文件。类似于 DOS 的 `DIR` 命令。

### 语法

```
mdir [-w] mdsdosdirectory

mdir [-a] [-f] [-w] mdsdosfile [msdosfile ...]
```

### 重要标志和选项
- `-a`: 列出文件以及普通文件。
- `-f`: 显示文件，但在列表末尾不显示总空闲空间。
- `-w`: 以宽输出显示文件。

# `messages`

### 描述

显示用户收件箱中（或如果命名了，则特定邮件文件夹）消息的数量。

### 语法

```
messages [folder]
```

### 重要标志和选项

无

# `mformat`

### 描述

格式化 MS-DOS 软盘。类似于 DOS 的 `FORMAT` 命令。

### 语法
`mformat _drive:`

### 重要标志和选项

无

# `mkdir`

### 描述

创建一个或多个目录。

### 语法
`mkdir [-p] [-m mode] [--parents] [--mode=mode] directory ...`

- `-m`/`--mode`: 使用与 `chmod` 命令相同的符号表示为创建的目录设置模式。如果未指定，则为目录分配默认模式。
- `-p`/`--parents`: 确保指定目录的父目录存在，并创建所需的缺失父目录。

# `mkdosfs`

### 描述

在指定设备上格式化 MS-DOS 文件系统。

### 语法
`mkdosfs [-c] [-F fatsize] [-n name] device`

### 重要标志和选项
- `-c`: 在格式化前检查坏块。
- `-F fatsize`: 指定要创建的文件分配类型。可以是 `12`（12 位位 FAT）或 `16`（16 位位 FAT）。程序将为你选择最佳选项，通常是 `16`。
- `-n name`: 将卷标签设置为指定的名称。名称长度可达 11 个字符。如果没有名称，将不设置卷标签。

# `mk2fs`

### 描述

格式化 Linux 第二扩展文件系统。

### 语法
`mk2fs [-c] [-m percentage] [-L label] device`

### 重要标志和选项
- `-c`: 在格式化前检查坏块。

# `mkfs`

- `-L label`: 设置指定的标签。
- `-m percentage`: 指定为超级用户预留块的百分比。默认设置为 5 %。

### 描述

创建一个文件系统（类似于在 DOS 中格式化驱动器）。可以选择地指定文件系统的块数。

### 语法

```
mkfs [-t filesystem] [-c] [-1 file] device [blocks]
```

### 重要标志和选项
- `-c`: 在格式化前检查设备的坏块。
- `-1 file`: 从指定文件读取该设备的坏块列表。
- `-t filesystem`: 指定应创建的文件系统类型。如果未 `/etc/fstab` 中未为设备找到其他替代方案，默认文件系统类型为 `minix`。

# `mkpasswd`

### 描述

生成随机密码并可选地将其分配给用户。

### 语法

```
mkpasswd [-2] [-1 number] [-d number] [-c number] [-C number]

-p file] [user]
```
