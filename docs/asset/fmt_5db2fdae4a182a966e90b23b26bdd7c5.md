
`pathname` 是要执行的命令的完整路径。后面跟着一个可变长度的字符字符串指针列表。这些将成为新程序中 `argv` 指向的数组的内容。`execl()` 中的指针列表应以 `NULL` 指针结尾。以下示例程序使用 `execl()` 执行简单命令 - `ls -l`：

```
#include <stdio.h>

main()
{
    execl("/bin/ls", "ls", "-l", 0);
    printf("Can only get here on error\n");
}
```

The first parameter to `execl()` in this example is the full pathname to the `ls` command. This is the file whose contents will be run, provided the process has execute permission on the file. The rest of the `execl()` parameters provide the strings to which the `argv` array elements in the new program will point. In this example, it means that the `ls` program will see the string `ls` pointed to by its `argv[0]`, and the string `-l` pointed to by its `argv[1]`.

在此示例中，传递给 `execl()` 的第一个参数是 `ls` 命令的完整路径名。这是将被运行的文件的内容，前提是进程对该文件具有执行权限。`execl()` 的其余参数提供了新程序中 `argv` 数组元素将指向的字符串。在此示例中，这意味着 `ls` 程序将看到其 `argv[0]` 指向的字符串 `ls`，以及其 `argv[1]` 指向的字符串 `-l`。

Normally the `exec()` calls don't return. In general, they can't because their function is to replace the text and user data segments in the process that calls them for some other program -- so there will be nothing to return to!

通常 `exec()` 调用不会返回。一般来说，它们不能返回，因为它们的功能是用另一个程序替换调用它们的进程中的文本段和用户数据段——因此将没有东西可返回！

However, if the `exec()` calls fail for any reason (usually because the file you are trying to execute doesn't exist or because you don't have execute permission for it) then they will return so that you can have the opportunity to do something about the error.

然而，如果 `exec()` 调用因任何原因失败（通常是因为你要执行的文件不存在或因为你没有执行权限），那么它们将返回，以便你有机会处理错误。

In addition to making all these parameters available to the new program, the `exec()` calls also pass a value for the variable:

除了使所有这些参数对新程序可用之外，`exec()` 调用还传递变量的值：

```
extern char **environ;
```

This variable has the same format as the `argv` variable except that the items passed via `environ` are the values in the environment of the process (like any exported shell variables), rather than the command line parameters. In the case of `execl()`, the value of the `environ` variable in the new program will be a copy of the value of this variable in the calling process.

该变量的格式与 `argv` 变量相同，只是通过 `environ` 传递的项目是进程环境中的值（如任何导出的 shell 变量），而不是命令行参数。在 `execl()` 的情况下，新程序中 `environ` 变量的值将是调用进程中该变量值的副本。

The `execl()` version of `exec()` is fine in the circumstances where you can explicitly list all of the parameters, as in the previous example. Now suppose you want to write a program that doesn't just run `ls`, but will run any program you wish, and pass it any number of appropriate command line parameters. Obviously, `execl()` won't do the job.

在可以显式列出所有参数的情况下（如前一个示例），`exec()` 的 `execl()` 版本是可以的。现在假设你想编写一个程序，它不仅运行 `ls`，还会运行你想要的任何程序，并传递任意数量的适当命令行参数。显然，`execl()` 不能胜任这项工作。

The example program below, which implements this requirement, shows, however, that the system call `execv()` will perform as required:

然而，下面实现此要求的示例程序表明，系统调用 `execv()` 将按要求执行：

```
#include <stdio.h>

main(int argc, char **argv)
{
    if (argc==1)
    {
        printf("Usage: run <command> [<parameters>]\n");
        exit(1);
    }

    execv(argv[1], &argv[1]);
    printf("Sorry... couldn't run that!\n");
}
```

The prototype for `execv()` shows that it only takes two parameters, the first is the full pathname to the command to execute and the second is the `argv` value you

`execv()` 的原型显示它只接受两个参数，第一个是要执行的命令的完整路径名，第二个是 `argv` 值你

想要传递到新程序中。在之前的示例中，该值是从传递给 `run` 命令的 `argv` 值派生的，这样 `run` 命令就可以接收你传递给它的命令行参数值并直接传递下去。

下面是使用 `run` 命令的典型命令序列：

```
$ run ls -l mtos
Sorry... couldn't run that!
$ run /bin/ls -l mtos
total 2
drwxr-xr-x  2 pc     book      1024 Apr  2 20:11 tdd
drwxr-xr-x  2 pc     book      1024 Apr  2 20:11 tsh
```

注意第一次尝试的失败，这是因为在使用 `execv()`（或 `execl()`）时，你需要指定要运行命令的完整路径名，正如第二次尝试的结果所示。

这里的问题是迄今为止介绍的两种 `exec()` 版本在查找你指定的命令时不会使用 `PATH` 环境变量中的值。然而，正如你可能猜到的那样，确实存在使用该变量的 `exec()` 版本。它们被称为 `execlp()` 和 `execvp()`，与前一对完全相同，但它们还会使用 `PATH` 的值来查找所需的命令。

`exec()` 的最后两个版本与前两个相同（即不使用 `PATH`），但它们允许你手动指定在新程序中出现在 `environ` 中的值，而不是接受自动默认值。它们被称为 `execle()` 和 `execve()`。下面是所有六个 `exec()` 变体的列表，以及它们所接受的参数数量和类型：
