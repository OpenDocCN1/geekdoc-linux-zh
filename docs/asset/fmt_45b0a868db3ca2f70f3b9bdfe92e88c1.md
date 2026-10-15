
```c
            while ((n = mq_receive(mqd, buf, attr.mq_msgsize, NULL)) >= 0) {

                printf("read: %ld bytes\n", (long)n);

            }

        }

        if (errno == EAGAIN)

            err_sys("mq_receive 错误");

    }

    exit(0);

}
```

图 13 配合 `sigwait` 使用 `mq_notify`。

```c
#include <unipipc.h>

int pipefd[2];

static void sig_usr1(int);
```

## 5.6 节 `mq_notify` 函数

```c
int main(int argc, char **argv) {

    int nfds;

    char *c;

    fd_set set;

    mqd_t mqd;

    void *buff = "buff";

    size_t n;

    struct mq_attr attr;

    struct sigevent sigev;

    if (argc != 2)

        err_sys("usage mqnotifysig <name>");

    mq = mq_open(argv[1], O_RDONLY | O_NONBLOCK);

    mq_getattr(mqd, &attr);

    buff = malloc(attr.mq_msgsize);

    pipe(pipefd);

    /* 建立信号处理程序，启用通知 */

    signal(SIGUSR1, sig_usr1);

    sigev.sig_notify = SIGEV_SIGNAL;

    sigev.sig_sig = SIGUSR1;

    mq_notify(mqd, &siggev);

    FD_ZERO(&set);

    for (;;) {

        FD_SET(pipefd[0], &set);

        nfds = select(pipefd[0] + 1, &set, NULL, NULL, NULL);

        if (FD_ISSET(pipefd[0], &set)) {

            if ((read(pipefd[0], c, attr.mq_msgsize)) > 0) {

                printf("%d bytes\n", (intds);

            }

            while ((n = mq_receive(mqd, buff, attr.mq_msgsize, NULL)) > 0) {

                printf("%d bytes\n", (long)n);

            }

        }

        if (errno == EAGAIN)

            err_sys("mq_receive 错误");

    }

}
```

```c
static void sig_usr1(int sig) {

    write(pipefd[1], "\0", 1); /* 写入 0 */

    return;

}
```

## 5.7 Posix 实时信号 99

```c
#include "unpipc.h"

mqd_t mqd;

struct mq_attr attr;

struct sigevent sigev;

static void notify_thread(union sigval sigev){ /* our thread函数 */

int main(int argc, char **argv) {

    if (argc != 2)

        err_quit("usage: mqpmgnotifythread <name>");

    mqd = MQ_open(argv[1], O_RDONLY | O_NONBLOCK);

    sigev.sigev_notify = SIGV_THREAD;

    sigev.sigev_value.s_ptr = NULL;

    sigev.sigev_function = notify_thread;

    sigev.sigev_attributes = NULL;

    mq_notify(mqd, &sigev);

    for (;;) { /* each thread does everything else */

        pause();

    }

    exit(0);

}

static void notify_thread(union sigval sigev) {

    size_t n;

    char *buf = buff;

    printf("notify_thread started\n");

    mq_notify(mqd, &sigev); /* reregister */

    while ((n = mq_receive(mqd, buf, attr.mq_msgsize, NULL)) >= 0) {

        printf("read %ld bytes\n", (long) n);

    }

    if (errno == EAGAIN)

        err_sys("mq_receive error");

    free(buf);

    pthread_exit(NULL);
}
```
