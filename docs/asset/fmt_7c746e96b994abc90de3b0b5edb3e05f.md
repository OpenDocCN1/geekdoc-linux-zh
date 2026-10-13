
## 描述

请参阅 `jobs(1)`。

# fgrep — 在文件中搜索固定字符字符串

### 概要

```
/usr/bin/fgrep [-bchilinsvx] [-e pattern-list] -f pattern-file [pattern] file ...
/usr/xpg4/bin/fgrep [-bchilinsvx] [-e pattern-list] -f pattern-file [pattern] file ...
```

## 描述

`fgrep` (fast grep) 命令在文件中搜索字符字符串并打印所有包含该字符串的行。`fgrep` 与 `grep(1)` 和 `egrep(1)` 不同。

因为它搜索的是字符串，而不是匹配表达式的模式。`fgrep` 使用了一种快速且紧凑的算法。
`fgrep` 将字符 `$` `*` `^` `|` `(` `)` 和 `\` 视为字文字，即 `fgrep` 不像 `egrep` 那样识别完整的正则表达式。由于这些字符对 shell 具有特殊含义，最安全的方法是用单引号 `'...'` 将整个字符串括起来。如果没有指定文件，`fgrep` 将使用标准输入。通常，每一行都会被复制到标准输出。如果有多个输入文件，会在每个找到的行之前打印文件名。

**注意** — 理想情况下应该只有一个 `grep` 命令；然而，没有一种单一算法能够跨越足够广泛的时空权衡范围。

行数的限制仅取决于可用虚拟内存的大小。
`/usr/xpg4/bin/fgrep` 命令与 `/usr/xpg4/bin/grep -F` 相同（参见 `grep(1)`）。可移植应用程序应使用 `/usr/xpg4/bin/grep -F`。

## 选项

- `-b` 在每行前显示该行所在的块号。此选项有助于通过上下文定位块号（第一个块为 0）。
- `-c` 仅打印包含模式的行数。
- `-e pattern-list` 在 `pattern-list` 中搜索字符串（当字符串以 `-` 开头时非常有用）。
- `-f pattern-file` 从 `pattern-file` 获取模式列表。
- `-h` 在搜索多个文件时抑制打印文件名。
- `-i` 在比较时忽略大小写区别。
- `-l` 仅打印一次包含匹配行的文件名，并用换行符分隔。当模式出现多次时，不要重复打印文件名。
- `-n` 在每行前显示该行在文件中的行号（第一行是 1）。
- `-s` 静默工作，即除错误消息外不显示任何内容。此选项对于检查错误状态时非常有用。
- `-v` 打印所有不包含模式的行。
- `-x` 仅打印完全匹配的行。

### 操作数

`file` 要搜索的文件路径名。如果没有指定文件，`fgrep` 将使用标准输入。

`pattern` 要搜索的字符串。对于 `/bin/fgrep`，请指定一个模式。
对于 `/usr/xpg4/bin/fgrep`，请指定一个或多个模式。

## 示例

接下来的示例使用了不带参数的 `fdformat`（针对新软盘），在软盘上成功创建了 SunOS 文件系统。

```
castle$ fdformat

Formatting 1.44 MB in /vol/dev/rdiskette0/untitled

Press return to start formatting floppy.
```

接下来的示例使用 `-d` 选项在软盘上成功创建了 DOS 文件系统。

```
castle$ fdformat -d

Formatting 1.44 MB in /vol/dev/rdiskette0/untitled

Press return to start formatting floppy.
```

## 用法

参阅 `largefile(5)` 了解 `fgrep` 处理大于 2 Gbytes 文件时的行为。

## 环境变量

参阅 `environ(5)` 了解影响执行的变量：`LC_COLLATE`、`LC_CTYPE`、`LC_MESSAGES` 和。

## 退出状态

`0` 找到匹配。
`1` 未找到匹配。
`2` 语法错误或无法访问文件。

## 属性

关于下述属性的描述，请参阅 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNwcsu |

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNcu |

## 参见

`cpio(1)`, `eject(1)`, `tar(1)`, `volcancel(1)`, `volcheck(1)`, `volmissing(1)`, `volmount(1)`, `mount(1M)`, `newfs(1M)`, `rmount(1M)`, `void(1M)`, `rmountconf(4)`, `void.conf(4)`, `attributes(5)`, `pcfs(7FS)`, `volfs(7FS)`

- 仅限 x86

- `fd(7D)`

# file — 文件类型

### 概要

```
/usr/bin/file [-h] [-m file] [-f ffile]
/usr/bin/file [-h] [-m file]
```

## 描述

`file` 命令对每个提供的文件执行一系列测试，可选地对 `logfile` 中列出的每个文件执行，以对其进行分类。如果是普通文件，则识别其类型。如果是 0 长度的文件，则被识别为空文件。如果是符号链接，则跟踪链接并对链接指向的文件进行测试。
魔数是一个数字或字符串常量，用于指示文件类型。默认情况下，`file` 尝试使用本地化的魔数文件 `/usr/lib/locale/LC_MESSAGES/magic`（如果存在）。如果没有则使用 `/etc/magic`。参阅 `magic(4)` 了解 `/etc/magic` 的格式。

### 操作数

`file` 包含要检查文件名的文件。
`file` 要测试的文件路径名。
`mfile` 替代魔数文件。

## 示例

接下来的示例显示目录下所有文件的类型。

```
castle$ file * directory

Art:

design.book: empty file

Mail: directory

Menu.start: empty file

ibliography: ascii text

checknr.1: [nt]ref, tbl, or eqn input text

dofile: ascii text

example.c: c program text

example.stringout: ascii text

kerberos: English text

local.cshrc: assembler program text

local.profile: ascii text

castle$
```

接下来的示例判断一个文件是否是二进制可执行文件。
`castle$ file "$1" | grep -Fq executable && printf "%s is executable.\\n" "$1"`

## 用法

参阅 `largefile(5)` 了解 `file` 处理大于 2 Gbytes (2**31 bytes) 文件时的行为。

如果文件不存在、无法读取或无法确定其文件状态，则不被视为影响退出状态的错误。输出指示文件已处理，但无法确定其类型。

## 选项

### 操作数

`file` 包含要检查文件名的文件。
`file` 要测试的文件路径名。
`mfile` 替代魔数文件。

## 退出状态

```
0          执行成功。
>0         发生错误。
```

## 文件

```
/etc/magic 幻数文件。
```

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|--- |--- |
|可用性 | SUNWcsu |
| CSI | Enabled |

## 参见

`ls(1)`, `filehdr(4)`, `magic(4)`, `attributes(5)`, `environ(5)`, `largefile(5)`

## 诊断

当指定 `-h` 选项且文件为符号链接时，`file` 会打印错误信息：
`symbolic link to file`

# filesync — 同步普通文件、目录或特殊文件

### 概要

```
/usr/bin/filesync [-aehmnqvy] [-o src | dst] [-f src | dst] |old | new] [-r directory ...]
/usr/bin/filesync [-aehmnqvy] -source dir -d dest-dir filename ...
```
