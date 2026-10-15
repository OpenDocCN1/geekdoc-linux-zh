

```
{
    int pid;

    pid = fork();
    if (pid == -1) {
        perror("Fork failed");
        exit(1);
    }
    /* Child process */
    if (pid == 0) {
        printf("Child's PID = %d\n", getpid());
        exit(0);
    }
    /* Parent process */
    printf("Parent's PID = %d\n", getpid());
    sleep(10);
    /* Parent process does not wait for the child */
    /* process and child becomes a zombie process */
    exit(0);
}
```

```
% gcc48 -w create_zombie.c -o create_zombie
% ./create_zombie
Parent's PID = 14978
Child's PID = 14979
<Ctrl+Z>
Suspended
% ps
  PID TT  STAT      TIME COMMAND
14522 1  Ss       0:00.42 -csh (csh)
14978 1  T        0:00.00 ./create_zombie
14979 1  Z        0:00.00 <defunct>
14986 1  R+       0:00.01 ps
% fg
zombie
%
```

在 Solaris 下的示例运行如下所示。注意你需要使用 ps -al 命令来显示僵尸进程的状态。

```
% ./create_zombie
Parent's PID = 12295
Child's PID = 12296
<Ctrl+Z>
Stopped (user)
```

```
% ps -al
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
0 Z 1007 12296 12295 0 0 - - 0 - ? 0:00 <defunct>
0 T 1007 12295 12294 0 40 20 ? 432 pts/1 0:00 ./create_zombie
0 O 1007 12297 12294 0 40 20 ? 2318 pts/1 0:00 ps
0 S 1007 12294 12166 0 40 20 ? 2179 ? pts/1 0:00 csh
% fg
zombie
%
```

当 init 进程的子进程终止时，init 会调用其中一个 wait() 系统调用来收集子进程的退出状态。因此，init 的子进程永远不会变成僵尸。子进程可能是由 init 直接创建的进程，也可能是因为进程的父进程在进程终止时已死亡或未等待而被 init 继承的进程。

## EXERCISE 19.11

在你的系统上重现前面的会话。create_zombie.c 程序是否按预期工作？

## 19.3.7 终止进程

进程可以使用 kill() 系统调用来终止其有权限终止的进程。由超级用户拥有的进程可以终止任何进程。我们将在第 19.5.4 节详细讨论此系统调用。

## 19.4 进程与文件描述符表

我们现在讨论 PPFDT 与进程间文件共享、I/O 重定向以及使用管道、FIFO 和套接字等不同通道进行进程间通信的重要性。我们将在第 19.4.1 节讨论文件共享的概念，并在第 19.4.2 节讨论 I/O 重定向。第 20 章详细描述了 UNIX 进程间通信。

### 19.4.1 进程间文件共享

如前所述，子进程会获得其父进程的 PPFDT 的副本。这意味着如果进程在创建子进程之前打开一个文件，则父进程和子进程都可以访问该打开文件的文件描述符。因此，对该打开文件进行的 I/O 操作对另一个进程是可见的。

程序 file_sharing.c 说明了父进程和子进程如何共享在子进程创建之前打开的文件。我们仅用一个文件来演示该概念，但它可扩展到多个文件。该程序将 filename 和 nbytes（以字节为单位的 I/O 大小）作为命令行参数，并以命令行参数指定的文件作为只读和写入方式打开。然后它创建一个继承 PPFDT 的子进程，因此继承了打开文件的文件描述符。父进程和子进程都对同一文件进行 I/O。该程序显示两个进程读取的数据以及两个进程中 I/O 后的文件指针位置，以验证两个进程都对同一文件进行 I/O。nbytes 参数可从 0 到 512 变化，因为读写缓冲区的大小已设置为 512 字节。我们在父进程中使用 sleep(1) 调用，以确保子进程在父进程之前执行 I/O。这样做是为了确保在两个进程中正确显示文件指针的值。程序列表之后有一些示例运行，以验证文件共享概念按所述工作。注意 foo 是现有文件的文件名。

```
% cat file_sharing.c
/* file_sharing.c: fileshare filename nbytes */
#include <fcntl.h>
#include <unistd.h>
#include <sys/wait.h>

#define SIZE 512

int main(int argc, char *argv[])
{
    int fd, n, nr, nbytes, pid, status;
    char buf[SIZE];

    /* Open file */
    if (argc != 3) {
        printf("$s filename nbytes\n", argv[1]);
        exit(1);
    }
    nbytes = atoi(argv[2]);
    if ((fd = open(argv[1], O_RDWR)) == -1) {
        perror("File opening");
        exit(1);
    }
    /* Create a child */
    pid = fork();
    /* Child process */
    if (pid == 0) {
        /* Read and display on stdout */
        if ((nr = read(fd, buf, nbytes)) == -1) {
            perror("Read failed");
            exit(1);
        }
        write(1, buf, nr); /* Throw on standard output */
        n = lseek(fd, 0L, SEEK_CUR);
        printf("\n\nChild: position of the file pointer after I/O is %d\n\n", n);
        close(fd);
```

