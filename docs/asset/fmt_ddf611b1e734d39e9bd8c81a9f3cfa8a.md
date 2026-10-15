
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <signal.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <sys/select.h>
#include <errno.h>

#define MAXLINE 1024

int had_alarm = 0;

void
recvfrom_alarm(int signo)
{
    had_alarm = 1;
}

int main(int argc, char *argv[])
{
    int sockfd;
    struct sockaddr_in addr;
    socklen_t len;
    char line[MAXLINE];
    int n;
    sigset_t mask;

    if (argc != 2) {
        fprintf(stderr, "Usage: %s <ip_address>\n", argv[0]);
        exit(1);
    }

    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket");
        exit(1);
    }

    memset(&addr, 0, sizeof(addr));
    addr.sin_family = AF_INET;
    addr.sin_port = htons(1234);
    addr.sin_addr.s_addr = inet_addr(argv[1]);

    sigemptyset(&mask);
    sigaddset(&mask, SIGALRM);
    sigprocmask(SIG_BLOCK, &mask, NULL);
    signal(SIGALRM, recvfrom_alarm);

    while (fgets(line, MAXLINE, stdin)) != NULL) {
        line[strcspn(line, "\n")] = 0;
        alarm(1);
        for (;;) {
            len = sizeof(addr);
            sigprocmask(SIG_UNBLOCK, &mask, NULL);
            if (had_alarm == 1) {
                had_alarm = 0;
                break;
            }
            n = recvfrom(sockfd, line, MAXLINE, 0, (struct sockaddr *)&addr, &len);
            if (n < 0) {
                if (errno == EINTR) {
                    printf("from: %s\n", line);
                    continue;
                }
                perror("recvfrom");
                break;
            }
            printf("from: %s\n", line);
        }
        sigprocmask(SIG_BLOCK, &mask, NULL);
    }

    close(sockfd);
    return 0;
}
```

如果我们编译并运行这个程序，它看起来运行良好，但带有竞态条件的程序大多数时候都是正确的！仍然存在一个问题：取消信号、调用`recvfrom`和阻塞信号是独立的系统调用。假设`recvfrom`返回了最后一个数据报，而信号在`recvfrom`和阻塞信号之间被递送。下一次调用`recvfrom`将阻塞。我们缩小了窗口，但问题仍然存在。

解决方案的一种变体是让信号处理程序在递送信号时设置全局标志。

```c
static void
recvfrom_alarm(int signo)
{
    had_alarm = 1;
}
```

标志在每次调用`alarm`时都会初始化为 0。我们的`dg_cli`函数在调用`recvfrom`之前检查此标志，如果标志非零，则不调用它。

```c
for (;;) {
    len = sizeof(addr);
    sigprocmask(SIG_UNBLOCK, &mask, NULL);
    if (had_alarm == 1) {
        had_alarm = 0;
        break;
    }
    n = recvfrom(sockfd, line, MAXLINE, 0, (struct sockaddr *)&addr, &len);
}
```

如果信号是在被阻塞期间（上一次从`recvfrom`返回）生成的，并且当我们在此代码中取消信号时，它将在`recvfrom`之前递送。但在测试标志和调用`recvfrom`之间仍然存在很小的时间窗口，信号可以在此时生成并递送，如果发生这种情况，`recvfrom`的调用将阻塞（当然，假设没有收到额外的回复）。

一个正确的解决方案是使用`pselect`（第 6.9 节），如图 18.7 所示。

## 18.5 态条件
