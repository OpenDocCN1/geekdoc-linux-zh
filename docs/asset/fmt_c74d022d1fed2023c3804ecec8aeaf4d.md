
```c
    if (fd < 0) {perror(MODEMDEVICE); exit(-1); }

/* 在使设备异步化之前安装信号处理程序 */

    struct sigaction sao;

    void signal_handler_IO(int status); // 注意：此处原文缺少声明

    sao.sa_handler = signal_handler_IO;

    sao.sa_mask = 0;

    sao.sa_flags = 0;

    sao.sa_restorer = NULL;

    sigaction(SIGIO,&sao,NULL);

/* 允许进程接收 SIGIO */

fcntl(fd, SETOWN, getpid());

/* 使文件描述符异步化（手册页说只有

fcntl(fd, O_APPEND | O_NONBLOCK 可以配合 FASYNC 工作） */

tcgetattr(fd,&oldtrio); /* 保存当前端口设置 */

/* 为输入设置新端口设置 */

bzero(&newtio, sizeof(newtio));

newtio.c_cflag = BAUDRATE | CRTSCTS | CS8 | CLOCAL | CREAD;

newtio.c_iflag = IGNPAR | IANL;

newtio.c_oflag = 0;

newtio.c_lflag = 0; /* 设置输入模式（非规范化，无回显...） */

newtio.c_cc[TIME] = 0; /* 字符间计时器未使用 */

newtio.c_cc[VMIN] = 5;   /* 阻塞读取直到接收 5 个字符 */

tcflush(fd, TCIFUSH);

tcsetattr(fd,TANnewtio);

/* 等待输入的循环。通常我们在这里做一些有用的操作 */

while (STOP==FALSE) {

    printf("\n");usleep(100000);

    /* 接收 SIGIO 后，wait_flag = FALSE，输入可用

    可以读取 */

    if (wait_flag==FALSE) {

        res = read(fd,buf,255);

        buf[res]=0;

        printf("%s:%d\n", buf, res);

        if (buf[0]=='z') STOP=TRUE; /* 如果只输入了 CR 则停止循环 */

        wait_flag = TRUE; /* 等待新输入 */

    }

}

/* 恢复旧端口设置 */

tcsetattr(fd,TCSANOW,&oldtio);

}
```

### 3.3 异步输入

```c
#include <termios.h>
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/signal.h>
#include <sys/types.h>

#define BAUDRATE 38400
#define MODEMDEVICE "/dev/ttySI"
#define _POSIX_SOURCE 1 /* POSIX 兼容源 */
#define FALSE 0
#define TRUE 1

volatile int STOP=FALSE;

void signal_handler_IO(int status);    /* 信号处理程序定义 */
int wait_flag=TRUE;                             /* 未接收信号时为 TRUE */

main()
{
    int fd,c, res;
    struct termios oldtio,newtio;
    struct sigaction sao;                       /* 信号动作定义 */
    char buf[255];

/* 以非阻塞模式打开设备（read 将立即返回） */
fd = open(MODEMDEVICE, O_RDWR | O_NOCTTY | O_NONBLOCK);
if (fd < 0) {perror(MODEMDEVICE); exit(-1); }

/* 在使设备异步化之前安装信号处理程序 */
sao.sa_handler = signal_handler_IO;
sao.sa_mask = 0;
sao.sa_flags = 0;
sao.sa_restorer = NULL;
sigaction(SIGIO,&sao,NULL);

/* 允许进程接收 SIGIO */
fcntl(fd, SETOWN, getpid());
/* 使文件描述符异步化（手册页说只有
fcntl(fd, O_APPEND | O_NONBLOCK 可以配合 FASYNC 工作） */

tcgetattr(fd,&oldtrio); /* 保存当前端口设置 */
/* 为输入设置新端口设置 */
bzero(&newtio, sizeof(newtio));
newtio.c_cflag = BAUDRATE | CRTSCTS | CS8 | CLOCAL | CREAD;
newtio.c_iflag = IGNPAR | IANL;
newtio.c_oflag = 0;
newtio.c_lflag = 0; /* 设置输入模式（非规范化，无回显...） */
newtio.c_cc[TIME] = 0; /* 字符间计时器未使用 */
newtio.c_cc[VMIN] = 5;   /* 阻塞读取直到接收 5 个字符 */

tcflush(fd, TCIFUSH);
tcsetattr(fd,TANOW,&newtio);

/* 等待输入的循环。通常我们在这里做一些有用的操作 */
while (STOP==FALSE) {
    printf("\n");usleep(100000);
    /* 接收 SIGIO 后，wait_flag = FALSE，输入可用
    可以读取 */
    if (wait_flag==FALSE) {
        res = read(fd,buf,255);
        buf[res]=0;
        printf("%s:%d\n", buf, res);
        if (buf[0]=='z') STOP=TRUE; /* 如果只输入了 CR 则停止循环 */
        wait_flag = TRUE; /* 等待新输入 */
    }
}
/* 恢复旧端口设置 */
tcsetattr(fd,TCSANOW,&oldtio);
}
```

```
********************************************************************
* 信号处理程序。将 wait_flag 设置为 FALSE，告知上方循环
* 字符已接收。
********************************************************************/
```

```c
void signal_handler_IO (int status)
{
    printf("received SIGIO signal.\n");
    wait_flag = FALSE;
}
```

### 3.4 等待多个源的输入

本节内容被极度简化。它仅作为一个提示，因此示例代码保持了简短。这不仅适用于串口，也适用于任何文件描述符集合。

`select` 及其配套宏使用 `fd-set`。这是一个位数组，其中每个有效的文件描述符数字都有一个位条目。`select` 会接受一个带有相关文件描述符位的 `fd-set`，并返回一个 `fd-set`，其中发生输入、输出或异常的文件描述符对应的位会被设置。对 `fd-set` 的处理通过提供的宏完成。另请参见 `select(2)` 手册页。

```c
#include <sys/time.h>

#include <sys/types.h>

#include <unistd.h>

main() {

    int fd1, fd2; /* 输入源 1 和 2 */

    fd_set readfs; /* 文件描述符集 */

    int maxfd; /* 使用的最大文件描述符 */

    int loop=1; /* 循环真 */

    /* open_source 打开设备，正确设置端口并返回文件描述符 */

    fd1 = open_source("/dev/ttyS1"); /* COM2 */

    if (fd1<0) exit(0);

    fd2 = open_source("/dev/ttyS2"); /* COM3 */

    if (fd2<0) exit(0);
```
