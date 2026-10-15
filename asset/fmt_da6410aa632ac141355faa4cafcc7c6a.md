
`37` `nbytes -= pagesize;`

`38` `}`

`39` `return (0);`

`40` `}`

```
图 A.17 Timing函数：start–time、stop–time 和 touch。
```

# `tv_sub` 函数如图 A.18 所示；它减去两个结构体，并将结果存储在第一个结构中。

```c
#include "unipc.h"

void
tv_sub(struct timeval *out, struct timeval *in)
{
    if ((out->tv_sec - in->tv_sec) < 0) {
        out->tv_sec--;
        out->tv_usec += 1000000;
    }
    out->tv_sec -= in->tv_sec;
}
```
图 A.18 `tv_sub` 函数：减去两个结构体。

在 Sparc 上，如果我们连续运行程序五次，得到：

```
solaris % bw_pipe 65536
bandwidth: 13.772 MB/sec
solaris % bw_pipe 65536
bandwidth: 13.791 MB/sec
solaris % bw_pipe 65536
bandwidth: 13.685 MB/sec
solaris % bw_pipe 65536
bandwidth: 13.663 MB/sec
solaris % bw_pipe 65536
bandwidth: 13.584 MB/sec
```

每次指定五次循环、每次循环 104856 字节、每次读写 65536 字节。这五次运行的平均值为 13.7 MB/sec，如图 A.2 所示。

## Posix 队列带宽程序

图 A.19 是我们测量 Posix 队列带宽的主程序。图 A.20 显示了 `writer` 和 `reader` 函数。该程序与之前测量管道带宽的程序类似。注意，当我们在程序中指定此值时，必须指定队列中存在的最大消息数。IPC 通道的容量影响性能，因为写入进程可以在调用阻塞的 `mq_send` 之前发送许多消息，强制切换上下文。该程序的性能取决于这个数字。将该数字从四改为八对图 A.2 没有影响，但在 Digital Linux 4.0 上此更改性能下降了 12%。我们本以为增加消息数量会提高性能，因为这可以减少上下文切换。但如果使用内存映射文件，这将增加文件的大小和映射内存。

## 附录 A

```c
1 #include "unpipe.h"
2 #define NAME "bw_pxmsg"
3 reader(int, mqd_t, int);
4 writer(int, mqd_t);
5 void *buf;
6 int totalbytes, xfersize;
7 int
8 main(int argc, char **argv)
9 {
10    int i, nloop, contpipe[2];
11    mqd_t mq;
12    pid_t childpid;
13    struct mq_attr attr;
14    if (argc != 4)
15        err_exit("usage: bw_pxmsg <loops> <mbytes> <bytes/write>", NULL);
16    totalbytes = atol(argv[2]) * 1024 * 1024;
17    xfersize = atoi(argv[3]);
18 
19    buf = malloc(xfersize);
20    Touch(buf, xfersize);
21    Pipe(contpipe);
22    mq_unlink(px_ip_name(NAME)); /* error OK */
23    attr.mq_msgsize = 4;
24    attr.mq_curmsgs = xfersize;
25    mq = mq_open(px_ip_name(NAME), O_RDWR | O_CREATE, FILE_MODE, &attr);
26    if ((childpid = Fork()) == 0) {
27        writer(contpipe[0], mq); /* child */
28        exit(0);
29    }
30    /* parent */
31    for (i = 0; i < nloop; i++) {
32        reader(contpipe[0], mq, totalbytes);
33        printf("bandwidth: %.3f MB/sec\n", totalbytes / (Stop_time-Start_time)/nloop);
34    }
35    kill(childpid, SIGTERM);
36    mq_close(mq);
37    mq_unlink(px_ip_name(NAME));
38    exit(0);
39 }
```
图 A.19 用于测量 Posix 队列带宽的主函数。

### 性能测量

```c
16 buf = calloc(xfersize);
17 Touch(buf, xfersize);
18 buf->ntype = 1;
```

```c
19 Pipe(cntpipe);
20 msqid = msgget(IPC_PRIVATE, IPC_CREATE | SVMSG_MODE);
21 if ((childpid = Fork()) == 0) {
22 writer(cntpipe, 0, msqid); /* / */
23 exit(0);
24 }
25 Start-time();
26 for (i = 0; i < nloop; i++) {
27 reader(cntpipe, msqid, totalbytes);
28 printf("%.3f MB/sec\n",
29 totalbytes / (Stop-time() / nloop));
30 }
```

图 A.21 用于测量 System V 消息队列带宽的 `main` 函数。

```c
34 void
35 writer(int confd, int msqid)
36 {
37 int ntrowrite;
38 for ( ; ; ) {
39 Read(confd, &ntrowrite, sizeof(ntrowrite));
40 while (ntrowrite > 0) {
41 Msgsnd(msqid, buf, xfersize, sizeof(long), 0);
42 ntrowrite -= xfersize;
43 }
44 }
45 }
```

```c
46 void
47 reader(int confd, int msqid, int nbytes)
48 {
49 ssize_t n;
50 Write(confd, &nbytes, sizeof(nbytes));
51 while ((nbytes > 0) &&
52 (n = msgrcv(msqid, buf, xfersize - sizeof(long), 0, 0)) > 0) {
53 nbytes = n + sizeof(long);
54 }
55 }
```

图 A.22 用于测量 System V 消息队列带宽的 `writer` 和 `reader` 函数。

## Doors 带宽程序

我们测量 `doors` API 带宽的程序比本节之前的程序更复杂，因为我们必须在创建门 之前进行 `fork`。我们的程序创建门，然后通过向管道写入数据通知子进程门可以打开。

另一个变化是，与图 A14 不同，`reader` 函数不再接收数据。相反，数据是由一个函数服务器接收的，该服务器是该门对应的服务器程序。图 A.23 显示了程序的概览。

```c
main() {
    parent() {
        ...
        Pipe(contpipe);
        if (Fork() == 0) {
            fork();
            doorfd = Door_create();
            Fatchat();
            Write(contpipe[1], _);
            exit(0);
        }
    }
    server() {
        if (end of data) {
            Write(contpipe[0], 0);
            return(0);
        }
    }
    reader() {
        Write(contpipe[1], _);
```
