
必须定义 `_GNU_SOURCE` 宏，因为 `<utmp.h>` 头文件包含功能测试宏。功能测试宏可用于控制程序编译时系统头文件中暴露哪些定义。这对于创建可移植应用程序很重要，因为它可以防止非标准定义暴露在程序中。如果你从程序中删除 `_GNU_SOURCE` 的定义并尝试使用 `getutent_r()`，将会得到一个编译时错误，因为该函数在头文件中的声明受条件预处理器指令保护，该指令仅在定义了 `_GNU_SOURCE` 时才为真。它本质上具有以下形式：

```
#ifdef __GNU_SOURCE
    extern int getutent_r (struct utmp *__buffer, struct utmp **__result) __THROW;
    /* more stuff here */
#endif
```

如果你将 `__GNU_SOURCE` 的定义放在 `include` 指令之后，它将毫无用处，因为当 `gcc` 预处理头文件时它尚未定义，因此在这种情况下你也会收到错误信息。

`feature_test_macros` 手册页描述了使用这些宏所需了解的一切。

这个线程安全版本的 `who` 的主程序，我们称之为 `who4.c`，与 `who3.c` 几乎相同：

```
1 列出 who4.c
2 #include <stdio.h>
3 #include <stdlib.h>
4 #include <unistd.h>

#define _GNU_SOURCE
#include <utmp.h>
#include <fcntl.h>
#include <time.h>

int main(int argc, char* argv[])
{
    struct utmp utbuf, *utbufp;
    int utmpfd;

    if ( (argc > 1) && (strcmp(argv[1], "wtmp") == 0) )
        utmpname(_PATH_WTMP);
    else
        utmpname(_PATH_UTMP);

    setutent();
    while( getutent_r(&utbuf, &utbufp) == 0 )
        show_info( &utbuf );
    endutent();
    return 0;
}
```

### 2.6.8 一个符合 POSIX 标准的版本

还有另一个版本的 `who` 程序，名为 `who_p.c`，位于服务器上本章的 `demos` 目录中。这个版本的独特之处在于它使用了符合 POSIX 标准的 `utmp` 接口。`utmp` 结构在所有 UNIX 版本中并不是标准的。我们上面描述的是 GNU 实现，也就是 Linux 系统上的实现。这个 GNU 版本包含在其他系统上可能不存在的成员。为了努力标准化 `utmp` 接口，自 2001 年以来的 POSIX 标准已将 `utmp` 结构的定义替换为 `utmpx` 结构。该结构仅保证具有以下成员：

| 类型 | 成员 | 描述 |
|------|------|------|
| char | ut_user[] | 用户登录名。 |
| char | ut_id[] | 未指定的初始化进程标识符。 |
| char | ut_line[] | 设备名称。 |
| pid_t | ut_pid | 进程 ID。 |
| short | ut_type | 条目的类型。 |
| struct timeval | ut_tv | 条目创建的时间。 |

此外，函数 `setutent()`、`getutent()` 和 `endutent()` 被相应的函数 `setutxent()`、`getutxent()` 和 `endutxent()` 所取代。一般来说，`utmpx` 结构可以定义与 `utmp` 结构不同的成员集合。实际上，Linux 系统将 `utmpx` 结构定义为与 `utmp` 结构相同，除非定义了 `_GNU_SOURCE` 宏。此外，Linux 系统定义了比 POSIX 更大的 `ut_type` 成员允许值集合。旨在可移植的程序可以使用功能测试宏进行条件编译，以在编译时检测系统上实际存在的结构。`who_p.c` 程序演示了如何做到这一点，但未包含在这些笔记中。

### 2.6.9 总结

前面的一组 `who` 命令的实现表明，可以通过手册页和头文件来了解足够多的关于某个命令的信息，从而实现它。`utmp` 接口并非在每个 UNIX 系统上都相同，因此有几种不同的方法来解决这个问题。例如，可以使用 GNU 的、非 POSIX 的、线程安全的接口版本，或者使用符合 POSIX 标准的 `utmpx` 接口。也可以使用较低层的系统调用，例如 `read()`，来直接访问 `utmpx` 或 `utmp` 结构。真正可移植的解决方案将使用功能测试宏，根据程序将要运行的系统来条件编译代码。这个练习一路上引入了各种概念，但我们还没有完成。稍后我们将回到这个问题，并提供一个更高效的解决方案。

## 2.7 以读/写模式使用文件

许多应用程序需要以读取和写入两种模式打开文件。`logout` 命令就是一个很好的例子。`logout` 命令必须更新 `utmp` 文件，在文件中找到要更新的记录（即读取它），然后修改该记录（写入它）。大多数 I/O 库允许以读写模式打开文件。

### 2.7.1 以读/写模式打开文件

回想一下，`open()` 系统调用的第二个参数是一组存储在整数中的标志，并且这些标志必须包含一个访问模式标志：`O_RDONLY`、`O_WRONLY` 和 `O_RDWR`。如果访问模式设置为 `O_RDWR`，则文件以读/写模式打开。在读/写模式下，进程可以读取文件并向文件写入。文件不会被截断，而如果以

`the O_CREAT` 标志。相反它是以当前位置指针指向文件开始处的方式打开的。当前位置指针是打开文件结构的一个成员，该数据结构是在内核打开文件时创建的。它指向文件中下一个要读取或写入的字节的位置。

例如，要打开路径存储在 C 字符串 `file_to_open` 中的文件，可以写：

```c
if ((fd = open(file_to_open, O_RDWR)) == -1) {
    perror(file_to_open);
    // handle error here
}
```

### 2.7.2 Logout Records

当用户从 UNIX 系统注销时，内核会执行一些记账任务。其中一项任务是更新 `utmp` 文件以指示用户已注销。特别是，它必须通过将 `ut_type` 成员从 `USER_PROCESS` 更改为 `DEAD_PROCESS` 来更改登录会话的 `utmp` 记录。它还必须将 `ut_time` 成员更改为当前时间并将 `ut_user` 和 `ut_host` 成员清零。

简而言之，注销过程必须执行以下操作：

- 1. 打开 `utmp` 文件以进行读取和写入。
- 2. 读取 `utmp` 文件直到找到注销发生的终端的记录。
- 3. 修改进程内存中 `utmp` 记录的副本，并用修改后的记录替换文件中的 `utmp` 记录，即修改 `utmp` 文件。
- 4. 关闭 `utmp` 文件。
