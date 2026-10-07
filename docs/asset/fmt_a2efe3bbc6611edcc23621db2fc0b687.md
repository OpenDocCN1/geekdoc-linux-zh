
- `shell` 是一个会话组长（session leader）。
- `shell` 创建的所有进程都在此会话中。
- 在单条命令行上创建的所有进程都在同一个进程组中。
- 如果 `shell` 支持作业控制或命令行在后台启动，则为这些进程形成一个新的新的进程组。
- `shell` 的进程组之一是前台进程组，它可以与控制终端进行交互。

## 11.6 ush 中的后台进程

后台进程的主要操作属性是：`shell` 不等待它完成，且它不会被键盘发送的 `SIGINT` 终止。后台进程看起来是独立于终端运行的。本节探讨了后台进程的信号处理。一个工作正常的 `shell` 必须防止终端生成的信号，处理来自后台进程的输入，并处理子进程与其控制终端脱离的问题。

程序 11.11 显示了 `ush` 的修改，允许命令在后台执行。命令行末尾的符号 (`&`) 指定了 `ush` 应该在后台运行该命令。程序假设行内最多有一个符号，且如果存在，它位于末尾。`shell` 在 `fork` 子进程之前确定命令是否在后台执行，因为父进程和子进程都知道此信息。如果命令在后台执行，子进程会调用 `setpgid`，使其不再处于其会话的前台进程组中。父 `shell` 不等待后台子进程。

### 程序 11.11 ush.c

一个尝试通过更改进程组来处理后台进程的 `shell`。

```
#include <limits.h>
#include <setjmp.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#define BACK_SYMBOL '&'
#define PROMPT_STRING "ush5"
#define QUIT_STRING "q"

void executecmd(char *incmd);
int sigsetup(struct sigaction *def, struct sigaction *catch, sigset_t *mask, void (*handler)(int));

static sigjmp_buf jumptrompt;
static volatile sig_atomic_t okaytojump = 0;

/* ARGS USED / */
static void jumphd(int signalum) {
    if (!okaytojump) return;
    okaytojump = 0;
    siglongjmp(jumptrompt, 1);
}

int main(void) {
    char *backp;
    sigset_t blockmask;
    pid_t childpid;
    struct sigaction defhandler;
    int inbackground;
    char inbuf[MAX_CANON];
    int len;

    if (sigsetup(&handler, &blockmask, jumphd) == -1) {
        perror("Failed to setup signal");
        return 1;
    }

    for (;;) {
        if (sigprocmask(SIG_BLOCK, &blockmask, NULL) == -1) {
            perror("Failed to block signals");
            return 1;
        }

        printf("%s>> ", PROMPT_STRING);
        if (fgets(inbuf, MAX_CANON, stdin) == NULL) {
            sigprocmask(SIG_UNBLOCK, &blockmask, NULL);
            break;
        }

        len = strlen(inbuf);
        if (inbuf[len - 1] == '\n') {
            inbuf[len - 1] = '\0';
        }

        if (strcmp(inbuf, QUIT_STRING) == 0) {
            break;
        }

        if (inbuf[len - 1] == BACK_SYMBOL) {
            inbuf[len - 1] = '\0';
            inbackground = 1;
        } else {
            inbackground = 0;
        }

        if ((childpid = fork()) == -1) {
            perror("Failed to fork");
        } else if (childpid == 0) {
            if (inbackground) {
                setpgid(0, 0);
            }
            sigprocmask(SIG_UNBLOCK, &blockmask, NULL);
            executecmd(inbuf);
            exit(0);
        } else {
            if (inbackground) {
                setpgid(childpid, childpid);
            }
            sigprocmask(SIG_UNBLOCK, &blockmask, NULL);
            if (!inbackground) {
                wait(NULL);
            }
        }
    }
    return 0;
}
```

# 练习题 11.26

在 `us5` 下多次执行几次 `ls` 命令。然后执行 `ps -a`（仍在 `shell` 下）。观察到之前的 `ls` 进程显示为 `<defunct>`。退出 `shell` 并再次执行 `ps -a`。解释这些进程在 `shell` 退出前后的状态。

答案：由于没有进程等待它们，这些进程变成了僵尸进程。它们会保持这种状态，直到 `shell` 退出。此时，`init` 成为这些进程的父进程，并且 `init` 会定期等待它们，子进程最终会死亡。

程序 11.12 中的 `shell` 在后台执行时，会发生僵尸进程问题。当命令要在后台运行时，`shell` 会执行一次额外的 `fork` 调用。第一个子进程立即退出，留下后台进程作为一个孤儿进程，可以被 `init` 领养。`shell` 会等待所有子进程，包括后台进程，因为后台进程立即退出，而孙子进程会被 `init` 领养。

```c
sigset_t blockmask;
pid_t childpid;
struct sigaction defhandler, handler;
int background;
char inbuf[MAX_CANON+1];
```

```c
if (setup(&defhandler, &handler, &blockmask, jumpd) == -1) {
    perror("Failed to set shell signal handling");
    return 1;
}
```

```c
for(;;) {
    if ((sigsetjmp(jumptrompt, 1)) && /* if return from signal, \n */
        (fputs("n", stdout) == EOF)) {
        continue;
    }
    if (fputs(PROMPT_STRING, stdout) == EOF) {
        continue;
    }
    if (gets(inbuf, MAX_CANON, stdin) == NULL) {
        continue;
    }
    if (*inbuf + strlen(inbuf) - 1) == '\n') {
        *(inbuf + strlen(inbuf) - 1) = 0;
        if (strcmp(inbuf, QUIT_STRING) == 0)
            break;
    }
    if ((backp = strchr(inbuf, BACK_SYMBOL)) == NULL) {
        background = 0;
    } else {
        *backp = 0;
        if (sigprocmask(SIG_BLOCK, &blockmask, NULL) == -1)
            perror("Failed to block signals");
        }
        if ((childpid = fork()) == -1) {
            perror("Failed to fork child to execute command");
            return 1;
        } else if (background && (fork() != 0) && (setpgid(0, 0) == -1)) {
            return 1;
        }
        if ((sigaction(SIGINT, &defhandler, NULL) == -1) ||
            (sigaction(SIGQUIT, &defhandler, NULL) == -1) ||
            (sigprocmask(SIG_UNBLOCK, &blockmask, NULL) == -1)) {
            perror("Failed to set signal handling for command ");
            return 1;
        }
        execcmd(inbuf);
        perror("Failed to execute command");
        return 1;
    }
    if (sigprocmask(SIG_UNBLOCK, &blockmask, NULL) == -1)
        perror("Failed to unlock signals");
    wait(NULL);
}
return 0;
```

### 练习 11.27

在程序给出的 `shell` 中以 `rusers` 身份运行一个长时间的后台进程。

### 11.12. 当你输入 Ctrl-C 时会发生什么？

答案：

后台进程不会被中断，因为它不是前台进程组的一部分。父 `shell` 会捕获 `SIGINT` 并跳回主提示符。

### 练习 11.28

使用练习 11.25 中的 `showid` 函数来确定管道中的三个进程中哪一个成为进程组组，哪几个是 `ush6` 中 `shell` 的子进程。对分别在前台和后台启动的管道执行此操作。

答案：

如果父进程在前台启动管道，所有进程都与 `shell` 相同的进程组，且 `shell` 是进程组组。管道中的第一个进程是 `shell` 的子进程，其他的是孙子进程。如果 `shell` 在后台启动管道，它的父进程最终将是 `init`。其他进程是管道中第一个进程的子进程或孙进程。

如果 `shell` 执行作业控制，僵进程问题会更复杂。在这种情况下，`shell` 必须能够检测后台进程是否被信号（例如 `SIGSTOP`）停止。`waitpid` 函数有一个检测由信号停止的选项，但无法检测孙子进程。程序 11.12 中的后台进程是孙子进程，由于额外的 `fork`，`ush` 无法检测到它。

程序 11.13 显示了使用 `waitpid` 处理僵进程的直接方法。为了检测后台进程是否被信号停止，`ush7` 对后台进程使用了带有 `WNOHANG` 参数的 `waitpid`，而不是强制创建一个额外的子进程。`waitpid` 第一个参数为 `-1` 表示等待任何进程。如果命令不是后台命令，则显式地等待相应的子进程完成。

### 程序 11.13 ush7.c

一个使用 `waitpid` 处理僵尸后台进程的 `shell`。

```c
#include <limits.h>
#include <setjmp.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <wait.h>
#define BACK_SYMBOL '&'
#define PROMPT_STRING "ush7"
#define QUIT_STRING "q"
```
