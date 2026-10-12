
# 进程控制

## 第11章

### 11 进程控制

```c
fprintf(stderr, "cmdpath=%s\n", cmdpath);
}

fprintf(stderr, "about to execve()\n");

if 1
    execve(cmdpath, argv, envp);
else
    dummy_argv[0] = "./child_demo4";
    dummy_argv[1] = "one";
    dummy_argv[2] = "two";
    dummy_argv[3] = "three";
    dummy_argv[4] = NULL;
    dummy_envp[0] = "PATH=/bin:/usr/bin";
    dummy_envp[1] = NULL;

execve("./child_demo4", dummy_argv, dummy_envp);
/* 除非出错，否则永远不会到达这里 */

fprintf(stderr, "execve() failed\n");
perror("execve()");
/* 我们将偷懒地让进程终止
/* 清理打开的文件描述符 */
exit(255);

} else {
    /* 父进程 */
    pid=rc;

if 0
    rc=wait4(pid, &status, 0, NULL);
else
    rc=waitpid(pid, &status, 0);
endif

if(rc<0) {
    /* wait4 设置了 errno */
    return(-1);
}
if(WIFEXITED(status)) {
    fprintf(stderr, "child_pipev(): child exited normally\n");
    return(int) (WEXITSTATUS(status));
} else if(WIFSIGNALED(status)) {
    fprintf(stderr, "child_pipev(): child caught signal\n");
    errno = EINTR;
    return(-1);
} else {
```

继续

```c
fprintf(stderr,"child_pipev: unknown child status\n\n/* 我们应该更好地地处理停止的进程 */
errno = EINTR;
return(-1);
}
```

```c
void child_init()
{
}
```

```c
void child_term()
{
}
```

# `child_demo1.c` 程序

列表 11.3 显示的 `child_demo1.c` 程序通过调用四个进程演示了子进程库，这些进程所做的仅仅是宣布自己的存在、睡眠随机的时间，然后死亡。死亡的进程会被重新启动。在没有特殊理由的情况下，它为几个常见信号安装了信号处理程序，并通过调用 `longjmp()` 和杀死子进程来对时间和信号和其他信号做出响应。在这里使用 `longjmp()` 略有风险，因为函数中的局部变量没有声明为 `volatile`，因此编译器可能存储在寄存器中的任何变量在执行 `longjmp()` 之后将具有随机值。未来的版本可能会修复这一疏忽。

### 列表 11.3 `child_demo1.c`

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

#include <child.h>
```

```c
void child_process_(
    child_info_t *child_info_p,
    void *private_p
) {
    int rc;
    int sleep_time;
    assert(child_info_p);

/* 撤销父进程的信号设置 */
signal(SIGTERM, SIG_DFL);
signal(SIGINT, SIG_DFL);
signal(SIGQUIT, SIG_DFL);

/* 这是子进程 */
printf(stderr,
    "Child process #%d starting, pid=%d, parent=%d\n",
    child_info_p->number,
    child_info_p->pid,
    child_info_p->ppid
);

/* 这里我们应该做一些有用的工作 */
/* 反之，我们将睡眠一段时间然后死亡 */
sleep_time = random() & 0x7F;
printf(stderr,
    "Child process #%d sleeping for %d seconds\n",
    child_info_p->number,
    sleep_time
);
sleep(sleep_time);

printf(stderr,
    "Child process #%d exiting, pid=%d, parent=%d\n",
    child_info_p->number,
    child_info_p->pid,
    child_info_p->ppid
);
}
```

```c
child_group_info_t child_group_1;
jmp_buf jump_env;
```

继续

```c
void sig_handler(int signal) {
    fprintf(stderr, "pid %d received signal %d\n",
           getpid(), signal);
    child_restart_children = 0;

    #if 0
        /* 唤醒 wait() */
        /* 不不起 * */
        raise(SIGCHLD);
    #endif
}

longjmp(jump_env, 1);

/* 我们选择不再再次调用 signal() */
/* 下一个信号可能会杀死我们 * */
}

main() {
    int i;
    int child;
    child_group_info_t child_group_1;
    child_groups_t child_groups;
    int rc;

    #if 0
        dup2(stderr, NULL, 0);
    #else
        dup2(stderr, NULL);
    #endif

    /* 注意：进程继承此 */
    signal(SIGTERM, sig_handler);
    signal(SIGINT, sig_handler);
    signal(SIGQUIT, sig_handler);

    child_group_create(&child_group_1, 4, child_process_, NULL);

    child_groups.ngroups = 1;
    child_groups.group[0] = &child_group_1;

    rc = setjmp(jump_env);
    if(rc == 0) {
        /* 正常执行 */
        child_groups_keepalive(&child_groups);
    } else {
        /* 异常处理器 */
        /* 我们得到了 setjmp() */
        /* 恢复默认信号处理程序 */
        signal(SIGTERM, SIG_DFL);
        signal(SIGINT, SIG_DFL);
        signal(SIGQUIT, SIG_DFL);

        child_groups_kill(&child_groups);
        exit(0);
    }
```

# `child_demo2.c` 程序

列表 11.4 显示的 `child_demo2.c` 是 `child_demo1.c` 的扩展。它实现了一个原始服务器，派生了 4 个进程，每个进程通过请求处理该请求的状态来响应任何请求。每个请求在处理后都会终止。在 fork 的情况下，必须通过给每个子进程限制生存周期来防止内存泄漏和其他问题。使用 `alarm` 也是好的，这样如果请求在规定时间内未处理，子进程将会死亡。

### 列表 11.4 `child_demo2.c`
