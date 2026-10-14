
## `sort`

```
Fedora 9 05/13/2008
Fedora 10 11/25/2008
SUSE 10.1 05/11/2006
SUSE 10.2 12/07/2006
SUSE 10.3 10/04/2007
SUSE 11.0 06/19/2008
Ubuntu 6.06 06/01/2006
Ubuntu 6.10 10/26/2006
Ubuntu 7.04 04/19/2007
Ubuntu 7.10 10/18/2007
Ubuntu 8.04 04/24/2008
Ubuntu 8.10 10/30/2008
```

尽管我们使用了选项的长形式以提高清晰度，`-k 1,1 -k 2n` 与之完全等价。在第一次使用 `key` 选项时，我们指定了一个字段范围作为第一个键。由于我们只想将排序限制在第一个字段，因此指定了 `1,1`，这意味着“从第 1 个字段开始，到第 1 个字段结束”。在第二次使用时，我们指定了 `2n`，这意味着第 2 个字段是排序键，并且排序应为数值排序。可以在键说明符的末尾包含一个选项字母，以指示要执行的排序类型。这些选项字母与 `sort` 程序的全局选项相同：`b`（忽略前导空格）、`n`（数值排序）、`r`（反向排序）等等。

我们列表中的第三个字段包含一个不便于排序的日期格式。在计算机上，日期通常以 `YYYY-MM-DD` 的顺序格式化，以便于按时间顺序排序，但我们的日期采用的是美国格式 `MM/DD/YYYY`。我们如何按时间顺序对这个列表进行排序？

幸运的是，`sort` 提供了方法。`key` 选项允许在字段内指定偏移量，因此我们可以定义字段内的键：

```
[me@linuxbox ~]$ sort -k 3.7nbr -k 3.1nbr -k 3.4nbr distros.txt
Fedora    10    11/25/2008
Ubuntu    8.10  10/30/2008
SUSE      11.0  06/19/2008
Fedora    9     05/13/2008
Ubuntu    8.04  04/24/2008
Fedora    8     11/08/2007
Ubuntu    7.10  10/04/2007
SUSE      10.3  10/04/2007
Fedora    7     05/31/2007
Ubuntu    7.04  04/19/2007
SUSE      10.2  12/07/2006
Ubuntu    6.10  10/26/2006
Fedora    6     10/24/2006
Ubuntu    6.06  06/01/2006
SUSE      10.1  05/11/2006
Fedora    5     03/20/2006
```

通过指定 `-k 3.7`，我们指示 `sort` 使用从第三个字段第 7 个字符开始的排序键，这对应于年份的开始。同样，我们指定 `-k 3.1` 和 `-k 3.4` 来分离日期的月份和日期部分。我们还添加了 `n` 和 `r` 选项以实现反向数值排序。`b` 选项用于抑制日期字段中的前导空格（这些空格的数量因行而异，从而影响排序结果）。

有些文件不使用制表符和空格作为字段分隔符；例如 `/etc/passwd` 文件：

```
[me@linuxbox ~]$ head /etc/passwd
root:x:0:0:root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games::/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
```

该文件中的字段以冒号（`:`）分隔，那么我们如何使用键字段对该文件进行排序？`sort` 提供了 `-t` 选项来定义字段分隔符字符。要按第七个字段（账户的默认 shell）对 `passwd` 文件进行排序，

```
[me@linuxbox ~]$ sort -t ':' -k 7 /etc/passwd | head
me:x:1001:1001:Myself,,,:/home/me:/bin/bash
root:x:0:0:root:/root:/bin/bash
dhcp:x:101:102::/nonexistent:/bin/false
gdm:x:106:114:GNOME Display Manager,,,:/var/lib/gdm:/bin/false
lp1ip:x:104:7:HPLIP system user,,,:/var/run/hplip:/bin/false
klog:x:103:104:/home/klog:/bin/false
messagebus:x:108:119::/var/run/dbus:/bin/false
polkituser:x:110:122:PolicyKit,,,:/var/run/PolicyKit:/bin/false
pulse:x:107:116:PulseAudio Daemon,,,:/var/run/pulse:/bin/false
```

通过指定冒号字符作为字段分隔符，我们可以按第七个字段进行排序。

## `uniq`—报告或省略重复行

与 `sort` 相比，`uniq` 程序非常轻量。`uniq` 执行一项看似微不足道的任务。给定一个已排序的文件（包括标准输入），它会删除任何重复行并将结果发送到标准输出。它通常与 `sort` 结合使用，以清理输出中的重复项。

> 注意：虽然 `uniq` 是传统上常与 `sort` 一起使用的 Unix 工具，但 GNU 版本的 `sort` 支持 `-u` 选项，可从排序输出中删除重复项。

让我们创建一个文本文件来试用：

```
[me@linuxbox ~]$ cat > foo.txt
a
b
c
a
b
c
```

要让 `uniq` 实际发挥作用，输入必须先排序：

```
[me@linuxbox ~]$ sort foo.txt | uniq
a
b
c
```

这是因为 `uniq` 仅删除彼此相邻的重复行。

`uniq` 有多个选项。表 20-2 列出了常见的选项。

### Table 20-2: Common `uniq` Options

| Option | Description |
| --- | --- |
| `-c` | 在输出重复行之前，先输出该行出现的次数列表。 |
| `-d` | 仅输出重复行，而不是唯一行。 |
| `-f n` | 忽略每行开头的 `n` 个字段。字段由空白分隔，就像在 `sort` 中一样；然而，与 `sort` 不同，`uniq` 没有设置替代字段分隔符的选项。 |
| `-i` | 在行比较期间忽略大小写。 |
| `-s n` | 跳过（忽略）每行开头的 `n` 个字符。 |
| `-u` | 仅输出唯一行。这是默认值。 |

这里我们看到 `uniq` 使用 `-c` 选项来报告在文本文件中找到的重复次数：

```
[me@linuxbox ~]$ sort foo.txt | uniq -c
2 a
2 b
2 c
```

## Slicing and Dicing

我们接下来要讨论的三个程序用于从文件中剥离文本列并以有用的方式重新组合它们。

### cut—Remove Sections from Each Line of Files

`cut` 程序用于从一行中提取一段文本并将其输出到标准输出。它可以接受多个文件参数或从标准输入读取。

指定要提取的行段有些 awkward，并使用表 20-3 中显示的选项指定。

### Table 20-3: cut Selection Options

| Option | Description |
| --- | --- |
| `-c char_list` | 提取由 `char_list` 定义的行部分。列表可能由一个或多个用逗号分隔的数字范围组成。 |
| `-f field_list` | 提取由 `field_list` 定义的行中的一个或多个字段。列表可能包含一个或多个字段或用逗号分隔的字段范围。 |
| `-d delim_char` | 当指定 `-f` 时，使用 `delim_char` 作为字段分隔字符。默认情况下，字段必须由单个制表符分隔。 |
| `--complement` | 提取整行文本，但排除由 `-c` 和/或 `-f` 指定的部分。 |

As we can see, `cut` extracts text in a fairly inflexible manner. `cut` is best used to extract text from files produced by other programs, rather than text directly input by humans. Let's look at our `distros.txt` file and see if it is "clean" enough to be a good specimen for our `cut` examples. If we use `cat` with the `-A` option, we can see if the file meets our requirements for tab-delimited fields.
