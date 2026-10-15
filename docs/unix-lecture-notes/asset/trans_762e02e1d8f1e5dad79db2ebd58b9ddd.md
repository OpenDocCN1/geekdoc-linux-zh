

![](img/edd55012c780b4e999320d08ab27959e_444_0.png)

## 图 8.6：迭代服务器中使用的 FIFO。

服务器和客户端使用的消息结构，以及所有必要的包含文件和通用定义，都包含在头文件 upcase1.h 中，如以下清单所示。

### 清单 8.12：upcase1.h

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
#include <limits.h>
#include <signal.h>
#include <errno.h>
#include <sys/wait.h>
#include <sys/stat.h>
#include <ctype.h>

#define PUBLIC      "/tmp/UPCASE1_PIPE"
#define HALFPIPE_BUF    (PIPE_BUF / 2)

typedef struct _message {
    char    fifo_name[HALFPIPE_BUF];    /* private FIFO pathname */
    char    text[HALFPIPE_BUF];         /* message text           */
} message;
```

由于消息不得大于 PIPE_BUF 字节，并且应足够通用以允许 FIFO 路径名具有较大的大小，因此结构在 FIFO 名称的长度和要发送到服务器的文本的长度之间平均分配。因此，HALFPIPE_BUF 被定义为 PIPE_BUF 的一半，并用作待翻译字符串中的最大字节数。

我们这次从客户端代码开始。客户端采取的基本步骤如下。

- 1. 它确保标准输入和输出均未重定向。
- 2. 它注册其信号处理程序。
- 3. 它在 /tmp 中创建其私有 FIFO。
- 4. 它尝试以非阻塞模式打开公共 FIFO 以进行写入。
- 5. 它进入一个循环，在其中重复
  - (a) 从标准输入读取一行，并且
  - (b) 重复
    - i. 获取输入文本中下一个 HALFPIPE_BUF-1 大小的块，
    - ii. 通过公共 FIFO 向服务器发送消息，
    - iii. 打开其私有 FIFO 以进行读取，
    - iv. 从私有 FIFO 读取服务器的回复，
    - v. 将服务器的回复复制到其标准输出，并且
    - vi. 关闭其私有 FIFO 的读端。
- 6. 它关闭公共 FIFO 的写端并删除其私有 FIFO。

客户端清单如下。

### 清单 8.13：upcaseclient1.c

```
#include "upcase1.h"   /* All required header files are included in  */
                         /* this shared header file. */

#define PROMPT   "string: "
#define UPCASE   "UPCASE: "
#define QUIT     "quit"

const char   startup_msg[] =
"upcased1 does not seem to be running. "
"Please start the service.\n";

volatile sig_atomic_t  sig_received = 0;
struct msg  msg;

/***************************************************************/
/*                        Signal Handlers                      */
/***************************************************************/

void on_sigpipe( int signo )
{
    fprintf(stderr, "upcased is not reading the pipe.\n");
    unlink(msg.fifo_name);
    exit(1);
}

void on_signal( int sig )
{
    sig_received = 1;
}
/***********************************************************************/
/*
 *                          Main Program                             *
 */
/***********************************************************************/

int main( int argc, char *argv[] )
{
    int         strLength;      /* number of bytes in text to convert     */
    int         nChunk;         /* index of text chunk to send to server  */
    int         bytesRead;      /* bytes received in read from server     */
    int         privatefifo;    /* file descriptor to read-end of PRIVATE */
    int         publicfifo;     /* file descriptor to write-end of PUBLIC */
    static char buffer[PIPE_BUF];
    static char textbuf[BUFSIZ];

    struct sigaction handler;

    /* Only run if we are using the terminal. */
    if ( !isatty(fileno(stdin)) || !isatty(fileno(stdout)) )
        exit(1);

    /* Register the on_signal handler to handle all keyboard signals */
    handler.sa_handler = on_signal;     /* handler function */
    if ( ((sigaction(SIGINT, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGHUP, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGQUIT, &handler, NULL)) == -1 ) ||
         ((sigaction(SIGTERM, &handler, NULL)) == -1 )
        ) {
        perror("sigaction");
        exit(1);
    }

    handler.sa_handler = on_sigpipe;
    if ( sigaction(SIGPIPE, &handler, NULL) == -1 ) {
        perror("sigaction");
        exit(1);
    }

    /* Create hopefully unique name for private FIFO using process-id */
    sprintf(msg.fifo_name, "/tmp/fifo%d",getpid());

    /* Create the private FIFO */
    if ( mkfifo(msg.fifo_name, 0666) < 0 ) {
        perror(msg.fifo_name);
        exit(1);
    }

    /* Open the public FIFO for writing */
    if ( (publicfifo = open(PUBLIC, O_WRONLY | O_NONBLOCK) ) == -1 ) {
        if ( ENXIO == errno )
            fprintf(stderr,"%s", startup_msg);
        else
```
