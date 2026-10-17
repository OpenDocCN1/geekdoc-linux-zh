
```bash
$ ./fifo2 O_RDONLY NONBLOCK &
[1] 160
Process 160 opening FIFO
$ ./fifo2 O_WRONLY
Process 161 result 3
Process 161 result 3
Process 161 finished
Process 161 finished
[+] Done
```

这两个可能是最常见的打开模式组合。欢迎自由使用示例程序来实验其他组合。

## 读取和写入 FIFO

使用 `O_NONBLOCK` 模式会影响 FIFO 上读和写调用的行为。

在空 FIFO（即一个使用 `O_NONBLOCK` 打开的 FIFO）上进行读取操作将等待直到有某些数据可读。相反，在没有数据的非阻塞 FIFO 上进行读取操作将返回 0 字节。

在满的 FIFO 上进行写入将等待直到数据可以写入。在无法接受所有写入字节的 FIFO 上进行写入，将：

- 如果请求小于或等于 `PIPE_BUF` 字节且数据可以写入，则失败。

- 写入部分数据，如果请求大于 `PIPE_BUF` 字节，则返回实际写入的字节数，这可能为 0。

FIFO 的大小是一个重要的考虑因素。系统对可以缓冲的数据量有一个限制，这通常在 `limits.h` 中找到。在 Linux 和许多其他 Unix 类系统上，这个限制通常是 4096 字节，但在某些系统上可能低至 512 字节。系统保证，在已以 `O_WRONLY` 打开（即阻塞的）的 FIFO 上写入 `PIPE_BUF` 或更少字节的数据，要么写入所有字节，要么一个都不写。

虽然在单个 FIFO 写入者和单个 FIFO 读取者的简单情况下，这个限制并不非常重要，但使用单个 FIFO 让许多不同的程序向单个 FIFO 读取器发送请求是很常见的。如果多个不同的程序尝试同时写入 FIFO，那么确保不同程序的数据块不会交织至关重要——也就是说，每次写入必须是“原子的”。你如何做到这一点呢？

嗯，如果你确保所有的写入请求都是针对阻塞 FIFO 的且大小小于 `PIPE_BUF` 字节，系统将确保数据永远不会交织。通常情况下，将通过 FIFO 传输的数据限制为 `PIPE_BUF` 字节块是一个好主意，除非你使用单个写入者和单个读取者进程。

## 进程间通信：管道

### 尝试一下——使用 FIFO 进行进程间通信

为了展示无关进程如何使用命名管道进行通信，我们需要两个独立的程序，`fifo3.c` 和 `fifo4.c`。

1. 第一个程序是我们的生产者程序。它在需要时创建管道，然后尽可能地向其写入数据。

注意，为了说明起，我们不在乎数据是什么，所以我们没有去初始化缓冲区。两个列表都显示了相对于 `fifo2.c` 的更改，并删除了所有的命令行参数。

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <limits.h>
#include <sys/types.h>
#include <sys/stat.h>

#define FIFO_NAME "/tmp/my_fifo"
#define PIPE_BUF 4096
#define TEN_MG (10*1024*1024)

int main() {
    int fd, res;
    int mode = O_WRONLY;
    int bytes_sent = 0;
    char buffer[PIPE_BUF];

    if (access(FIFO_NAME, F_OK) == -1) {
        res = mkfifo(FIFO_NAME, 0777);
        if (res != 0) {
            fprintf(stderr, "Could not create fifo %s\n", FIFO_NAME);
            exit(EXIT_FAILURE);
        }
    }

    printf("Process %d opening FIFO\n", getpid());
    fd = open(FIFO_NAME, mode);
    printf("Process %d result %d\n", getpid(), fd);
    while (bytes_sent < TEN_MG) {
        res = write(fd, buffer, PIPE_BUF);
        if (res == -1) {
            fprintf(stderr, "Write error on pipe\n");
            exit(EXIT_FAILURE);
        }
        bytes_sent += res;
    }

    close(fd);
    printf("Process %d finished\n", getpid());
    exit(EXIT_SUCCESS);
}
```

2. 第二个程序是消费者，它比生产者简单得多。它从 FIFO 中读取数据。

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <limits.h>
#include <sys/types.h>
#include <sys/stat.h>

#define FIFO_NAME "/tmp/my_fifo"
#define PIPE_BUF 4096
#define TEN_MG (10*1024*1024)

int main() {
    int fd, res;
    int mode = O_RDONLY;
    int bytes_read = 0;
    char buffer[PIPE_BUF];

    printf("Process %d opening FIFO\n", getpid());
    fd = open(FIFO_NAME, mode);
    printf("Process %d result %d\n", getpid(), fd);

    if (fd != -1) {
        do {
            res = read(fd, buffer, PIPE_BUF);
            bytes_read += res;
        } while (res > 0);
        close(fd);
    } else {
        exit(EXIT_FAILURE);
    }

    printf("Process %d finished, %d bytes read\n", getpid(), bytes_read);
    exit(EXIT_SUCCESS);
}
```

## 第 13 章

### 尝试一下——一个示例客户端/服务器应用程序

1. 首先，我们需要一个头文件 `client.h`，它定义了客户端和服务器程序通用的数据。为了方便起见，它还包含了所需的系统头文件。

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <limits.h>
#include <sys/types.h>
#include <sys/stat.h>

#define SERVER_FIFO_NAME "tmp/serv_fifo"
#define CLIENT_FIFO_NAME "tmp/cli_%d_fifo"

#define BUFFER_SIZE 20

struct data_to_pass_st {
    pid_t client_id;
    char some_data[BUFFER_SIZE - 1];
};
```

2. 对于服务器程序 `server.c`。在本节中，我们创建并打开了服务器管道（pipe）。它被设置为只读且为阻塞模式。在睡眠（出于演示目的）之后，服务器从客户端读取任何数据，这些数据包含了 `data_to_pass_st` 结构体。

```c
#include "client.h"
#include <ctype.h>

int main() {
    int server_fifo_fd, client_fifo_fd;
    struct data_to_pass_st my_data;
    int read_res;
    char client_fifo[256];
    char *tmp_char_ptr;

    mkfifo(SERVER_FIFO_NAME, 0777);
    server_fifo_fd = open(SERVER_FIFO_NAME, O_RDONLY);
    if (server_fifo_fd == -1) {
        fprintf(stderr, "Server fifo failure\n");
        exit(EXIT_FAILURE);
    }

    sleep(10); /* lets clients choose for demo purposes */
    do {
        read_res = read(server_fifo_fd, &my_data, sizeof(my_data));
        if (read_res > 0) {
```

3. 在此阶段，我们对从客户端获取的数据进行一些处理：我们将 `some_data` 中的所有字符转换为大写字母，并根据接收到的 `client_pid` 转换 `CLIENT_FIFO_NAME`。

```c
tmp_char_ptr = my_data.some_data;
while (*tmp_char_ptr) {
    *tmp_char_ptr = toupper(*tmp_char_ptr);
    tmp_char_ptr++;
}
sprintf(client_fifo, CLIENT_FIFO_NAME, my_data.client_pid);
```

4. 然后我们将处理后的数据发回，以只写、阻塞模式打开客户端管道。最后，通过关闭文件并取消链接（unlink）来关闭服务器 FIFO。

```c
client_fd = open(client_fifo, O_WRONLY);
if (client_fd != -1) {
    write(client_fifo_fd, &my_data, sizeof(my_data));
    close(client_fifo_fd);
}
while (read_res > 0);
close(server_fifo_fd);
unlink(SERVER_FIFO_NAME);
exit(EXIT_SUCCESS);
```

5. 这里是 `client.c`，该程序的第一部分如果服务器 FIFO 已经存在，则将其作为文件打开。它获取了自己的进程 ID（PID），这构成了发送到服务器的数据的一部分。客户端 FIFO 被创建，为下一节做好了准备。

```c
#include "client.h"
#include <ctype.h>

int main() {
    int server_fifo_fd, client_fifo_fd;
    struct data_to_pass_st my_data;
    int times_to_send;
    char client_fifo[256];

    server_fifo_fd = open(SERVER_FIFO_NAME, O_WRONLY);
    if (server_fifo_fd == -1) {
        fprintf(stderr, "Sorry, no server\n");
        exit(EXIT_FAILURE);
    }

    my_data.client_pid = getpid();
    sprintf(client_fifo, CLIENT_FIFO_NAME, my_data.client_pid);
    if (mkfifo(client_fifo, 0777) == -1) {
        fprintf(stderr, "Sorry, can't make %s\n", client_fifo);
        exit(EXIT_FAILURE);
    }
}
```

6. 在五个循环中的每一个中，客户端都会发送到服务器。然后打开客户端 FIFO（只读、阻塞模式）并读回数据。最后，关闭服务器 FIFO 并从内存中移除客户端 FIFO。

```c
for (times_to_send = 0; times_to_send < 5; times_to_send++) {
    sprintf(my_data.some_data, "Hello from %d", my_data.client_pid);
    printf("%d %s ", my_data.client_pid, my_data.some_data);
    write(server_fifo_fd, my_data, sizeof(my_data));
    client_fifo_fd = open(client_fifo, O_RDONLY);
    if (client_fifo_fd == -1) {
        if (read(client_fifo_fd, &my_data, sizeof(my_data)) > 0) {
            printf("received: %s\n", my_data.some_data);
        }
        close(client_fifo_fd);
    }
}
close(server_fifo_fd);
unlink(SERVER_FIFO_NAME);
```

要测试这些，我们使用以下命令：

```bash
$ server &
$ for i in 1 2 3 4 5; do ./client &; done
```

输出如下：

```text
1234 Hello from 1234
1235 Hello from 1235
1236 Hello from 1236
1237 Hello from 1237
1238 Hello from 1238
```

## 进程间通信：管道

现在我们已经看到了如何使用命名管道来实现简单的客户端/服务器系统，我们可以回顾 CD 数据库应用程序并进行转换。我们将引入一些处理，以便在进程被中断时执行清理操作。我们将使用旧的 db 版本，使代码尽可能简单。

在详细查看新版本之前，我们将编译该应用程序。输入 `server -i` 允许程序初始化一个新的 CD 数据库。

不用说，除非服务器正在运行，否则客户端无法运行。以下是显示程序如何组合的 makefile。

```makefile
all:
	server client

CC=cc
CFLAGS=-pedantic -Wall

# 为了调试取消下一行的注释
# DFLAGS=-DEBUG_TRACE=1 -g

# 我们正在使用哪个版本的哪个 dbm。
# 这假设 gdb 已预安装在标准位置，但我们将使用
# gdb 兼容程序，我们模拟 ndbm。
# 我们这样做是因为 ndbm 是 dbm 版本的“标准”。
# 根据你的发行版，这些可能需要更改。
DBM_INC_PATH=/usr/include/gdb
DBM_LIB_PATH=/usr/lib
DBM_LIB_FILE=gdb
```

## 第 13 章

```makefile
.c.o:

$(CC) $(DFLAGS) -I$(DBM_INC_PATH) $(DFLAGS) -c c$$

app_ui.o: app_ui.c cd_data.h
cd_dbm.o: cd_dbm.c cd_data.h
client_f.o: client.c cd_data.h cliserv.h
pipe_imp.o: pipe_imp.o cd_data.h cliserv.h
server.o: server.c cd_data.h cliserv.h

client: app_ui.o clientif.o pipe_imp.o
$(CC) -o client $(DFLAGS) app_ui.o clientif.o pipe_imp.o

server: server.o cd_dbm.o pipe_imp.o
$(CC) -o server -L$(DBM_LIB_PATH) $(DFLAGS) server.o cd_dbm.o pipe_imp.o
-l$(DBM_LIB_FILE)

clean:
rm -f server client_app *.o
```

### 目标

我们的目标是将应用程序中与数据库的部分与应用程序的用户界面部分分离。我们还希望运行一个单服务器进程，但允许许多客户端同时运行。此外，我们希望对现有代码的修改尽可能少。在可能的情况下，我们将保持现有代码不变。

为了保持简单，我们还希望能够在应用程序内部创建（并删除）管道，这样在使用之前就不需要系统管理员在我们在使用之前创建命名管道了。

此外，确保我们永远不会为了某个事件而进行“忙等待”（等待 CPU 时间）是非常重要的。正如我们所看到的，Linux 允许我们通过阻塞来等待事件，而不消耗大量的资源。我们应该利用管道的阻塞特性来确保高效使用 CPU。毕竟，从理论上讲，服务器可能会等待几个小时直到请求到达。

### 实现

在第 7 章看到的应用程序早期单进程版本中，我们使用了一组数据访问例程来处理数据。这些例程是：
