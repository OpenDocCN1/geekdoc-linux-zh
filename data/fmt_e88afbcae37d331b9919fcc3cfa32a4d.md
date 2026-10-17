
# 使用 RCS 版本控制

## 比较版本

接下来，比较 `1.2` 和 `1.3`：

```
$ rdiff -r1.2 -r1.3 prn_env
```

```
=============================
RCS file: RCS/prn_env.c,v
retrieving revision 1.2
retrieving revision 1.3
diff -r1.2 -r1.3
< /* $Id: prn_env.c,v 1.1 1999/01/06 03:10:17 kwall Exp $
---
> /* $Id: prn_env.c,v 1.3 1999/01/06 03:12:22 kwall Exp $
> sleep(5);
```

`rdiff` 是一个用于查看 RCS 文件更改或将多个版本合并为单个版本的实用程序。对于 GNU Emacs，`Emacs` 拥有一种先进的版本控制模式 `VC`，支持 `RCS`、`CVS` 和 `SCCS`。要从 RCS 仓库检入或检出文件，输入 `C-x v` 或 `C-x q` 并遵循提示。如果你想第一次将正在编辑的文件放入仓库（称为在 RCS 中“注册”文件），你需要输入 `C-x i`。所有 Emacs 版本控制命令都以 `C-x v` 开头。图 7.1 展示了 Emacs 会话中的一个文件。Emacs RCS 模式极大地增强了 Emacs 的基本功能。如果你是 Emacs 的粉丝，我鼓励你探索 Emacs 的 `VC` 模式。

# 图 7.1

在 Emacs 中用 RCS 注册文件。

```c
#include <stdio.h>

#include <stdlib.h>

#define HAVE_RCS_X 1

#include <unistd.h>

#include "config.h"

int main() {

    int retval=0;

    #ifdef HAVE_RCS_X

        printf("have(vn)\n");

    else

        printf("no(vn)\n");

    #endif

    #ifdef _UTIME_NULL

        printf("utime have NULL\n");

    else

        printf("utime doesn't have NULL\n");

    #endif

    return retval;

}
```

![](img/66fe6c242a0e6a79aeee4012c6ff547_112_0.png)

## 其他 RCS 命令

除了 `ci`、`ident` 和 `diff`，RCS 工具套还包括 `log`、`clean`、`merge` 等等。这些额外的命令扩展了你对源码的控制，允许你合并或删除 RCS 文件、查看日志条目并执行其他管理功能。

### rclean

`clean` 正如其名：清理 RCS 工作文件。基本语法是 `clean [options] [file ... ]`。单独的 `clean` 命令将删除所有检出后锁定的文件和未更改的文件。`-u` 选项告诉 `clean` 解锁锁定文件并移除未更改的文件。你可以使用 `-r` 格式指定要删除的版本。

```
$ clean -r2.3 foobar.c
```

删除了 `foobar.c` 的 `2.3` 版本。

### log

`log` 打印存储在 RCS 仓库中的日志消息和其他信息。例如，`log prn_env.c` 将显示 `prn_env.c` 所有版本的日志信息。`-R` 选项告诉 `log` 只显示文件名。要查看仓库中的所有文件，例如 `log -R RCS/*` 是正确的命令（当然，你也可以一直使用 `ls -1 RCS`）。如果你只想查看锁定文件列表，在 `log -R -L RCS/*` 中使用 `-L` 选项。要查看由用户名锁定的所有文件的日志信息，使用 `-u` 选项：

```
$ log -uomer RCS/*
```

### rcs

`rcs` 命令主要是一项管理命令。在正常用法中，虽然如果你检出一个只读文件并进行了不想丢失的更改，它很有用，但 `rcs -1 filename` 会在查看工作文件的同时锁定并检出 `filename`。如果你需要解除他人检出的文件的锁定，则应使用 `rcs -u filename` 命令。该文件将被解锁，并向原始锁定者发送一条消息，解释你为什么要破坏锁定。当你进行回溯（recall）时，每当你检查一个文件，都可以输入一条检查消息，说明发生了什么变化或你做了什么。如果你在消息中犯了拼写错误或其他错误，或者想添加额外信息，可以使用以下 `rcs` 命令：

```
$ rcs -mrev:msg
```

`rev` 是你想要修正或修改的消息，`msg` 是你想要添加的修正后信息或额外信息。

### rcsmerge

`rcsmerge` 尝试将多个版本合并到一个单一工作文件中。通用语法如下：

```
rcsmerge -Ancestor -rDescendant Working_file -p Merged_file
```
