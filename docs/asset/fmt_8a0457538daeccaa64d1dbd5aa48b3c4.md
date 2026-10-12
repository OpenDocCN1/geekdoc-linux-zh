
```c
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

```c
close(connection);

} /* while */

fprintf(stderr,

  "Child process #%d exiting, pid=%d, parent=%d\n",

  child_p->number,

  child_p->pid,

  child_p->ppid

);
```

`child_group_info_t child_group_1;`
`jmp_buf jump_env;`

```c
void sig_handler(int signal)

{

  fprintf(stderr, "pid %d received signal %d\n",

  getpid(), signal);

  child_restart_children = 0;
```

```c
#if 0

  /* 唤醒 wait() */

  /* 不起 */

  raise(SIGCHLD);

#endif
```

`longjmp(jump_env,1);`

> /* 我们选择在此不再调用 signal() */
> /* 下一个信号可能会杀死我们 */

`int port = 1236;`

```c
main()

{

  int i;

  int child;

  child_group_info_t child_group_1;

  child_groups_t child_groups;

  int rc;

  struct sockaddr_in tcpaddr;

  tcpaddr.sin_family = AF_INET;

  tcpaddr.sin_addr.s_addr = INADDR_ANY;

  tcpaddr.sin_port = htons(port);
```

继续

## 列表 11.4 sock 续上

```c
listen_sock = socket(AF_INET, SOCK_STREAM, IPPROTO_IP);

if(listen_sock<0) perror("socket");

assert(listen_sock>=0);
```

```c
fprintf(stderr, "listening on port %d\n", port);
```

```c
#if 1

rc=bind(listen_sock, (struct sockaddr *) &tcpaddr,

sizeof(tcpaddr));

#else

rc=bind(listen_sock, (struct sockaddr *) &tcpaddr, 4);

#endif

if(rc!=0) perror("bind");

assert(rc==0);

rc=listen(listen_sock,10);

if(rc!=0) perror("listen");

assert(rc==0);
```

```c
#if 0

setvbuf(stderr, NULL, _IOLBF, 0);

#else

setbuf(stderr, NULL);

#endif
```

> /* 子进程会继承这个 */
`signal(SIGTERM, sig_handler);`
`signal(SIGINT, sig_handler);`
`signal(SIGQUIT, sig_handler);`

`child_group_create(&child_group_1, 4, 4, child_process_1, NULL);`

`child_groups.ngroups = 1;`
`child_groups.group[0]=&child_group_1;`

```c
rc=setjmp(jump_env);
if(rc==0) {
    /* 正常程序执行 */
    child_groups_keepalive(&child_groups);
} else {
    /* 异常处理器 */
    /* 我们通过 setjmp() 到达这里 */
}
/* 恢复信号处理程序为默认 */
signal(SIGTERM, SIG_DFL);
```

```c
signal(SIGINT, SIG_DFL);
signal(SIGQUIT, SIG_DFL);

child_groups_kill(&child_groups);
exit(0);
}
```

## child_demo3.c 程序

列表 11.5 所示的 `child_demo3.c` 程序演示了 `child_pipe()` 函数的使用。它将调用由 `argv[1]` 指定的程序，并传递命令行参数中找到的参数。它仅仅复制了自己的环境作为子进程的环境。另一个程序 `child_demo4.c`（包含在 CD-ROM 中但未列出）会打印它的参数和环境，对于测试 `child_demo3.c` 非常有用。

## 列表 11.5 child_demo3.c

```c
#include <sys/time.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <assert.h>
#include <sys/types.h>
#include <wait.h>
#include <fcntl.h>
#include <signal.h>
#include <errno.h>
#include <sys/socket.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <limits.h>

#include "child.h"

int debug=0;

extern char **environ;

main(int argc, char *argv[]) {
    // ... (此处为原文截断处，翻译保持一致)
}
```

# 进程信息 (Process Info)

在任何时刻，系统中运行的每个用户进程在 `/proc` 下都有目录；该目录的名称是进程号的十进制表示。此外，`/proc/self` 是指向当前进程目录的符号链接（该链接对于每个进程看起来都不同）。这些目录中包含许多文件。

在接下来的章节中，`$pid` 将替换为进程的进程标识符。这些特殊文件大部分可以使用 `more`、`cat`、`strings` 查看，或者使用 `grep` 进行搜索。`strings` 的 `-f` 选项会打印文件名，这在配合通配符时非常方便。

> 注意
>
> 源文件 `/usr/src/linux/fs/proc/array.c` 似乎包含了大多数实际为每个进程条目生成 `/proc` 输出的例程。

# cmdline 文件 (The cmdline File)
