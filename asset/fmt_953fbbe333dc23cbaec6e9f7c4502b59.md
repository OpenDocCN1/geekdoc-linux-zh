
# 代码实现

```c
#define READ_FD 0
#define WRITE_FD 1
#define RD_CHUNK 10
#define ATOMIC

#ifndef PIPE_BUF
#define PIPE_BUF POSIX_PIPE_BUF
#endif

void do_nothing( int signo)
{
    return;
}

int main(int argc, char* argv[] )
{
    int i, repeat;
    int bytesread;
    int msgglen;
    pid_t child1, child2;
    int fd[2];
    int outfd;
    char message[RD_CHUNK+1];
    char *Child1_Chunk, *Child2_Chunk;
    long Chunk_Size;

    static struct sigaction sigact;

    sigact.sa_handler = do_nothing;
    sigfillset(&(sigact.sa_mask));
    sigaction(SIGUSR1, &sigact , NULL);

    /* check proper usage */
    if ( argc < 2 ) {
        fprintf(stderr, "Usage: %s size\n", argv[0]);
        exit(1);
    }

    /* try to create pipe */
    if ( -1 == pipe(fd)) {
        perror("pipe call");
        exit(2);
    }

    repeat = atoi(argv[1]);
#if defined ATOMIC
    Chunk_Size = PIPE_BUF;
#else
    Chunk_Size = PIPE_BUF + 200;
#endif
```

```c
printf("Chunk size = %ld\n", Chunk_Size);
printf("Value of PIPE_BUF is %d\n", PIPE_BUF);

Child1_Chunk = calloc(Chunk_Size, sizeof(char));
Child2_Chunk = calloc(Chunk_Size, sizeof(char));
if ( ( NULL == Child1_Chunk ) ||
     ( NULL == Child2_Chunk ) ) {
    perror("calloc");
    exit(2);
}

/* create the string that child1 writes */
Child1_Chunk[0] = '\0'; /* just to be safe */
for ( i = 0; i < Chunk_Size-2; i++ )
    strcat(Child1_Chunk, "X");
strcat(Child1_Chunk,"\n");

/* create the string that child2 writes */
Child2_Chunk[0] = '\0'; /* just to be safe */
for ( i = 0; i < Chunk_Size-2; i++ )
    strcat(Child2_Chunk, "Y");
strcat(Child2_Chunk,"\n");

/* create first child process */
switch ( child1 = fork() ) {
case -1: /* fork failed — exit */
    perror("fork()");
    exit(3);

case 0: /* child1 code */
    msgglen = strlen(Child1_Chunk);
    pause();
    for ( i = 0; i < repeat; i++ ) {
        if ( write(fd[WRITE_FD], Child1_Chunk, msgglen )
            != msgglen ) {
            perror("write");
            exit(4);
        }
    }
    close(fd[WRITE_FD]);
    exit(0);
default: /* parent creates second child process */
    switch ( child2 = fork() ) {
    case -1: /* fork failed — exit */
        perror("fork()");
        exit(5);

    case 0: /* child2 code */
        msgglen = strlen(Child2_Chunk);
        pause();
        for ( i = 0; i < repeat; i++ ) {
            if ( write(fd[WRITE_FD], Child2_Chunk, msgglen )
                != msgglen ) {
```

```c
perror("write");
    exit(6);
}
}
    close(fd[WRITE_FD]);
    exit(0);
default: /* parent code */
    outfd = open("pd2_output",
        O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if ( -1 === outfd ) {
        perror("open");
        exit(7);
    }

    close(fd[WRITE_FD]);
    kill(child1, SIGUSR1);
    kill(child2, SIGUSR1);
    while ( ( bytesread = read( fd[READ_FD], message, RD_CHUNK) )
        != 0 )
        if ( bytesread > 0 ) { /* more data */
            write(outfd, message, bytesread);
        }
        else {          /*read error */
            perror("read()");
            exit(8);
        }

    close(outfd);
    /* collect zombies */
    for ( i = 1; i <= 2; i++ )
        if ( wait(NULL) === -1 ) {
            perror("wait failed");
            exit(9);
        }
    close(fd[READ_FD]);
    free(Child1_Chunk);
    free(Child2_Chunk);
}
    exit(0);
}
```

## Notes

- 父进程是读取者；两个子进程是写入者。每个子进程调用 `pause()` 来开始，以便它们都不会立即抢占处理器。父进程在准备好从管道读取时向它们发送 `SIGUSR1` 信号。

- 每个子进程向管道写入大小为 `Chunk_Size` 的块。`Chunk_Size` 要么是 `PIPE_BUF`，要么比它大 200 字节。

- 父进程从管道读取并将数据写入名为 `pd2_output` 的文件。当 `read()` 返回 0 时，子进程已完成写入并关闭了管道，因此父进程关闭输出文件并调用 `wait()` 来收集子进程的退出状态。

- 程序在管道操作开始之前打印 `PIPE_BUF` 的值和实际的块大小。

首先按原样编译程序，将可执行文件命名为 `pipedemo2`。运行 `pipedemo2` 时，输出将显示写入是原子的——每个子进程通过一次 `write` 写入的字符串末尾都有换行符，在输出中，每一段 X 都会以换行符结尾，每一段 y 也会以换行符结尾。输出中不会出现字符串 `Xy` 或 `yX`，因为内核对并发写入进行了序列化，并且每次子进程写入时，它都会写入整个字符串，即 X 或 y。输出并不能证明它是原子的；它只是表明没有输出被交错，因此没有写入被中断。

每个子进程应写入两千次或更多，以便我们看到它们各自竞争共享管道的可能性，因此程序应使用 2000 或更大的命令行参数运行。手工检查输出以确定是否存在交错输出的行会很繁琐。下面的脚本旨在自动完成此操作：
