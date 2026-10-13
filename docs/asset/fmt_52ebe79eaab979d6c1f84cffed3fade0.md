
RCS 将 `$Log$` 关键字替换为你在检入期间提供的日志消息。然而，RCS 并不是替换之前的日志条目，而是将新消息插入到最后一个日志条目上方。列表 7.2 给出了 `$Log$` 关键字在多次检入后扩展的示例：

### 列表 7.2 几次检入后的 $LOG$ 关键字

```
* Idle$
* $Id: howdy.c,v 1.1 1998/12/07 22:39:01 kwall Exp $
* howdy.c
* 用于演示 RCS 使用的示例代码
* Kurt Wall
* 列表 7.1

* * * *
* $Id:howdy.c,v 1.5 1999/01/07 23:07:35 kwall Exp $
* howdy.c
* 用于演示 RCS 使用
示例代码
* Kurt Wall
* 列表 7.1

* * * *
* $.::....111111


.


0演示演示.


 Kurt

*   7.1

* * * *
* $Id:howdy.c,v 1.4 1999/01/06 03:04:40 kwall Exp $
* howdy.c
* 用于演示 RCS 使用
* Kurt Wall
* 列表 7.1

* * * *
* $Id:howdy.c,v 1.3 1999/01/04 14:40:55 kwall Exp $
* howdy.c
```

`$Id$` 字符串的格式取决于你的系统，这些字段将（如下）。

## Linux 编程工具箱

### 第一部分

## 其他 RCS 关键字

| 关键字 | 描述 |
| :--- | :--- |
| `$Author$` | 检入用户的登录名 |
| `$Date$` | 检入时的日期和时间 |
| `$Header$` | 文件的完整路径 |
| `$Locker$` | 锁定用户的登录名 |
| `$Name$` | 符号名称 |
| `$Revision$` | 分配给该版本的版本号 |
| `$Source$` | 文件的完整路径（注：此处原文 Source 可能是误，通常 `$Source$` 指源文件路径） |
| `$State$` | 版本的状态：Exp（实验性）、Stab（稳定）、Rel（已发布） |

### ident 命令

`ident` 命令通过从文件中提取字符串。此功能让你发现使用了哪些版本。为了说明，创建列表 7.3 所示的源文件。

### 列表 7.3 ident 命令

```c
/* $Id$
* prn_env.c
* 显示环境变量的值
* Kurt Wall
* 列表 7.3
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

static char rcsid[] = "$Id\n";

int main(void)
```

程序 `prn_env.c` 遍历 `unistd.h` 中声明的数组以打印环境变量的值（详情见 `man(3) environ`）。语句 `static rcsid[] = "$Id\n";` 利用 RCS 的关键字扩展创建一个包含该值的静态文本缓冲区。使用 `-u` 选项检入 `prn_env.c`（`ci prn_env.c`）并编译链接程序（`gcc prn_env.c -o prn_env`）。忽略 `rcsid` 定义但未使用的警告。如果你想，可以运行程序，执行执行 `ident prn_env`。如果一切正常，将遵循如下：

```
$ ident prn_env
prn_env:
$Id: prn_env.c,v 1.1 1999/01/06 03:04:40 kwall Exp $
```

`$ID` 关键字如前所述扩展并由 `gcc` 编译到二进制文件中。为了确认，通过源代码并将源代码中的 ID 字符串与 `ident` 的输出进行比较。这两个字符串将匹配。

### rcsdiff

如果你需要查看工作文件与其对应的 RCS 文件之间的差异，请使用 `diff` 命令。`rcsdiff` 使用 `diff(1)` 命令（讨论

## 使用 RCS 进行版本控制

第 7 章 111

在第 6 章中，我们学习了“比较和合并源代码”来比较文件版本。最简单的形式是 `rcsdiff filename`，`rcsdiff` 将仓库中文件的最新版本与文件的工作副本进行比较。你也可以使用 `-r` 选项比较特定版本。

考虑示例程序 `prn_env.c`。检出一个锁定版本并删除 `static char` 缓冲区。结果应该如下：

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
```

```c
int main(void)
{
    extern char **environ;
    char *my_env = environ;

    while(*my_env) {
        fprintf(stdout, "%s\n", my_env);
        my_env++;
    }
    return EXIT_SUCCESS;
}
```

现在，执行命令 `rcsdiff prn_env.c`。RCS 编译并显示以下内容：

```
$ rcsdiff prn_env.c
============================================
RCS file: RCS/prn_env.c,v
retrieving revision 1.1
diff -r1.1 prn_env.c
1d0
< static char rcsid[] =
  - $Id: prn_env.c,v.1 1999/01/06 03:04:40 Exp kwall $
```

正如我们在第 6 章中学到的，此 diff 输出意味着如果版本 1.1 中的第 11 行没有被删除，它将出现在 `prn_env.c` 的第 10 行。要使用 `-r` 选项查看特定版本，请将 `prn_env.c` 检入仓库，然后以锁定状态重新检出，在 `return` 语句上方添加 `sleep(5)`，最后使用 `-u` 选项将第三个版本检回。现在你仓库中应该有 `prn_env.c` 的三个版本。

使用 `rcsdiff` 比较特定文件版本的通用格式为：

```
rcdiff [ -r FILE1 ] -r FILE2 ] FILENAME
```

首先，比较版本 1.1 和工作文件：

```
$ rcsdiff -r1.1 prn_env.c
============================
RCS file: RCS/prn_env.c,v
retrieving revision 1.1
diff -r1.1 prn_env.c
1c
/* * Id: prn_env.c,v 1.1 1999/01/06 03:10:17 kwall Exp $
/> * Id: prn_env.c,v 1.3 1999/01/06 03:12:22 kwall Exp $
11d10
< static char rcsid =
-*"Id: prn_env.c,v 1.1 1999/01/06 03:04:40 Exp $\n"
>
sleep(5);
```

接下来，比较 1.2 和 1.3：

```
$ rcsdiff -r1.2 -r1.3 prn_env.c
============================
RCS file: RCS/prn_env.c,v
retrieving revision 1.2
retrieving revision 1.3
diff -r1.2 -r1.3
1c
/* * Id: prn_env.c,v 1.1 1999/01/06 03:10:17 kwall Exp $
---
/> * Id: prn_env.c,v 1.3 1999/01/06 03:12:22 kwall Exp $
20a21
nsleep(5);
```

`rcsdiff` 是一个实用的工具，用于检查 RCS 文件或将多个版本合并为单个版本。

对于 GNU Emacs，Emacs 拥有先进的版本控制模式 VC，它支持 RCS、CVS 和 SCS。例如，要从 RCS 仓库中检入或检出当前文件，请输入 `C-x v` 或 `C-x q` 并按照提示操作。如果你想将当前编辑的文件首次放入仓库（这被称为“注册”文件——使用 RCS 注册），你需要输入 `C-x v i`。Emacs 的所有版本控制命令都以 `C-x v` 前缀。图 7.1 展示了 Emacs 会话中带有 RCS 的文件。

Emacs 的 RCS 模式大大增强了 RCS 的基本功能。如果你是 Emacs 的粉丝，我鼓励你探索 Emacs 的 VC 模式。

### 图 7.1

在 Emacs 中用 RCS 注册文件。
