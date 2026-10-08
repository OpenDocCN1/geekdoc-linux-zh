
从这个输出中可以看出，用户 *games* 仅出现在活动的 /etc/passwd 文件中，用户 *operator1* 仅出现在 /etc/passwd.backup 文件中，而其他所有条目都出现在这两个文件中。

以下是 **cmp** 和 **diff** 命令的总结。

**cmp** - 比较两个文件的内容。返回两个文件之间第一个差异的字节位置和行号。

![](img/75f39fc91296b889c0653851accdfd46_656_0.png)

![](img/75f39fc91296b889c0653851accdfd46_656_1.png)

**选项**

- **-l** 显示文件中所有差异的字节位置及不同的字符。
- **-s** 静默运行，即仅返回退出代码。

**diff** - 比较两个文件并报告不同的行。

**选项**

- **-b** 忽略行尾的空白。
- **-i** 忽略大小写差异。
- **-t** 在输出中将制表符扩展为空格。
- **-w** 忽略空格和制表符。

![](img/75f39fc91296b889c0653851accdfd46_656_2.png)

## dircmp

为什么止步于比较文件呢？你的用户区域中可能还有许多目录。**dircmp** 可以比较两个目录并生成关于目录内容的信息。

首先，让我们对两个目录执行长列表显示：

![](img/75f39fc91296b889c0653851accdfd46_657_0.png)

```bash
$ ls -l krsort.dir.old
total 168
-rwxr-xr-x 1 denise users 34592 Oct 31 11:27 krsort
-rwxr-xr-x 1 denise users 3234 Oct 31 11:27 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 31 11:27 krsort.dos
-rw-r--r-- 1 denise users 9922 Oct 31 11:27 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 31 11:27 krsortorig.c
$
$ ls -l krsort.dir.new
total 168
-rwxr-xr-x 1 denise users 34592 Oct 31 15:17 krsort
-rwxr-xr-x 1 denise users 32756 Oct 31 15:17 krsort.dos
-rw-r--r-- 1 denise users 9922 Oct 31 15:17 krsort.q
-rwxr-xr-x 1 denise users 3234 Oct 31 15:17 krsort.test.c
-rwxr-xr-x 1 denise users 3085 Oct 31 15:17 krsortorig.c
$
```

从这个列表中，你可以清楚地看到每个目录都有一个唯一的文件。krsort.c 仅出现在 krsort.dir.old 目录中，而 krsort.test.c 仅出现在 krsort.dir.new 目录中。现在让我们使用 dircmp 来告知这两个目录之间的差异：

![](img/75f39fc91296b889c0653851accdfd46_657_1.png)

```bash
$ dircmp krsort.dir.old krsort.dir.new
krsort.dir.old only and krsort.dir.new only Page 1
./krsort.c ./krsort.test.c

Comparison of krsort.dir.old krsort.dir.new Page 1
directory same
./krsort same
./krsort.dos same
./krsort.q same
./krsortorig.c same
$
```

这是一个有用的输出。首先，列出了仅出现在一个目录中的文件。然后，列出了两个目录共有的文件。

以下是 **dircmp** 命令的总结。

### dircmp - 比较目录。

| 选项 | 描述 |
| :--- | :--- |
| -d | 比较两个目录中同名文件的内容，并生成一份报告，说明需要执行哪些操作才能使文件相同。 |
| -s | 抑制关于不同文件的信息。 |

## cut

有时，你的输出包含过多的字段。当我们之前发出 **llsum** 命令时，它生成了四个字段：FILENAME、OWNER、SIZE 和 TYPE。如果我们想只查看 FILENAME 和 SIZE 怎么办？我们可以修改 **llsum** 脚本，或者使用 **cut** 命令通过以下命令来消除 OWNER 和 TYPE 字段：

```bash
$ llsum | cut -c 1-25,37-43

FILENAME            SIZE
README              810
backup_files        3408
biography           427
cshtest            1024
gkill              1855
gkill.out           191
hostck              924
ifstat             1422
ifstat.int          2147
ifstat.out          723
introdos           54018
introux            52476
letter             23552
letter.auto        69632
letter.auto.recover 71680
letter.backup      23552
letter.lck            57
letter.recover     69632
llsum              1267
llsum.orig         1267
llsum.out          1657
llsum.tomd.out     1356
pspg               670
pspg.int            802
pspg.out            122
sam_adduser        1010
ttdol              1024
trash              4554
trash.out           329
typescript         74
```

列出的文件占用 3 (0.373
平均文件大小为 1305

![](img/75f39fc91296b889c0653851accdfd46_659_0.png)

![](img/75f39fc91296b889c0653851accdfd46_659_1.png)

这从 llsum 生成了一个列表，并将其通过管道传递给 cut。仅提取了第 1 到 25 个字符和第 37 到 43 个字符。这些字符对应于我们想要的字段。在输出的末尾有两行仅部分打印。我们不需要这些行，因此我们可以使用 grep -v 来消除它们并打印所有其他行。该命令的输出保存在输出末尾的文件 llsum.out 中，我们稍后会用到它：

```bash
$ ./llsum | grep -v "bytes" | cut -c 1-25,37-43
```

```
FILENAME                SIZE
README                810
backup_files         3408
biography             427
cshtest             1024
gkill               1855
gkill.out            191
hostck               924
ifstat              1422
ifstat.int           2147
ifstat.out            723
introdos            54018
introux             52476
letter              23552
letter.auto         69632
letter.auto.recover 71680
letter.backup 23552
letter.lck 57
letter.recover 69632
llsum 1267
llsum.orig 1267
llsum.out 1657
llsum.tomd.out 1356
psg 670
psg.int 802
psg.out 122
sam_adduser 1010
tdo1an 1024
trash 4554
trash.out 329
typescript 1242
```

```bash
$ llsum | grep -v "bytes" | cut -c 1-25,37-43 > llsum.out
$
```

以下是 cut 命令的总结，包含一些常用的选项。

**cut** - 从每行中提取指定的字段。

**选项**

- **-c list** 基于字符位置进行提取，如示例所示。
- **-f list** 基于字段进行提取。
- **-d char** 使用 -f 选项时，d 后面的字符是分隔符。分隔符是分隔字段的字符。

## paste

可以通过多种方式合并文件。如果你想按行合并文件，可以使用 **paste** 命令。

![](img/75f39fc91296b889c0653851accdfd46_661_0.png)

第二个文件的第一行粘贴到第一个文件第一行的末尾，依此类推。

让我们使用刚刚介绍过的 **cut** 命令，仅提取权限字段（即第 1 到 10 个字符），以获取文件的权限。然后我们将这些保存到文件 ll.out 中：

![](img/75f39fc91296b889c0653851accdfd46_661_1.png)

```bash
$ ls -al | cut -c 1-10
```

```
total 798
drwxrwxrwx
drwxrwxrwx
-rwxrwxrwx
-rwxrwxrwx
-rwxrwxrwx
drwxr-xr-x
-rwxrwxrwx
-rw-r--r--
-rwxrwxrwx
-rwxrwxrwx
-rwxr-xr-x
-rw-r--r--
-rw-f--r--
-rwxrwxrwx
-rw-f--r--
-rw-f--r--
-rw-1w-rw-
-rw-f--r--
-rw-f--f--
-rw-f--f--
-rw-f--f--
-rwxrwxrwx
-rwxr-xr-x
-rw-f--f--
-rw-f--f--
-rwxrwxrwx
-rwxr-xr-x
-rw-f--f--
-rwxrwxrwx
drwxr-xr-x
-rwxrwxrwx
-rw-f--f--
-rw-f--f--
```

```bash
$ ls -al | cut -c 1-10 > ll.out
$ paste - llsum.out
```

![](img/75f39fc91296b889c0653851accdfd46_661_2.png)

现在我们可以使用 **paste** 命令将保存在 ll.out 文件中的权限粘贴到 llsum.out 文件中的其他文件相关信息上：

```bash
$ paste llsum.out ll.out
FILENAME             SIZE      total 792
README               810      -rwxrwxrwx
backup_files         3408     -rwxrwxrwx
biography            427      -rwxrwxrwx
cshtest              1024     drwxr-xr-x
gkill                1855     -rwxrwxrwx
gkill.out            191      -rw-r--r--
hostck               924      -rwxrwxrwx
ifstat               1422     -rwxrwxrwx
ifstat.int            2147    -rwxr-xr-x
ifstat.out             723     -rw-r--r--
intros               54018    -rw-r--r--
introux              52476    -rwxrwxrwx
letter               23552    -rw-r--r--
letter.auto          69632    -rw-r--r--
letter.auto.recover  71680    -rw-r--r--
letter.backup        23552    -rw-r--r--
letter.lck            57      -rw-rw-rw-
letter.recover      69632     -rw-r--r--
ll.out               1057     -rw-r--r--
llsum                1267     -rwxrwxrwx
llsum.orig           1267     -rwxr-xr-x
llsum.out            1657     -rw-r--r--
llsum.tomd.out       1356     -rw-r--r--
psg                  670      -rwxrwxrwx
psg.int              802      -rwxr-xr-x
psg.out              122      -rw-r--r--
sam_adduser          1010     -rwxrwxrwx
tdolan               1024     drwxr-xr-x
trash                4554     -rwxrwxrwx
trash.out            329      -rw-r--r--
typescript           679      -rw-r--r--
$
```

![](img/75f39fc91296b889c0653851accdfd46_662_0.png)

这生成了一个列表，其中包含来自 llsum.out 的 FILENAME 和 SIZE 以及来自 ll.out 的权限。

![](img/75f39fc91296b889c0653851accdfd46_662_1.png)

如果两个文件具有相同的第一字段，你可以使用 join 命令合并这两个文件：

![](img/75f39fc91296b889c0653851accdfd46_662_2.png)

以下是 paste 和 join 命令的总结，包含一些常用的选项：

