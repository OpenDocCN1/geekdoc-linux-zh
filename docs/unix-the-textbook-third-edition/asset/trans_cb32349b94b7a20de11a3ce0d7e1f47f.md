
在 writer 进程的终止中。此信号的默认动作是内核终止该进程并显示 “Broken pipe” 消息。当一个 reader 进程从一个 widowed pipe 中读取时，在 reader 读取完管道中的所有数据后，它会收到一个 end-of-file (eof) 消息。这意味着对 widowed pipe 的 read() 系统调用返回值为 0。

在所示的 broken_pipe.c 程序中，我们演示了如何创建一个 widowed pipe。该程序创建了一个管道，显示管道的读端和写端描述符，关闭管道的读端（即没有 reader 可以从管道读取），并使用管道的写端写入问候消息。我们编译该程序以生成 brokenp 文件中的可执行代码。程序的执行在它尝试在关闭读端后向管道写入之前工作得完美。write() 系统调用会生成 SIGPIPE 信号，并且由于内核的默认动作，在程序终止之前会显示 “Broken pipe” 消息。

```
% cat broken_pipe.c
#include <unistd.h>

int main(void)
{
    int data_channel[2], nw;

    if (pipe(data_channel) == -1) {
        perror("Pipe failed");
        exit(1);
    }

    printf("The pipe descriptors are: \n");
    printf("      Read end: %d\n", data_channel[0]);
    printf("      Write end: %d\n", data_channel[1]);
    close(data_channel[0]);
    nw = write(data_channel[1], "Hello, world!\n", 14);
    printf("This and subsequent statements are never executed.\n");
    exit(0);
}
% gcc46 broken_pipe.c -w -o brokenp
% ./brokenp
The pipe descriptors are:
      Read end: 3
      Write end: 4
Broken pipe
%
```

请注意，程序的编译和执行是在 BSD 系统上完成的。在 Solaris 上，程序的编译和工作方式与 BSD 系统相同，只是它在终止进程时不会显示 “Broken pipe” 错误消息。你可以使用 signal() 调用拦截 SIGPIPE 信号，显示所需的错误

消息并终止程序。你将在本章末尾的一个问题中被要求这样做。

## EXERCISE 20.1

编译并运行上一节中的 create_pipe.c、pipe_talk.c、pipe_2way_talk.c 和 broken_pipe.c 程序，以确保它们在你的系统上按预期工作。

## 20.5 同一计算机上不相关进程之间的通信

同一台机器上的两个或多个相关或不相关进程可以使用多种 UNIX IPC 通道进行通信，包括命名管道（也称为 FIFO）和套接字。我们在本节讨论 FIFO，在第 20.6 节讨论套接字。之前，我们在第 9.15 节讨论过 FIFO。我们对该主题的处理集中在命令行使用 FIFO 将 shell 命令连接起来以执行现有命令无法完成的复杂任务上。在这里，我们讨论 FIFO 作为 IPC 通道的底层结构细节以及允许创建 FIFO 并使用它们的 UNIX 应用程序编程接口（API）。

如前所述，FIFO 是一个命名管道。它是一个在文件系统命名空间中具有名称的管道，具有关联的文件类型，包含其属性的相关内核数据结构，以及包含管道中传输数据的内存有界缓冲区。FIFO 的管道部分，即内存缓冲区，是在进程打开 FIFO 时创建的，并在进程关闭 FIFO 时被销毁。因此，与纯粹是内存对象且进程持久的管道不同，FIFO 是磁盘和内存对象的混合体。其管道部分是进程持久的，而名称部分是文件系统持久的。总结一下，当你创建一个 FIFO 时，内核会在内存中创建一个管道，并通过文件系统命名空间中的路径名以及包括 inode 在内的相关资源将其与文件系统连接起来。这使你能够将 FIFO 作为文件系统对象访问。

要将 FIFO 用作 IPC 通道，你需要用路径名创建它，然后以读、写或两者方式打开它。然而，正如预期的那样，就像管道一样，FIFO 也没有与之关联的文件指针。新的数据写入 FIFO 的当前末端，现有数据从 FIFO 的前端读取。
