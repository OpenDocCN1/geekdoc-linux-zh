
该选项告诉 grep 在将模式与 intro 中的行进行匹配时忽略大写和小写之间的差异。因此，包含 the 或 The 的行将被打印，包含 THE、ThE、tHE 等的行也一样。

表 3.5 展示了你可以指定给 grep 的其他正则表达式类型，以及它们会匹配的模式类型。

**表 3.5 一些 grep 示例**

| 命令 | 输出 |
|---|---|
| `grep '[A-Z]' list` | 来自 list 的包含大写字母的行 |
| `grep '[0-9]' data` | 来自 data 的包含数字的行 |
| `grep '[A-Z]...[0-9]' list` | 来自 list 的包含以大写字母开头、以数字结尾的五字符模式的行 |
| `grep '\.pic$' filelist` | 来自 filelist 的以 .pic 结尾的行 |

### -v 选项

有时候，你关注的不是找出包含指定模式的行，而是找出不包含该模式的行。这正是 grep 的 -v 选项的作用：反转匹配任务的逻辑。在下一个例子中，grep 被用来找出 intro 中所有不包含模式 UNIX 的行。

```text
$ grep -v 'UNIX' intro                 Print all lines that don't contain UNIX
Thompson and Dennis Ritchie at Bell Laboratories
in the late 1960s. One of the primary goals in
environment that promoted efficient program
development.
$ 
```

### -l 选项

有时候，你可能不想看到实际匹配模式的行，而只想找到包含该模式的文件的文件名。例如，假设当前目录中有一组 C 程序（按照惯例，这些文件名以 .c 后缀结尾），而你想知道哪些程序使用了名为 Move_history 的变量。下面是一种找到答案的方法：

```text
$ grep 'Move_history' *.c              Find Move_history in all C source files
exec.c:     MOVE   Move_history[200] = {0};
exec.c:          cpymove(&Move_history[Number_half_moves -1],
exec.c: undo_move(&Move_history[Number_half_moves-1];
exec.c: cpymove(&last_move,&Move_history[Number_half_moves-1]);
exec.c: convert_move(&Move_history[Number_half_moves-1],
exec.c: convert_move (&Move_history[Number_half_moves-1],
makemove.c: MOVE Move_history[i];
makemove.c:     if ( Move_history[i].from != BOOK (i,j,from) OR
makemove.c:         Move_history[i].to != BOOK (i,j,to) )
testch.c:GLOBAL MOVE Move_history[100] = {0};
testch.c:    Move_history[Number_half_moves-1].from = move.from;
testch.c:    Move_history[Number_half_moves-1].to = move.to;
$
```

仔细查看上面的输出，你会发现有三个文件——exec.c、makemove.c 和 testch.c——使用了这个变量。

给 grep 加上 -l 选项后，你会得到包含指定模式的文件的列表，而不是文件中匹配的行：

```text
$ grep -l 'Move_history' *.c        List the files that contain Move_history
exec.c
makemove.c
testch.c
$
```

由于 grep 惯例上是每行列出一个文件，你可以把 grep -l 的输出通过管道传给 wc，从而统计包含某个特定模式的文件数量：

```text
$ grep -l 'Move_history' *.c | wc -l
        3
$
```

上面的命令显示恰好有三个 C 程序文件引用了变量 Move_history。现在，为了确认你确实在认真阅读：如果你使用不带 -l 选项的 grep，并把输出通过管道传给 wc -l，你统计的又是什么呢？

### -n 选项

如果在 grep 中使用 -n 选项，文件中匹配指定模式的每一行前面都会加上对应的行号。从前面的例子可以看到，testch.c 是引用变量 Move_history 的三个文件之一；下面展示如何精确定位文件中引用该变量的具体行：

```text
$ grep -n 'Move_history' testch.c        Precede matches with line numbers
13:GLOBAL MOVE Move_history[100] = {0};
197:    Move_history[Number_half_moves-1].from = move.from;
198:    Move_history[Number_half_moves-1].to = move.to;
$
```

可以看到，Move_history 在 testch.c 的第 13、197 和 198 行被使用。

对于 Unix 专家来说，grep 是最常用的程序之一，因为它在模式匹配方面灵活而精巧。它非常值得学习。

## sort

最基础的 `sort` 命令非常容易理解：给它输入若干行，它会按字母顺序对它们进行排序，并把结果显示为输出：

```text
$ sort names
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
Tony
$
```

默认情况下，`sort` 会读取指定输入文件中的每一行，并按升序排序。

特殊字符按照字符的内部编码进行排序。例如，空格字符在内部表示为数字 32，双引号表示为数字 34。这意味着前者会排在后者之前。尤其是在其他语言和区域设置中，排序顺序可能会有所不同，因此尽管通常可以保证 `sort` 对字母数字输入的表现符合预期，但外语字符、标点符号和其他特殊字符的排序顺序并不总是一如所料。

`sort` 有许多选项，可让排序操作更加灵活。这里我们只介绍其中少数几个选项。

### -u 选项

`-u` 选项告诉 `sort` 从输出中消除重复行。

```text
$ sort -u names
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
$
```

这里可以看到，包含 Tony 的重复行已从输出中消除。许多老派 Unix 用户会使用单独的程序 `uniq` 来完成同样的事情，所以如果你阅读系统 shell 脚本，经常会看到 `sort | uniq` 这样的组合。这些都可以用 `sort -u` 来替代！

### -r 选项

使用 -r 选项可以反转排序顺序：

```text
$ sort -r names          Reverse sort
Tony
Tony
Ralph
Lucy
Fred
Emanuel
Charlie
$
```

### -o 选项

默认情况下，sort 将排序后的数据写入标准输出。如果希望将结果写入文件，可以使用输出重定向：

```text
$ sort names > sorted_names
$
```

或者，你可以使用 -o 选项来指定输出文件。只需在 -o 后面直接写出输出文件的名称即可：

```text
$ sort names -o sorted_names
$
```

这将对 names 进行排序，并将结果写入 sorted_names。

-o 选项的价值在哪里？通常，你会想对文件中的行进行排序，并用排序后的数据替换原始文件。但输入

```text
$ sort names > names
$
```

是不会生效的——它最终会清空 names 文件！然而，使用 -o 选项时，可以将输出文件的名称指定为与输入文件相同的名称：

```text
$ sort names -o names
$ cat names
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
Tony
$
```

### 提示

如果你的过滤器或进程将要替换原始输入文件，请务必小心，并确保在数据被覆盖之前一切都能按预期工作。Unix 擅长很多事情，但没有 *unremove* 命令来恢复丢失的数据或文件。

### -n 选项

假设你有一个文件，其中包含成对的 (x, y) 数据点，如下所示：

```text
$ cat data
5    27
2    12
3    33
23   2
-5   11
15   6
14   -9
$
```

再假设你想把这些数据输入到一个名为 `plotdata` 的绘图程序中，但该程序要求传入的数据对必须按 *x* 值递增的顺序排序（x 是每行的第一个值）。

`sort` 的 `-n` 选项指定将行中的第一个字段视为*数字*，并按算术方式进行排序。比较一下不使用 `-n` 选项和使用 `-n` 选项时 `sort` 的输出：

```text
$ sort data
-5   11
14   -9
15   6
2    12
23   2
3    33
5    27
$ sort -n data    Sort arithmetically
-5   11
2    12
3    33
5    27
14   -9
15   6
23   2
$
```

### 跳过字段

如果你需要按 *y* 值（即每行的第二个数字）对数据文件排序，可以使用以下选项告诉 `sort` 从第二个字段开始：

`-k2n`

而不是 `-n`。`-k2` 表示跳过第一个字段，并从每行的第二个字段开始排序分析。类似地，`-k5n` 表示从每行的第五个字段开始，并按数值对数据进行排序。

```text
$ sort -k2n data
14     -9
23      2
15      6
-5     11
2      12
5      27
3      33
$
```

*从第二个字段开始排序*

默认情况下，字段由空格或制表符分隔。如果要使用不同的分隔符，则必须使用 `-t` 选项。

### -t 选项

如前所述，如果你跳过字段，`sort` 会假定字段由空格或制表符分隔。`-t` 选项可以指示其他情况。在这种情况下，`-t` 后面的字符被视为分隔符。

再看一下示例密码文件：

```text
$ cat /etc/passwd
root:*:0:0:The super User:/:/usr/bin/ksh
steve:*:203:100::/users/steve:/usr/bin/ksh
bin:*:3:3:The owner of system files:/: 
cron:*:1:1:Cron Daemon for periodic tasks:/: 
george:*:75:75::/users/george:/usr/lib/rsh
pat:*:300:300::/users/pat:/usr/bin/ksh
uucp:nc823cisiLiZM:5:5::/usr/spool/uucppublic:/usr/lib/uucp/uucico
asg:*:6:6:The Owner of Assignable Devices:/: 
sysinfo:*:10:10:Access to System Information:/:/usr/bin/sh
mail:*:301:301::/usr/mail:
$
```

如果你想按用户名（每行的第一个字段）对这个文件进行排序，只需发出以下命令：

```text
sort /etc/passwd
```
