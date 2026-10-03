
```bash
export CVSROOT=/usr/local/cvs_repository
```

由于我们将更改仓库中的一个文件，因此你应该将第 15 章中使用的某些程序复制到单独的目录。现在切换到此目录并调用 `cvs import`：

```bash
$ cvs import -m"A Simple Project" simple_project no_vendor first_last /pointers.c \
/sizeof.c \
/type_conversion.c
```

此模块未创建冲突

此命令创建了模块，即 `$CVSROOT` 中名为 `simple_project` 的目录。CVS 还将这三个文件以 RCS 编码格式（带有 `.v` 后缀）存放在该目录中。每行开头的字母 `N` 表示这些文件是新的。`-m` 选项描述了导入的文件，最后两个参数用于分配供应商标签（vendor tag）和发布标签（release tag）。CVS 将这些字符串整合到编码文件中。仓库现在已准备就绪。

## 第 16 章：程序开发工具

当使用目录名作为参数时，CVS 会以递归方式运行。它在导入时复制仓库中的目录结构，并在检出（checkout）时复制沙箱结构。与 RCS 不同，你不需要为模块的每个文件发布单独的命令（尽管你也可以这样做）。

## 16.11.3 检出 (Checkout)

我们现在需要创建一个沙箱，即一个在检出时保存文件的独立目录。让我们创建一个名为 `cvs_sandbox` 的目录，进入该目录，然后使用 `cvs checkout`（或 `cvs co`）命令。以下命令从仓库检出 `sizeof.c` 文件：

```bash
$ cvs checkout simple_project/sizeof.c
simple_project/sizeof.c
```

`U` 表示该文件没有被其他人修改过。要检出整个模块，只需指定模块名作为参数即可：

```bash
$ cvs checkout simple_project
cvs checkout: Updating simple_project
simple_project/pointers.c
simple_project/type_conversion.c
```

在任何情况下，CVS 都会在 `cvs_sandbox` 中创建 `simple_project` 目录并将文件放在其中。由于 `sizeof.c` 之前已被检出，CVS 更新了检出的模块。该目录现在包含一个名为 `CVSROOT` 的子目录和三个 C 程序（带有 `.c` 扩展名）。

## 16.11.4 编辑与提交 (Checking In)

现在切换到目录 `simple_project`（沙箱）并编辑 `sizeof.c` 文件。我们被告知浮点常量类型为 `double`，让我们通过包含此行来验证：

```c
printf("Size of 4.6: %ld bytes\n", sizeof(4.6));
```

在成功编译并执行程序后（发现 4.6 占据了 8 个字节！），现在可以使用 `cvs commit`（或 `cvs ci`）命令提交文件。使用 `-m` 选项以避免调用 vi 编辑器：

```bash
$ cvs commit -m"Additional printf for checking type of 4.6"
cvs commit: Examining...
/usr/local/cvs_repository/simple_project/sizeof.c,v -- sizeof.c
new revision: 1.2; previous revision: 1.1
```

现在你在仓库中有两个版本的 `sizeof.c`。为了确保无误，使用 `cvs diff` 命令查找两个版本之间的差异。使用 `-r` 选项指定指定最新版本对比的发布版本：

```bash
$ cvs diff -r1.1 -r1.2
cvs diff: Diffing .
Index: sizeof.c
============================================
RCS file: /usr/local/cvs_repository/simple_project/sizeof.c,v
retrieving revision 1.1
retrieving revision 1.2
diff -r1.1 -r1.2
13a4
  > printf("Size of %d: %ld bytes\n", sizeof(4));
```

你可以看到 `diff` 命令正在工作，输出显示了两个版本之间的差异。

## 16.11.5 合并与解决冲突

CVS 允许多个用户合并更改。然而，当两个用户修改同一行时，可能会发生冲突。当用户尝试更新时，CVS 会检测到冲突。用户必须通过编辑文件来决定保留哪些更改：

```text
<<<<<<< sizeof.c
1.3
=======
1.4
>>>>>>>
```

## 16.11.6 设置标签与导出仓库

在某些时刻，你可能希望锁定一个或多个文件交付客户，而不影响开发工作。CVS 通过 `rtag` 和 `export` 命令实现这一点。例如，要为模块的所有文件应用标签 `Version_1_0`，你需要这样使用 `cvs rtag` 命令：

```bash
$ cvs rtag Version_1_0 simple_project
cvs rtag: Tagging simple_project
```

以后你可以从仓库中提取相同的文件。你不能在当前的沙箱中这样做，因为会覆盖现有文件。现在切换到另一个目录并重复命令，使用 `-d` 选项将文件下载到：

```bash
$ cvs export -r Version_1_0 -d /path/to/export/ simple_project
```

此外，除了使用 `-r` 选项外，你还可以使用 `-O` 选项设置日期。这样你就可以在沙箱中保留最新文件，而在另一个目录中保留标记为 `Version_1_0` 的文件。

## 16.11.7 其他功能

### 添加文件

有时，你需要向仓库添加文件。`cvs add` 命令（调度）文件的添加，但并不会添加它们。只有在你执行 `cvs commit` 时，仓库才会更新：

```bash
$ cvs add arrays.c
cvs add: scheduling file `arrays.c` for addition
cvs use: `commit` to add this file permanently
$ cvs commit -m"arrays.c added"
/usr/local/cvs_repository/simple_project/arrays.c,v --- arrays.c
initial revision: 1.1
```

### 删除文件

可以使用 `cvs remove` 命令从仓库删除文件。该命令同样会将仓库中的文件标记为删除。只有在你从沙箱中删除文件后，才能实际删除。你需要再次执行 `cvs commit`：

```bash
$ cvs remove dos2unix.c
cvs remove: file 'dos2unix.c' still in working directory
$ rm dos2unix.c
$ cvs remove dos2unix.c
cvs remove: scheduling 'dos2unix.c' for removal
cvs remove: use 'cvs commit' to remove this file permanently
$ cvs commit -m"File deleted"
cvs commit: Examining .
/usr/local/cvs_repository/simple_project/dos2unix.c <- dos2unix.c
revision: delete; previous revision: 1.3
```

![](img/4a1db50d3e2a8e380c74d6ab7426fc8e_562_0.png)

对存储库进行的任何更改必须通过 `cvs commit` 命令完成。为了实现非交互式行为，每当使用 `cvs commit` 时请使用 `-m` 选项。

**使用帮助** `cvs commit` 命令提供了一满屏幕的命令，你可以自行尝试。精简的输出显示了一些实用的命令：

- `history` 显示存储库访问历史
- `import` 使用供应商分支将源导入到 CVS
- `init` 如果不存在，则创建一个 CVS 存储库
- `log` 打印文件的历史信息
- `ls` 列出 CVS 中可用的文件
- `rdiff` 在版本之间创建“补丁”格式的差异
- `remove` 从存储库中删除条目
- `log` 打印模块的历史信息
- `tag` 为模块添加符号标记
- `status` 显示已检出文件的状态信息
- `tag` 为已检出的文件版本添加符号标记
- `unedit` 撤销编辑命令
- `update` 使工作树与存储库保持同步

你可以通过 `cvs -H 命令名` 查找有关命令的更多详细信息。你会发现 `ls` 和 `status` 命令对于学习存储库中的文件名以及判断箱中的文件是否为最新版本非常有用。

# 16.12 使用 gdb 调试程序

当程序运行不正常时，我们使用的首要措施是在程序中易出错的位置使用 `printf` 语句来打印导致不当行为的变量值。这种技术对于大型或复杂的程序不起作用。此外，它还让我们留下了大量的清理工作，因为这些诊断语句必须从最终代码中精确地删除。每个程序员都必须学会如何使用调试器。

调试器是一个控制另一个程序执行的程序。它通过在任何指定时刻捕获程序环境来实现这一点。程序员随后可以查看该时刻变量的状态，并在必要时对其进行更改。调试器还可以指定断点，使程序在何处停止，或者允许一次执行一个或多个语句。程序必须使用 cc 或 gcc 的 `-g` 选项进行编译，调试器才能工作。

在最后一节中，我们讨论了由 GNU 提供的 `gdb`。由于它的流行，我们选择了 gdb 而不是本书上一版介绍的 BSD-Ddb。gdb 可以与 C++、Fortran 和 Java 程序一起工作，并适用于所有 Linux 系统以及大多数其他平台（包括 Windows）。如果你的调试器可以用以下方式使用：

- 调试模式（Debug Mode）：在此模式下，调试器运行程序并允许你监控每条语句的执行。
- 附加模式（Attach Mode）：gdb 可以附加到任何运行中的进程，并使程序使用的内存中的信息可用。
- 事后模式（Post-mortem mode）：如果程序崩溃（例如非法访问内存），gdb 可以通过检查转储的核心文件（名为 `core.pid` 的文件）来确定崩溃原因。

gdb 最常用的命令如表 16.3 所示。在本章中，我们将使用调试模式下的 gdb 来定位程序 `parsing` 中的两个 bug（图 16.8）。该程序提示输入多行字符串，使用 `scanf` 保存字符串，并使用 `strtok` 库函数将其拆分为单词。`printf` 语句旨在将每个字符串单独打印。所有调试器都会在诊断消息中显示行号，为了方便起见，我们使用了 `nl` 对这些行进行编号。

# 表 16.3 gdb 命令

| 命令 | 意义 |
|---|---|
| `list` | 显示 10 行源代码 |
| `list m, n` | 显示从 m 行到 n 行的源代码 |
| `run` | 执行程序直到遇到下一个断点或观察点 |
| `cont` | 继续执行 |
| `next` | 执行下一条语句（函数被视为单条语句） |
| `step` | 执行下一条语句但进入函数内部 |
| `break n` | 在行号 n 处设置断点 |
| `break function` | 在调用函数的行设置断点 |
| `break n condition` | 如果条件为真，在行号 n 处设置断点 |
| `watch x` | 在变量或表达式 x 上设置断点 |
| `whatis x` | 显示变量或表达式 x 的类型 |
| `display x` | 显示变量或表达式 x 的值 |
| `print x` | 同上 |
| `edit` | 使用 EDITOR 变量定义的编辑器编辑源文件 |
| `quit` | 退出 gdb |

# 图 16.8 包含两个 bug 的 stdio.c

| 行 | 代码 |
|---|---|
| 1 | `#include <stdio.h>` |
| 2 | `#include <string.h>` | /* 用于 strtok */ |
| 3 | `#define BUSIZE 200` | /* * 命令行的最大长度 */ |
| 4 | `#define ARGSIZE 40` | /* * 参数的最大数量 */ |
| 5 | `#define DELIM "\n\t\r"` | /* * 空格字符 */ |
| 6 | `int main (void) {` |
| 7 | `int i, n;` |
| 8 | `char buf[BUSIZE];` |
| 9 | `char *args[ARGSIZE];` |
| 10 | `printf("Enter multiline string: ");` |
| 11 | `scanf("%s", buf);` |
| 12 | `args = strtok(buf, DELIM);` |
| 13 | `while (args != NULL) {` |
| 14 | `printf("%s\n", args);` |
| 15 | `args = strtok(NULL, DELIM);` |
| 16 | `}` |
| 17 | `return 0;` |
| 18 | `}` |

*(注：原文图 16.8 的文本严重损坏；上述表格已根据标准的 C 编程模式和提供的上下文环境进行了重建。)*

# 你的 UNIX/Linux：终极指南

输入 "help all" 获取所有命令列表。

输入 "help" 后接命令名称获取完整文档。

输入 "apropos" 搜索与 "word" 相关的命令。

如果无歧义，允许使用命令缩写。

此调试器将其命令分为 12 类。输出最后一行的功能可以稍微减轻你的输入负担。例如，与其使用 `break 10` 在第 10 行设置断点，你可以使用 `b 10`、`br 10` 等，因为 `break` 是唯一以 b 开头的 gdb 命令。

让我们来识别设置断点的命令。我们推测它属于 `breakpoints` 类别，接下来的跟踪输出显示 `break` 是要使用的命令：

```
(gdb) help breakpoints
```

让程序在某些点停止。

命令列表：

- `watch` 为表达式设置监视点
- `break` -- 在指定的行或函数处设置断点
- `catch` -- 设置检查点以捕获事件
- `clear` -- 清除指定行或函数处的断点
- `commands` -- 设置命中断点时执行的命令
- `condition` -- 指定断点 N 仅当 COND 为真时才中断
- `delete breakpoints` -- 删除断点或自动显示表达式
- `disable breakpoints` -- 禁用某些断点
- `enable` -- 启用某些断点

我们可以在命令名后使用 help 来获取特定上下文的帮助。help 命令定义了一个断点，以下是你应该使用它的方式：

```
(gdb) help break
在指定的行或函数处设置断点。
break [LOCATION][thread THREADNUM] [if CONDITION]
LOCATION 可以是行号、函数名，或者 "" 和地址。
如果指定了行号，在该行代码的开始处中断。
如果指定了函数，在函数的代码开始处中断。
如果指定了地址，在那个精确的地址中断。
```

注意，断点可以设置在任何行或函数上。命中断点后，程序将暂停以便你干预。当调用 `cont`、`next` 或 `step` 命令时，可以恢复程序执行。

# 16.1.2 使用断点

为了识别断点，我们需要先列出程序。`list` 命令显示源程序，这意味着源文件必须存在于可执行文件相同的目录下。每次调用都会显示后续 10 行，但 `list` 也可以配合范围（如 `list 11,20`）来显示任何代码段：

```bash
gdb list 11,20
n = 1;

printf("Enter a multiword string: ");
scanf("%[^\n]", buf);   /* 匹配除 \n 外的所有字符 */
clargs[0] = strtok(buf, DELIM);   /* 第一个单词 */
((clargs[n] = strtok(NULL, DELIM)) != NULL)
++;
/* 提取剩余单词 */
clargs[n] = NULL;   /* 将指针设置为 NULL */
```

由于程序没有产生输出，我们首先想在第 16 行设置一个断点，以评估 `clargs[0]` 和 `buf` 的值。`run` 执行程序：

```
(gdb) break 16
Breakpoint 1 at 0x400612: file parsing.c, line 16.
(gdb) run
Starting program: /home/smart/personal/project2/parsing
Enter a multiword string: There is a fly in the soup
```

```
Breakpoint 1, at parsing.c:16
clargs[0] = strtok(buf, DELIM);   /* 第一个单词 */
```

gdb 按照命令调用的顺序对所有断点和监视点进行编号。程序通过了 parsing.c 第 16 行的 1 号断点。此程序没有使用参数，但对于使用参数的程序，必须在 `run` 时指定参数（例如 `run < fool > foo`），而不是在调用 gdb 时。

此时，我们可以使用 `print` 或 `display` 命令检查两个变量：
