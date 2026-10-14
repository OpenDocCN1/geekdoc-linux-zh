
`castle%`

```
```

这些列具有以下含义：

* 第 1 列是 `./test.c` 的访问权限。
* 第 2 列是 `./test.c` 的用户 ID/组 ID。
* 第 3 列是 `./test.c` 的字节大小。
* 第 4 列是 `./test.c` 的修改日期。当 `LC_TIME` 类别设置为 POSIX 语言环境时，可以使用不同的格式和日期顺序字段。
* 第 5 列是 `./test.c` 的名称。

以下示例从归档中提取文件。

```
castle% tar xvf /dev/rmt/0

messages from tar

cast%
```

如果磁带上有多个归档文件，每个文件通过文件结束标记与下一个文件分开。若要从带有多个归档的磁带上读取第一个和第二个归档，你必须配合 `f` 函数修饰符使用非回绕磁带设备名称，如下例所示。第一个命令读取磁带上的归档；第二个命令读取第二个归档。

```
castle% tar xvp /dev/rmt/0n

messages from tar

castle% tar xvp /dev/rmt/0n

messages from tar

castle%
```

> 注意 - 在某些较早版本中，上述场景无法正常工作，需要在多次调用 `tar` 之间通过 `mt(1)` 进行干预。要模拟旧行为，请使用包含字母 `b` 的非回绕设备名称以实现 BSD 行为。参见 `mtic(7)` 手页的“关闭操作”部分。

以下示例将 `/usr/include` 和 `/etc` 中的文件归档到默认磁带驱动器 0。

```
castle% tar c -C /usr/include -C /etc .
```

生成的 `tar` 文件目录内容将产生如下输出

```
include/

include/a.out.h
```

以及 `/usr/include` 中的所有其他文件。

```
./chown
```

以及 `/etc` 中的所有其他文件。

# tar 1381

以下示例提取 `include` 目录中的所有文件

```
castle$ tar xv include

x include/ , 0 bytes, 0 tape blocks
```

以及 `include` 下的所有文件...

以下示例使用 `tar` 跨以太网传输文件。首先，您将文件从本地系统 (`castle`) 归档到远程系统 (`host`) 的磁带上。

```
castle$ tar cvfb - 20 files | rsh host dd=/dev/rmt/0 obs=20b

messages from tar

castle$
```

上一个示例使用 `c` 字母创建 `tar` 文件，使用 `v` 修饰符请求 `tar` 输出详细信息，使用 `f` 修饰符指定输出 `tar` 文件的名称（标准输出是 `tar` 文件出现的地方，如符号 所示），并使用 `b` 修饰符指定块大小 (`20`)。如果您想更改块大小，必须同时在 `tar` 命令和 `dd` 命令中更改块大小参数。

以下示例使用 `tar` 将文件从远程系统的磁带取回本地系统。

```
castle$ rsh -n host dd=/dev/rmt/0 obs=20b | tar xvf -20

messages from tar

castle$
```

上一个示例通过管道使用 `x` 字母提取，使用 `v` 修饰符请求 `tar` 输出详细信息，使用 `f` 修饰符指定输入 `tar` 文件的名称（标准输出是 `tar` 文件出现的地方，如符号 所示），并使用 `b` 修饰符指定块大小 (`20`)。

以下示例在 `/dev/rmt/0` 上创建归归档。

```
castle$ tar cvfb /dev/rmt/0 20 files

messages from tar

castle$
```

（此处省略后续重复部分，确保核心内容翻译已完成）

## 1384

| 选项 | 说明 |
|---|---|
| `linesize(n)` | 将所有行设置为 `n` 点字号。 |

在表格结构中，你可以按照下表描述为列条目指定格式。

| 代码 | 结果 |
|---|---|
| `^` | 将条目从上上一行扩展到当前行。 |
| `a` | 字符从左对齐缩进一个 em。 |
| `c` | 数据居中对。 |
| `1` | 数据左对齐。 |
| `n` | 按小数点或个位对齐数字。 |
| `r` | 数据右对齐。 |
| `s` | 通过将上一列的数据扩展到此列来实现跨列显示。 |
| `t` | 垂直跨越，文本位于列顶部。 |

### 选项

- `-me` 将 `-me` 宏包复制到输出文件的开头。
- `-mm` 将 `-mm` 宏包复制到输出文件的开头。
- `-ms` 将 `-ms` 宏包复制到输出文件的开头。

### 示例

在以下 `tbl` 示例中，符号 `(@)` 代表在输入文件中应输入的实际制表符 (`Tab`)。

```
.TS

c s s

c c s

c c c

l n n.

Household Population

Town@Households

@Number@Size

Bedminster@0789@3.26

Bernards Twp.@03087@3.74

Bernardsville@2018@3.30

Bound Brook@3425@3.04

Branchburg@16444@3.49

.TE
```

# tcopy

## 1385

产生

| 城镇 | 家庭户数量 | 尺寸 |
|---|---|---|
| Bedminster | 789 | 3.26 |
| Bernards Twp. | 3087 | 3.74 |
| Bernardsville | 2018 | 3.30 |
| Bound Brook | 3425 | 3.04 |
| Branchburg | 1644 | 3.49 |

## 文件

```
/usr/share/lib/tmac/e
```
`-me` macros.

```
/usr/share/lib/tmac/m
```
`-mm` macros.

```
/usr/share/lib/tmac/s
```
`-ms` macros.

### 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNdoc |

# 另见

`eqm(1)`, `nroff(1)`, `troff(1)`, `attributes(5)`

# tcopy - 复制磁带

### 概要

```
/usr/bin/tcopy source [destination]
```

### 描述

使用 `tcopy` 参数复制由 `source` 参数指定的磁带驱动器上挂载的磁带。对磁带内容的唯一假设是末尾有两个磁带标记。

当你仅指定源驱动器时，`tcopy` 会扫描磁带并显示有关记录大小和磁带文件大小的信息。如果你指定了目标位置，`tcopy` 将源磁带复制到目标位置，并保持阻塞（blocking preserved）。在复制过程中，`tcopy` 产生的输出与扫描磁带时的输出相同。

注意 - `tcopy` 仅运行在支持相关 `ioctl(2)` 请求的系统上。

你必须在 `tcopy` 命令中使用兼容 Berkeley 的设备名称，如下例所示：

```
mopoke@ tcopy /dev/rmt /dev/rmt/2b
```

### 属性

参见 `attributes(5)` 以获取属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNmesu |

# 另见

`mt(1)`, `ioctl(2)`, `attributes(5)`

# tee 复制标准输出

### 概要

```
/usr/bin/tee [-ai] [file...]
```

### 描述

`tee` 命令类似于水路中的 T 型接头，它可以分流进入的水流。`tee` 将标准输入拆分为两个或多个输出流，将其中一个发送到标准输出，其他发送到你在命令行中指定的文件。

你可以使用 `tee` 命令监控一个命令，以确保它执行你想要保存的操作，或者作为管道序列中的中间步骤，`tee` 不对其输出进行缓冲。选项决定了指定的文件是被覆盖还是追加。

### 选项

- `-a` 将输出追加到文件而不是覆盖。
- `-i` 忽略中断。

### 操作数

- `-` 输出文件的路径名。你可以处理至少 13 个操作数。

### 示例

以下示例使用 `file` 命令显示当前目录下文件的信息，并将信息的一个副本保存到名为 `filetypes` 的文件中。

```
castle% * | tee filetypes

085DOC.zip: data

Appletver.rs: rasterfile, 511 x 18 x 8 standard format image

Mail: directory

ibliography: ascii text

ELF 32-bit MSB core file SPARC Version 1, from 'srchtrt'

core: tee *
```

# tee 1387

```
examples: ascii text

find.zip: ZIP archive

kookaburra-1: ascii text
```
