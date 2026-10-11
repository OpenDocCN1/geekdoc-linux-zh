
## 管道

注意表 8-1 指出，重定向仅发生在命令与文件之间，反之亦然。你还可以将一个命令的标准输出作为另一个命令的标准输入进行发送。为此，你必须使用管道 `|` Shell 元字符，并在其两侧指定命令。然后，Shell 会将左侧命令的标准输出发送到右侧的命令，后者会将该信息解释为标准输入。此过程如图 8-2 所示。

> **注意**
> 
> 包含管道 `|` 元字符的整个命令通常被称为 **管道**。

> **提示**
> 
> 在大多数键盘上，可以通过按 Shift+\ 来创建管道符号。

![](img/09bf13b782f71165e17bb3839040c96a_306_0.png)

例如，`ls -l /etc` 命令的标准输出太大，无法在一个终端屏幕上显示。要将此命令的标准输出发送到逐页查看标准输入的 `less` 命令，可以使用以下命令：

```
[root@server1 root]# ls -l /etc | less
total 3564
-rw-r--r--   1 root     root      15276 Mar 22 12:20 a2ps.cfg
-rw-r--r--   1 root     root      2562 Mar 22 12:20 a2ps-site.cfg
drwxr-xr-x   4 root     root      4096 Jun 11 08:45 acpi
-rw-r--r--   1 root     root      46 Jul 16 15:34 adjtime
drwxr-xr-x   2 root     root      4096 Jun 11 08:47 aep
-rw-r--r--   1 root     root      688 Feb 17 00:35 aep.conf
-rw-r--r--   1 root     root      703 Feb 17 00:35 aeplog.conf
drwxr-xr-x   4 root     root      4096 Jun 11 08:47 alchemist
-rw-r--r--   1 root     root      1419 Jan 26 10:14 aliases
-rw-r----.  1 root     smmsp    12288 Jul 19 13:19 aliases.db
drwxr-xr-x   2 root     root      4096 Jun 11 11:11 alternatives
```

```
drwxr-xr-x    3 amanda disk        4096 Jun 11 10:16 amanda
-rw-r--r--    1 amanda disk          0 Mar 22 12:28 amandates
-rw-------    1 root root          688 Mar  4 22:34 amd.conf
-rw-r----s    1 root root         105 Mar  4 22:34 amd.net
-rw-r--r--    1 root root         317 Feb 15 14:33 amacrontab
-rw-r--r--    1 root root         331 May  5 08:07 at.conf
-rw-r--r--    1 root root        6203 Jul 16 15:34 aasound.state
drwxr-xr-x    3 root root        4096 Jun 11 10:37 atalk
-rw-------    1 root root          1 May  5 13:39 at.deny
-rw-r--r--    1 root root         325 Apr 14 13:39 auto.master
-rw-r--r--    1 root root         581 Apr 14 13:39 auto.misc
:
```

### 注意

在 `|` 元字符周围不需要空格；命令 `ls -l /etc|less` 和 `ls -l /etc | less` 是等价的。

管道的一种常见用法是减少在终端屏幕上显示的信息量，针对那些显示信息过多的命令。请看以下 `mount` 命令的输出：

```
[root@server1 root]# mount
/dev/hdc2 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
/dev/hdc1 on /boot type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
[root@server1 root]# _
```

为了仅查看包含从辅助主 IDE 硬盘（/dev/hdc）挂载的文件系统信息的那些行，可以将 `mount` 命令的标准输出作为标准输入发送到 `grep` 命令，如下面的输出所示：

```
[root@server1 root]# mount | grep /dev/hdc
/dev/hdc2 on / type ext3 (rw)
/dev/hdc1 on /boot type ext3 (rw)
[root@server1 root]# _
```

前一个输出中的 `grep` 命令接收 `mount` 命令的完整输出，然后仅显示包含 /dev/hdc 的那些行。`grep` 命令通常接受两个参数；第一个指定要搜索的文本，第二个指定要搜索的文件名。前一个输出中使用的 `grep` 命令不需要第二个参数，因为要搜索的材料来自标准输入（`mount` 命令）而不是来自文件。

此外，你可以使用多个管道 `|` 元字符在命令行上将信息从一个命令传递到另一个命令，其方式类似于工厂的流水线。制造工厂通常包含几个部门，每个部门都非常出色地完成一项专门任务。例如，一个部门可能组装产品，另一个部门可能涂漆，还有一个部门可能包装产品。每个产品必须经过每个部门才能完成。

同样，Linux 拥有许多可以以某种方式操纵数据的命令。这些命令的管道化可以比作制造工厂的流程；信息由一个命令操纵，然后被操纵的信息被发送到另一个命令，该命令进一步操纵它。经过这种方式的几个命令操纵后，信息变成了用户期望的形式。此过程如图 8-3 所示。

![](img/09bf13b782f71165e17bb3839040c96a_308_0.png)

图 8-3 多个命令的管道

任何可以从标准输入接收并输出到标准输出的命令都称为过滤器命令。需要注意的是，像 `ls` 和 `mount` 这样的命令不是过滤器命令，因为它们不接受来自其他命令的标准输入，而是从系统查找信息并显示给用户。因此，这些命令必须位于管道的开头。其他命令，如 `vi` 编辑器是交互式的，因此不能存在于管道中，因为它们不能从标准输入接收并输出到标准输出。

Linux 用户可以使用数百个过滤器命令；表 8-2 列出了本书中常用的一些常见过滤器命令。

表 8-2 常见过滤器命令

| 命令 | 描述 |
| :--- | :--- |
| `sort` | 按字母数字顺序对文件中的行进行排序 |
| `sort -r` | 按字母数字顺序对文件中的行进行逆序排序 |
| `wc` | 统计文件中的行数、字数和字符数 |
| `wc -l` | 统计文件中的行数 |
| `wc -w` | 统计文件中的字数 |
| `wc -c` | 统计文件中的字符数 |
| `pr` | 为打印格式化文件（有多个可用选项）；它在每页顶部放置日期和页码 |
| `pr -d` | 以双倍行距格式化文件 |
| `tr` | 替换文件文本中的字符 |
| `grep` | 显示文件中匹配正则表达式的行 |
| `nl` | 为文件中的行编号 |
| `awk` | 可以使用模式-动作语句提取、操纵和格式化文本 |
| `sed` | 可以使用搜索和替换表达式操纵文本 |

例如，取莎士比亚《罗密欧与朱丽叶》的序言：

```
[root@server1 root]# cat prologue
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny.
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whole misadventured piteous overthrows
Do with their death bury their parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, no might could remove,
Is now the two hours' traffick of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

如果你想要将前一个文件中的所有小写 a 字符替换为大写 A 字符，按每行第一个字符对内容排序，将输出设为双倍行距，并逐页查看结果，可以使用以下管道：

```
[root@server1 root]# cat prologue | tr a A | sort | pr -d | less
2002-05-30 09:32 Page 1

And the continuance of their parents' rage,
A pair of star-cross'd lovers take their life;
Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.

The which if you with pAtient eArs Attend,

Two household, both alike in dignity,
:
```

前一个例子中使用的命令通过 `less` 命令将最终的标准输出显示到终端屏幕。在许多情况下，你可能希望显示管道结果，同时也希望保留硬盘上文件中的副本。因此，存在 **tee 命令**，它是一个过滤器命令，从标准输入接收信息，并将该信息发送到文件，同时也发送到标准输出。

要在显示到终端屏幕之前保存操纵后的序言副本（使用 `less` 命令显示），可以使用以下命令：

```
[root@server1 root]# cat prologue | tr a A | sort | pr -d | tee newfile | less
2002-05-30 09:32 Page 1

And the continuAnce of their pARENTs' rAge.

A pAir of stAr-cross'd lovers tAke their life;

Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.
```

