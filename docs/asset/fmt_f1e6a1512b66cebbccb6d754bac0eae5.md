
```c
int traceChildProcess(pid_t tracedPid)
{
    int status = 0; // 此函数的返回值
    int sRC = 0; // 系统调返回值
    int status = 0; // 停止子进程的状态
    pid_t stoppedPid = 0; // 停止子进程的 PID
    struct user_regs_struct registers;

    while (stoppedPid = waitpid(tracedPid, &status, 0) != -1)
    {
        src = ptrace(TRACE_GETREGS, stoppedPid, 0, &registers);
        if (-1 == src)
        {
            printf("ptrace failed with request \"TRACE_GETREGS\":%s\n", strerror(errno));
            mRC = 1;
            goto exit;
        }

        if (registers.eax == -ENOSYS)
        {
            fprintf(stderr, " ");
        } else {
            if (registers.eax < 0) {
                // 错误情况
                fprintf(stderr, "Err: %s\n", strerror(abs(registers.eax)));
            } else {
                // 返回码
                fprintf(stderr, "%08x\n", registers.eax);
            }
        }

        switch (registers.eax)
        {
            case NR_open:
                // 获取文件名
                fileName[1024] = "";
                readString(stoppedPid, (void *)registers.ebx, fileName, 1024);
                fprintf(stderr, "%s, %08x, %08x\n", fileName, registers.ecx, registers.edx);
                break;
            case NR_exit:
                // 停止子进程退出，所以
                fprintf(stderr, "%08x, %08x, %08x\n", registers.ebx, registers.ecx, registers.edx);
                goto exit;
            default:
                fprintf(stderr, "%08x, %08x, %08x", registers.ebx, registers.ecx, registers.edx);
                break;
        }
    }
    ptrace(TRACE_SYSCALL, stoppedPid, 0, 0);
exit:
    fclose(stdin);
    fclose(stderr);
    fclose(stdout);
    exit(1);
    return mRC;
}
```

```c
int main(int argc, char *argv[])
{
    int mRC = 0; // 此函数的返回值
    pid_t cpid; // 子进程 ID
    cpid = fork();

    if (cpid > 0) {
        // 父进程
        traceChildProcess(cpid);
    } else if (cpid == 0) {
        // 子进程
        spawnChildProcess(argc, &argv[1]);
    } else {
        fprintf(stderr, "Could not fork child (%s)\n", strerror(errno));
        mRC = 1;
    }

    return mRC;
}
```

## 2.6.2 系统调用追踪代码解释

`spawnChildProcess()` 函数派生子进程并运行 `ptrace(TRACE_TRACEME)` 以确保子进程在进入或退出系统调用时停止。该函数执行被追踪的进程。

`traceChildProcess()` 函数等待子进程停止（通常是因为系统调用进入或退出），并使用 `ptrace(TRACE_GETREGS)` 获取寄存器信息。特别是，它测试 `eax` 寄存器以判断进程是处于进入还是退出状态。如果 `eax` 的值不等于 `-ENOSYS`，则假设进程停止在调用出口处。`eax` 为正值表示系统调用执行成功，返回码将包含成功的返回码。如果返回码为负数，则假设发生了错误，并在 strace 输出中打印错误。

当系统调用进入时，原始 `eax` 将包含系统调用号。当识别出系统调用后，系统调用约定提供了参数信息：

`readString(stoppedPid, (void *)registers.ebx, fileName, 1024); fprintf(stderr, "%s, %08x, %08x\n", fileName, registers.ecx, registers.edx);`

# 第3 章

## /proc 文件系统

## 3.1 引言

Linux 如今如此受欢迎的一个大原因是，它结合了来自其 UNIX 祖先的许多优秀特性。其中一个特性就是 `/proc` 文件系统，它继承自 System V，并且是所有主流发行版所包含的内核的标准部分。由于某些发行版提供了其他发行版不具备的内容，因此并没有标准的 `/proc` 规范；因此，使用时应保持一定的谨慎。

`/proc` 文件系统是 Linux 提供的检查和配置操作系统内部运行机制的最机制之一。它可以被视为直接观察内核数据结构和内核对系统视图的窗口。对于用户来说，它就像 `/home` 一样是一个文件系统，因此可以使用所有常用的文件操作程序和系统调用来处理它，如 `cat(1)`、`more(1)`、`grep(1)`、`open(2)`、`read(2)` 和 `write(2)`¹¹。如果权限足够，通过从 shell 提示符中使用 `>` 字符将输出重定向到文件，或在应用程序中调用系统调用 `write(2)`，也可以轻松地向某些文件写入值。

本章的目标不是作为 `/proc` 文件系统的详尽参考，因为那本身就会是一部著作。其目标是指出并检查一些与问题确定和系统诊断相关的高级特性和技巧。为了更通用的参考，我建议阅读 `proc(5)` man 手页。

> 注意：如果你在系统上安装了内核源码，我建议阅读 `/usr/src/linux/Documentation/filesystems/procfs.txt`。

¹ 当 Linux 操作名称后面带有括号中的数字时，该数字直接引用 man 章节号。第 1 节用于可执行程序或 shell 命令，第 2 节用于系统调用（内核提供的函数）。输入 `man 2 read` 将读取第 2 节的 read 系统调用。

## 3.2 进程信息

除了查看和操作系统信息外，获取进程信息是 `/proc` 文件系统的另一个放异彩的地方。当你查看 `/proc` 下的文件列表时，你会立即注意到大量由数字标识的目录。这些数字代表进程 ID（PID），并包含关于该 PID 的更详细信息。所有的 Linux 系统都有 `/proc/1` 目录。ID 为 1 的始终是 "init" 进程，它是系统启动期间第一个启动的进程。尽管这是一个特殊程序，但它和其他进程一样是一个进程，`/proc/1` 目录将包含与其他任何进程相同的信息，包括你用于查看内容以及任何其他目录的 `ls` 命令！接下来的章节将详细介绍在 `/proc/<pid>` 目录中可以找到的最有用信息，例如查看 CPU 和内存配置信息，以及理解可以增强应用程序和系统故障排除的设置。

### 3.2.1 /proc/self
