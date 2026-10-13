
// (parent)进程关闭输入描述符并从输出描述符读取数据：

`read(file_descriptors[INPUT], buf, sizeof(buf));`

### 命名管道

命名管道（也称为 FIFO）只能用于共享文件系统的进程之间的通信。匿名管道的优点可以在独立启动的进程之间进行通信（不需要 fork 新进程）。编写使用命名管道的应用程序时，以下 man 页将有用：

- `man 2 open`—打开用 `mkn` 创建的命名管道
- `man 2 read`—从管道读取
- `man 2 write`—写入管道

CD-ROM 上的 `src/IPC/PIPES` 目录包含两个示例程序 `read_pipe.c` 和 `write_pipe.c` 以及一个说明如何使用 UNIX `mknod` 工具设置命名管道的“read me”。我假设可以使用 UNIX `pipe` 系统调用创建匿名管道，但我发现命名管道更方便。命名管道用于以下示例。如果你复制了 `src` 目录，进入 `src/IPC/PIPES` 并执行以下命令：

```
mknod a_pipe p

make
```

`mknod` 工具用于创建特殊文件。`mknod` 在命令行上接受文件名之前的参数以及文件名之后的类型类型。参数 `p` 表明特殊文件 `a_pipe` 是 FIFO 文件。当使用 `mknod` 创建 FIFO 文件时，文件名之前不允许任何参数。

你可以在两个独立的窗口中运行 `read_pipe` 和 `write_pipe` 示例程序。正如 `read_pipe.c` 源码所示，打开并读取命名管道与读取“普通”文件完全一样：

```c
FILE * in_file;

char buf[80];

in_file = fopen("a_pipe", "r");

if (in_file == NULL) {
    perror("Error in fopen");
    exit(1);
}

read(buf, 1, 80, in_file);
printf("received from pipe: %s\n", buf);
close(in_file);
```

## 进程通信与网络编程
第三部分

系统实用函数 `perror` 既可以打印字符串消息参数（在本例中，为 "Error in fopen"），也可以打印最后一个错误。由于命名管道可以与标准文件 I/O 函数 `fopen`、`fread` 和 `fwrite` 使用，因此命名管道非常易用。此外，在 `write_pipe.c` 源文件中，我们向命名管道写入数据与写入“普通”文件相同：

```c
FILE * out_file;

char buf[80];

out_file = fopen("a pipe", "w");

if (out_file == NULL) {
    perror("Error opening pipe");
    exit(1);
}

sprintf(buf,"*this is test data for the named pipe example\n");
fwrite(buf, 1, 80, out_file);
close(out_file);
```

使用命名管道是两个访问相同文件的程序之间传递数据的简单方法。在阅读示例程序的源码时，你可以查阅 `fopen`、`fread`、`fwrite` 和 `fclose` 的 man 手页以获取这些系统调用的文档。这些示例程序仅通过 C 风格字符串传递数据。你可能还想通过管道传递二进制数据，例如 C++ 对象的结构体（如果结构体或对象不包含指向其他对象的指针或引用）。如果你在具有不同 CPU 类型的计算机之间传递二进制数据，你可能需要担心 `int`、`long`、`float` 等基本类型的数据兼容性以及结构体和 C++ 对象的对齐问题。如果你在为异构环境编写分布式应用程序，你可能想要使用 RPC 或 CORBA。

### 总结

管道通过无名管道提供了父进程与子进程之间、以及通过命名管道提供了在同一机器上运行进程之间的简单 IPC（进程通信）方法。接下来的七章将涵盖其他 IPC 方法。尽管使用套（第19章介绍）是实现 IPC 最通用的方法，但你应该学会如何编写管道，因为许多旧的 UNIX 工具都是使用它们编写的。

## 消息队列

作者：Mark Watson

### 本章内容

- 创建示例消息队列程序 276
- 运行示例消息队列程序 278

## 276
进程通信与网络编程
第三部分

消息队列类似于使用管道，但其优点是允许为消息标记特定的消息类型。消息接收者可以请求下一个可用的消息类型（通过指定所需的消息类型为0），或者通过指定正非零的消息类型来请求特定类型的下一条消息。消息队列用于运行在同一台计算机上的进程之间的通信。在第19章“TCP/IP与套接编程”中，套接编程被用于为运行在不同计算机上的程序提供通信解决方案。本章的任何更正更新可以在 `http://www.markwatson.com/books/linux_prog.html` 找到。

与管道一样，消息队列在很大程度上是因为历史原因而。许多旧的 UNIX 程序使用消息队列。

## 创建示例消息队列程序

本节使用示例程序 `message_q.c` 展示如何设置消息队列，然后使用它发送和接收消息。这个单一示例程序对消息队列进行读写。在实际应用中，一个程序向消息队列写入，另一个程序从消息队列读取。在阅读示例程序 `message_q.c` 的源码时，你可能需要检查 `msgget`、`msnd`、`msgrcv` 和 `msgctnl` 的 man 手页。在接下来的章节“信号量”的示例中，`ftok` 系统函数被用于根据当前目录名获取唯一键；这里也使用了 `ftok`：

```c
key_t unique_key = ftok(".", 'a'); // 'a' 可以是任何字符
```

`ftok` 调用提供了一种根据程序运行的当前目录计算键的方便方法。如果我们从同一个目录启动多个程序，并使用之前的 `ftok` 调用来计算唯一键，那么它们就可以访问同一个消息队列。`msgget` 函数使用由其唯一键标识的键：

```c
int id = msgget(unique_key, IPC_CREAT | 0666);
```

`msgget` 的第一个参数是通过调用 `ftok` 计算出的唯一键。第二个参数指定了消息队列的文件权限。在本例中，同一个程序对消息队列进行读写操作，因此 `msgget` 使用了 `IPC_CREAT` 标志。如果你在两个独立的程序之间通过消息队列发送数据（这显然是使用消息队列的标准方法），应该只有一个程序使用 `IPC_CREAT` 标志创建消息队列。示例程序 `message_q.c` 在退出前删除了消息队列，但也可以创建消息队列并供许多程序复用。变量 `id` 的值（`msgget` 调用的返回值）将传递给所有的 `msgsnd`、`msgrcv` 和 `msgctl` 调用。数据结构类型 `msgbuf` 定义在文件 `/usr/include/linux/msg.h` 中

```c
/* 用于 msgsnd 和 msgrcv 用的消息缓冲区 */
struct msgbuf {
    long mtype;
    char mtext[1];
}; /* 消息类型 */
/* 消息文本 */
```

在使用消息队列的应用中，我们需要定义自己的数据结构，如下：

```c
struct msgbuf {
    long mtype;
    char mtext[80];
};
```

在 `message_q.c` 中发送消息之前，我们填充了 `msgbuf`：

```c
message_buf.mtype = 123;
sprintf(message_buf.mtext,"test message");
```

我们可以使用 `msgsnd` 系统调用向队列添加消息：

```c
msgsnd(id, &message_buf, sizeof(message_buf), 0);
```

在 `message_q.c` 中接收消息时，我们定义了如下：

```c
int status = msgrcv(id, &message_buf, 80, 123, 0);
```

第三个参数 `80` 指定了消息的大小。第四个参数 `123` 指定了返回的类型。第五个参数 `IPC_NOWAIT` 指定 `msgrcv` 调用是否等待。使用 `IPC_NOWAIT` 会在没有可用消息时使调用立即返回。如果你希望 `msgrcv` 调用阻塞等待消息，可以使用值零 代替 `IPC_NOWAIT`。

当你用完消息队列后，可以使用 `msgctl` 系统调用关闭它：

```c
msgctl(id, IPC_RMID, NULL);
```
