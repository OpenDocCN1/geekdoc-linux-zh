
# 第 9 章：简单过滤器

## 9.6 head: 显示文件的开头

`head` 命令显示文件的顶部。默认情况下，它显示前 10 行：

```
head group1
```

你可以使用 `-n` 选项（POSIX 强制）来指定行数并显示，例如文件的前三行：

```
$ head -n 3 group1
root:x:0:root
bin:x:1:root,bin,daemon
users:x:200:henry,image,enquiry
```

或者在某些系统上使用 `-3 group1`。

`head` 可以以富有想象力的方式使用。假设你第二天回来工作，发现你想不起你编辑的文件名。由于 `ls -lt` 按照修改时间顺序显示文件，因此从列表中选取第一个文件并将其作为 `vi` 编辑器的参数应该可以解决问题。这需要命令替换：

```
vi `ls -t | head -n 1`
```

打开最后修改的文件进行编辑。

你可以在 `rc` 文件中将其定义为别名，这样别名命令就一直可以供你使用。

`head` 与 `grep` 命令 (10.2) 使用，以限制显示几行。以下序列选取在 `IMG SRC:` 单词之后包含字符串 `GIF` 的前五行：

```bash
grep "IMG SRC.*GIF" quote.html | head -n 5
```

引号字符串中使用的正则表达式 `*` 表示任意数量的字符。在这里，意味着 SRC 和 GIF 之间可以有任何内容（甚至没有）。

### 选取字节而非行

![](img/4a1db50d3e2a8e380c74d6ab7426fc8e_287_1.png)

虽然 POSIX 使用 `tail` 来处理字符，但 GNU `head` 也可以执行该任务。它还可以按块、千字节和兆字节的分块选取数据。因此，如果 `cmp` 没有告诉你第四十七个字符在哪里，`-c` 选项将准确显示差异所在的位置：

```
$ head -c47 group1
root:x:0:root
bin:x:1:root,bin,daemon
users:x:2
```

## 9.7 tail: 显示文件的结尾

你也可以按其他单位选取数据：

```
head -c b shortest
head -c 2m README
```

第一个 512 字节块

多达 2 兆字节

与其 `head` 对应，`tail` 命令显示文件的结尾。它提供了一种额外的行地址方法，并且和 `head` 一样，不带参数时显示最后 10 行。最后三行通过这种方式显示：

```
$ tail -n 3 group1
dialout:x:19:root,henry
lp:x:18:1lp
cron:x:16:cron
```

## 9.5 diff: 将一个文件转换为另一个

`diff` 是第三个可以显示文件差异的命令。与它的同类成员 `cmp` 和 `comm` 不同，它还会告诉你一个文件中的哪些行需要修改才能使两个文件相同。当与同一个文件使用时，它会产生详细的输出：

```
$ diff group[12]
3c3
< users:x:200:henry,image,enquiry
---
> users:x:100:henry,image,enquiry
5,6c5,6
< dialout:x:18:root,henry
< lp:x:19:1lp
---
> dialout:x:19:root,henry
> lp:x:18:1lp
> cron:x:16:cron
```

修改第一个文件的第 3 行

修改此行

是修改第 5 到 6 行

替换这两行

为这两行

在第一个文件中追加第 7 行

此行

`diff` 使用某些特殊的符号和指令来指示使两个文件相同所需的更改。你应该理解这些指令，因为它们被 `sed` 命令使用，它是系统上最强大的命令之一。

每条指令都使用一个地址命令。`3c3` 更改一行，更改后行号仍为 `3`。`7a8` 在第 7 行之后添加一行，从而在第二个文件中产生第 8 行。另一个指令 `5,6c5,6` 修改了两个行。仔细查看两个文件，以确认这些行中建议的更改足以使文件相同。

### 维护文件的多个版本 (-e)

`diff -e` 会产生一组指令（类似于上述），但这些指令可以配合 `ed` 编辑器（本文未讨论）使用，将一个文件转换为另一个。这种机制允许我们完整存储最旧的文件，只存储连续版本之间的更改，从而节省空间。我们在源代码控制系统 (SCCS) 中有更好的方法来实现这一点，但如果差异很少，`diff` 仍然很有用。SCCS 将在第 16 章中讨论。

## 9.4 comm: 比较两个已排序文件

如果你只是想知道两个文件是否相同，请不带任何选项使用 `cmp`。

![](img/4a1db50d3e2a8e380c74d6ab7426fc8e_287_0.png)

数字作为选项前缀。你也可以组合选项并只显示那些共有的行：

```
comm -3 fool foo2
comm -13 fool foo2
```

最后一个示例和另一个（使用 `-23` 选项的示例）比你想象的更具实用价值。我们将在本章结束时考虑一个使用该命令的示例。

## 9.9 paste: 合并文件行

形成单行。这可能没有太大用，因此我们将使用 `-d` 选项配合多个分隔符来一次合并三行。

如果我们将分隔符指定为 `:\n`，分隔符将循环使用。第一行和第二行将用 `:` 分隔符连接，第三行和第四行也是如此。第三行和第四行将用换行符分隔。列表用尽后，它将重复使用。这正是我们需要的。

```
$ paste -s -d ":\n" addressbook
barry wood@yahoo.com:245-690-4004
charles harris:charles_harris@heavens.com
james wilcocks:wilcocks@heavens.com:190-349-0743
```

看如何使用 `paste` 对单个文件按指定方式合并行？表格数据通常被拆分，每列单独占一行，在这些情况下 `paste` 非常有用。

## 9.10 sort：对文件排序

排序是按升序或降序对数据进行排序。在 UNIX 中，我们使用 `sort` 命令通过指定一个或多个键来对整行或部分行进行排序。类似于 `cut`，`sort` 可以识别字段并在指定的字段上排序。我们将通过对文件 `shortlist` 来考虑重要的 `sort` 选项。这是一个包含五行人员数据库的文本文件：

```
$ cat shortlist
2233:charles harris :g.m. :sales :12/12/52: 90000
9876:bill johnson :director :production:03/12/50:130000
5678:robert dylan :d.g.m. :marketing :04/19/43: 85000
2365:john woodcock :director :personnel :05/11/47:120000
5423:barry wood :admin :08/30/56:160000
```

每行都有由 `:` 分隔的字段。员工的详细信息存储在每行中。一个人通过员工 ID、姓名、职位、部门、出生日期和薪水（顺序相同）来识别。该文件特意设计为固定格式以便于阅读（你将在第 10 章中使用该文件的扩展版本）。

默认情况下，`sort` 按 ASCII 顺序对行排序——空格优先，大写字母，最后是小写字母：

```
$ sort shortlist
2233:charles harris :g.m. :sales :12/12/52: 90000
2365:john woodcock :director :personnel :05/11/47: 120000
5423:barry wood :admin :08/30/56: 160000
5678:robert dylan :d.g.m. :marketing :04/19/43: 85000
9876:bill johnson :director :production:03/12/50:130000
```

### 表 9.2 sort 选项

| 选项 | 说明 |
| :--- | :--- |
| `-t char` | 使用分隔符 char 识别字段 |
| `-k n` | 按第 n 个字段排序 |
| `-k m,n` | 从第 m 个字段开始并在第 n 个字段结束排序 |
| `-k m.n` | 从第 m 个字段的第 n 列开始 |
| `-u` | 删除重复行 |
| `-n` | 按数值排序 |
| `-r` | 反转排序顺序 |
| `-f` | 将小写转换为等效的大写字母（不区分大小写的排序） |
| `-m list` | 合并列表中的已排序文件 |
| `-c` | 检查文件是否排序 |
| `-o fname` | 将输出置于文件名 |

排序从每行的第一个字符开始，只有当两行的字符相同时，才会继续到下一个字符。使用选项，你可以更改默认排序序列并在多个键（字段）上进行排序。

### 9.10.1 sort 选项

`sort` 选项总结在表 9.2 中。在本版中，我们使用 `-k`（key） POSIX 选项来识别键（字段），而不是上一版中使用的 `+n` 和 `-n` 形式（其中 n 是字段编号）。与 `cut` 和 `paste` 不同，`sort` 使用连续的空格作为默认字段分隔符（`cut` 和 `paste` 中是制表符）。我们将使用 `-t` 选项来指定分隔符。

#### 按主键排序 (-k)

让 `-k` 选项按第二个字段（姓名）排序。该选项应该是 `-k 2`：

```
$ sort -t: -k 2 shortlist
5423:barry wood :admin :08/30/56:160000
9876:bill johnson :director :production:03/12/50:130000
2233:charles harris :g.m. :sales :12/12/52:90000
2365:john woodcock :director :personnel :05/11/47:120000
5678:robert dylan :d.g.m. :marketing :04/19/43:85000
```

排序顺序可以通过 `-r`（反转）选项反转。以下序列反转了之前的排序：

```
$ sort -r -k 2 shortlist
5678:robert dylan :d.g.m. :marketing :04/19/43:85000
2365:john woodcock :director :personnel :05/11/47:120000
2233:charles harris :g.m. :sales :12/12/52:90000
9876:bill johnson :director :production:03/12/50:130000
5423:barry wood :admin :08/30/56:160000
```

`sort` 以一种奇特的方式组合了选项。之前的命令也可以写成：

```
sort -t: -k 2 shortlist
```

#### 按次键排序

你可以对多个键进行排序；例如，你可以提供一个次键进行排序。如果主键是第三字段，次键是第二个字段，那么你需要为每个 `-k` 选项指定排序结束的位置。如下：

```
$ sort -t: -k 3,3 -k 2,2 shortlist
5423:barry wood :admin :08/30/56:160000
5678:robert dylan :d.g.m. :marketing :04/19/43:85000
9876:bill johnson :director :production:03/12/50:130000
2365:john woodcock :director :personnel :05/11/47:120000
2233:charles harris :g.m. :sales :12/12/52:90000
```

这按职位和姓名排序文件。`-k 3,3` 选项表示从第三字段开始并在同一字段结束。

#### 按列排序

你还可以指定字段内的字符位置作为排序的开始。如果你按出生年份对文件排序，你需要排序到该字段的第七列和第八列：

```
$ sort -t: -k 5.7,5.8 shortlist
5678:robert dylan :d.g.m. :marketing :04/19/43:85000
2365:john woodcock :director :personnel :05/11/47:120000
9876:bill johnson :director :production:03/12/50:130000
2233:charles harris :g.m. :sales :12/12/52:90000
5423:barry wood :admin :08/30/56:160000
```

该选项也使用 `-k m.n` 形式，其中 n 是 m 字段中的字符位置。因此，`-k 5.7,5.8` 意味着从第五字段的第七列开始并在第八列结束。

#### 数值排序 (-n)

当 `sort` 作用于数字时，会发生奇怪的情况。按第三字段（包含数字 group-id）对 `group` 文件排序时，你会得到奇怪的结果：

```
$ sort -t: -k 3,3 group1
root:x:0:root
bin:x:1:root,daemon
dialout:x:18:root,henry
lp:x:19:lp
users:x:200:henry,image,enquiry
adm:x:25:adm,daemon
ftp:x:50:
```

200 在 25 上！

这可能不是你预期的，ASCII 排序序列将 200 置于 25 之上（0 的 ASCII 值比 5 小）。这可以通过 `-n`（数值）选项覆盖：

```
$ sort -t: -k 3,3 -n group1
root:x:0:root
bin:x:1:root,daemon
dialout:x:18:root,henry
lp:x:19:lp
adm:x:25:adm,daemon
ftp:x:50:
users:x:200:henry,image,enquiry
```

按数值字段对文件排序时，始终使用 `-n` 选项。如果有其他需要纯 ASCII 排序的排序字段，可以在列规格 `-k 3,3` 加上 `n`。
