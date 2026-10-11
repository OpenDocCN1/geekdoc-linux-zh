
## df

| 文件系统 | 1K 块 | 1K 已用 | 1K 可用 | 使用率% | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda2 | 6198436 | 5136020 | 747544 | 88% | / |
| /dev/hda5 | 61431520 | 27720248 | 30590648 | 48% | /d |
| none | 256616 | 0 | 256616 | 0% | /dev/shm |

tmpfs 文件系统类型提供了一块 RAM 盘，即内存的一部分，其使用方式类似于磁盘。此外，tmpfs 文件系统利用 Linux 内核的虚拟内存机制，使其能够突破固定大小限制而增长。如果你的系统中拥有大量 RAM，这种方法可以带来显著的性能提升。为了测试性能，我们首先从 /usr/share/dict/linux.words 文件开始，该文件是一个按排序排列的正确拼写单词列表，每行一个单词。然后我们将该文件随机化，使其不再排序，并创建了一个包含该随机版本文件 500 份副本的更大文件：

```bash
$ ls -l /tmp/randwords.big

-rw-r--r-- 1 arnold devel 204652500 Sep 18 16:02 /tmp/randwords.big
```

有多少个单词？超过 2200 万个！

然后我们对该文件进行了排序，首先使用默认的 /tmp 目录，然后设置 TMPDIR 为 /dev/shm：⁵

```bash
$ time sort /tmp/randwords.big > /dev/null

real 1m32.566s
user 1m23.137s
sys 0m1.740s

$ time TMPDIR=/dev/shm sort /tmp/randwords.big > /dev/null

real 1m28.257s
user 1m18.469s
sys 0m1.602s
```

有趣的是，使用 RAM 盘仅比使用常规文件略快一点。（在一些进一步的测试中，它甚至更慢！）我们推测内核的缓冲区缓存（参见 4.6.2 节，“使用 creat() 创建文件”，第 109 页）在此发挥作用，相当有效地加速了文件 I/O。⁶

RAM 盘有一个显著的缺点：它受限于系统中配置的 `swap space`（交换空间）大小。⁷ 当我们尝试对一个包含随机单词文件 1,000 份副本的文件进行排序时，RAM 盘空间耗尽，而常规的 `sort` 则成功完成。

在自己的程序中使用 TMPDIR 很简单。我们提供以下大纲：

```c
const char template[] = "myprog.XXXXXX";
char *tmpdir, *tfile;
size_t count;
int fd;

if ((tmpdir = getenv("TMPDIR")) == NULL)
    tmpdir = "/tmp";  // 如果存在则使用 TMPDIR 值
                     // 否则，默认为 /tmp
count = strlen(tmpdir) + strlen(template) + 2;  // 计算文件名大小
tfile = (char *) malloc(count);                 // 为其分配空间
if (tfile == NULL)
    /* recover */                               // 检查错误

sprintf(tfile, "%s/%s", tmpdir, template);       // 创建最终模板
fd = mkstemp(tfile);                             // 创建并打开文件
/* 通过 fd 使用模板 ... */
close(fd);                                        // 清理
unlink(tfile);
free(tfile);
```

根据应用程序的需求，你可能希望在打开文件后立即取消链接（unlink）该文件，而不是将其作为清理过程的一部分。

## 12.4 自杀式退出：abort()

有时候，程序确实无法继续运行。通常，最好的做法是生成一条错误消息并调用 `exit()`。然而，特别是对于可能是编程问题的错误，仅仅退出是不够的，还需要生成核心转储（core dump），以便将正在运行的程序的状态保存到文件中，供日后通过调试器检查。这正是 `abort()` 函数的职责：

```c
#include <stdlib.h>
void abort(void);   /* ISO C */
```

abort() 函数向进程本身发送 SIGABRT 信号。即使 SIGABRT 被阻塞或忽略，这种情况也会发生。随后，SIGABRT 的正常行为（即生成核心转储）便会执行。

abort() 运作的例子是本章开头描述的 assert() 宏。当 assert() 发现其表达式为假时，它会打印一条错误消息，然后调用 abort() 来转储核心。

根据 C 标准，abort() 是否执行任何清理操作是依赖于实现的。在 GNU/Linux 中它会执行：在程序退出之前，所有 <stdio.h> FILE * 流都会被关闭。但请注意，对于使用基于文件描述符系统调用的打开文件，不会执行任何操作。（如果打开的所有文件只是文件或管道，则无需执行任何操作。虽然我们对此不予讨论，但文件描述符也用于网络连接，而不干净地关闭它们是不当做法。）

## 12.5 非局部跳转

> “直接进监狱。不要经过 GO。不要领取 200 美元。”
> ——《大富翁》——

你肯定知道 goto 是什么：一种将控制流转移到当前函数内其他位置标签处的机制。当适度使用时，goto 语句有助于提高函数的可读性和正确性。（例如，当所有错误检查都使用 goto 跳转到函数末尾的一个标签（如 clean_up）时，该标签处的代码随后会进行清理工作 [关闭文件等] 并返回。）但如果不当使用，goto 语句可能会导致所谓的“意大利面条式代码”，其逻辑变得无法跟踪。

C 语言限制了 goto 语句只能跳转到当前函数内的标签。许多 Algol 家族语言（如 Pascal）允许 goto“跳出”嵌套函数，进入先前的调用者函数。然而在 C 中，在该语言本身的语法范围内，没有办法跳转到不同函数中的位置，即使是调用者函数也是如此。这种跳转被称为非局部跳转（nonlocal goto）。

非局部跳转为什么有用？考虑一个读取命令并处理它们的交互式程序。假设用户启动了一个长时间运行的任务，感到沮丧或改变了主意，然后按下 CTRL-C 生成 SIGINT 信号。当信号处理程序运行时，它可以跳回主读取-命令-并处理循环的开始处。ed 行编辑器提供了这个概念的一个直接示例：

```bash
$ ed -p '> ' sayings            启动 ed，使用 '> ' 作为提示符
sayings: No such file or directory
> a                               追加文本
Hello, world
Don't panic
^C                                生成 SIGINT
?                                 “通用”错误消息
> 1,$p                            ed 返回命令循环
Hello, world                      '1,$p' 打印所有行
Don't panic
> w                               保存文件
25
> q                               完成
```

在内部，ed 在命令循环之前设置一个返回点，然后信号处理程序执行一个非局部跳转回到该返回点。

### 12.5.1 使用标准函数：setjmp() 和 longjmp()

非局部跳转是通过 setjmp() 和 longjmp() 函数实现的。这些函数有两种形式。传统的例程由 ISO C 标准定义：

```c
#include <setjmp.h>         ISO C
int setjmp(jmp_buf env);
void longjmp(jmp_buf env, int val);
```

jmp_buf 类型在 <setjmp.h> 中 typedef 定义。setjmp() 将当前“环境”保存到 env 中。env 通常是一个全局或文件级静态变量，以便可以从被调用的函数中使用。此环境包含跳转到调用 setjmp() 位置所需的所有信息。jmp_buf 的内容本质上是依赖于机器的；因此，jmp_buf 是一个不透明类型（opaque type）：你使用它而无需知道其内部内容。

当调用 setjmp() 将当前环境保存到 jmp_buf 时，它返回 0。当使用非局部跳转到达此处时，它返回非零值：

```c
jmp_buf command_loop;            在全局层级
... 然后在 main() 中 ...
if (setjmp(command_loop) == 0)   状态保存正常，继续执行
;
else                              我们通过非局部跳转到达此处
  printf("?\n");                 ed 的著名消息
... 现在启动命令循环 ...
```

longjmp() 执行跳转。第一个参数是一个必须已通过 setjmp() 初始化的 jmp_buf。第二个是一个非零整数值，setjmp() 在原始环境中将返回该值。这样就可以区分是设置环境还是通过非局部跳转到达。

C 标准规定，即使 longjmp() 使用 0 作为第二个参数调用，setjmp() 仍返回非零值。在这种情况下，它改为返回 1。

能够传递一个整数值并让 setjmp() 的返回值返回该值是很有用的；它允许用户级代码区分跳转的原因。例如，gawk 利用此功能来处理循环内的 break 和 continue 语句。（awk 语言故意在循环语法上类似于 C，包括 while、do-while 和 for 循环，以及 break 和 continue。）setjmp() 的使用如下所示（来自 gawk 3.1.3 发行版中的 eval.c）：

```c
507   case Node_K_while:
508       PUSH_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
509
510       stable_tree = tree;
511       while (eval_condition(stable_tree->lnode)) {
512           INCREMENT(stable_tree->exec_count);
513           switch (setjmp(loop_tag)) {
514               case 0: /* 正常非跳转 */
515                   (void) interpret(stable_tree->rnode);
516                   break;
517
518               case TAG_CONTINUE: /* continue 语句 */
519                   break;
520
521               case TAG_BREAK: /* break 语句 */
522                   RESTORE_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
523                   return 1;
524               default:
525                   cant_happen();
526               }
527           }
528       RESTORE_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
529       break;
```

这段代码片段代表一个 while 循环。第 508 行通过使用保存的 jmp_buf 变量栈来管理嵌套循环。第 511–524 行运行 while 循环（使用 C 的 while 循环！）。第 511 行测试循环的条件。如果条件为真，第 513 行根据 setjmp() 的返回值执行 switch。如果是 0（第 514–516 行），则第 515 行运行语句体。然而，当 setjmp() 返回 TAG_BREAK 或 TAG_CONTINUE 时，

