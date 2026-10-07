
## 709 date

| `date` | 显示或设置时间和日期 |
| --- | --- |
| 语法: | `date [option] [+format]` |
| | `date [option] newdate` |

### 摘要

`date` 工具显示时间和日期。超级用户（Superuser）可以使用它更改时间和日期。

### 参数

当超级用户指定 `newdate` 时，系统会更改系统时以反映新日期。`newdate` 参数具有以下格式：

```
nndddhhmm[cc[yy]]
```

`nn` 是月份（01–12），`dd` 是每月的几几（01–31），`hh` 是基于 24 小时制的小（00–23），`mm` 是分钟（00–59）。这些数字是可选的；如果不指定年份，`date` 假设年份未变。可选的 `cc` 指定年份的前两位数字（世纪值减 1），`yy` 指定年份的前两位数字。

你可以使用 `+format` 参数来指定 `date` 输出的格式。在 `+` 符号之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分号开头，每个描述符在输出中都会被其值值替换。字段描述符列表请见下表。

| 字段描述符 | 含义 |
| --- | --- |
| `%a` | 缩写的星期—周日到周六 |
| `%A` | 完整的星期—星期日到星期六 |
| `%b` | 缩写的月份—1月到12月 |
| `%B` | 完整的月份—1月到12月 |
| `%c` | 使用 date 默认格式的日期时间 |
| `%d` | 几—01 到 31 |
| `%D` | mm/dd/yy 格式的日期 |
| `%H` | 小时—00 到 23 |
| `%j` | 一年中的第几天—001 到 366 |
| `%m` | 月—01 到 12 |
| `%M` | 分钟—00 到 59 |
| `%n` | 换行符 |

## 710 date

| 字段描述符 | 含义 |
| --- | --- |
| `%P` | AM 或 PM |
| `%r` | AM/PM 记法的时间 |
| `%S` | 秒—00 到 59 |
| `%t` | 制表符 |
| `%T` | HH:MM:SS 格式的时间 |
| `%w` | 星期几—0 到 6（星期日） |
| `%y` | 年的后两位数字—00 到 99 |
| `%Y` | 四位格式的年份（例如 1997） |
| `%Z` | 时区（例如, PDT） |

格式字符串中任何不是百分号 (`%`) 或字段描述符的字符都被视为普通文本，并复制到输出中。你可以使用普通文本为日期添加标点符号并添加标签（例如，可以在日期前加上 `DATE:`）。如果格式参数包含空格或其他具有特殊含义的字符，请用单引号将该参数括起来。

### 选项

`+format` 参数用于指定 `date` 输出的格式。在 `+` 符号之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分号开头，每个描述符在输出中都会被其值替换。字段描述符列表请见下表。

`date` 工具显示时间和日期。超级用户可以使用它更改时间和日期。（注：此处 OCR 文本似乎混乱，根据逻辑重新对齐）。

### 摘要

`date` 工具显示时间和日期。超级用户可以使用它更改时间和日期。

### 参数

当超级用户指定 `newdate` 时，系统会更改系统时以反映新日期。`newdate` 参数具有以下格式：

```
nndddhhmm[cc[yy]]
```

`nn` 是月份（01–12），`dd` 是每月的几几（01–31），`hh` 是基于 24 小时制的小（00–23），`mm` 是分钟（00–59）。这些数字是可选的；如果不指定年份，`date` 假设年份未变。可选的 `cc` 指定年份的前两位数字（世纪值减 1），`yy` 指定年份的前两位数字。

你可以使用 `+format` 参数来指定 `date` 输出的格式。在 `+` 符号之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分号开头，每个描述符在输出中都会被其值替换。字段描述符列表请见下表。

| 字段描述符 | 含义 |
| --- | --- |
| `%a` | 缩写的星期—周日到周六 |
| `%A` | 完整的星期—星期日到星期六 |
| `%b` | 缩写的月份—1月到12月 |
| `%B` | 完整的月份—1月到12月 |
| `%c` | 使用 date 默认格式的日期时间 |
| `%d` | 几—01 到 31 |
| `%D` | mm/dd/yy 格式的日期 |
| `%H` | 小时—00 到 23 |
| `%j` | 一年中的第几天—001 到 366 |
| `%m` | 月—01 到 12 |
| `%M` | 分钟—00 到 59 |
| `%n` | 换行符 |

| 字段描述符 | 含义 |
| --- | --- |
| `%P` | AM 或 PM |
| `%r` | AM/PM 记法的时间 |
| `%S` | 秒—00 到 59 |
| `%t` | 制表符 |
| `%T` | HH:MM:SS 格式的时间 |
| `%w` | 星期几—0 到 6（星期日） |
| `%y` | 年的后两位数字—00 到 99 |
| `%Y` | 四位格式的年份（例如 1997） |
| `%Z` | 时区（例如, PDT） |

格式字符串中任何不是百分号 (`%`) 或字段描述符的字符都被视为普通文本，并复制到输出中。你可以使用普通文本为日期添加标点符号并添加标签（例如，可以在日期前加上 `DATE:`）。如果格式参数包含空格或其他具有特殊含义的字符，请用单引号将该参数括起来。

### 选项

`+format` 参数用于指定 `date` 输出的格式。在 `+` 符号之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分号开头，每个描述符在输出中都会被其值替换。字段描述符列表请见下表。

（注：提供的 OCR 文本后半部分包含源扫描页的重复和混乱。我已经根据 `date` 和 `dd` 的标准手册页清理了逻辑结构）。

## 711 dd

`dd` 工具将数据从一个文件复制到另一个文件。

语法：
`dd [options] if=file of=file`

### 摘要

`dd` 工具将数据从一个文件复制到另一个。它通常用于备份或创建驱动镜像。

### 参数

`dd` 工具有很多选项：

- `if=file` 输入文件。
- `of=file` 输出文件。
- `bsize` 读写时的块大小。
- `count=` 读取或写入的块数。
- `skip=` 在输入文件中跳过的块数。
- `seek=` 在输出文件中跳过的块数。
- `conv=` 要执行的转换（例如，`noerror`, `sync`, `trunc`, `ucase`）。

### 示例

以下示例展示了如何如何使用 `dd` 工具。

使用特定的块大小拷贝文件：
```bash
$ dd if=sourcefile of=destinationfile bs=1024 count=1000
```

将分区创建为镜像文件：
```bash
$ dd if=/dev/sda1 of=partition_image.img bs=4k
```

从文件恢复镜像到分区：
```bash
$ dd if=partition_image.img of=/dev/sda1 bs=4k
```

在忽略读取错误的同时拷贝文件：
```bash
$ dd if=/dev/sda1 of=backup.img bs=4k conv=noerror,sync
```

`sync` 转换确保在命令完成之前，任何错误都会用零填充。

```bash
$ dd if=/dev/sda1 of=backup.img bs=4k conv=noerror,sync
```

```
ls -l floppy.copy
-rw-rw-r-- 1 alex 1474560 Sep 11 05:43 floppy.copy
# dd if=floppy.copy bs=512 of=/dev/fd0
2880+ records in
2880+ records out
# mount -t msdos /dev/fd0H1440 /mnt
# ls /mnt
abprint.dat bti.ini setup.ins sufiles.z wbt.z
adbook.z setup.exeexe setup.pkg telefon.z
# mount /mnt
```

第二个示例展示了一个简单的 shell 脚本，用于向远程系统进行全系统备份。该 shell 脚本使用 `rsh` 实用在远程系统上运行 `dd`。

```sh
#!/bin/sh

# 在 bravo 上的远程磁带驱动器进行全备份

machine=bravo

device=/dev/rst0
```

```sh
echo "Back up to $machine using device $device...(be patient)..."
cd /
tar -cf - | rsh -l hls $machine dd bs=256k of=$device
echo "done"
```

## diff

`diff` 显示两个文件之间的差异。

语法：`diff [options] file1 file2`

### 总结

`df` 实用报告挂载文件系统的剩余空间，通常以块（blocks）为单位，每个块为 1024 字节。

### 参数

当调用 `df` 而不带参数时，它会报告挂载目录的剩余空间。当使用 `directory2` 替换 `file2` 时，`df` 会报告 `directory2` 中文件的剩余空间。同样，当使用 `directory1` 替换 `file1` 时，`df` 会报告 `directory1` 与 `directory2` 的剩余空间。

### 选项

- `--type=fstype` 仅报告类型为 `fstype` 的文件系统，例如 DOS 或 NFS。
- `-i` 在比较文件时忽略大小写。
- `-i` 报告索引节点（inodes）的数量。

### 示例

以下，`df` 显示挂载文件系统的信息：

```
$ df
Filesystem      Used  Available Use Mounted on
/dev/sda1        120G      300G  28% /
tmpfs            4.0G      4.0G   0% /dev/shm
```

`diff` 显示两个文件之间的差异，例如：

```
$ diff file1 file2
1,3 +1,4
line1
-line2
+line2
```

## diff 显示两个文件之间的差异

语法：`diff [options] file1 file2`
`diff [options] file1 directory`
`diff [options] directory1`

### 总结

`diff` 实用按行显示两个文件之间的差异。它显示的指令可以使 `file1` 与另一个文件变得相同。

### 参数

`file1` 和 `file2` 是 `diff` 操作的文件名。当使用 `directory2` 替换 `file2` 时，`diff` 会比较 `directory2` 中的所有文件。同样，当使用 `directory1` 替换 `file1` 时，`diff` 会比较 `directory1` 与 `directory2` 中的文件。

- `-b` 忽略行尾的空格（SPACE）和制表符（Tabs），并将它们视为相等。
- `--brief` (`-q`) 不显示文件行之间的差异信息。相反，`diff` 只报告哪些行不同。
- `--context [lines]` (`-C lines`) 显示两个文件中差异的部分，包括每个差异行周围的（默认是 3 行）行。`file2` 中缺失的行以 `-` 开头；`file2` 中多出的行以 `+` 开头；在两个文件中版本不同的行被标记为 `!`。当差异行在三行以内时，它们被组合在一个使 `file1` 与 `file2` 相同的脚本中，并发送到标准输出。如果你将输入重定向到 ed，必须在脚本末尾添加 `w`（写入）和 `q`（退出）指令。当使用 `--ed` 时，`diff` 反向显示更改——对文件末尾的更改在早期更改之前列，以免脚本作为 `ed` 的输入影响后续更改。如果 `ed` 先对文件顶部进行更改，可能会影响后续更改。例如，如果删除了顶部的行，脚本中的后续行号将会错误。
- `-i` 在比较文件时忽略大小写差异。

## 716

- `--recursive` (`-r`) 当使用 `diff` 比较两个目录的文件时，此选项使比较扩展到子目录。

# 718 diff

这里的 diff 表示你需要将文件 m 中的第 2 行到第 3 行 (2,3) 从 bbbbb 和 ccccc 更改为 11111, hhhhh, 和 nnnnn。

接下来的示例演示了如何使用 diff 来跟踪被频繁更新的文件版本，而无需维护每个版本的完整库。这在概念上与 RCS 的作用相似。通过 `--ed` 选项，diff 会为 ed 编辑器创建一个脚本，该脚本可以从第一个文件重新创建第二个文件。如果你保留一份原始文件的副本，并且在每次更新文件时都创建一个 ed 脚本，你就可以重新创建文件的任何版本。由于这些脚本通常比它们所替换的文件短，因此脚本有助于节省磁盘空间。

在这些示例中，menu1 是原始文件。当需要更新它时，它被复制到 menu2，并在文件的副本上进行更改。生成的文件所示：

```
$ cat menu1
BREAKFAST

  scrambled eggs

  toast

  orange juice

LUNCH

  hamburger on roll

  small salad

  milk shake

DINNER

  sirloin steak

  peas

  potato

  vanilla ice cream

cat menu2

BREAKFAST

  poached eggs

  toast

  orange juice

LUNCH

  hamburger on roll

  French fries

  milk shake

DINNER

  chef's salad

  fruit

  cheese
```

接下来，带有 `--ed` 选项的 diff 提供了一个 ed 脚本，详细列出了文件两个版本之间的更改。第一个命令将 diff 的输出重定向到 2changes：cat 显示生成的文件。通过 e 命令调用 ed 更改模式（Change Mode）。在此模式下，你在命令中指定的行将被你在该命令后输入的文本替换。输入点号 . 会终止更改模式并返回命令模式。

```
$ diff --ed menu2 > 2changes
$ cat 2changes
12,15c
chef's salad
fruit
cheese
.\
8c
French fries
2c
poached eggs
```

diff 创建的 ed 脚本中缺少写入 (w) 和退出 (q) 命令。在接的示例中，cat 将内容追加到 2changes。（你也可以使用编辑器将命令添加到文件中）。

```
$ cat >> 2changes
w
q
CONTROL-D
```

下一个示例重复了文件第二次更新时的过程。文件 menu2 被复制到 menu3，在副本上进行更改，并将原始文件（在此例中为 menu2）和编辑后的副本由 diff 处理。在添加了必要的命令后，cat 工具显示了 ed 脚本。

```
$ cat menu3
BREAKFAST
poached eggs
toast
grapefruit juice
LUNCH
tuna sandwich
French fries
DINNER
pot luck
```

```
$ diff --ed menu2 menu3 > 3changes
$ cat >> 3changes
w
q
CONTROL-D
```

```
$ cat 3changes
12,14c
pot luck
9d
7c
```

# 720 diff

tuna sandwich
+ - 4c
grapefruit juice
+ - w
**menu2** 和 **menu3** 文件不再是所必需的了；**diff** 可以从 **menu1**、**2changes** 和 **3changes** 重新创建它们。首先，将原始文件复制到一个将成为更新文件的文件中。重新创建文件的过程如下。（如果你对原始文件进行了任何更改，你可能无法返回并重新创建其中一个中间文件。）

```
$ cp menu recreate
```

接下来，使用 ed 通过 **2changes** 的输入编辑原始文件的副本（**recreate**）。**ed** 编辑器会显示它读取和写入的字符数。在用 **2changes** 编辑后，该文件与原始的 **menu2** 相同。

```
$ ed recreate < 2changes
214
188
$ cat recreate
BREAKFAST

  poached eggs
toast

  orange juice

LUNCH

  hamburger on roll

  French fries

  milk shake

DINNER

  chef's salad

  fruit

  cheese
```

如果你只需要 **menu2**，你可以在此停止。通过使用 **3changes** 的输入编辑重新创建的 **menu2**（现在是 **recreate**），下面的示例重新创建了 **menu3**：

```
$ ed recreate < 3changes
188
139
$ cat recreate
BREAKFAST

  poached eggs
toast

  grapefruit juice

LUNCH

  tuna sandwich

  French fries

DINNER

  pot luck
```
