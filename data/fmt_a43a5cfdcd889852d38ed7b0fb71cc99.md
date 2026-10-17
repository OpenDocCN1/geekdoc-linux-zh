
```c
printf("%-8.8s ", (s == NULL) ? "??" : s);

t = ac.atime;

loc = localtime(&t);

if (loc == NULL)

    printf("Unknown time\n");

} else {

    strftime(timeBuf, TIME_BUF_SIZE, "%Y-%m-%d %H:%M:%S", loc);

    printf("%s ", timeBuf);

}

printf("%-7.2f %-7.2f\n", (double)compTOLL(ac.utime) +

    compTOLL(ac.stime) / sysconf(_SC_CLK_TCK),

    (double)compTOLL(ac.etime) / sysconf(_SC_CLK_TCK));

}

if (numRead == -1)

    errExit("read");

exit(EXIT_SUCCESS);

}
```

# 进程会计 第 3 版本文件

从内核 2.6.8 开始，Linux 引入了进程会计文件的替代版本，解决了传统会计文件的局限性。要使用这种替代版本（Version 3），在编译内核之前必须启用 `CONFIG_BSD_PROCESS_ACCT_V3`。

在使用 Version 3 时，会计操作的区别在于写入会计文件的格式。新格式如下：

```c
struct acct_v3 {
    char        ac_flag;      /* 会计标志位 */
    char        ac_version;   /* 会计版本 (3) */
    u_int16 ac_tty;       /* 进程控制终端 */
    u_int32 ac_exitcode;  /* 进程终止状态 */
    u_int32 ac_uid;        /* 用户 ID */
    u_int32 ac_gid;        /* 组 ID */
    u_int32 ac_pid;       /* 进程 ID */
    u_int32 ac_ppid;      /* 父进程 ID */
    u_int32 ac_atime;     /* 开始时间 (time_t) */
    float       ac_etime;     /* 运行时间 (时钟周期) */
    comp        ac_utime;    /* 用户 CPU 时间 (时钟周期) */
    comp        ac_stime;     /* 系统 CPU 时间 (时钟周期) */
    comp        ac_mem;      /* 平均内存使用 (KB) */
    comp        ac_io;       /* 读写字节（未使用） */
    comp        ac_rw;       /* 读写块（未使用） */
    comp        ac_minfl;     /* 小缺页中断 */
    comp        ac_majf;      /* 大缺页中断 */
    comp        ac_swaps;    /* 交换次数（未使用；Linux 特有） */
};
#define ACCT_COMM 16
char ac_comm[ACCT_COMM]; /* 命令名 */
```

```c
#define _GNU_SOURCE
#include <sched.h>
int clone(int (*func) (void *, void *child_stack, int flags, void *func_arg, ...
    /* pid_t *ptid, struct user_desc *tls, pid_t *ctid */);
```

返回 `clone` 成功后的进程 ID，出错时返回 `-1`。
