
- The `WIFSIGNALED(status)` macro returns true if the child process was terminated by a signal. If it returns true, then the `WTERMSIG(status)` macro returns the number of the signal that caused the child process to terminate. The `WTERMSIG()` macro should only be used if `WIFSIGNALED()` returned true.

- The `WCOREDUMP(status)` macro returns true if the child produced a core dump. This macro should only be used if `WIFSIGNALED` returned true. This macro is not specified in POSIX.1-2001 ; only use this enclosed in `#ifdef WCOREDUMP ... #endif`.

## 7.9.3 使用 `wait()`

Listing 7.11 contains an example that puts together the use of `fork()`, `exit()`, and `wait()`. It is the typical way in which these three primitives are used. In this example the user is prompted to supply an exit value for the child, which is then passed to the `exit()` call, to show that the value is then available to the parent in the `wait()` call.

### Listing 7.11: `waitdemo2.c`

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <signal.h>
```

```c
void child()
{
    int exit_code;
    printf("I am the child and my process id is %d.\n",getpid());
    sleep(2);
    printf("Enter a value for the child exit code:");
    scanf("%d",&exit_code);
    exit(exit_code);
}

int main(int argc, char* argv[])
{
    int pid;
    int status;

    printf("Starting up...\n");
    if ( -1 == (pid = fork())) {
        perror("fork");
        exit(1);
    }
    else if ( 0 == pid )
        child();
    else { /* parent code */
        printf("My child has pid %d and my pid is %d.\n", pid, getpid());
        if ((pid = wait(&status)) == -1) {
            perror("wait failed");
            exit(2);
        }
        if (WIFEXITED(status)) { /* low order byte of status equals 0 */
            printf("Parent: Child %d exited with status %d.\n", pid, WEXITSTATUS(status));
        }
        else if ( WIFSIGNALED(status) ) {
            printf("Parent: Child %d exited with error code %d.\n", pid, WTERMSIG(status));
#ifdef WCOREDUMP
            if ( WCOREDUMP(status) )
                printf("Parent: A core dump took place.\n");
#endif
        }
    }
    return 0;
}
```

### Notes.

- 当子进程显示如下信息时

    ```
    I am the child and my process id is 5666.

    Enter a value for the child exit code:
    ```

    输入一个退出码并观察它在父进程的 `wait()` 调用结束后由父进程打印出来。然后再次运行程序，但这次从另一个终端使用 `kill` 命令向子进程发送信号，即

    ```
    $ kill -10 5666
    ```

    并观察父进程显示的消息

    ```
    Parent: Child 5666 exited with error code 6.
    Parent: A core dump took place.
    ```

- 使用条件编译宏是因为如上所述，`WCOREDUMP` 宏并非在所有 UNIX 系统上都可用。

有时父进程并不太关心其子进程是如何终止的。父进程可以明确地告诉内核它不关心子进程何时以及是否终止，通过设置 `SA_NOCLDWAIT` 标志，该标志会阻止向其自身传递 `SIGCHLD` 信号。它使用 `sigaction()` 调用执行此操作：

```
const struct sigaction act;
act.sa_flags = SA_NOCLDWAIT;
sigaction (SIGCHLD, &act, NULL);
```

请注意，在此调用中设置信号处理程序并非必要；只需传递 `sa_flags` 字段即可。如果一个进程已向内核表明它对子进程不感兴趣，那么当子进程终止时，子进程的状态将不会传递给其父进程。子进程将被立即完全终止。同样，当父进程将 `SIGCHLD` 的动作设置为 `SIG_IGN` 时，状态将被丢弃，子进程完全终止。

如果父进程既未设置 `SA_NOCLDWAIT`，也未将 `SIGCHLD` 的动作设置为 `SIG_IGN`，并且当前正在执行下面描述的任何 `wait()` 调用，则状态将被传递给父进程，并向其发送 `SIGCHLD` 信号。如果父进程当前未等待，那么当父进程调用 `wait()` 时，它将收到状态。但是，如果父进程未执行任何形式的 `wait()`，则子进程将被转换为僵尸进程。僵尸进程是一个非活动进程，它将在其父进程稍后执行 `wait()` 调用时被删除。僵尸进程存在的目的仅仅是为了在将来向其父进程提供其状态值。

问题的另一面是当一个进程在其子进程之前终止时会发生什么。当一个进程终止并且有子进程时，这些子进程并不会随之终止。`init()` 进程登场。`init()` 进程会收养孤儿进程，因此如果一个进程终止并且有任何子进程，它们将被 `init()` 收养。当子进程终止时，它们的退出状态将被发送给 `init()`。

## 7.9.4 Using `waitpid()`

`waitpid()` 函数有三个参数。第一个是要等待的子进程的进程 ID，第二个是要存储状态的变量的指针，最后一个是可选的标志集合。如果 `pid` 为 -1，则它告诉内核该进程将等待任何子进程，如 `wait()`。将 `pid` 设置为 0 表示仅等待与父进程在同一进程组中的子进程。将 `pid` 设置为 -G，其中 G 为某个正整数，表示等待任何进程组 ID 为 G 的子进程。

有三个标志可以传递给 `waitpid()`：

- `WNOHANG` 如果没有子进程已退出，则立即返回。

- `WUNTRACED` 如果子进程已停止（但未通过 `ptrace(2)` 跟踪），也返回。即使未指定此选项，也会提供已停止的被跟踪子进程的状态。

- `WCONTINUED`（自 Linux 2.6.10 起）如果已停止的子进程通过传递 `SIGCONT` 而恢复，也返回。

下面的程序清单 7.12 结合了前述的一些想法，并演示了 `waitpid()` 与 `WNOHANG` 标志的使用。

### 程序清单 7.12：`waitpiddemo.c`
