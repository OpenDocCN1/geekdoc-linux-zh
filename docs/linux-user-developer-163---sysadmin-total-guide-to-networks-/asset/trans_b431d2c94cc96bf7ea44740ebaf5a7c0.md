

web 和 mark，使用 TCP/IP 工作以接受来自世界的网络连接。我们目前不需要太担心这一点；在后续教程中将涵盖更多的 TCP/IP 网络编程。

所开发的服务器将执行另一个简单任务：使用计数器统计成功连接的总数。程序每当接收到信号时，就会向日志文件写入消息，显示计数器的数值。`USUSR` 信号将通知服务器。

`advanced.c` 的完整源代码基于 `logging.c`，当你在开发自己的服务器时，可以使用 `advanced.c` 作为模板。

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <signal.h>
#include <fcntl.h>
#include <string.h>
#include <sys/time.h>
#include <sys/resource.h>
#include <socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
```

```c
int counter = 0;

#define DEFINE_LOCK "/tmp/advanced.pid"
#define LOGMODE S_IRUSR_IWUSR

#define MAXSIZE 1000
int createUDP(int port)

int sockfd;
struct sockaddr_in in_server;

sockfd = socket(AF_INET, SOCK_DGRAM, 0);
```

```c
memset(&server_address, 0, sizeof(server_address));
server_address.sin_family = AF_INET;
server_address.sin_addr = htonl(INADDR_ANY);
server_address.sin_port = htons(port);
```

```c
bind(sockfd, (struct sockaddr*)&server_address,
     sizeof(server_address));
return sockfd;
```

```c
static void signal_handler(int sig) {
    if (sig == SIGHUP) {
        syslog(LOG_INFO, "Total number of %d:", counter);
        printf("unknown signal!\n");
    }
    return;
}
```

```c
static void signal_handler2(int sig) {
    if (sig == SIGUSR1) {
        // Delete lockfile
        // NEEDS TO BE IMPLEMENTED
        syslog(LOG_INFO, "Exiting...");
        exit(0);
    } else {
        printf("unknown signal!\n");
    }
    return;
}
```

# 使用 syslog 日志

`syslog` 库实现的包允许你非常容易地创建服务器。你的服务器展示了如何使用 `syslog` 记录信息，`syslog` 系统提供了一个简单的接口。

查看 syslog 服务器，它产生的输出格式如下：

```
Jan 21 18:51:55 server1
Jan 21 18:51:56 server2
```

遗憾的是，你需要在网络常见的输出中执行服务器。

![](img/f4a034c4fbc20906a013558fa4e058a2_32_0.png)

左：配合使用命令在后台运行你的进程

# 教程进程

检查提供的服务器代码，你可以使用端口号 1234 与其他部分进行测试。一旦安装了让其运行的工具，你就可以离开了。使用 `syslog` 代理将能够从你的服务器发送日志到：

```
Jan 27 10:34:16 my-server-1 server[1234]: Connection from 172.168.1.1
```

记住 Perl 是一种解释型，每个人都知道。这是你的服务器进程源代码：

```c
// NEEDS TO BE IMPLEMENTED
```

```c
int fd = open(logfile, O_RDWR|O_CREATE, MODE);
if (fd < 0) {
    exit(0);
}
ftruncate(fd, 0);
sprintf("%s\n", getpid());
write(fd, buffer, strlen(buffer)+1);
close(fd);
```

```c
if (signal(SIGHUP, handle_sigup) == SIG_ERR) {
    syslog(LOG_INFO, "There was an error handling the SIGHUP!\n\n");
    return -1;
}
```

```c
if (signal(SIGUSR1, handle_sigusr1) == SIG_ERR) {
    syslog(LOG_INFO, "There was an error handling the SIGUSR1!\n\n");
    return -1;
}
```

```c
struct sockaddr_in client_address;
int port = 12345;
char line[MAXSIZE];
int sockfd;
socklen_t slen = 0;
sockfd = createudp(0);
syslog(LOG_INFO, "The UDP server is running!\n");
```

```c
while (1) {
    alen = sizeof(client_address);
    n = recvfrom(sockfd, line, MAXSIZE, 0, (struct sockaddr *)&client_address, &alen);
    syslog(LOG_INFO, "Got: %s, from %s\n", line, inet_ntoa(client_address.sin_addr));
    counter++;
}
return 0;
```

# 更多信号处理

服务器进程以特殊方式处理信号。Apache Web 服务器可以处理 TERM、USR1、HUP 和 WINCH 信号。TERM 信号允许 Apache 进程立即尝试杀死它所有的子进程，应该只在紧急情况下使用。然后父进程也会退出。USR1 信号导致 Apache 进程建议子进程：

```
// 如果锁文件已经存在，则退出
```

![](img/f4a034c4fbc20906a013558fa4e058a2_33_0.png)

```bash
mtsouk@mail:~$ ls -l /var/run/
total 36
drwxr-xr-x 2 root root      60 Dec 14 21:33 apache2
-rw-r-- 1 root root       5 Dec 14 21:33 atd.pid
```

