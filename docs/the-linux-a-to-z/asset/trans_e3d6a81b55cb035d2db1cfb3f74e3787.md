
```
lastpid = pid;
}
else
{
    /* 3 */
    if (ptr->infd==0 && backgnd==TRUE)
        ptr->infd = open("/dev/null", O_RDONLY);

    /* 4 */
    if (ptr->infd!=0)
    {
        close(0);
        dup(ptr->infd);
    }

    if (ptr->outfd!=1)
    {
        close(1);
        dup(ptr->outfd);
    }

    /* 5 */
    if (backgnd==FALSE)
    {
        signal(SIGINT, SIG_DFL);
        signal(SIGQUIT, SIG_DFL);
    }

    /* 6 */
    for (i = 3; i<OPEN_MAX; ++i)
        close(i);

    /* 7 */
    execvp(ptr->av[0], ptr->av);
    exit(1);
}
}
```

forkexec() 函数以指向即将执行的简单命令相关联的 struct cmd 的指针作为参数。请记住，该结构包含命令将用于其标准输入和标准输出的文件描述符（尽管重定向尚未发生），它还包含指向命令行参数（包括命令名本身）的指针数组，这些参数将成为命令的 argv 参数。

编号注释在此函数中描述如下：

- 1. 第一个任务是 fork() 一个子进程并存储返回的进程 ID。
- 2. 在父进程中，如果此命令行要在后台运行，则每个子进程的进程 ID 在创建时将被显示。每个子进程的进程 ID 也存储在变量 lastpid 中。随着命令行中的简单命令从左到右执行，lastpid 的最终值将是最后创建的简单命令（即最右边的简单命令）的进程 ID。这是 wait() 在此命令行要在前台执行时将查找的进程 ID。
- 3. 在子进程中，首先发生的是一个相当微妙的测试。如果这是要在后台运行的命令行，则必须防止它从键盘获取输入。事实上，只有管道中的第一个简单命令才能从键盘获取输入，因为其余所有命令都将通过管道、重定向获取其标准输入。因此，如果这是要在后台运行的命令行，并且将作为当前简单命令的标准输入的文件描述符（infd）仍设置为键盘（infd==0），那么这必须是管道中的第一个简单命令，并且需要将其标准输入从键盘转移走，以确保它不会尝试从中读取。最简单、最安全的方法就是在这种情况下设置自动输入重定向。用于此重定向的最明显的文件就是标准文件 /dev/null，如果进程尝试从中 read()，它会立即返回 EOF。使用这种简单机制可以使微型 shell 不必参与任何类型的作业控制功能。
- 4. 下一个阶段实际上是通过操作文件描述符来执行输入和输出重定向，如果它们已从默认值更改。
- 5. 如果这是前台管道，则当前简单命令被设置成可以由键盘上的中断或退出信号终止，除非它随后做出特定的相反规定。
- 6. 下一步是关闭除标准输入、输出和错误输出之外的所有文件描述符，以便此进程无法干扰 shell 设置的任何管道或 I/O 重定向文件，除了它应该通过标准文件描述符 0、1 和 2 看到的那些。
- 7. 最后，简单命令由 execvp() 系统调用执行，使用其 av[] 数组中的值作为命令名和 argv 指针。

### 20.2.8 check 函数

```
check(char *ptr)
{
    char *tptr;

    while (*lineptr==' ')
        lineptr++;

    tptr = lineptr;

    while (*ptr!='\0' && *ptr==*tptr)
    {
        ptr++;
        tptr++;
    }

    if (*ptr!='\0')
        return(FALSE);
    else
    {
        lineptr = tptr;
        return(TRUE);
    }
}
```

check() 函数将作为参数传递给它的字符串与从 lineptr 位置开始的 line[] 数组中的字符进行比较。如果找到匹配项，则 lineptr 会向前移动超出匹配的字符，并返回 TRUE 值。如果 check() 未找到匹配项，则返回 FALSE 值，并且 lineptr 保持不变，以便可以从 line[] 数组中的同一位置开始对其他字符串进行检查。

### 20.2.9 getname 函数

```
getname(char *name)
{
    int i;

    for (i = 0; i<MAXNAME; ++i)
    {
        switch (*lineptr)
        {
        case '>':
        case '<':
        case '|':
        case '&':
        case ',':
        case '\n':
        case '\t':
            *name = '\0';
            return;

        default:
            *name++ = *lineptr++;
            break;
        }
    }

    *name = '\0';
}
```

此函数只是将文件名最多复制 MAXNAME 个字符到其 name 参数指向的 char 数组中。

## 练习

- 1. 使用 bash 和 tsh 输入以下每条包含错误的命令行，看看 shell 会做什么。你观察到的结果是你期望的吗？你希望的是什么？尝试其他命令和其他 shell（如果有的话），你现在怎么想？
- 2. 为微型 shell 添加一个简单的机制，使其能够执行内置命令。
- 3. 为微型 shell 添加 cd 和 history 内置命令，并允许它使用 ! 操作符重复历史列表中的以前命令。

```
$ cat /etc/passwd >output1 >output2
$ cat </etc/passwd </etc/motd
$ cat /etc/passwd | | grep root
$ cat /etc/passwd >output3 | grep root
```

## 答案

- 1. 糟糕……。假设你认为错误消息是家常便饭，标准 shell 的表现并不太好，对吧？
- 2. 添加内置命令的简单方法是在 parse() 函数顶部添加以下代码：

```
parse()
{
```
```c
int i;

if (builtin())
    return 0;

/* 1 */
command(0);
/* etc...*/
```
```

然后编写一个 builtin() 函数，该函数检查内置命令关键字，并在找到它们时执行任何所需的操作。如果 builtin() 函数返回 true（非零）值以表示找到了内置命令，则 parse() 将在该点返回，而不会尝试进一步执行命令行：

```c
builtin()
{
    if (check("exit"))
        exit(0);
    else
        return 0;
}
```
- 3. 要添加这三个额外的内置命令，可以按如下方式修改 builtin() 函数：

```c
builtin()
{
    if (check("exit"))
        exit(0);
    else if (check("cd"))
        return do_cd();
    else if (check("history"))
        return do_history();
    else if (check("!"))
        return do_repeat_command();
    else
        return 0;
}
```

do_cd() 函数然后可以从 line[] 数组中提取目录名并使用 chdir() 系统调用进行更改。对于 ! 和 history 命令，你需要修改 getline() 函数，以便在键盘上输入的行在输入时被存储。然后 history 命令可以列出存储中的所有命令，而 ! 命令可以将适当的存储命令复制回 line[] 数组。do_repeat_command() 然后可以从 builtin() 返回零，以便 line[] 将被正常解析。

## 杂项系统调用

这里有远多于我有空间详细描述的系统调用（目前有一百四十多个）。然而，在结束之前，我们仍有几个需要查看的系统调用。

从 shell 命令提示符可以执行的所有命令只能通过调用一些底层系统调用来执行其操作，以从操作系统获取所需的系统服务。在若干情况下，这意味着一个专门用于提供特定服务的新系统调用。

下一组系统调用属于此类。

### 21.1 umask 系统调用

你会记得 umask 命令用于设置文件创建掩码。umask 值在每次创建文件时都会使用，作为安全措施，以确保你运行的进程无法创建具有比你想要给予更多访问权限的新文件。这是通过在代表你创建的任何文件的模式位中重置 umask 值中的权限位来实现的。

umask 命令在内部由同名底层系统调用的调用实现：

```
#include <sys/types.h>
#include <sys/stat.h>

mode_t umask(mode_t mask);
```

对 umask() 系统调用的调用将文件创建掩码设置为指定的掩码值。仅保存 mask 中的权限位，其他位的值将被忽略。

umask() 的返回值只是文件创建掩码的先前值，因此此系统调用既可用于获取也可用于设置所需值。
