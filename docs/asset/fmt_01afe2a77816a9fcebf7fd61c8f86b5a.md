
```c
#include <sys/types.h>
#include <sys/sem.h>
#include <ctype.h>
#include <sys/time.h>/* semtimedop() 的声明 */
#include <time.h>
/* 我们允许的单个 semop() 的最大操作数 */
#define MAXSEMAPOS 100

static void usageError(char *progName)
{
    fprintf(stderr, "Usage: %s semop [op] ...\n", progName);
    fprintf(stderr, "op 为 either [-+]|value[u]\n");
    fprintf(stderr, "Or: <semnum>[0]\n");
    fprintf(stderr, "n includes IPC_NOWAIT in 'op'\n");
    fprintf(stderr, "u includes SEM_UNDO in 'op'\n");
    fprintf(stderr, "The operations in argument are \nin a single semop() call\n");
    fprintf(stderr, "e.g.: 0+1,1-2,un\n");
    fprintf(stderr, "0+1,1-2,0=n\n");
    exit(EXIT_FAILURE);
}
}

/* 解析 'arg' 中用逗号分隔的操作，并将它们返回数组 'ops' 中。返回操作数量作为结果。 */
static int parseOps(char *arg, struct sembuf semops[])
{
    char *comma, *sign, *remaining, *flags;
    int numOps;
    /* 'arg' 中的操作数 */
    for (numOps = 0, remaining = arg; numOps++) {
        if (numOps >= MAXSEMAPOS)
            usageError("Too many operations (maximum=%d): %s\n", MAXSEMAPOS, arg);
        if (*remaining == '\0')
            usageError("Trailing comma or empty argument: %s\n", arg);
        if (!isdigit((unsigned char) *remaining))
            usageError("Expected digit: %s\n", arg);
        semops[numOps].sem_num = strtol(remaining, &sign, 10);

        if (*sign == '\0' || strchr(sign, "=") == NULL)
            usageError("Expected ',', or '=' in %s\n", sign);
        if (!isdigit((unsigned char) *(sign + 1)))
            usageError("Expected digit after %c in %s\n", sign, arg);
        semops[numOps].sem_op = strtol(sign + 1, &flags, 10);

        if (*sign == '-')    /* 反转操作符号 */
            semops[numOps].sem_op = -semops[numOps].sem_op;
        elif (*sign == '=0')    /* 应该是 '=0' */
            if (semops[numOps].sem_op != 0)
                usageError("Expected =0 in %s\n", arg);

            semops[numOps].sem_flg = 0;
            for (flags; flags++) {
                if (flags == 'n')
                    semops[numOps].sem_flg |= IPC_NOWAIT;
                else if (flags == 'u')
                    semops[numOps].sem_flg |= SEM_UNDO;
                else
                    break;
            }

        if (*flags != ',' && *flags != '\0')
            usageError("Bad trailing character (%c) in %s\n", flags, arg);

        comma = strchr(remaining, ',');
        if (comma == NULL)
            break;
        else /* 无逗号 -> 更多操作 */
            remaining = comma + 1;
    }
    return numOps + 1;
}

int main(int argc, char *argv[]) {
    struct sembuf sops[MAXSEMAPOS];
    int ind, nsops;

    if (argc < 2 || strcmp(argv[1], "--help") == 0)
        usageError(argv[0]);

    for (ind = 2; argv[ind] != NULL; ind++) {
        nsops = parseOps(argv[ind], sops);

        printf("%ld, %s: about to semop() [%s]\n", (long) getpid(),
               currtime("%T"), argv[ind]), sops, nsops);

        if (semop(atoi(argv[1]), 0, "semid") == -1)
            errExit("semop (PID=%ld):\n", (long) getpid());

        printf("%ld, %s: semop completed [%s]\n", (long) getpid(),
               currtime("%T"), argv[ind]);
    }

    exit(EXIT_SUCCESS);
}
```

使用列表 47-8 中的程序，以及本章中显示的其他程序，我们可以如下 shell 所示研究 System V 信号量的操作。我们首先使用一个程序创建一个包含两个信号量的集合，并将其初始化为1 和 0：

```
$svsem_create -p 2
32769
$svsem_set 32769 1 0 (PID=3658)
Semaphore changed
```

我们在本章中没有显示 `svsem_create.c` 的代码，但它在源码发行中提供。该程序对信号量的功能与46-1（第938页）相同；即它创建一个信号量集合。唯一的区别是 `svsem_create.c` 接收一个额外的参数指定要创建集合的大小。

接下来，我们启动列表 47-8 程序的三个后台实例对信号量集合执行 `sem()`。程序在操作前后都会打印消息。这些消息包含了时间，我们可以看到每个操作何时开始何时完成，并且可以跟踪多个实例的操作。

```
$svsem_op 32769 0-1,1-1 &
3659, 16:02:05: about to semop() [0-1,1-1]
[1] 3659

$svsem_op 32769 1-1 &
3660, 16:02:22: about to semop() [1-1]
[2] 3660

$svsem_op 32769 0=0 & 3661, 16:02:27: about to semop() [0=0]
[3] 3661
```

在上面的输出中，我们看到程序打印了一条消息说要执行 `semop()` 操作，但没有打印任何后续消息，因为 `semop()` 阻塞了。调用被阻塞是因为信号量的值为 0。

现在，我们使用列表 47-3 中的程序来检查信号量集合：
