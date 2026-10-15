
`cvs remove`: 1 file exists; use '`rm`' to remove it first

```bash
$ rm newdemo3
```

```bash
$ ls
CVS README newdemo4 newdemo5 present.1 present.2 present.3
```

```bash
$ cvs remove newdemo3
```

`cvs remove`: scheduling '`newdemo3`' for removal

`cvs remove`: use '`cvs commit`' to remove this file permanently

```bash
$ cvs commit newdemo3
```

`/tmp/10806aa`: 10 lines, 316 characters.

```bash
$ ls CVSROOT/workshop_demos newdemo4,v newdemo5,v present.1 present.2 present.3
Attic README,v
```

## 709 date 显示或设置时间和日期

语法：`date [option] [+format]`
`date [option] newdate`

### 摘要

`date` 工具用于显示时间和日期。超级用户（Superuser）可以使用它来更改时间和日期。

### 参数

当超级用户指定一个新的 `newdate` 时，系统会更改系统时以反映新日期。
`newdate` 参数具有以下格式：

```
ndddhhmm[cc/yy]
```

`nn` 是月份（01–12），`dd` 是日期（01–31），`hh` 是基于 24 小时制的（00–23），`mm` 是分钟（00–59）。最后四位是可选的；如果不指定年份，`date` 假设年份没有变化。`cc` 指定年份的前两位（世纪值减 1），`yy` 指定年份的后两位。

你可以使用 `+format` 来指定 `date` 输出的格式。跟在 `+` 之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分比符号 `%` 开头，每个描述符在输出中都会替换为其值。字段列表见下表：

| 字段描述符 | 含义 |
| :--- | :--- |
| `%a` | 缩写的星期—周日到周六 |
| `%A` | 完整的星期—星期日到星期六 |
| `%b` | 缩写的月份—1月到12月 |
| `%B` | 完整的月份—1月到12月 |
| `%c` | `date` 使用的默认格式日期时间 |
| `%d` | 日期—01 到 31 |
| `%D` | mm/dd/yy 格式的日期 |
| `%H` | 小时—00 到 23 |
| `%j` | 一年中的第几天—001 到 366 |
| `%m` | 月份—01 到 12 |
| `%M` | 分钟—00 到 59 |
| `%n` | 换行符 |

## 710 date

| 字段描述符 | 含义 |
| :--- | :--- |
| `%P` | AM 或 PM |
| `%r` | AM/PM 符号的时间 |
| `%S` | 秒—00 到 59 |
| `%t` | 制表符 |
| `%T` | HH:MM:SS 格式的时间 |
| `%w` | 星期几—0 到 6 (0-为周日) |
| `%y` | 年份的后两位—00 到 99 |
| `%Y` | 四位数格式的年份（例如, 1997） |
| `%Z` | 时区（例如, PDT） |

格式字符串中任何不是百分比符号 (`%`) 或字段描述符的字符都被视为普通文本，并复制到输出中。你可以使用普通文本为日期添加标点符号和标签（例如，可以在日期前加上 `DATE:`）。如果格式参数包含空格（SPACES）或其他对 shell 有特殊含义的字符，请用单引号将之括起来。

### 选项

- `-u` universal 显示或设置时间和日期
- `+format` 指定 `date` 输出的格式。在 `+` 之后，你可以指定一个由字段描述符和文本组成的格式字符串。字段描述符以百分比符号 开头，每个描述符在输出中都会替换为其值。字段列表见下表：

| 字段描述符 | 含义 |
| :--- | :--- |
| `%a` | 缩写的星期—周日到周六 |
| `%A` | 完整的星期—星期日到星期六 |
| `%b` | 缩写的月份—1月到12月 |
| `%B` | 完整的月份—1月到12月 |
| `%c` | `date` 使用的默认格式日期时间 |
| `%d` | 日期—01 到 31 |
| `%D` | mm/dd/yy 格式的日期 |
| `%H` | 小时—00 到 23 |
| `%j` | 一年中的第几天—001 到 366 |
| `%m` | 月份—01 到 12 |
| `%M` | 分钟—00 到 59 |
| `%n` | 换行符 |

| 字段描述符 | 含义 |
| :--- | :--- |
| `%P` | AM 或 PM |
| `%r` | AM/PM 符号的时间 |
| `%S` | 秒—00 到 59 |
| `%t` | 制表符 |
| `%T` | HH:MM:SS 格式的时间 |
| `%w` | 星期几—0 到 6 (0-为周日) |
| `%y` | 年份的后两位—00 到 99 |
| `%Y` | 四位数格式的年份（例如, 1997） |
| `%Z` | 时区（例如, PDT） |

格式字符串中任何不是百分比符号 (`%`) 或字段描述符的字符都被视为普通文本并复制到输出中。你可以使用普通文本为日期添加标点符号和标签（例如，可以在日期前加上 `DATE:`）。如果格式参数包含空格（SPACES）或其他对 shell 有特殊含义的字符，请用单引号将之括起来。

## 712 dd

| 类型 | 含义 |
| :--- | :--- |
| ascii | 将 EBCDIC 转换为 ASCII。这允许你在大型机及类似设备上读取磁带。 |
| block | 每当读取一行输入（即字符序列）时，输出一个带换行符（NEWLINE）的块。 |
| ebcdic | 将 ASCII 转换为 EBCDIC。这允许你在大型机及类似设备上写入磁带。 |
| lcase | 在复制数据时将大写转换为小写。 |
| noerror | 如果发生读取错误，`dd` 通常会终止。此转换允许 `dd` 继续处理数据。这在尝试从坏介质恢复数据时有用。 |
| ucase | 在复制数据时将小写转换为大写。 |

`dd` 工具允许你使用简写表示法提供大数字参数。在数字后面加上 `n` 表示该数字乘以 512，加上 `k` 则将数字乘以 1024。

### 示例

第一个示例展示了如何使用 `dd` 工具制作软盘的精确副本：首先将磁盘内容复制到硬盘上的文件，然后在向软盘驱动器插入一张新磁盘后，将该文件复制回软盘。无论软盘上有什么内容都有效。在这种情况下，它是一个 DOS 格式的磁盘。在第二次调用 `dd` 后，副本也是 DOS 格式的磁盘。示例开头和结尾的 `mount`, `ls`, `mount` 序列验证了原始磁盘和副本包含相同的文件。

示例中创建的 `floppy.copy` 文件是原始软盘的精确副本。你可以使用 `dosemu` 应用程序（见第 932 页）访问该文件的内容（如果它是软盘的话）。

```bash
# mount -t msdos /dev/fd0H1440 /mnt
# ls /mnt
abaprint.dat bti.ini setup.ins sufiles.z wbt.z
adbook.2z setup.exe setup.pkg telephone.z
# umount /mnt
# dd if=/dev/fd0 bs=512 >floppy.copy
2880+0 records in
2880+0 records out
```

```bash
ls -l floppy.copy speedy 147560 Sep 11 05:43 floppy.copy
-rw-rw-r-- 1 alex
# dd if=floppy.copy bs=512 of=/dev/fd0
2880+0 records in
2880+0 records out
# mount -t msdos /dev/fd0H1440 /mnt
# ls /mnt
abaprint.dat bti.ini setup.ins suptiles.z wbt.z
adbook.z setup.exe setup.pkg telephon.z
# umount /mnt
```

第二个示例展示了一个简单的 shell 脚本，用于对远程系统进行全系统备份。该脚本使用 `rsh` 实用在远程系统上运行 `dd`。

```bash
#!/bin/sh
# 对 bravo 上的远程磁带进行全备份
machine=bravo
device=/dev/rst0
echo -n "Backing to $machine using device $device...(请耐心等待)..."
cd /
tar -cf - | rsh -l h1 $machine dd=256k of=$device
echo "Full backup to $machine ($device) done on \`date` >/etc/last.backup
echo "done."
```

## 714 df

| `df` | 显示可用磁盘空间 |
| :--- | :--- |
| 语法: | `df [options] [filesystem-list]` |

### 总结

`df` (disk free) 实用工具报告任何挂载设备或目录上剩余的可用空间（以块为单位）。通常每个块为 1 千字节 (1K) 或 1024 字节。

### 参数

当不带任何参数调用 `df` 时，它会报告每个当前挂载设备的空闲空间。`filesystem-list` 是一个可选列表，包含一个或多个路径名，用于通过设备路径名或其挂载目录的路径名来指定你想要报告的挂载文件系统。

### 选项

- `--type=ftype` (-t ftype) 仅报告关于 `ftype` 类型文件系统的信息，例如 MSDOS 或 NFS。
- `--inodes` (-i) 报告已使用和空闲的 inode 数量，而不是报告块。

### 示例

下面，`df` 显示了机器上所有挂载文件系统的信息：

```bash
$ df
Filesystem 1024-blocks Used Available Capacity Mounted on
/dev/hdb1 31720 21124 8958 70% /
/dev/hdb4 60063 212 56749 0% /tmp
/dev/sda1 297635 249681 32582 88% /usr
/dev/sda5 96167 5236 85965 6% /usr/tmp
/dev/sda4 199271 13857 50123 73% /usr/X386
/dev/sda3 640281 59375 47831 92% /usr/local
/dev/sda6 50555 20343 27602 42% /store
/dev/hdb3 198275 181155 6874 96% /home
/dev/hda2 107628 75300 32328 70% /C:
```

下一个示例显示了挂载的 DOS 文件系统的信息：

```bash
$ df -t msdos
Filesystem 1024-blocks Used Available Capacity Mounted on
/dev/hda2 107628 75300 32328 70% /C:
```

## 显示两个文件之间的差异

```bash
Syntax: diff [options] file1 file2
diff [options] file1 directory
diff [options] file2 directory
diff [options] directory1 directory2
```
