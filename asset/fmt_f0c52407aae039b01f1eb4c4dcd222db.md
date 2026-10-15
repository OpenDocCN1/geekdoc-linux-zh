
命令 `ci howdy.c` 会要求输入文件的描述，将其复制到 RCS 目录并删除原始文件。别担心，你还有一个工作文件。注意该文件是只读的；如果你想编辑它，必须先锁定它。要做到这一点，请使用 `ci` 的 `-l` 选项（`-l howdy.c`），`-l` 表示锁定，如表 7.1 所示。

```bash
$ ci -l howdy.c

RCS/howdy.c,v

enter description, terminated with single '.' or of file:

NOTE: 这不是日志消息！

>> Simple program to illustrate RCS usage

>> initial revision: 1.1

done

$ co -l howdy.c

RCS/howdy.c,v

revision 1.1 (locked)

done
```

为了看到版本控制的作用，对工作文件进行更改。如果你还没有这样做，请检出并锁定文件（`co -l howdy.c`）。修改你想要的内容，但我建议在 `printf()` 字符串中添加 `"\n"`，因为 Linux（在 UNIX）不像 Windows 那样会自动添加换行符。

```c
printf(stdout, "Howdy, Linux programmer!\n");
```
*(注：此处原文示例代码中缺少了 \n，根据上下文补全或保持逻辑一致）*

```c
printf(stdout, "Howdy, Linux programmer!\n");
```

接下来，将文件检回，RCS 将将修订号增加到 1.2，询问你所做的更改，将你的更改合并到 RCS 文件中并（令人恼地）删除原始文件。为了防止在操作期间删除工作文件，请对 `ci` 使用 `-l` 或 `-u` 选项。

```bash
$ ci -l howdy.c

RCS/howdy.c,v

new revision: 1.2; previous revision: 1.1

enter log message, terminated with single '.' or end of file:

>> Add newline

>> .

done
```

在配合 `ci` 使用时，`-l` 和 `-u` 选项会在检入程序完成后隐含地检出文件。`-l` 锁定文件以便继续编辑，而 `-u` 则检出一个解锁或只读的工作文件。

除了 `-l` 和 `-u`，`ci` 和 `co` 还接受两个实用的选项：`-r`（用于修订）和 `-f`（强制）。`-r` 告诉 RCS 你想操作哪个版本。RCS 假设你想处理最新版本；`-r` 覆盖此默认设置。例如，`ci -r2 howdy.c`（等同于 `ci -r2.1 howdy.c`）会创建 `howdy.c` 的版本2.1。`-r1.7 howdy.c` 检出 1.7 版本，忽略工作目录中存在的更高版本。

`-f` 选项用于覆盖当前工作文件。默认情况下，如果工作目录中已存在同名工作文件，RCS 将中止检出操作。如果你真的搞砸了工作文件，`co -l f howdy.c` 是一个实用的工具，可以丢弃你的所有更改并从良好的源文件重新开始。配合 `ci` 使用时，`-f` 会强制检入未发生更改的文件。

# RCS 关键字

RCS 关键字是一种特殊的类宏令牌，用于在源文件、对象文件二进制插入并维护标识信息。这些令牌的形式为 `KEYWORDS`。当检出包含 RCS 关键字的文件时，RCS 将 `KEYWORDS` 扩展为 `KEYWORD:`。

# $Id

例如，列表 7.1 顶部的特殊字符串 `$Id` 是一个 RCS 关键字。第一次检出 `howdy.c` 时，RCS 将其扩展为类似：

$Id: howdy.c,v 1.1 1998/12/07 22:39:01 kwall Exp $

# Linux 编程工具箱
## 第一部分

$ID 字符串的格式为：

$KEYWORD: FILENAME REV_NUM DATE TIME AUTHOR STATE LOCKER $

在你的系统中，这些字段大部分将具有不同的值。如果你检出（checkout）了一个带有锁的文件，你还会在 Exp 条目之后看到你的登录名。

## $Log$

RCS 将 $Log 关键字替换为你在提交（check in）时提供的日志消息。然而，RCS 并不是替换之前的日志条目，而是将新的日志消息插入到日志条目的上方。列表 7.2 展示了在几次提交后，$Log 关键字是如何展开的示例：

### 列表 7.2 几次提交后的 $LOG 关键字

```
/ Id: howdy.c,v 1.5 1999/01/04 23:07:35 kwall Exp kwall $$

* howdy.c

* 用于演示 RCS 用途的示例代码

* Kurt Wall

* 列表 7.1

*

* ********** 修订历史 **********

* Log: howdy.c,v $$

* Revision 1.5 1999/01/04 23:07:35 kwall

* 为修订历史添加了漂亮的边框

*

* Revision 1.4 1999/01/04 14:41:55 kwall

* 为 main 添加了用于处理命令行的参数

*

* Revision 1.3 1999/01/04 14:40:15 kwall

* 添加了 Log 关键字。

*********************************

*/
#include <stdio.h>
#include <stdlib.h>
```

```c
int main(int argc, char **argv)
{
	printf(stdout, "Howdy, Linux programmer\n");
	return EXIT_SUCCESS;
}
```

$Log 关键字使得查看某个特定文件内部所做的更改非常方便。从上到下阅读，更改历史列表将最近的更改列在前面。

## 其他 RCS 关键字

表 7.2 列出了其他 RCS 关键字以及 RCS 展开每个关键字的方式。

| 关键字 | 描述 |
| --- | --- |
| $Author | 提交修订版本的用户登录名 |
| $Date | 修订提交的日期和时间，采用 UTC 格式 |
| $Header | RCS 文件的完整路径、修订号、日期、时间、作者、状态、锁定者（如果已锁定） |
| $Locker | 锁定修订版本的用户登录名（如果未锁定，该字段为空） |
| $Name | 用于检出修订版本的符号名称（如果有的话） |
| $RCSfile | 不带路径的 RCS 文件名 |
| $Revision | 分配给修订版本的修订号 |
| $Source | RCS 文件的完整路径 |
| $State | 修订的状态：Exp（实验性），默认值：Stab（稳定）：Rel（已发布） |

## ident 命令

`ident` 命令在所有类型的文件中定位 RCS 关键字。此功能让你发现在特定的程序发布版本使用了哪些模块的哪些版本。为了说明，请创建列表 7.3 所示的源文件。

### 列表 7.3 ident 命令

```c
/* $Ids
 * prn_env.c
 * 显示环境变量的值。
 * Kurt Wall
 * 列表 7.3
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
static char rcsid[] = "$Id\n";
int main(void)
{
  extern char **environ;
  char *my_env = environ;
  while(*my_env) {
    fprintf(stdout, "%s\n", *my_env);
    my_env++;
  }
  return EXIT_SUCCESS;
}
```

该程序 `prn_env.c` 可以在源文件中工作并查看该文件中的更改。通过 `man(3) environ` 了解环境变量的值。`static char rcsid[] = "$Id\n";` 语句利用 RCS 关键字来生成标识符。使用 `-u` 选项检出带有锁的文件（`ci -u prn_env.c`），然后编译并链接程序（`gcc -o prn_env.c. prn_env.c`）。如果一切运行正常，你应该得到类似下面的输出：

$Id: prn_env.c v 1.1 1999/01/06 03:04:40 kwall Exp

`ident` 通过从源文件、对象文件和二进制文件中提取 `$KEYWORD: VALUE $` 格式的字符串来工作。事实上，它也可以不是关键字的单词。这允许你在程序中嵌入额外信息，例如公司名称。嵌入信息是定位问题非常有用的工具。此功能的奇妙之处在于 RCS 会自动更新标识字符串——这对程序员和项目经理来说是巨大的福音。

## rcsdiff

如果你需要查看工作文件与其对应的 RCS 文件之间的差异，请使用 `rcsdiff` 命令。`rcdiff` 使用 `diff(1)` 命令（在第六章“比较和合并源文件”中讨论）来比较文件版本。在最简单的形式下，`rcdiff filename` 将存储中的最新修订版本与工作副本进行比较。你可以使用 `-r` 选项比较特定的版本。

考虑示例程序 `prn_env.c`。检出它的锁定版本并删除静态缓冲区。结果应该如下：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(void) {
    extern char **environ;
    char *my_env = environ;
    while(*my_env) {
        fprintf(stdout, "%s\n", *my_env);
        my_env++;
    }
    return EXIT_SUCCESS;
}
```

现在，执行命令 `rcdiff prn_env.c`。它编译并显示以下内容：

```
$ rcsdiff prn_env.c
===================================================
RCS file: RCS/prn_env.c,v
retrieving revision 1.1
diff -r.1 prn_env.c
1d10
< static char rcsid[] =
- $Id: prn_env.c, v 1.1 1999/01/06 03:04:40 kwall Exp kwall $$
```

正如第六章中学过的，如果此输出意味着如果没有删除，版本 1.1 中的第 11 行将出现在 `prn_env.c` 的第 10 行。要查看特定版本，请使用 `-r` 选项。

# rcs

`rcs` 命令主要是一项管理命令。在正常用法中，它在两个方面非常有用：如果你以只读模式检出一个文件并并了不想丢失的更改，使用 `rcs -l filename` 将以锁定方式检出文件名，而不会覆盖工作文件。如果你需要解除对他人检出的文件的锁定，则应使用 `rcs -u filename` 命令。该文件将被解锁，并向原始锁定者发送一条消息，附带关于你为何破坏锁定的解释。正如你可能记得的，每当你检查文件时，你都可以输入一条消息说明了什么变化或你做了什么，或者简单地为其添加额外信息，你可以使用以下 rcs 命令：

```
$ rcs -mrev:msg
```

`rev` 是你想要修正或修改消息的版本号，`msg` 是你想要添加的额外信息。

# rcsmerge

`rcsmerge` 尝试将多个版本合并到一个单一的工作文件中。其通用语法为

```
rcsmerge -rAncestor -rDescendant Working_file -p Merged_file
```

`Descendant`（后代）和 `Working_file`（工作文件）都必须源自 `Ancestor`（祖先）。`-p` 选项告诉 `rcsmerge` 将输出发送到 stdout，而不是覆盖 `Working_file`。通过重定向到 `Merged_file`，你可以检查合并结果。虽然 `rcsmerge` 在合并文件方面尽了最大努力，但结果可能是不可预测的。`-p` 选项可以防止这种不可预测性的影响。

关于 RCS 的更多信息，请参阅这些页面：`rcs(1)`, `ci(1)`, `co(1)`, `rcsinfo(1)`, `rcsdiff(1)`, `rsclean(1)`, `rcsmerge(1)`, `log(1)`, `rcsfile(1)` 和 `ident(1)`。

## 总结

在本章中，你学习了 RCS，即版本控制系统。`ci` 和 `co` 及其它们的各种选项和参数；RCS 的基础命令。RCS 关键字允许你识别代码和编译程序中的字符串，这些字符串稍后可以通过 `ident` 命令提取。你还学习了其他有用但较少使用的 RCS 命令，包括 `rcsdiff`、`rsclean`、`rcsmerge` 和 `log`。

# 在 Emacs 中创建程序

由 Kurt Wall 和 Mark Watson 编写

## 本章内容

- Emacs 简介 116
- 支持编程的功能 125
- 使用 Emacs Lisp 自动化开发 132

# 第 8 章

# Emacs 简介

Emacs 提供了一个丰富且高度可配置的编程环境。事实上，你可以在早上启动 Emacs，在你编译代码时，你可以跟进上晚晚在 alt.vampire.flonk.flonk.flonk 上的帖子，发送软件补丁，获取专业咨询，并编写你的文档，而无需离开 Emacs。你这一章从 Emacs 开始，重点介绍 Emacs 为程序员提供的功能。

Emacs 拥有悠久的历史，正如人们对当前发行版本为 20.3（本章使用的版本）的软件所预期的那样，但我们不再赘述它。Emacs 的名称来源于理查德·斯托曼（Richard Stallman）最初为 TECO 编辑器编写的“编辑宏”（editing macros）。斯托曼写了关于 Emacs 历史的自述，可以在 http://www.gnu.org/philosophy/stallman-kth.html 在线查看（你也将很好了解 GNU 的哲学基础）。

> 世界被分为三类人——使用 Emacs 的人、偏好 vi 的人以及其他人。关于 Emacs 还是 vi 的问题引发了许多口战。

评价 Emacs 巨大的功能集时，一位机智者说：“Emacs 是一个大操作系统，但 UNIX 有更多程序。”我对 Emacs 幽默一直感兴趣。请将 Emacs 相关内容发送到 kwall@xmission.com，并在主题行某处注明“Emacs Humor”。

任何程序员编辑器的真理在 Emacs 上同样适用：在学习 Emacs 上投入的时间在开发过程中将获得数倍回报。本章提供了足够的信息让你能够开始使用 Emacs，并介绍了许多增强其作为 C 开发环境用途的功能。然而，Emacs 太大了，在一个章节内无法涵盖。完整的教程是《Sams Teach Yourself Emacs in 24 Hours》。更多详细信息，请参阅由自由软件基金发布的《GNU Emacs Manual》和《GNU Emacs Lisp Reference Manual》，以及 O'Reilly 出版的《Learning GNU Emacs and Writing GNU Emacs Extensions》。

# 在 Emacs 中创建程序

# 启动和停止 Emacs

启动 Emacs，输入 `emacs` 或 `emacs filename`。如果你在系统中配置并运行了 X，尝试输入 `emacs` 来启动 Emacs 的图形化版本（以前被称为 Lucid Emacs）。如果 Emacs 是在支持 Athena 组件的情况下构建的，Emacs 将具有鼠标支持和下拉菜单。根据你输入的命令，你应该会看到一个类似于图 8.1、8.2 或 8.3 的屏幕。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_142_0.png)

编辑窗口
状态栏

![](img/69b363a7d7f58dc8d0b8c78c0052826f_142_1.png)

编辑窗口
状态栏

```
---*scratch* (Interaction-L-All)--
```
