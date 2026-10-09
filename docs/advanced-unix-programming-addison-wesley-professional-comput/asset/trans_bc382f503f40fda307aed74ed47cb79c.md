

在客户端进程不断出现和消失的同时运行。由于任何具有适当权限的进程都可以打开一个 FIFO，因此很容易让服务器创建一个具有固定名称的进程，以便客户端可以打开它。

在本章中，我们将使用所有引入的进程间通信机制来在进程之间传递消息——即短片段的结构化数据，而不是像第 6 章中那样传递数据流。不过，请记住，你当然也可以使用 FIFO 来传递数据流。

### 7.2.2 一个简单的 FIFO 示例

我们将从两个程序开始：一个服务器和一个客户端。服务器持续运行，等待客户端发送消息。在这个例子中，消息是一个需要转换为大写的字符串。服务器将其转换并发送回客户端，然后循环等待下一条消息，这条消息可能来自不同的客户端。示例客户端向服务器发送几个字符串，显示结果，然后退出。

我们这样启动服务器：

```bash
$ smsg_server&
server started
[1] 8725
$
```

然后我们这样运行一个客户端：

```bash
$ smsg_client
client 8747: started
client 8747: apple sauce --> APPLE SAUCE
client 8747: tiger --> TIGER
client 8747: mountain --> MOUNTAIN
client 8747: done
```

图 7.1 展示了服务器、客户端和 FIFO 的布局。服务器创建一个供所有客户端使用的单输入 FIFO，名为 "fifo_server"，每个客户端（图中显示了两个）创建自己的 FIFO，名称中嵌入进程 ID 以确保唯一性，用于接收服务器的回复。在图中，客户端 8748 已经发送了一个消息（用矩形表示），其中包含要转换的数据（"tiger"）及其进程 ID。服务器从其输入 FIFO 读取该消息，转换数据（为 "TIGER"），然后使用发送的进程 ID（8748）确定写入结果消息的 FIFO 名称。因此，只有一个公共的服务器 FIFO，但每个客户端都有一个独立的回复 FIFO。

![Figure 7.1](img/41b4c8f6d6a5c349eee321a301703d97_423_0.png)

**图 7.1** 带有两个客户端的服务器。

客户端和服务器必须使用相同的算法来根据客户端进程 ID 组成 FIFO 名称，所以我的示例为此目的使用了一个共享的函数：

```c
bool make_fifo_name(pid_t pid, char *name, size_t name_max)
{
    snprintf(name, name_max, "fifo%d", (long)pid);
    return true;
}
```

一个公共头文件定义了固定的服务器 FIFO 名称和一个消息结构体：

```c
#define SERVER_FIFO_NAME "fifo_server"

struct simple_message {
    pid_t sm_clientpid;
    char sm_data[200];
};
```

以下是服务器程序的代码：

```c
int main(void)
{
    int fd_server, fd_client, i;
    size_t nread;
    struct simple_message msg;
    char fifo_name[100];

    printf("server started\n");
    if (mkfifo(SERVER_FIFO_NAME, PERM_FILE) == -1 && errno != EEXIST)
        EC_FAIL
    ec_negl( fd_server = open(SERVER_FIFO_NAME, O_RDONLY) )
    while (true) {
        ec_negl( nread = read(fd_server, &msg, sizeof(msg)) )
        if (nread == 0) {
            errno = ENETDOWN;
            EC_FAIL
        }
        for (i = 0; msg.sm_data[i] != '\0'; i++)
            msg.sm_data[i] = toupper(msg.sm_data[i]);
        ec_false( make_fifo_name(msg.sm_clientpid, fifo_name,
            sizeof(fifo_name)) )
        ec_negl( fd_client = open(fifo_name, O_WRONLY) )
        ec_negl( write(fd_client, &msg, sizeof(msg)) )
        ec_negl( close(fd_client) )
    }
    /* never actually get here */
    ec_negl( close(fd_server) )
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

以下是服务器执行的操作：

-   它创建其 FIFO，仅当 `mkfifo` 返回的错误不是 FIFO 已存在时才失败，因为它可能由服务器之前的运行遗留下来。
-   它以读取模式打开其 FIFO。这将会阻塞，直到有写入者出现，因此在任何客户端运行之前启动服务器是没问题的。
-   每次循环中，它读取一条消息，转换数据，打开客户端的 FIFO，将结果消息写入该 FIFO，然后关闭它。
-   由于我们没有提供显式停止服务器的方式，它将无限期地停留在循环中，直到被 `kill` 命令终止（在我们的示例中未显示）。

你可能已经可以想象客户端程序需要做什么。以下是代码：

```c
int main(int argc, char *argv[])
{
    int fd_server, fd_client = -1, i;
    ssize_t nread;
    struct simple_message msg;
    char fifo_name[100];
    char *work[] = {
        "apple sauce", "tiger", "mountain",
        NULL
    };

    printf("client %ld started\n", (long) getpid());
    msg.sm_clientpid = getpid();
    ec_false(make_fifo_name(msg.sm_clientpid, fifo_name,
        sizeof(fifo_name)) )
    if (mkfifo(fifo_name, PERM_FILE) == -1 && errno != EEXIST)
        EC_FAIL
    ec_negl( fd_server = open(SERVER_FIFO_NAME, O_WRONLY) )
    for (i = 0; work[i] != NULL; i++) {
        strcpy(msg.sm_data, work[i]);
        ec_negl(write(fd_server, &msg, sizeof(msg)) )
        if (fd_client == -1)
        {
            ec_negl( fd_client = open(fifo_name, O_RDONLY) )
            ec_negl( nread = read(fd_client, &msg, sizeof(msg)) )
            if (nread == 0) {
                errno = ENETDOWN;
                EC_FAIL
            }
        }
        printf("client %ld: %s --> %s\n", (long) getpid(),
            work[i], msg.sm_data );
    }

    ec_negl( close(fd_server) )
    ec_negl( close(fd_client) )
    ec_negl( unlink(fifo_name))
    printf("Client %ld done\n", (long) getpid();
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

客户端执行以下操作：

-   创建其 FIFO。
-   以写入模式打开服务器 FIFO。这将会阻塞，直到服务器以读取模式打开它，因此在服务器启动之前启动客户端是没问题的。
-   对于每个要转换的字符串，它组成消息，将其写入服务器，如果有必要，打开自己的客户端以读取模式，并读取结果。
-   在所有字符串转换完成后，它关闭其打开的文件描述符，并取消其 FIFO 的链接，因为其他客户端使用它的可能性不大。

有两点坏消息要告诉你：第一，客户端和服务器都有类似性质的 bug，第二，我展示客户端输出时撒谎了。事实上，客户端的输出是这样的：

```bash
$ smsg_client
client 8747: started
client 8747: apple sauce --> APPLE SAUCE
ERROR:    0: main [/asp/c7/smsg_client.c:46] 0
           *** ? (100: "Network is down") ***
$
```

发生了什么？bug 是什么？位置信息和 `errno` 值告诉我们，客户端从其自己的 FIFO 获取了文件结尾（end-of-file）。既然客户端刚刚向服务器发送了消息，为什么没有数据呢？问题是时序问题：服务器在每条消息后关闭其客户端 FIFO 文件描述符，并且在客户端从其写入操作转向 `read` 之前没有来得及重新打开它。因此，由于没有打开用于写入的文件描述符，客户端获取了文件结尾，如 6.2.2 节所述。

修复方法非常简单。如果客户端保持一个用于向其自己的 FIFO 写入的文件描述符打开，即使它永远不会写入，这将强制对其 FIFO 的任何 `read` 阻塞，直到有数据写入其中（由服务器写入），这正是我们想要的行为。因此，为了修复客户端，我们只需声明另一个文件描述符变量，如下所示：

```c
int fd_client_w = -1;
```

然后像这样，与读取文件描述符一起打开它：

```c
if (fd_client == -1)
    ec_negl( fd_client = open(fifo_name, O_RDONLY) )
if (fd_client_w == -1)
    ec_negl( fd_client_w = open(fifo_name, O_WRONLY) )
```

（我们也应该将它与 `fd_client` 一起关闭。）在大多数 UNIX 系统上，你还可以通过打开一个同时用于读取和写入的文件描述符来修复客户端，但这是非标准的。

因此，使用此修复方法重新运行客户端，我们现在得到以下输出：

```bash
client 8937 started
client 8937: apple sauce --> APPLE SAUCE
client 8937: tiger --> TIGER
client 8937: mountain --> MOUNTAIN
Client 8937 done
ERROR: 0: main [/asp/c7/smsg_server.c:33] 0
*** ? (100: "Network is down") ***
```

仍然不正确！现在*服务器*抱怨它从*它的* FIFO 获取了文件结尾。原因是客户端在不再工作后关闭了服务器 FIFO 的写入端，并且由于没有其他客户端正在运行，服务器获取了文件结尾。我们不希望那样——我们希望服务器继续运行，理想情况下在其读取中阻塞，直到有消息到来。修复方法与客户端的修复方法类似——服务器保持一个用于写入其自己的 FIFO 的文件描述符打开，以避免文件结尾。（我不展示代码——你可以很容易地找出来。）

修复服务器后，不仅两个程序都能平稳运行，我们甚至可以运行多个客户端：

```bash
$ smsg_client & smsg_client & smsg_client & smsg_client
client 9001 started
client 9001: apple sauce --> APPLE SAUCE
client 9001: tiger --> TIGER
[2] 9001
client 9002 started
client 9002: apple sauce --> APPLE SAUCE
client 9002: tiger --> TIGER
[3] 9002
[4] 9003
client 9004 started
client 9004: apple sauce --> APPLE SAUCE
client 9004: tiger --> TIGER
client 9003 started
client 9003: apple sauce --> APPLE SAUCE
client 9003: tiger --> TIGER
client 9002: mountain --> MOUNTAIN
client 9001: mountain --> MOUNTAIN
client 9004: mountain --> MOUNTAIN
client 9003: mountain --> MOUNTAIN
Client 9001 done
Client 9002 done
Client 9004 done
[2]-  Done      smsg_client
[3]-  Done      smsg_client
$ Client 9003 done
[4]+  Done      smsg_client
```

