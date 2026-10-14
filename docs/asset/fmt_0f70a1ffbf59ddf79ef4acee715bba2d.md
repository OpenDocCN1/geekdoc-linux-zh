
`sched_setparam()` 系统调用提供了 `sched_setscheduler()` 功能的子集。它在保持策略不变的情况下修改进程的调度优先级。

```c
#include <sched.h>

int sched_setparam(pid_t pid, const struct sched_param *param);
```

成功时返回 0，失败时返回 -1

`pid` 和 `param` 参数与 `sched_setscheduler()` 相同。

成功的 `sched_setparam()` 调用会将 `pid` 指定的进程移动到其优先级水平队列的末尾。

列表 35-2 中的程序使用 `sched_setscheduler()` 根据其命令行参数设置指定进程的策略和优先级。第一个参数是指定调度策略的字母，第二个是整数优先级，其余参数是要需要更改调度属性的进程 PID。

## 列表 35-2：修改进程调度策略和优先级

```c
#include <sched.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int j, pol;
    struct sched_param sp;

    if (argc < 4) {
        fprintf(stderr, "Usage: %s <policy> <priority> <pid> [pid2 ...]\n", argv[0]);
        exit(EXIT_FAILURE);
    }

    if (strcmp(argv[1], "f") == 0) pol = SCHED_FIFO;
    else if (strcmp(argv[1], "r") == 0) pol = SCHED_RR;
    else if (strcmp(argv[1], "o") == 0) pol = SCHED_OTHER;
    else if (strcmp(argv[1], "b") == 0) pol = SCHED_BATCH;
    else if (strcmp(argv[1], "i") == 0) pol = SCHED_IDLE;
    else {
        fprintf(stderr, "Unknown policy: %s\n", argv[1]);
        exit(EXIT_FAILURE);
    }

    sp.sched_priority = atoi(argv[2]);

    for (j = 3; j < argc; j++) {
        if (sched_setscheduler(atoi(argv[j]), pol, &sp) == -1) {
            perror("sched_setscheduler");
        } else {
            printf("Successfully updated pid %s\n", argv[j]);
        }
    }

    return 0;
}
```

执行成功后，`sched_getscheduler()` 返回表 35-1 所示的策略之一。

列表 35-3 中的程序使用了 `sched_getscheduler()` 和 `sched_getparam()` 来获取作为命令行参数给出的所有进程 ID 的策略和优先级。接下来的 Shell 会话演示了该程序的使用，以及列表 35-2：

```bash
$ su
Password:
# sleep 100 &
[1] 2006
# ./sched_view 2006
2006: OTHER 0
# ./sched_set -f 25 2006
# ./sched_view 2006
2006: FIFO 25
```

```
获取权限以便我们可以设置实时调度
创建一个进程
查看 sleep 进程的初始策略和优先级
将进程切换到 SCHED_FIFO，优先级为 25
验证更改
```

## 列表 35-3：获取进程调度策略和优先级

```c
#include <sched.h>
#include "tlpi_hdr.h"

int
main(int argc, char *argv[]) {
    int j, pol;
    struct sched_param sp;

    for (j = 1; j < argc; j++) {
        pol = sched_getscheduler(atoi(argv[j]), 0);
        if (pol == -1)
            errExit("sched_getscheduler: ");
    }

    if (sched_getparam(atoi(argv[j]), &sp) == -1)
        errExit("sched_getparam: ");

    printf("%s: %s %d\n", argv[j],
        (pol == SCHED_OTHER) ? "OTHER" :
        (pol == SCHED_RR) ? "RR" :
        (pol == SCHED_FIFO) ? "FIFO" : "")
    #ifdef SCHED_BATCH
    /* Linux 特有 */
    (pol == SCHED_BATCH) ? "BATCH" : "")
    #endif
    #ifdef SCHED_IDLE
    /* Linux 特有 */
    (pol == SCHED_IDLE) ? "IDLE" : "")
    #endif

    printf("%d\n", sp.sched_priority);
}
exit(EXIT_SUCCESS);
```
