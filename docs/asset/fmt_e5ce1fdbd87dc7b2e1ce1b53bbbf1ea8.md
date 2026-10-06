
```
$ rcs -u xbuff.c
RCS file: RCS/xbuff.c
unlocked
$ rcs -o1 xbuff.c
RCS file: RCS/xbuff.c,v
deleting revision 1.1
done
```

当删除早期版本时，后期版本 `1.2` 不会重新编号。如果最新版本是 `1.2`，下一个 `ci` 将创建一个 `1.3`。当你删除一个版本时，该版本的更改不会被丢弃，它们会合并到下一个发布级别（如果有）。然而，你将无法回到被删除的版本。

与 `ci` 工具一样，`rcs` 工具会更改 RCS 文件；因此适用相同的权限标准。

# 源代码管理 567

```
15c15,19
< * (计算 pi 到 10000 位：在 PDP-11/44 上小于9 cpu 小时，
```

```
* (计算 pi 到 10000 位：在 PDP-11/44 上小于9 cpu 小时
* 486dx2/66 [Linux 1.2.13]: 126 cpu 秒
* 486dx4/100 [Linux 1.2.13]: 92 cpu 秒
```

```
>
21c25
< #define MAXNUM 100000 /* 最大允许精度
---
< #define MAXNUM 1000000 /* 最大允许精度 */
$
```

如果你使用 `-r` 选项指定一个版本，`rdiff` 会将指定的版本与工作文件进行比较。

```
$ rdiff -rl1.2 pi.c
=====================================================
RCS file: RCS/pi.c,v
retrieving revision 1.2
diff -rl1.2 pi.c
80c80
< outnum(r); /* 显示结果 */
---
> inform(r); /* 显示结果 */
153a154,166
>
> inform(a) /* 显示结果（给定的大数 a） */
> long[a];
{
printf("\n\n\n\tPI Calculation\n\n\n");
printf("\n\t# of words\t= %d\n\n", nwd);
printf("\n\t# of digits/word\t= %d\n\n", NDS);
printf("\n\t# of accurate places\t= %d\n\n", places);
printf("\n\t# Arithmetic message is %d\n\n", WDSZ);
printf("\n\n\tPI is: %s\n\n");
 outnum(a);
$
```

# 并发版本系统 (CVS)

虽然 RCS 作为源代码管理系统易于使用，但它存在以下问题：

- 项目只能被组织为单个文件的集合，而不是一个单一的集成单元。例如，如果一个项目很大并涉及多个目录，RCS 要求每个目录都要关联版本文件。多个版本文件会使得收集特定发布所需的文件变得困难，而且如果有多个开发人员，很难跟踪每个人的贡献。
- RCS 使用的锁定机制来控制对 RCS 文件的访问，使得两个或更多人无法同时修改一个文件，即使这些修改涉及文件的不同部分。这种类型的锁定对于小规模的版本控制可能有用，但如果开发团队正在合作完成一个大型项目，往往会阻碍进度。

并发版本系统（或 CVS）通过将整个文件集合视为单一单元来解决这些问题，使得在大型项目上工作变得容易，并允许多个用户在同一个 CVS 上工作，同时也为 CVS 系统提供了宝贵的自文档功能。

# CVS 如何存储版本文件

在 CVS 中，版本文件存储在公共区域作为源代码仓库。该区域由环境变量 `CVSROOT` 的值标识，该值持有仓库的绝对路径。你的系统管理员可以告诉你要使用什么 `CVSROOT` 值，或者你可以创建自己的私有仓库。

源代码仓库组织为文件和目录的层级集合。在 CVS 中，你并不限制于一次只检出一个文件；你可以检出一个包含许多文件的整个子目录——通常是特定项目的所有文件。`CVSROOT` 的子目录可以检出一个称为“模块”`module` 的单一单元。多个人可以同时检出并修改同一个模块内的文件。

CVS 用户通常会在特殊目录中检出他们正在工作的所有模块。如果你想遵循这种做法，必须在检出模块之前使用 `cd` 进入你的工作目录。当你检出一个模块时，CVS 会复制模块的树形结构。开发者可以检出并编辑 CVS 文件，因为原始文件保留在源代码仓库中；仓库中的文件以受控的方式进行不频繁的修改。

为了简化后续章节，工作目录的路径由变量 `CVSWORK` 提供；所有模块都可以认为是 `CVSWORK` 的子目录。尽管这对 CVS 并没有特殊意义，但你可能会发现为自己的工作定义这样一个变量很有帮助。

# 内置 CVS 帮助

RCS 使用了几个不同的程序，而 CVS 使用单一工具 `cvs`。要列出 `cvs` 部分的选项和程序，请使用 `-H` 选项。

```
$ cvs -H
Usage: cvs [cvs-options] command [command-options] [files...]
```

```
Where 'cvs-options':
-H 显示命令的用法信息
-Q 让 CVS 极其安静
-q 让 CVS 稍微安静
-r 将检出的文件设为只读
-w 将检出的文件设为可读写（默认）
-l 关闭历史日志
-n 不执行任何会更改磁盘的操作
-t 显示程序执行的跟踪 -- 尝试使用 -n
```

- CVS 版本和版权信息
- `bindir` 在 'bindir' 中查找 RCS 程序
- `editor` 使用 'editor' 编辑日志信息
- `CVS_root` 覆盖 `$CVSROOT` 作为根目录

# 更新他人的更改

当另一个开发者提交了文件的新版本时，CVS 不会通知你。要使你的 `compute.c` 版本变为最新，你需要运行 `update` 命令。

## 源代码管理 571

复制。只有当你尝试将更改提交到源仓库时，才会学习这一点。要合并 CVS 源文件的最新修订，请使用 `cvs update` 命令：

```
$ cvs update compute.c
RCS file: /usr/local/src/master/Project2/compute.c,v
retrieving 1.9
retrieving 1.10
Merging differences between 1.9 and 1.10 into compute.c
M compute.c
```

对 `compute.c` 工作副本所的更改将保持完好，因为 `update` 命令将源仓库中的最新版本与更新命令中指定的版本合并。如果检测到重叠更改，`cvs update` 命令将通知你。

## 向仓库添加新文件

你可以使用 `cvs add` 命令为你正在处理的模块的每个部分安排将新文件添加到源仓库。一旦你移动到包含文件的目录，请使用 `cvs add` 命令并列出你想要添加的文件。

```
$ cd $CVSWORK/Project2
$ ls
CVS compute.c shuffle tabout2.c data.h randomfile.h tabout1.c
$ cvs add tabout[1-2]
cvs add: scheduling file 'tabout1.c' for addition
cvs add: scheduling file tabout2.c for addition
cvs add: use 'cvs commit' to add these files permanently
```

`add` 命令标记 `tabout1.c` 和 `tabout2.c` 文件进入仓库。在发出 `commit` 命令之前，这些文件对其他人不可用。这种暂存机制允许你在使用 `cvs update` 命令将更改合并到工作副本之前，先准备几个文件。

## 从仓库删除文件

`cvs remove` 命令记录了你想要从源仓库删除文件的事实，和 `add` 命令一样，它不会影响源仓库。要从仓库中删除文件，你必须先删除该文件的工作副本，如下所示：

```
$ cvs remove shuffle.c
cvs remove: file 'shuffle.c' still in working directory
cvs remove: 1 file exists; use 'rm' to remove it first
$ rm shuffle.c
$ cvs remove shuffle.c
cvs remove: scheduling 'shuffle.c' for removal
cvs remove: use 'cvs commit' to remove this file permanently
```

使用 `rm` 删除 `shuffle.c` 的工作副本后，调用 `cvs remove` 命令。再次，在文件实际从源仓库中删除之前，你必须发出 `commit` 命令。

## 其他 CVS 命令

虽然上述命令对于模块的大部分工作已经足够，但你可能还会发现其他一些有用的命令。

## 572 第 14 章：编程工具

**发布版本标记（Tagging a Release）。** 你可以使用通用标签（或标记）标记模块中当前存在的文件。一旦你标记了模块的文件，即使这些文件从那以后被修改、添加或删除，你也可以完全相同的格式重新创建它们。这使你能够冻结一个发布，同时允许在下一个发布上继续开发。

```
$ cvs rtag Release_1 Project1
cvs rtag: Tagging Project1
```

`Project1` 模块已标记为标签 `Release_1`。你可以使用此标签配合 `cvs export` 来提取这些文件在此时冻结时的状态。

**提取发布版本（Extracting a Release）。** `cvs export` 命令允许你提取冻结并标记的文件。

```
$ cvs export -r Release_1 -d R1 Project1
cvs export: Updating R1
R1/scm.txt
```

此命令的作用类似于 `cvs checkout` 命令，但它不会创建 CVS 支持文件。你必须提供 `-r` 选项来识别发布版本或使用 `-D` 选项指定日期。`-d` 选项指示 `cvs` 将模块的文件放入目录 `R1`，而不是使用模块名称作为目录。

**删除工作文件（Removing Working Files）。** 当你完成对仓库检出的文件的修改后，你可能决定从工作目录中删除模块的副本。一种简单的方法是进入工作目录并递归删除该模块。例如，如果你想删除 `Project2` 的工作副本，可以使用以下命令：

```
$ cd $CVSWORK
$ rm -rf Project2
```

仓库将不受影响。然而，如果你对文件进行了更改但尚未提交这些更改，使用上述方法将导致这些更改丢失。在这种情况下，`cvs release` 命令很有帮助。

```
$ cd $CVSWORK
$ cvs release -d Project2
```

`release` 命令也会删除工作文件，但会首先检查每个文件，查看它是否已被标记为添加到仓库但尚未提交。如果是这样，`release` 命令会警告你并要求你确认删除该文件的意图。如果你愿意，可以修复问题并重新执行 `release` 命令。如果仓库中的文件比你工作目录中的版本更新，`release` 也会警告你。这让你有机会在删除文件之前更新并提交你的文件。

## 向仓库添加模块

到此为止对 CVS 的讨论假设模块已经存在于 CVS 仓库中。如果你想向仓库添加新模块，请使用 `import` 命令。首先，移动到包含模块的目录，然后使用 `import` 命令列出模块名称和目录名称：

```
$ cd $CVSWORK/Project2
$ cvs import -m "initial check" Project2
```

`import` 命令在仓库中创建一个新模块。`-m` 选项允许你为模块提供描述。如果你不使用 `-m` 选项，CVS 将使用当前日期作为描述。导入完成后，你必须使用 `commit` 命令将文件添加到仓库：

```
$ cvs commit -m "initial check"
```

模块现在位于仓库中，其他人可以使用 `checkout` 命令获取其副本。

# 源代码管理 575

```
CVSROOT 支持: 每次更改时运行 mkmodules。
CVSROOT -i mkmodules CVSROOT
pmodules -i mkmodules CVSROOT modules
logininfo -i mkmodules CVSROOT logininfo
commitinfo -i mkmodules CVSROOT commitinfo
rcsinfo -i mkmodules CVSROOT rcsinfo
editinfo -i mkmodules CVSROOT editinfo
```
