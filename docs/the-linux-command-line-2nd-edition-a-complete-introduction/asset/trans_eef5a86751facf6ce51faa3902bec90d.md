

```
Ubuntu    7.04  04/19/2007
SUSE      10.2  12/07/2006
Ubuntu    6.10  10/26/2006
Fedora    6     10/24/2006
Ubuntu    6.06  06/01/2006
SUSE      10.1  05/11/2006
Fedora    5     03/20/2006
```

通过指定 -k 3.7，我们指示 sort 使用从第三个字段的第七个字符开始的排序键，这对应于年份的开始。同样，我们指定 -k 3.1 和 -k 3.4 来分离日期的月份和日期部分。我们还添加了 n 和 r 选项来实现反向数字排序。b 选项被包含在内以抑制日期字段中的前导空格（其数量因行而异，从而影响排序结果）。

某些文件不使用制表符和空格作为字段分隔符；例如，/etc/passwd 文件：

```
[me@linuxbox ~]$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
```

该文件中的字段以冒号 (:) 分隔，那么我们如何使用键字段对该文件进行排序？sort 提供了 -t 选项来定义字段分隔符字符。要按第七个字段（账户的默认 shell）对 passwd 文件进行排序，我们可以这样做：

```
[me@linuxbox ~]$ sort -t ':' -k 7 /etc/passwd | head
me:x:1001:1001:Myself,,,:/home/me:/bin/bash
root:x:0:0:root:/root:/bin/bash
dhcp:x:101:102:/nonexistent:/bin/false
gdm:x:106:114:Gnome Display Manager:/var/lib/gdm:/bin/false
hplip:x:104:7:HPLIP system user,,,:/var/run/hplip:/bin/false
klog:x:103:104::/home/klog:/bin/false
messagebus:x:108:119::/var/run/dbus:/bin/false
polkituser:x:110:122:PolicyKit,,,:/var/run/PolicyKit:/bin/false
```

```
pulse:x:107:116:PulseAudio daemon,,,:/var/run/pulse:/bin/false
```

通过指定冒号字符作为字段分隔符，我们可以对第七个字段进行排序。

## uniq

与 sort 相比，uniq 程序是一个轻量级工具。uniq 执行一项看似微不足道的任务。给定一个已排序的文件（包括标准输入），它会删除任何重复的行并将结果发送到标准输出。它通常与 sort 结合使用，以清除输出中的重复项。

> **提示：** 虽然 uniq 是一个传统 Unix 工具，常与 sort 一起使用，但 GNU 版本的 sort 支持 -u 选项，可从排序输出中删除重复项。

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

请记住输入 Ctrl-d 以终止标准输入。现在，如果我们对文本文件运行 uniq：

```
[me@linuxbox ~]$ uniq foo.txt
a
b
c
a
b
c
```

结果与原始文件没有区别；重复项未被删除。对于 uniq 实际执行其工作，输入必须先排序：

```
[me@linuxbox ~]$ sort foo.txt | uniq
a
b
c
```

这是因为 uniq 仅删除彼此相邻的重复行。
uniq 有几个选项。以下是常见的选项：

Table 20-2: Common uniq Options

| Option | Description |
| --- | --- |
| -c | 输出重复行的列表，并在前面加上该行出现的次数。 |
| -d | 仅输出重复的行，而不是唯一的行。 |
| -f n | 忽略每行开头的 n 个字段。字段以 sort 中的空白分隔；然而，与 sort 不同，uniq 没有设置备用字段分隔符的选项。 |
| -i | 比较行时忽略大小写。 |
| -s n | 跳过（忽略）每行开头的 n 个字符。 |
| -u | 仅输出唯一的行。这是默认值。 |

在这里我们看到 uniq 使用 -c 选项报告在文本文件中找到的重复项数量：

```
[me@linuxbox ~]$ sort foo.txt | uniq -c
  2 a
  2 b
  2 c
```

## Slicing And Dicing

我们接下来要讨论的三个程序用于从文件中提取文本列并以有用的方式重新组合它们。

## cut

cut 程序用于从一行中提取一段文本并输出提取的内容

