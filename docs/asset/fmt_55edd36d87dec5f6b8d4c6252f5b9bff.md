
```
/***************
/ General Polling Algorithm
while ( /** Transferring Data **/)
{
  if ( /** check a channel for readiness **/)
    /** process the channel **/
  /** Do some computation **/
}
...
```

在此代码段中，计算部分非常重要。Linux 使用基于优先级的轮转调度。当任务进行更多 CPU 密集型处理（较少的 I/O 密集型处理）时，其有效优先级会增加。如果你省略计算部分，你的任务将陷入紧密循环，在几乎什么都没做的同时增加调度偏好。紧密循环对任务调度非常不利。你的任务最终可能会主导调度时间，却只完成很少的工作。

此外，如果你想不到在等待通道释放时该做什么，请不要使用延迟循环或`sleep()`。除非你需要实时响应，否则延迟循环或`sleep()`会违背轮询的目的。要么使用超时，要么让程序阻塞。

## 轮询读取器

轮询让任务在等待更多数据的同时获取并处理部分信息。使用轮询读取器，程序获取并处理数据。通常，处理和数据读取是相关的，并且你必须启用非阻塞 I/O 才能在读/写级别进行轮询。使用`fcntl()`系统调用来启用非阻塞 I/O，如下所示：

```
#include <fcntl.h>
int fcntl(int fd, int command, int option);
```

与`read()`系统调用类似，该命令接受文件描述符（`fd`）或套接字描述符（`sd`）。命令是`F_SETFL`，选项是`O_NONBLOCK`。此系统调用还有更多选项。请参阅附录 C 获取更广泛的列表。

```
if ( fcntl(sd, F_SETFL, O_NONBLOCK) != 0 )
    perror("Fcntl--could not set nonblocking");
```

例如，假设你正在编写一个音频播放器插件。与其等待整个片段从互联网下载完毕，你可能希望在接收数据的同时播放。当然，由于数据可能经过压缩，程序必须将数据转换为机器可读形式。代码片段可能类似于清单 8.1 中找到的代码。

## 示例 8.1。轮询读取示例

```c
/*************************************************************/
/** Polling Read Example: reading an audio stream, ***/
/** processing the data, and playing it. ***/
/*************************************************************/
...
if ( fcntl( sd, F_SETFL, O_NONBLOCK ) != 0 )
    perror("fcntl--could not set nonblocking");
...
done = 0;
while ( !done )
{
    int bytes;
    Queue ProcessingQueue;
    Queue OutputQueue;
    /**** Get any pending data ****/
    if ( (bytes = recv( sd, buffer, sizeof( buffer ), 0 )) > 0 )
        QueueData( ProcessingQueue, buffer);
    /**** Convert a certain number of bytes from the ****/
    /**** processing queue--typically faster than recv() ****/
    ConvertAudio( ProcessingQueue, OutputQueue);
    if ( /*** output queue is far enough ahead **/ )
        PlayAudio( OutputQueue );
    /**** If data stream is done & output queue empty... ****/
    if ( bytes == 0 && /***--output queue empty---*/ )
        done = 1;
}
...
```

此示例接收数据，将其入队并进行处理。然而，它确实存在一个问题：如果两个队列中都没有数据，`while`语句将变成一个紧密循环。为了解决这个问题，您可以插入一个延迟，因为音频是一个实时问题。

### 轮询写入器

程序的运行速度比任何 I/O 函数都快得多。（事实上，为了提高计算机性能，应增加内存并替换旧的、缓慢的 I/O。仅仅获得更快的 CPU 效果并不显著。）因此，当您的程序发送消息或提出任何请求时，操作系统会使您的程序暂停相当长的时间。

轮询写入器具有与轮询读取器类似的算法。将数据生成和处理与发送器结合是一个好主意。准备工作是相同的：使用相同参数的`fcntl()`系统调用。

您可能需要在轮询写入器中处理的问题恰好与读取器相反。读取器可能没有数据可处理，从而导致读取器陷入紧密循环。写入器可以比`send()`更快地生成数据并传输它（写入器堆积）。

例如，考虑清单 8.2中的算法，用于将照片从数码相机发送到少数几个客户端。

## 示例 8.2。轮询写入器示例

```c
/*************************************************************/
/** Polling Writer Example: sending an image to several ***/
/*** clients. ***/
/*************************************************************/
...
int pos[MAXCLIENTS];
zero( pos, sizeof( pos) );
for ( i = 0; i < ClientCount; i++ )
if ( fcntl(client[i], F_SETFL, O_NONBLOCK) != 0 )
perror( "Fcntl--could not set_nonblocking" );
...
done = 0;
/*--- repeat until all the clients get the whole message ---*/
while ( !done )
{
int bytes;
done = 1;
/*--- For all clients... ---*/
for ( i = 0; i < ClientCount; i++ )
/*--- If still more to send to client... ---*/
if ( pos[i] < size )
{
/*--- send msg, tracking how many bytes sent ---*/
bytes = send(client[i], buffer+pos[i],
size-pos[i], 0 );
if ( bytes > 0 )
{
pos[i] += bytes;
/*--- if all the clients are done, exit ---*/
if ( pos[i] < size )
done = 0;
}
}
}
...
```

在此代码中，必须单独跟踪每个客户端，因为它们可能以不同的速率接收数据。`pos`整数数组跟踪每个客户端正在处理的缓冲区中的字节位置。您可以扩展此算法以包含超时机制。

另一个问题可能是，您的服务器在第一个图像仍在发送时可能会收到另一个图像，从而导致写入器堆积。为了解决这个问题，请选择以下选项之一：

- 将新消息附加到旧消息上。

- 取消最后一条消息并开始发送新消息。

- 更改相机的帧率。

在所有情况下，请根据数据的重要性、可能丢失的数据量以及连接的波动程度来选择选项。关于准则列表，请参阅第 4 章“对等节点之间发送消息”。

## 轮询连接

一种更罕见的轮询算法涉及连接来自不同端口的客户端。服务器等待客户端连接，通常，服务器程序只提供一个端口。虽然这是惯例，但您可以打开程序内任意数量的端口。然而，设计者认为程序具有特定目的，端口提供特定服务。

某些端口服务非常基础且琐碎，为每个服务编写程序都是浪费时间、精力和内存。但是，一个套接字只能连接到一个端口。相反，考虑编写一个轮询套接字程序，如下所示：
