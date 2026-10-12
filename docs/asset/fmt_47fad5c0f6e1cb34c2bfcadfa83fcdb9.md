
| 删除到行尾 | `^k` | `^^a` | `D` |

| 定义区域（输入此按键标记区域开始，将光标移动到目标区域结束） | `^SPACE` | `^^` (`Ctrl` `caret`) | `v` |

| 剪切区域 | `^w` | `^k` | `d` |

| 复制区域 | `M-w` | `M-^` | `y` |

| 粘贴区域 | `^y` | `^u` | `p` |

| 获取帮助 | `^h` | `^g` | `:help` |

| 查看手册 | `^h i` | `^g` | `:help` |

> `^a` 仅当通过 `M-k` 启用 `nano` 的剪切到末尾功能时。

## 文件属性

- `stat` 显示文件和目录的属性。
- `wc` 统计文件的字节数、单词数和行数。
- `du` 测量文件和目录的磁盘占用情况。
- `file` 识别（猜测）文件的类型。
- `mimetype` 识别（猜测）文件的 `MIME` 类型。
- `touch` 更改文件和目录的时间戳。
- `chown` 更改文件和目录的所有者。
- `chgrp` 更改文件和目录的用户组。
- `chmod` 更改文件和目录的保护模式。
- `umask` 为新文件和目录设置默认模式。
- `lsattr` 列出文件和目录的扩展属性。
- `chattr` 更改文件和目录的扩展属性。

在检查 `Linux` 文件时，请记住内容只是故事的一部分。每个文件和目录还有描述其所有者、大小、访问权限和其他信息的属性。`ls -l` 命令（参见第 61 页的“基本文件操作”）显示了其中一些属性。其他命令允许你查看并更改这些以及其他属性。

## `stat`

`stdin stdout --file opt --help --version`

`stat [options]`

`stat` 命令列出文件（默认）或文件系统（`-f`）的属性：

```
stat -f myfile
File: 'myfile'
Size: 1168 Blocks: 8
Block: 4096 regular file
Device: 811/2065
```

（注：由于原文提供的 `stat` 示例输出内容不完整，此处保留了其结构并翻译了可可见字段）

## `file`

`stdin stdout -file --help --version`

`file [options] files`

`file` 命令报告文件的类型。输出是根据文件内容和其他因素得出的推测：

`+ → file /etc/hosts /usr/bin/who letter.docx`

`/etc/hosts: ASCII text`

`/usr/bin/who: ELF 64-bit LSB executable ...`

`letter.docx: Microsoft Word 2007+`

### 有用选项

- `-b` 省略文件名（输出的左列）。
- `-i` 打印文件的 `MIME` 类型，例如 `"text/plain"` 或 `"audio/mpeg"`，而不是默认输出。
- `-f name_file` 从给定的 `name_file` 读取文件名（每行一个），并报告它们的类型。之后，像往常一样处理命令行上的文件名。
- `-L` 跟踪符号链接，报告目标文件的类型，而不是链接本身的类型。
- `-z` 如果文件是压缩的（参见第 126 页的“压缩、打包和加密”），则检查未压缩后的内容以决定文件类型，而不是报告`"compressed data."`。

## `mimetype`

`stdin stdout -file --opt --help --version`

`mimetype [options] files`

`mimetype` 命令类似于 `file -i` 命令，会打印文件的 `MIME` 类型（如 `text/plain` 或 `application/pdf`），但提供了更多选项。

`+ → mimetype photo.jpg sample.pdf zipfile.zip`

`photo.jpg: image/jpeg`

`sample.pdf: application/pdf`

`zip.zip: application/zip`

### 有用选项

- `-b` 省略输出开前的文件名。
- `-d` 打印更详细的描述，例如 `"JPEG image"` 或 `"ZIP archive."`
- `-l language` 当提供 `-d` 选项时，用指定的语言打印文件类型。语言代码是标准的双字母代码，如代表德语的 `de` 和代表葡萄语的 `pt`。
- `-L` 对于符号链接，打印所链接文件的类型而不是链接本身（类型为 `inode/symlink`）。

## `touch`

`stdin stdout -file --opt --help --version`

`touch [options] files`

`touch` 命令更改与文件相关的两个时间戳：修改时间（文件数据最后被更改的时间）和访问时间（文件最后被读取的时间）。要将这两个时间戳都设置为当前时刻，请运行：

`+ → touch myfile`

你可以将这些时间戳设置为任意值，例如：

`→ touch -d "November 18 1975" myfile`

如果给的文件不存在，`touch` 会创建一个同名的空文件（参见第 79 页的“快速创建文件”）。

### 有用选项

- `-a` 仅更改访问时间。
- `-m` 仅更改修改时间。
- `-c` 如果文件不存在，则不创建（通常情况下，`touch` 会创建它）。
- `-d timestamp` 设置文件的时间戳。接受许多格式，从 `"12/28/2001 3pm"` 到 `"28-May"`（假设为今年，时间为午夜），再到 `"next tuesday 13:59"`，最后到 `"0"`（今天午夜）。可以尝试并使用 `stat` 检查结果。完整文档可查阅 `info`。
- `-t timestamp` 使用特定格式精确设置文件时间戳，格式为 `[[CC][YY]MMDDhh[.ss]]`。`CC` 是双数的世纪，`YY` 是双数的年份，`MM` 是双数的月份，`DD` 是双数的日期，`hh` 是双数的小时，`mm` 和 `ss` 是双数的秒。例如，`-t 20230812150047` 意味着 2023 年 8 月 12 日 15:00:47。

## `chown`

```bash
chown [options] user_spec files
```

`chown` 命令更改文件和目录的所有者。在大多数情况下，它需要超级用户权限。要将用户 `"smith"` 设置为几个文件和一个目录的所有，请运行：

`+ - sudo chown smith myfile myfile2 mydir`

`user_spec` 参数可以是以下任何一种形式：

| `user_spec` | 含义 |
|---|---|
| `smith` | 存在的用户名 |
| `1001` | 数字用户 `ID` |
| `smith:party` | 存在的用户名和组名，用冒号分隔 |
| `1001:234` | 数字用户 `ID` 和组 `ID`，用冒号分隔 |
| `:party` | 存在的组名，前面带有一个冒号 |
| `--reference=file` | 与文件 `file` 相同的用户和组值 |

### 有用选项

- `--dereference` 跟踪符号链接并对它们所指向的文件进行操作。
- `-R` 递归地更改整个目录树的所有者。

## `chgrp`

`stdin stdout file --opt --help --version`

`chgrp [options] group_spec files`

`chgrp`（更改组）命令设置文件和目录的组所有权：

`+ -> chgrp users myfile myfile2 mydir`

`group_spec` 参数可以是以下任何一种形式：

- `-` 组名或数字组 `ID`
- `--reference=file`，将另一个给定文件设置为相同的组所有权

有关组的更多信息请参见第 192 页的“组管理”。

### 有用选项

- `--dereference` 跟踪符号链接并对它们所指向的文件进行操作。
- `-R` 递归地更改整个目录树的组。

## `chmod`

`stdin stdout file --opt --help --version`

`chmod [options] permissions files`

`chmod`（更改模式）命令保护文件和目录免受未经授权的用户的影响。典型的八进制权限如下：

```
chmod 600 myfile      你的私人文件
chmod 644 myfile      所有人读取
chmod 700 mydir       你的私有目录
chmod 755 mydir       所有人可读可执行
```

图 2-2. 文件权限位

在第三种符号形式中，每个字符串由三部分组成：

### 范围（可选）

`+` `u` 代表用户，`g` 代表组，`o` 代表其他用户，`a` 代表所有用户。默认是 `a`。

### 命令

`+` 添加权限；`–` 删除权限；或 `=` 设置绝对权限，忽略现有权限。

### 权限

`r` 代表读取，`w` 代表修改，`x` 代表执行（对于目录代表进入），`X` 代表条件执行（后文介绍），`u` 代表复制用户权限，`g` 代表复制组权限，`o` 代表复制其他权限，`s` 代表 `setuid`（设置用户 `ID`）或 `setgid`（设置组 `ID`），`t` 代表粘性位。
