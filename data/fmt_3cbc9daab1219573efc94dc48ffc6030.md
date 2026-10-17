
列表 11.3 显示的 `child_demo.c` 程序通过调用四个进程来演示子进程，这些进程除了宣布自己的存在、随机睡眠后死亡。进程会自动重启。由于某种原因，它为几个信号安装了信号处理器，在这里通过 `longjmp()` 响应这些信号略有风险，因为函数中的局部变量没有声明，因此编译器可能存储在寄存器中的任何变量将具有来自 `longjmp()` 的随机值。未来的版本可能会修复这个问题。

# 列表 11.3 child_demo.c

```c
#include <sys/time.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <assert.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <fcntl.h>
```

## 进程控制

第11 章

# 11 进程控制

```c
#include <signal.h>
#include <setjmp.h>
#include <child.h>

void child_process_1(
    child_info_t *child_info_p,
    void *private_p
){
    int rc;
    int sleep_time;
    assert(child_info_p);

    /* 撤销父进程的信号设置 */
    signal(SIGTERM, SIG_DFL);
    signal(SIGINT, SIG_DFL);
    signal(SIGQUIT, SIG_DFL);

    /* 这是子进程 */
    fprintf(stderr, "Child process #%d starting, pid=%d, parent=%d\n",
        child_info_p->number,
        child_info_p->pid,
        child_info_p->ppid);

    /* 这里我们应该做一些工作 */
    /* 然而，我们将睡眠一段时间然后死亡 */
    sleep_time = random() & 0x7F;
    fprintf(stderr, "Child process #%d sleeping for %d seconds\n",
        child_info_p->number,
        sleep_time);
    sleep(sleep_time);

    fprintf(stderr, "Child process #%d exiting, pid=%d, parent=%d\n",
        child_info_p->number,
        child_info_p->pid,
        child_info_p->ppid);
}

child_group_info_t child_group_1;
jmp_buf jump_env;
```

```c
void sig_handler(int signal)
{
    fprintf(stderr, "pid %d received signal %d\n",
        getpid(), signal);
    child_restart_children = 0;

    #if 0
    /* 唤醒 wait() */
    /* 不不起 */
    raise(SIGCHLD);
    #endif

    longjmp(jump_env, 1);

    /* 我们选择在此再次调用 signal() */
    /* 下一个信号可能会杀死我们 */
}

main() {
    int i;
    int child;
    child_group_info_t child_group_1;
    child_groups_t child_groups;
    int rc;

    #if 0
        setvbuf(stderr, NULL, _IBF, 0);
    #else
        setvbuf(stderr, NULL);
    #endif

    /* 注意：子进程继承这些 */
    signal(SIGTERM, sig_handler);
    signal(SIGINT, sig_handler);
    signal(SIGQUIT, sig_handler);

    child_group_create(&child_group_1, 4, child_process_1, NULL);

    child_groups.ngroups = 1;
    child_groups.group[0]=&child_group_1;

    rc=setjmp(jump_env);
    if(rc==0)
        /* 正常程序执行 */
```

```c
child_groups_keepalive(&child_groups);
} else {
  /* 异常处理器 */
  /* 我们在这里 setjmp() */
  /* 恢复默认信号处理器 */
  signal(SIGTERM, SIG_DFL);
  signal(SIGINT, SIG_DFL);
  signal(SIGQUIT, SIG_DFL);
  child_groups_kill(&child_groups);
  exit(0);
}
```

## 列表 11.4 延续

```c
#include <string.h>
#include <limits.h>
#include "child.h"
int debug=1;
int listen_sock;
```

```c
void child_process_1(
    child_info_t *child_p,
    void *private_p
) {
    int rc;
    int sleep_time;
    int connection;
    struct sockaddr remote_addr;
    int addr_size;
    struct hostent *remote_host;
    char buf[1024];
    char *p;
    int requests_remaining = 10;
    int read_fd;
    int write_fd;
    FILE *in;
    FILE *out;
    char s[128];
    assert(child_p);
```

```c
requests_remaining = 10;
    /* 取消父进程的信号设置 */
    signal(SIGTERM, SIG_DFL);
    signal(SIGINT, SIG_DFL);
    signal(SIGQUIT, SIG_DFL);
```

```c
/* 这是子进程 */
    fprintf(stderr,
        "Child process %d starting, pid=%d, parent=%d\n",
        child_p->number,
        child_p->pid,
        child_p->ppid);
```

```c
while(requests_remaining--) {
    addr_size=sizeof(remote_addr);
    connection = accept(listen_sock,
        (struct sockaddr *) &remote_addr,
        (socklen_t *)&addr_size);
    printf(stderr, "accepted connection\n");
```

```c
    remote_host = gethostbyaddr(
        (void *) &remote_addr.sin_addr,
        addr_size, AF_INET);
    /* 我们从不费去释放 remote_host 字符串 */
    /* gethostbyaddr() 的 man页没有提到 */
    /* 分配/释放内存或重用问题 */
```

```c
/* 来自 DNS 的返回值可能是敌恶的 */
```

```c
if(remote_host) {
    assert(strlen(remote_host->h_name));
    assert(remote_host->h_length==4); /* 无 IPv6 */
```

```c
if(debug) {
    printf(stderr, "from: %s\n", remote_host->h_name);
    }
    strncpy(s,remote_host->h_name,sizeof(s));
} else {
    if(debug) {
        printf(stderr,
            "from: %s\n", inet_ntoa(remote_addr.sin_addr));
    }
    strncpy(s,inet_ntoa(remote_addr.sin_addr),sizeof(s));
}
```

```c
    read_fd = dup(connection);
    write_fd = dup(connection);
    assert(read_fd>=0);
    assert(write_fd>=0);
    in = fdopen(read_fd, "r");
    out = fdopen(write_fd, "w");
    assert(in);
    assert(out);
```

```c
/* 执行一些工作 */
while(1) {
    buf[0]=0;
    p = fgets(buf, sizeof(buf), in);
    if(!p) break; /* 连接可能已断 */
    buf[sizeof(buf)-1]=0;
    p=strrchr(buf,'\n');
    if(p) *p=0; /* 擦除换行符 */
}
```

继续

## 列表 11.4 延续

```c
    p=strchr(buf,'\r');
    if(p) *p=0; /* 擦除回车 */
    printf(stderr,buf="%s\n",buf);
    p=strchr(buf, ':');
    if(p) {
        /* 我们到达这里是因为我们开始输出数据 */
        /* 一旦接收到 GET * 就开始输出响应 */
        /* 可能是一个 http 头部 */
        /* 忽略它 */
    } else if(strstr(buf,"GET")) {
        fprintf(stderr,"GET\n");
        fprintf(out,"HTTP/1.0 200 OK");
        fprintf(out,"Content-type: text/html\n");
        fprintf(out,"\n\n");
        fprintf(out,"HTML\n");
        fprintf(out,"<HEAD>\n");
        fprintf(out,"<TITLE>\n");
        fprintf(out,"Status Page\n");
        fprintf(out,"</TITLE>\n");
        fprintf(out,"</HEAD>\n");
        fprintf(out,"BODY\n");
        fprintf(out,"<h1>\n");
        fprintf(out,"Status Page\n");
        fprintf(out,"<HR>\n");
        fprintf(out,"<BRnumber=%d\n",child_p->number);
        fprintf(out,"<BR-pid=%d\n",child_p->pid);
        fprintf(out,"<BR-ppid=%d\n",child_p->ppid);
        fprintf(out,"<BR>requests remaining=%d\n",requests_remaining);
        fprintf(out,"</BODY>\n");
        fprintf(out,"</HTML>\n");
        break;
    } else {
        /* ??? */
    }
    printf(stderr,"closing connection\n");
    /* 清理工作 */
    fclose(in);
    close(out);
    close(read_fd);
    close(write_fd);
    close(connection);
} /* while循环 */
printf(stderr,
  "Child process %#d exiting, pid=%d, parent=%d\n",
  child_p->number,
  child_p->pid,
  child_p->ppid
);
child_group_info_t child_group_1;
jmp_buf jump_env;
void sig_handler(int signal)
{
  printf(stderr, "pid %d received signal %d\n",
  getpid(), signal);
  child_restart_children = 0;
}
#if 0
  /* 唤醒 wait() */
  /* 不起作用 */
  raise(SIGCHLD);
#endif
longjmp(jump_env,1);
/* 我们选择不再在此处再次调用 signal() */
/* 下一个信号可能会杀死我们 */
int port = 1236;
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
