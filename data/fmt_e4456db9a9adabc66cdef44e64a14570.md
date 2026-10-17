
```c
#include <sys/time.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <assert.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <fcntl.h>
#include <signal.h>
#include <setjmp.h>
#include <socket.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <limits.h>

#include "child.h"

int debug = 1;

int listen_sock;

void child_process_(
    child_info_t *child_p,
    void *private_p
) {
    int rc;
    int sleep_time;
    int connection;
    struct sockaddr_in remote_addr;
    int addr_size;
    struct hostent *remote_host;
    char buf[1024];
    char *p;
    int requests_remaining;
    int read_fd;
    int write_fd;
    FILE *in;
    FILE *out;
    char s[128];
    assert(child_p);

    requests_remaining = 10;

    /* 撤销父进程的信号设置 */
    signal(SIGTERM, SIG_DFL);
    signal(SIGINT, SIG_DFL);
    signal(SIGQUIT, SIG_DFL);

    /* 这是子进程 */
    fprintf(stderr,
        "Child process #%d starting, pid=%d, parent=%d\n",
        child_p->number,
        child_p->pid,
        child_p->ppid
    );

    while(requests_remaining > 0) {

        addr_size = sizeof(remote_addr);

        connection = accept(listen_sock,
            (struct sockaddr *)remote_addr,
            &addr_size);
        printf(stderr, "accepted connection\n");

        remote_host = gethostbyaddr(
            (void *) &remote_addr.sin_addr,
            addr_size, AF_INET);

        /* 我们从未释放 remote_host 字符串 */
        /* gethostbyaddr() 的页面没有提到
        /* 分配/释放或重用问题 */

        /* 来自 DNS 的返回值可能是敌性的 */

        if(remote_host) {
            assert(strlen(remote_host->h_name) < 128);
            assert(remote_host->h_length == 4); /* 无 IPv6 */

            if(debug) {
                printf(stderr, "from: %s\n", remote_host->h_name);
            }
            strncpy(s, remote_host->h_name, sizeof(s));
        } else {
            if(debug) {
                printf(stderr, "from: %s\n", inetoa(remote_addr.sin_addr));
            }
            strncpy(s, inetoa(remote_addr.sin_addr), sizeof(s));
        }

        read_fd = dup(connection);
        write_fd = dup(connection);
        assert(read_fd >= 0);
        assert(write_fd >= 0);
        in = fdopen(read_fd, "r");
        out = fdopen(write_fd, "w");
        assert(in);
        assert(out);

        /* 做一些工作 */

        while(1) {
            buf[0] = 0;
            fgets(buf, sizeof(buf), in);
            if(!buf) break; /* 连接可能已死亡 */
            buf[sizeof(buf)-1] = 0;
            p = strrchr(buf, '\n');
            if(p) *p = 0; /* 消除换行符 */
        }

        close(in);
        close(out);
        close(read_fd);
        close(write_fd);
        close(connection);

        requests_remaining--;
    }
    exit(0);
}
```

# 系统编程

第 II 部分

## 列表 11.4 续上

```c
p=strchr(buf,'\r');
if(p) *p=0; /* 擦除回车 */

printf(stderr,buf="%s\n",buf);
p=strchr(buf,':');
if(p) {
    /* 我们永远不会到达这里，因为我们一开始 * */
    /* 一旦接收到 GET 就会输出响应 */
    /* 可能是一个 http 头部 */
    /* 忽略它 */
    ;
} else if (strstr(buf,"GET")) {
    printf(stderr,"GET\n");
    printf(out,"HTTP/1.0 200 OK\n");
    printf(out,"Content-type: text/html\n");
    printf(out,"\n");
    printf(out,"<html>\n");
    printf(out,"<HEAD>\n");
    printf(out,"<TITLE>\n");
    printf(out,"Status Page\n");
    printf(out,"</TITLE>\n");
    printf(out,"</HEAD>\n");
    printf(out,"<BODY>\n");
    printf(out,"<h1>\n");
    printf(out,"Status Page\n");
    printf(out,"</h1>\n");
    printf(out,"<BR>number=%d\n",child_p->number);
    printf(out,"<BR>pid=%d\n",child_p->ppid);
    printf(out,"<BR>requests remaining=%d\n",
        requests_remaining);
    printf(out,"</BODY>\n");
    printf(out,"</html>\n");
    break;
    /* ??? */
}
```

```c
printf(stderr,"closing connection\n");
/* 结束 */
fclose(in);
fclose(out);
close(read_fd);
close(write_fd);
```

# 进程控制 第 11 章
