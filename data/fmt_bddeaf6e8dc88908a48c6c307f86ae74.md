
```c
1 /* ch15-badmem1.c --- do bad things with memory */
2
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 int main(int argc, char **argv)
7 {
8     char *p;
9     int i;
10
11     p = malloc(30);
12
13     strcpy(p, "not 30 bytes");
14     printf("p = <&s>\n", p);
15
16     if (argc == 2)
17         if (strcmp(argv[1], "-b") == 0)
18             p[42] = 'a';    /* touch outside the bounds */
19         else if (strcmp(argv[1], "-f") == 0) {
20             free(p);        /* free memory and then use it */
21             p[0] = 'b';
22         }
23     }
24
25     /* free(p); */
26
27     return 0;
28 }
```

该程序执行简单的命令行选项检查来决定如何错误行为：`-b` 会触及越界内存，`-f` 会尝试使用已释放的内存。（第 18 行和第 21 行分别是有风险的操作。）请注意，如果没有选项，指针永远不会被释放（第 25 行）；Electric Fence 不会捕获这种情况。

使用 Electric Fence 的一种保证在 Unix 和 GNU/Linux 系统上都能工作的方式是将其与程序静态链接。然后应该从调试器中运行该程序。（Electric Fence 的文档明确指出，Electric Fence 不应该与生产二进制文件链接。）以下会话演示了这个过程，并展示了两种命令行选项发生的情况：

```bash
$ cc -g ch15-badmem1.c -lefence -o ch15-badmem1     # 编译；静态链接
$ gdb ch15-badmem1                                    # 从调试器运行
gdb (gdb) 5.3
...  # 尝试 -b 选项
(gdb) run -b
Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -b
[New Thread 8192 (LWP 28021)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.   # SIGSEGV: GDB 打印位置
 (Switching to Thread 8192 (LWP 28021))
 0x080485b6 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:18
                                                    p[42] = 'a';       /* 触及越界内存 */
(gdb) run -f                                       # 现在尝试 -f 选项
The program being debugged has been started already.
Start it from the beginning? (y or n) y            # 是的，真的

Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -f
[New Thread 8192 (LWP 28024)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.          # 再次 SIGSEGV
 (Switching to Thread 8192 (LWP 28024))
 0x080485e8 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:21
                                                    p[0] = 'b';
```

在支持共享库和 `LD_PRELOAD` 环境变量的系统（包括 GNU/Linux）上，你不需要显式链接 `efence` 库。相反，`ef` shell 脚本安排以正确的设置运行程序。

虽然我们没有详细描述其机制，但 GNU/Linux（以及其他 Unix 系统）支持共享库，这是库例程的特殊版本，保留在磁盘上的单个文件中，而不是复制到每个可执行程序的二进制文件中。共享库在磁盘上节省一些空间，并且可以节省系统内存，因为使用共享库的所有程序共享同一个内存中的库副本。代价是程序启动较慢，因为程序和共享库在程序开始运行之前必须结合起来。（这通常对用户是透明的。）

`LD_PRELOAD` 环境变量导致系统的程序加载器（将可执行文件读入内存）在标准库之前链接一个特殊库。`ef` 脚本利用此功能来链接 Electric Fence 版本的 `malloc()` 套件。因此，甚至不需要重新链接。这个例子演示了 `ef`：

```bash
$ cc -g ch15-badmem1.c -o ch15-badmem1            # 正常编译
$ ef ch15-badmem1 -b                                 # 使用 ef 运行，转储核心

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>
/usr/bin/ef: line 20: 28005 Segmentation fault     (core dumped)
( export LD_PRELOAD=libefence.so.0.0.0; exec $* )

$ ef ch15-badmem1 -f                                 # 使用 ef 运行，再次转储核心

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>
/usr/bin/ef: line 20: 28007 Segmentation fault     (core dumped)
( export LD_PRELOAD=libefence.so.0.0.0; exec $* )

$ ls -l core*                                        # Linux 为我们提供单独的核心文件
-rw------- 1 arnold devel 217088 Aug 28 15:40 core.28005
-rw------- 1 arnold devel 212992 Aug 28 15:40 core.28007
```

GNU/Linux 创建在文件名中包含进程 ID 号的核心文件。在这种情况下，这种行为是有用的，因为我们可以单独调试每个核心文件：
