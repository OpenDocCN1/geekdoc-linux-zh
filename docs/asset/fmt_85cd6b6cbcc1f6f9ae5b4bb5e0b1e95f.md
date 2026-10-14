
```c
#include "tlpi_hdr.h"

static int idata = 111;      /* 分配在数据段 */

int
main(int argc, char *argv[])
{
    int istack = 222;      /* 分配在栈中 */
    pid_t childPid;

    switch (childPid = fork()) {
        case -1:
            errExit("fork");

        case 0:
            idata *= 3;
            istack *= 3;
            break;

        default:
            sleep(3);          /* 给子进程一个执行机会 */
            break;
    }

    /* 父进程和子进程都来到这里 */
    printf("PID=%ld %s idata=%d istack=%d\n", (long)getpid(),
           (childPid == 0) ? "child" : "parent", idata, istack);

    exit(SUCCESS);
}
```

## 24.2 父进程与子进程之间的文件共享
