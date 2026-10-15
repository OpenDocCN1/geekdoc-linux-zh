
- 当文件的新版本完成后，你必须通过 `delta` 工具将其返回 SCCS 文件。该命令通过仅保存旧版本与新版本之间的差异，优化了 SCCS 文件的存储。在你返回文件之前，`get` 工具不允许任何其他人检出该文件。

- `sect` 工具允许你查看特定 SCCS 文件的当前编辑活动。

SCCS 还包含 `help`、`pr`、`comb`、`what` 和 `unget` 工具。我们将研究更高级的 SCCS 选项，让我们来看一个示例会话。在此过程中，请注意某些系统的 SCCS 工作方式各不相同；我建议你必须查看本文中的 SCCS 示例是否与你系统的 SCCS 版本一致。请注意，我讨论 SCCS 是因为它与大多数版本的 UNIX 兼容。其他可能更适合你需求的源码控制软件也可以从互联网上免费获取（[例如，GNU 的修订控制系统 (RCS)]），也可以通过付费购买商业用版本。

## 创建 SCCS 文件

```
Utility: admin -iname -flist -dlist -ename -aname sccsfile
```

`admin` 是一个 SCCS 工具，允许你创建和操作文件名。`sccsfile` 应该有一个前缀。`-i` 选项会创建一个名为 `sccsfile` 的文件。`-fl` 和 `-dl` 选项分别允许你锁定和解锁一组列出的“a”发布版本。`-a` 和 `-e` 选项分别允许你从能够获取可编辑版本 SCCS 文件的文件的列表中添加或删除具名用户。一旦创建了 SCCS 文件，你可以删除原始文件。如果你从任何与 SCCS 相关的工具处获得错误，请调用 SCCS `help` 工具，并将消息代码作为其参数。

SCCS `admin` 命令的描述。

要创建一个 SCCS 文件，请使用 `admin` 工具，其工作方式如图 12.16 所示。在下面的示例中，我创建了 `reverse.c` 源文件的 SCCS 版本：

```
$ ls -l reverse.c ...查看原始文件。
-rw-r--r-- 1 root root 266 1月 7 17 reverse.c
$ admin -reverse.c sccsfile ...创建 SCCS 文件。
No id (cm7)
$ help cm7 ...帮助 cm7
No id
1.1
```

图 12.17 提供了 `help` 工具的摘要。

```
Utility: help { message }
```

`help` 是一个 SCCS 工具，用于显示消息的解释。消息是由警告或错误生成的。

## 检出文件

要创建 SCCS 文件的只读副本，请使用图 12.18 所示的 `get` 工具。在以下示例中，我检出了 `reverse.c` 的一个版本：

```
$ ls -l s.reverse.c ...查看原始文件。
-r--r---- 1 root root 411 1月 7 17 s.reverse.c
$ get s.reverse.c ...检出。
```

`get` 工具允许允许你获取之前的版本。如果你想要可编辑版本，请使用 `-e` 选项，这会锁定文件：

```
$ get -e s.reverse.c ...检出可写版本。
$ ls -l reverse.c ...查看它。
-rw-r--r-- 1 root root 266 1月 7 18 reverse.c
```

`get` 命令的描述。

## 监控 SCCS 活动

`s` 工具显示与命名文件相关的活动列表。其工作方式如图 12.19 所示。这里是之前示例中 `sact` 的输出：

```
$ sact s.reverse.c ...监控“reverse.c”的活动
1.1 1.2 glass 98/01/07 18:05:11
```

`sact` 是一个 SCCS 工具，显示命名 SCCS 文件的当前活动。输出包含现有差异的版本、新差异的版本、使用 `-e` 检出文件的用户身份，以及执行 `get -e` 的日期和时间。

SCCS 命令 命令的描述。

## 撤销检出并返回文件

如果你执行了 `get` 然后又希望从未执行过，可以使用 `unget` 工具来撤销 `get`，其工作方式如图 12.20 所示。`unget` 将 SCCS 文件恢复到原来的状态，删除非 SCCS 生成的文件，并解锁文件供他人使用。如果多个版本当前正在编辑，使用 `-r` 选项来指定你想撤销的版本。默认情况下，`unget` 将文件移回 SCCS 文件。

## 创建新的增量 (Delta)

假设你检出了 `reverse.c` 的可编辑版本，并对其进行了修改，使其使用指针而不是数组下标。以下是新版本的列出：

```c
1 /* REVERSE.C *
2
3 #include <stdio.h>
4 #include "reverse.h"
5
6
7 reverse (before, after)
8
9 char *before;
10 char *after;
11
12 {
13 char* p;
14
15 p = before + strlen(before);
16
17 while (p-- != before)
18     *after++ = *p;
19
20     *after = NULL;
21 }
```

当保存文件的新版本时，你必须使用 `delta` 命令将其返回到 SCCS 文件，其工作方式如图 12.21 所示。以下是一个示例：

```bash
$ delta s.reverse.c ...返回修改过的检出版本。
comments? 将函数转换为使用指针 ...注释。
没有 id 关键字 (cm7)
1.2 ...新版本号。
5 inserted ...插入 ...修改的描述。
7 deleted ...删除
16 unchanged ...未更改
$ ls -l reverse.c ...原始文件已删除。
未找到 reverse.c
$
```

> 工具：`delta -trevision -n { sccfile}+`

`delta` 是一个 SCCS 工具，用于将已检出的文件返回到指定的 SCCS 文件。新版本通过图 12.21 所示的 `delta` 命令返回。新版本的增量等于旧增量号加 1。默认情况下，`delta` 描述你对文件所做的修改。在返回文件时，`delta` 会提示输入注释。如果你想返回特定版本，必须使用 `-r` 参数。

图 12.21

`delta` 命令说明。

## 获取文件的历史

要获取文件的历史列表，使用 `prs` 工具，其工作方式如图 12.21（应为 12.22）所示。以下是一个示例：

```bash
$ prs s.reverse.c ...显示文件。
reverse.c:
1.2 ...版本号。
5 inserted ...插入 ...修改。
7 deleted ...删除
16 unchanged ...未更改
$ get -p s.reverse.c ...将文件输出到标准输出。
2.1
... 
$ get -e -r2 s.reverse.c ...检出版本 2。
2.1
23 行
$ vi reverse.c ...编辑可写副本。
... 在文件顶部添加了以下行：
/*
Module: reverse.c
SCCS Id: 2.1
Time: 98/01/07 22:32:38
*/
... 文件剩余部分
$ delta s.reverse.c ...返回新版本。
comments? 添加了增量
2.1
6 inserted
0 deleted
21 unchanged
$ _
```

> 工具：`prs -trevision -n { sccfile}+`

`prs` 是一个 SCCS 工具，用于显示与文件相关的历史。默认情况下，它会显示所有版本。如果你想限制显示特定版本，可以使用 `-r` 参数。

图 12.22

`prs` 命令说明。

## SCCS 关键字

一些特殊的序列可以放置在文件中，当 `get` 读取文件时可见。图 12.23 显示了如何使用这些序列。这些关键字通常出现在文件的顶部。

图 12.23

SCCS 关键字说明。

## 创建新发布

要为 SCCS 文件创建一个新发布，通过 `get` 的 `-r` 参数指定新发布号。新发布号基于最新版本。在以下示例中，我为 `reverse.c` 创建了发布 2：
