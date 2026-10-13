
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
#include <sys/socket.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <limits.h>

#include "child.h"

int debug = 1;
int listen_sock;

void child_process_1(
    child_info_t *child_p,
    void *private_p
) {
    int rc;
    int sleep_time;
    int connection;
    struct sockaddr_in remote_addr;
    int addr_size;
    struct in_ent *remote_host;
    char buf[1024];
    char *p;
    int requests_remaining = 10;
    int read_fd;
    int write_fd;
    FILE *in;
    FILE *out;
    char s[128];
    assert(child_p);

    requests_remaining = 10;

    /* undo signal settings from parent */
    signal(SIGTERM, SIG_DFL);
    signal(SIGINT, SIG_DFL);
    signal(SIGQUIT, SIG_DFL);

    /* This is child process */
    fprintf(stderr,
        "Child process #%d starting, %d, parent=%d\n",
        child_p->number,
        child_p->pid,
        child_p->ppid
    );

    while (requests_remaining > 0) {
        addr_size = sizeof(remote_addr);
        connection = accept(listen_sock, (struct sockaddr *)&remote_addr, (socklen_t *)&addr_size);
        if (connection < 0) {
            fprintf(stderr, "accept error\n");
            continue;
        }
        fprintf(stderr, "accepted connection\n");

        remote_host = gethostbyaddr(remote_addr.sin_addr);
        if (remote_host) {
            if (strlen(remote_host->h_name) < 128) {
                strncpy(s, remote_host->h_name, 127);
                s[127] = '\0';
            } else {
                strncpy(s, remote_host->h_name, 127);
                s[127] = '\0';
            }
            fprintf(stderr, "from: %s\n", s);
        } else {
            fprintf(stderr, "from: %s\n", inet_ntoa(remote_addr.sin_addr));
        }

        read_fd = dup(connection);
        write_fd = dup(connection);
        in = fdopen(read_fd, "r");
        out = fdopen(write_fd, "w");

        /* do some work */
        while (fgets(buf, sizeof(buf), in)) {
            buf[0] = '\0';
            p = strchr(buf, '\n');
            if (p) {
                *p = '\0';
                break;
            }
            if (strstr(buf, "GET")) {
                fprintf(out, "HTTP/1.0 200 OK\n");
                fprintf(out, "Content-type: text/html\n");
                fprintf(out, "\n");
                fprintf(out, "<html>\n");
                fprintf(out, "<HEAD>\n");
                fprintf(out, "<TITLE>\n");
                fprintf(out, "Status Page\n");
                fprintf(out, "number=%d\n", child_p->number);
                fprintf(out, "pid=%d\n", child_p->pid);
                fprintf(out, "ppid=%d\n", child_p->ppid);
                fprintf(out, "requests remaining=%d\n", requests_remaining);
                fprintf(out, "</</body>\n");
                fprintf(out, "</html>\n");
                break;
            }
        }
        fclose(in);
        fclose(out);
        close(read_fd);
        close(write_fd);
        close(connection);

        requests_remaining--;
        if (requests_remaining == 0) {
            fprintf(stderr, "Child process #%d exiting, pid=%d, parent=%d\n",
                child_p->number,
                child_p->pid,
                child_p->ppid);
            break;
        }
    }
}
```

```c
signal(SIGINT, SIG_DFL);
signal(SIGQUIT, SIG_DFL);

child_groups_kill(&child_groups);
exit(0);
}
```

## child_demo3.c 程序

列表 11.5 所示的程序 `child_demo3.c` 演示了 `child_pipeve()` 函数的使用。它将调用由 `argv[1]` 指定的程序，并将剩余命令行中的参数传递给它。它仅仅是将自己的环境复制到子环境中。

另一个程序 `child_demo4.c` 包含在 CD-ROM 中但未列列表中，它会输出参数和环境，对于测试 `child_demo3.c` 很有用。

### 列表 11.5 child_demo3.c
