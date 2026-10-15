
```c
        Read(contpipe[1], _);

    }

}

child() {

...

    if (Fork() == 0) {

        Read(contpipe[0], 0);

        doorfd = Open(0);

        writer();

        exit(0);

    }

}

writer() {

    Read(contpipe[0], 0);

    while (more to send) {

        Write(datapipe[1], _);

        Door_call();

    }

}
```

![](img/1541bd224d292c30573e864db3959d59_481_0.png)

由于 doors 仅在 Solaris 下支持，我们简化了全工管道程序（4.4 节）。

与之前程序的另一个不同是消息传递和过程调用之间的根本区别。在我们的 Posix 队列程序中，`writer` 循环向队列写入消息，这是异步的。在某些，队列会满，或者进程会丢失时间片，`reader` 运行并读取消息。例如，如果队列持有八条消息，`writer` 每次写入八条，`reader` 每次读取八条，发送 N 条消息涉及 N/4 次上下文切换（从 `writer` 到 `reader` 是 N/8，`reader` 到 `writer` 也是 N/8）。但 doors API 在调用 `door_call()` 时会阻塞调用者，直到过程返回。交换 N 条消息涉及 N/2 次上下文切换。我们在测量 RPC 带宽时会遇到相同的问题。尽管上下文切换次数增加，请注意 doors 提供了最快的 IPC 带宽（25000 字节）。图 A.24 显示了程序的 `main()` 函数。图 A.25 显示了 `writer`、`server` 和 `reader` 函数。

## RPC 带宽程序

由于 Sun RPC 调用是同步的，我们面临与 doors 程序相同的限制。使用 RPC 生成两个程序（客户端和服务器）更容易，因为那是 `rpcgen` 生成的。图 A.26 显示了 RPC 规范。我们声明了一个接受不长度数据输入且无返回的过程。图 A.27 显示我们的客户端程序，图 A.28 显示我们的服务器过程。我们将协议（TCP 或 UDP）指定为命令行参数，允许我们测量两者。

## A.3 消息传递程序

```c
#include "unpipe.h"

void reader(int, int);
void writer(int);
void server(void *, char *, size_t,
    door_desc_t *, size_t n_descriptors);

int *buf;
int totalbytes, xfersize, contpipe[2];

int main(int argc, char **argv) {
    int i, nloop, doorfd;
    char c;
    pid_t childpid;
    size_t n;

    if (argc != 5)
        err_quit("usage: bw_door <pathname> <bytes> <write/read>", argv[0]);

    nloop = atoi(argv[2]);
    totalbytes = atoi(argv[3]) * 1024 * 1024;
    xfersize = atoi(argv[4]);

    buf = malloc(xfersize);
    Touch(buf, xfersize);

    unlink(argv[1]);
    pipe(contpipe); /* 假设为全工管道 */
    open(argv[1], O_CREAT | O_EXCL | O_RDWR);

    if ((childpid = Fork()) == 0) {
        /* child = writer */
        if (n = Read(contpipe[0], &c, 1) != 1)
            err_quit("child: pipe returned %d", n);
        doorfd = Open(argv[1], O_RDWR);
        exit(0);
    }

    writer(doorfd);

    /* parent = server */
    doorfd = door_create(server, NULL, 0);

    Write(contpipe[1], &c, 1); /* 通知 child 就绪 */
    Start-time();

    for (i = 0; i < nloop; i++)
        reader(doorfd);

    printf("door%d: %f MB/sec\n", doorfd, totalbytes / (Stop-time() / nloop));
    kill(childpid, SIGTERM);
    unlink(argv[1]);
    exit(0);
}
```

图 A.24 用于测量 doors API 带宽的 `main()` 函数。

## 性能测量

```c
void
writer(int doorfd) {
    int ntrowrite;

    arg_desc_ptr = NULL;      /* 解析描述符 */
    arg_desc_num = 0;
    arg_result = NULL;       /* 期望返回值 */
    arg_size = 0;

    for ( ; ) {
        Read(contpipe[0], &ntrowrite, sizeof(ntrowrite));
        while (ntrowrite > 0) {
            arg_data_ptr = buf;
            arg_data_size = xfersize;
            Door_call(doorfd, &arg);
            ntrowrite -= xfersize;
        }
    }
}
```

```c
static int ntoread;

server(void cookie, char *argp, size_t arg_size,
    door_desc_t *dp, size_t n_descriptors) {
    char c;

    ntoread += arg_size;
    if (nread >= ntoread) {
        /* 通知 reader 我们已全部完成 */
        Write(contpipe[0], &c, 1);
        Door_return(NULL, NULL, 0);
    }
}
```

```c
reader(int doorfd, int nbytes) {
    char c;
    size_t n;

    ntoread = nbytes;      /* server0 过程的全局变量 */
    nread = 0;

    Write(contpipe[1], &nbytes, sizeof(nbytes));
    if ((n = Read(contpipe[0], &c, 1) != 1) {
        err_quit("reader pipe returned %d", n);
    }
}
```

图 A.25 用于 doors API 带宽测量的 `writer`、`server` 和 `reader` 函数。

用于 Sun RPC 带宽测量。

```c
#define DEBUG      /* 让服务器在前台运行 */

struct data_in {
  opaque data[];      /* 变长度透明数据 */
};

program BW_SUNRPC_PROG {
  version BW_SUNRPC_VERS {
    void BW_SUNRPC(data_in) : 1;
  } = 1;
} = 0x3123001;
```

图 A.26 是 Sun RPC 带宽测量的 RPC 规范。

```c
#include "unpipe.h"
#include "bw_sunrpc.h"

void *buf;
int xfersize;

int
main(int argc, char **argv) {
    int nloop, ntwrite;
    CLIENT *cl;
    data_in in;

    if (argc < 6) {
```
