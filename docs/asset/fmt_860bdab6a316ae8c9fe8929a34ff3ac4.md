
jumps over the lazy dog.

`me@linuxbox ~$ cat -ns foo.txt`

1 The quick brown fox

2 jumps over the lazy dog.

```
```

在这个示例中，我们创建了 `foo.txt` 文件的新版本，其中包含两行被两个空行分隔的文本。经过 `cat -ns` 选项处理后，多余的空行被删除，剩下的行被赋予了编号。虽然对文本的操作来说并不是什么复杂的步骤，但它确实是一个过程。

## sort

`sort` 程序对标准输入或命令行指定的一个或多个文件内容进行排序，并将结果发送到标准输出。使用与 `cat` 相同的技术，我们可以按照如下方式演示直接从键盘处理标准输入：

```
me@linuxbox ~$ sort foo.txt
c
b
me@linuxbox ~$ cat foo.txt
a
b
c
```

在输入命令后，我们输入字母 c、b 和 a，然后按下 CTRL-D 表示文件结束。然后，我们查看生成的输出，并发现这些行现在按排序顺序显示了。

由于 `sort` 可以接受命令行上的多个文件作为参数，因此可以将多个文件合并成一个排序后的整体。例如，如果我们有三个文本文件并想将它们合并成一个排序后的文件，我们可以这样做：

```bash
sort file1.txt file2.txt file3.txt > final_sorted_list.txt
```

`sort` 具有几个有趣的选项。表 20-1 包含了部分列表。

### 表 20-1：常用的 sort 选项

| 选项 | 长格式选项 | 描述 |
| --- | --- | --- |
| -b | --ignore-leading-blanks | 默认情况下，排序是对整行进行的，从行的第一个字符开始。此选项导致 `sort` 忽略行首空格，并根据行的第一个非空白字符计算排序。 |
| -f | --ignore-case | 使排序不区分大小写。 |
| -n | --numeric-sort | 根据字符串的数值求值进行排序。使用此选项允许 `sort` 对数值而非字母值进行排序。 |
| -r | --reverse | 逆序排序。结果为降序而非升序。 |
| -k | keys=field1,field2 | 根据从 field1 到 field2 的键进行排序，而不是根据整行。请见下文讨论。 |
| -m | --merge | 将每个参数视为预先排序的文件。将多个文件合并为单个排序后的结果，而不执行任何额外的排序。 |
| -o | --output=file | 将排序后的输出发送到文件而不是标准输出。 |
| -t | --field-separator=char | 定义文件字段分隔符。默认情况下，字段由空格或制表符分隔。 |

尽管这些选项中的大部分都通俗易懂，但有些并不是如此。首先，让我们看看 `-n` 选项，它使得根据数值进行排序成为可能。我们可以通过对 `du` 命令的结果进行排序来确定占用磁盘空间最大的用户。通常，`du` 命令以模式名称的形式列出摘要结果。

```
$du -s /usr/share/* | head
252 /usr/share/aclocal
96 /usr/share/acplt-support
8 /usr/share/aduser
196 /usr/share/alcarte
344 /usr/share/alsa-base
8 /usr/share/anthy
12488 /usr/share/apmd
21440 /usr/share/app-install
```

## /usr/share/application-registry

在这个示例中，我们使用管道符到 `head` 将结果限制在前 10 行。我们可以通过这种方式产生一个数值排序的列表，对前 10 个空间占用者进行排序：

```
me@linuxbox ~# ls -s /usr/share/* sort -nr | head
509948 /usr/share/locale-langpack
242660 /usr/share/doc
197560 /usr/share/fonts
179144 /usr/share/gnome
146764 /usr/share/myspell
144304 /usr/share/gimp
135880 /usr/share/dict
76508 /usr/share/icons
68072 /usr/share/apps
62844 /usr/share/foomatic
```

通过使用 `n` 和 `r` 选项，我们产生了逆序排序，最大的值出现在前面的结果中。这种排序之所以有效，是因为数值出现在每行的开头。但如果我们想根据行内找到某个值对列表进行排序呢？例如，这里是 `ls -l` 的结果：

```
me@linuxbox ~# ls -l /usr/bin | head
total 152948 2025-04-04 02:42
-rwwxr-xr-x 1 root 34824 2016-11-27 06:08
-rwwxr-xr-x 1 root 101556 2023-05-27 08:22
-rwwxr-xr-x 1 root 105522 2016-08-15 10:34
-rwwxr-xr-x 1 root 3800 2025-04-14 03:51
-rwwxr-xr-x 1 root 7536 2025-04-29 00:19
-rwwxr-xr-x 1 root 3576 2025-04-29 07:57
-rwwxr-xr-x 1 root 20808 2025-01-03 18:02
-rwwxr-xr-x 1 root 489704 2025-10-09 17:02
```

暂时忽略 `ls` 可以按大小排序结果这一点，我们使用它按大小排序此列表：

```
me@linuxbox ~# ls -l /usr/bin | sort -nk | head
-rwwxr-xr-x 1 root 823416 2025-04-07 17:42
-rwwxr-xr-x 1 root 822292 2025-04-07 17:42
-rwwxr-xr-x 1 root 3746508 2025-03-07 23:45
-rwwxr-xr-x 1 root 3654020 2025-08-26 16:16
-rwwxr-xr-x 1 root 2928760 2025-09-10 14:31
-rwwxr-xr-x 1 root 2928756 2025-09-10 14:31
-rwwxr-xr-x 1 root 2602326 2025-10-10 12:56
-rwwxr-xr-x 1 root 2304684 2025-10-10 12:56
-rwwxr-xr-x 1 root 2241832 2025-04-04 15:55
-rwwxr-xr-x 1 root 2202476 2025-10-18 12:56
```

`sort` 的许多用途涉及对表格数据的处理，例如之前的命令的结果。如果我们将数据库术语应用于之前的表格，我们会说每行是一个记录，每个记录由多个字段组成，例如文件属性、链接数、文件名、大小等。`sort` 能够处理单个。在数据库术语中，我们可以指定一个或多个字段作为 `sort` 键。在上一个例子中，我们指定 `n` 和 `r` 选项来执行逆序排序，并指定 `-k5` 将第五字段作为排序的键。

该选项很有趣且具有许多功能，但首先我们需要讨论 `sort` 如何定义字段。让我们考虑以下包含单行作者名的简单文本文件：

William Shorts

默认情况下，`sort` 认为这一行有两个字段。第一个字段包含这些字符：

"William"

第二个字段包含这些字符：

"Short"

这意味着空白字符（空格和制表符）被用作字段之间的分隔符，并且在排序时分隔符包含在字段中。

查看我们输出中的如下行，我们可以看到一行包含八个字段，且第一个字段是大小：

```
-rwr-xr-x 1 root 823426 2025-04-07 17:42 inkscape
```

对于我们的下一系列实验，考虑包含2006年至2008年间发布的三个流行的 Linux 发行版的文件。文件的每行都有三个字段：发行版名称、版本号和 MM/DD/YYYY 格式的发布日期。

| SUSE | 10.2 | 12/07/2006 |
| Fedora | 10 | 11/25/2008 |
| SUSE | 11.0 | 06/19/2008 |
| Ubuntu | 8.04 | 04/24/2008 |
| Fedora | 8 | 11/08/2007 |
| SUSE | 10.3 | 10/04/2007 |
| Ubuntu | 6.10 | 10/26/2006 |
| Fedora | 7 | 05/31/2007 |
| Ubuntu | 7.10 | 10/18/2007 |
| SUSE | 10.1 | 04/19/2009 |
| Fedora | 6 | 06/01/2006 |
| Ubuntu | 7 | 10/24/2006 |
| SUSE | 9 | 05/13/2008 |
| Ubuntu | 8 | 10/30/2008 |
| Fedora | 5 | 03/28/2006 |

使用文本编辑器（也许，我们将输入这些数据并将文件命名为 `distros.txt`）。接下来，我们将尝试排序文件并观察这些结果：

```
me@linuxbox -$ sort distros.txt
Fedora 10 11/25/2008
Fedora 5 03/28/2006
Fedora 6 10/24/2006
Fedora 7 05/31/2007
Fedora 8 11/08/2007
Fedora 9 05/13/2008
SUSE 10.1 05/11/2006
SUSE 10.2 12/07/2006
SUSE 10.3 10/04/2007
SUSE 11.0 06/19/2008
Ubuntu 6.06 06/01/2006
Ubuntu 6.10 10/26/2006
Ubuntu 7.04 04/19/2007
Ubuntu 7.10 10/18/2007
Ubuntu 8.04 04/24/2008
```

嗯，大部分运行良好。问题出现在版本号的排序上。当 1 在字符集中于 5 之前时，版本 10 出现在顶部，而版本 9 掉到了底部。

为了解决这个问题，我们将让 `sort` 对多个键排序。我们希望对第一个字段进行字母排序，然后对第二个字段进行数值排序。`sort` 允许多次使用 `-k` 选项以便指定多个键。事实上，一个键可以包含一个字段范围。如果没有指定范围（如我们之前的示例所示），`sort` 将使用从指定字段开始延伸到行尾的键。这是多键排序的语法：

```
me@linuxbox -$ sort -key=1,1 --key=2n distros.txt
```

# Ubuntu 8.10 2008/10/30

虽然为了清晰起见我们使用了选项的完整形式，但 `-k 1,1 -k 2` 的效果完全相同。在第一个 key 选项实例中，我们指定了一个字段范围来包含第一个键。由于我们只想将排序限制在第一个字段，因此指定了 `1,1`，这意味着“从字段 1 开始到字段 1 结束”。在第二个实例中，我们指定了 `2n`，这意味着字段 2 是排序键，且排序应该是按数值的。键的末尾可以包含一个字母，以指定要执行的排序类型。其他选项与 `sort` 程序的全局选项相同：b（忽略空格）、n（数值排序）、r（反序排序）等。

我们列表中的第三字段包含一种不便于排序的格式。计算机通常格式化为 YYYY-MM-DD 以便于按时间顺序排序，但我们的数据使用的是美国格式 MM/DD/YYYY。我们该如何按时间顺序对此列表排序？

幸运的是，`sort` 并没有提供这种方法。`key` 选项提供了字段内的偏移量，因此我们可以在字段内定义键。

```
$ linux -js sort -k 3.7nbr -k 3.1nbr -k 3.4nbr distros.txt
Fedora 10 11/25/2008
Ubuntu 8.10 10/30/2008
SUSE 11.0 06/19/2008
Fedora 9 05/13/2008
Ubuntu 8.04 04/24/2008
Fedora 8 11/08/2007
Ubuntu 7.10 10/31/2007
SUSE 10.3 10/04/2007
Fedora 7 05/31/2007
Ubuntu 7.04 04/19/2007
SUSE 10.2 12/07/2006
Ubuntu 6.10 10/26/2006
Fedora 6 10/24/2006
Ubuntu 6.06 06/01/2006
SUSE 10.1 05/11/2006
Fedora 5 03/28/2006
```

通过指定 `-k 3,7`，我们指示 `sort` 使用从第三字段内第七个字符开始的键，这对应于日的开始。同样，我们指定了 `-k 3.1` 和 `-k 3.4` 来分离日期中的月份和日期部分。我们还添加了 `n` 和 `r` 选项来实现反序数值排序。包含 `b` 选项是为了抑制日期字段中的前导（这些数字行与行之间没有变化，从而影响排序结果）。

某些文件不使用制表符和空格作为字段分隔符；例如，这里是 `/etc/passwd` 文件：

```
$ linux head /etc/passwd
root:x:0:0:root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin/sh
bin:x:2:2:bin:/bin/sh
sys:x:3:3:dev:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/user/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lpd:x:7:7:lpd:/var/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
```

该文件的字段用冒号（:`）定义，那么我们如何使用键字段对该文件排序呢？`sort` 提供了字段分隔符。要对第七个字段（账户默认值）进行排序，我们可以这样做：

```
[melinuxbox ~$] sort -t ':' -k 7 /passwd | head
me:x:108:1001:Myself,,,/home/me/bash
root:x:0:0:/root:/bash
dhcp:x:101:102:nonexistent:/bin/false
gdm:x:106:114:Gnome Display Manager:/var/run/lib/gnome:/bin/false
hplp:x:104:107:Pulse system user,,,/run/hplp/false
klog:x:103:104:/home/klog:/bin/false
messagebus:x:118:119:,/var/run/dbus:/bin/false
polkituser:x:110:122:PolicyKit,,,/var/run/PolicyKit:/bin/false
pulse:x:107:116:PulseAudio daemon,,,/var/run/pulse:/false
```

通过指定冒号作为字段分隔符，我们可以对第七个字段进行排序。注意，`sort` 默认将多个空白字符序列（制表符和空格）视为单个分隔符，而其他分隔符则被视为单独处理。

## uniq

与 `sort` 相比，`uniq` 用于过滤重复行。`uniq` 仅检查相邻的重复行。要对整个文件进行去重，必须先通过 `sort`。

与 `sort` 相比，`uniq` 提供了许多选项来控制输出。例如，`-c` 可以显示重复行出现的次数，`-d` 仅显示重复行，`-u` 仅显示不重复行。`-i` 忽略大小写，`-w` 限制字符宽度。

与 `sort` 相比，`uniq` 运行非常快，因为它只需要处理相邻的行。假设我们有一个 `list.txt` 文件：

```
$ cat list.txt
apple
apple
banana
cherry
cherry
apple
```

此时运行 `uniq list.txt` 的输出：

```
apple
banana
cherry
apple
```

运行 `uniq -c list.txt` 的输出：

```
2 apple
1 banana
2 cherry
1 apple
```

运行 `uniq -d list.txt` 的输出：

```
apple
cherry
```

运行 `uniq -u list.txt` 的输出：

```
banana
```

忽略大小写：
```
$ uniq -i list.txt
apple
banana
cherry
cherry
apple
```

运行 `uniq -ic list.txt` 的输出：

```
2 apple
1 banana
2 cherry
1 apple
```
