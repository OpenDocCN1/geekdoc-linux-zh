
默认的`nice`值是`0`。`nice`值的允许范围是`–20`到`19`。这需要一些时间来适应。值越负，进程的优先级越高：`–20`是最高优先级（最不友好），`19`是最低优先级（最友好）。

`inc`参数是更改`nice`值的增量。使用`nice(0)`可以在不改变值的情况下获取当前值。如果`current_nice_value + inc`的结果超出`–20`到`19`的范围，系统会强制结果在该范围内。

> ¹ 这种进程往往表现出幼稚的行为。

#### 9.1.1.2 文件偏移量共享与 `read()`

```bash
$ cat data              # 显示演示数据文件内容
line 1
line 2
line 3
line 4

$ ls -l test1 ; cat test1
-rwxr-xr-x  1 amold   devel  93 Oct 20 22:11 test1
#!/bin/sh
read line ; echo p: $line   # 在父 shell 中读取一行并打印
( read line ; echo c: $line )  # 在子 shell 中读取一行并打印
read line ; echo p: $line   # 在父 shell 中读取一行并打印
$ test1 < data              # 运行该程序
p: line 1                   # 父进程从开头开始
c: line 2                   # 子进程从父进程停止的地方继续
p: line 3                   # 父进程从子进程停止的地方继续
```

`test1`的第一条可执行语句从标准输入读取一行，改变文件中的偏移量。`test1`的第二条语句在一个子shell中运行括号内包含的命令。这是一个由`fork()`创建的独立shell进程。子shell从父进程继承标准输入，包括当前的文件偏移量。该进程读取一行并更新到文件中的共享偏移量。当第三条语句在父shell中读取文件时，它从子进程停止的地方开始。

尽管`read`命令是shell的内建命令，但外部命令的行为方式相同。一些早期的Unix系统有一个`line`命令，用于读取一行输入（一次一个字符！）以便在shell脚本中使用；如果文件偏移量不是共享的，就不可能在循环中使用这样的命令。

#### 9.1.3.1 POSIX 与现实

返回值是新的`nice`值，如果发生错误则为`-1`。由于`-1`也是一个有效的`nice`值，因此在调用`nice()`时，你必须先将`errno`显式设置为零，然后再检查它，以确定是否出现了问题：

```c
int niceval;
int inc = /* whatever */;

errno = 0;
if ((niceval = nice(inc)) < 0 && errno != 0) {
    fprintf(stderr, "nice(%d) failed: %s\n", inc, strerror(errno));
    /* other recovery */
}
```

如果`inc`为负值且进程未以`root`身份运行，此示例可能会失败。

`Linux`使用的`-20`到`19`的`nice`值范围是历史遗留的；其历史至少可以追溯到`V7`。`POSIX`用更间接的语言表达了这种情况，这在保持历史兼容性的同时允许了实现灵活性。这也使得标准更难阅读和理解，但这就是你要读这本书的原因。那么，以下是`POSIX`对此的描述。

首先，系统维护的进程`nice`值范围为`0`到`(2 * NZERO) - 1`。常量`NZERO`定义在`<limits.h>`中，且至少为`20`。这给了我们`0-39`的范围。

其次，正如我们描述的，当前`nice`值与`incr`增量之和被强制调整到这个范围内。

最后，`nice()`的返回值是进程`nice`值减去`NZERO`。如果`NZERO`值为`20`，这就得出了我们最初描述的`-20`到`19`的原始范围。

结果是，`nice()`的返回值实际上范围是从`-NZERO`到`NZERO-1`，最好根据你的代码中的符号常量来编写。不过，实际上，你不太可能找到一个`NZERO`不是`20`的系统。

#### 9.1.4 启动新程序：`exec()` 族

一旦新进程开始运行（通过`fork()`），下一步就是让不同的程序在该进程中运行。有多个函数用于实现不同的目的：

```c
#include <unistd.h>
int execve(const char *filename, char *const argv[], char *const envp[]);
int execl(const char *path, const char *arg, ...);
int execlp(const char *file, const char *arg, ...);
int execlp(const char *path, const char *arg, ..., char *const envp[]);
int execv(const char *path, char *const argv[]);
int execvp(const char *file, char *const argv[]);
```

我们将这些函数称为“`exec()`族”。没有名为`exec()`的函数；相反，我们使用这个函数名来指代上述列出的任何函数。与`fork()`一样，“`exec`”在Unix术语中用作动词，意味着执行（运行）一个程序，也用作名词。

##### 9.1.4.1 `execve()` 系统调用

最简单的函数是`execve()`。它也是底层系统调用。其他的是包装函数，稍后将解释。

```c
int execve(const char *filename, char *const argv[], char *const envp[])
```

`filename`是要执行的程序名称。它可以是完全或相对路径名。该文件必须是内核可理解的可执行格式。现代系统使用`ELF`（Extensible Linking Format，可扩展链接格式）可执行格式。GNU/Linux理解`ELF`和几种其他格式。如果使用以`#!`特殊首行命名了解释器的可解释脚本，可以使用`execve()`执行它们。（不以“`#!`”开头的脚本会失败。）第`1.1.3`节“可执行文件”，第`7`页，提供了“`#!`”的使用示例。

`argv`是标准的C参数列表——一个指向参数字符串指针的数组，包括用于`argv[0]`的值，并以`NULL`指针结束。

`envp`是用于新进程的环境变量，其布局与`environ`全局变量相同（参见第`2.4`节“环境变量”，第`40`页）。在新程序中，此环境成为`environ`的初始值。

`exec()`调用不应返回。如果返回了，则出现了问题。最常见的情况是，请求的程序不存在，或者存在但不可执行（分别对应`errno`的`ENOENT`和`EACCES`）。还可能发生许多其他错误；参见`execve(2)`手册页。

假设调用成功，当前进程地址空间的内容将被丢弃。（内核会先安排将`argv`和`envp`数据安全地保存在某个地方。）内核加载新程序的可执行代码，以及任何全局和静态变量。接下来，内核使用传递给`execve()`的环境变量初始化环境，然后调用新程序的`main()`例程，传入传递给`execve()`的`argv`数组。它统计参数的数量，并将该值通过`argc`传递给`main()`。

此时，新程序正在运行。它不知道（也无法查明）之前在该进程中运行的是什么程序。请注意，进程ID不会改变。`exec`时许多其他属性保持不变；我们稍后会详细介绍这一点。

做一个宽松的类比，`exec()`之于进程，就像人生角色之于人。在一天中的不同时刻，同一个人可能充当父母、配偶、朋友、学生或工作者、商店顾客等角色。然而，执行不同角色的始终是同一个底层的人。同样，进程——其`PID`、打开的文件、当前目录等——不变，而它所执行的特定任务——使用`exec()`运行的程序——可以改变。

##### 9.1.4.2 包装函数：`execl()` 等

另外五个作为包装函数的函数，提供了更便捷的`execve()`接口。第一组函数都接受参数列表，每个参数作为显式函数参数传递：

```c
int execl(const char *path, const char *arg, ...)
```

第一个参数`path`是要执行文件的路径名。后续参数（从`arg`开始）是要放置在`argv`中的各个元素。与前面一样，必须显式包含`argv[0]`。必须传递一个终止`NULL`指针作为最后一个参数，以便`execl()`知道参数列表在哪里结束。新程序继承当前程序`environ`变量中的任何环境。
