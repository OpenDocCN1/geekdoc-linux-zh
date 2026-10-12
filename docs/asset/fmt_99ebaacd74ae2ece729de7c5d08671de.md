
/*300*/ `.word` `sys_set_robust_list`, `sys_get_robust_list`, `sys_migrate_pages`, `sys_mbind`,

`sys_get_mempolicy`, `sys_kexec_load`, `sys_move_pages`, `sys_getcpu`, `sys_epoll_pwait`

/*310*/ `.word` `sys_utimensat`, `sys_signalfd`, `sys_timerfd`, `sys_eventfd`, `sys_fallocate`

表定义在 IA-32 处理器中。

### arch/x86/kernel/syscall_table_32s

```assembly
ENTRY (sys_call_table)

    long sys_restart_syscall      /* 0 old-setup() 系统调用, 用于重新启动 */

long sys_exit

long sys_fork

long sys_read

long sys_write

long sys_open                /* 5 //
long sys_close
```

```assembly
.long sys_utimensat          /* 320 //
long sys_signalfd

long sys_timerfd

long sys_eventfd

long sys_fallocate
```

`.long` 语句的目的是对齐内存中的条目。

这种方式定义的表具有 C 数组的属性，因此可以使用指针算术进行处理。`sys_call_table` 是基础指针并指向数组的开头，也就是说，内核在表中找到适当的位置，该处的指针指向所需的处理函数。

## 返回值的含义

通常，负值表示错误，正值表示成功。

## 用户模式

虽然上面提到的错误代码定义为负数，但这里显示的代码是正数。处理 Unix 系统调用时常见的“经典”错误是：

```c
/* asm-generic/errno.h *
#define EPERM      1 /* 操作允许 */
#define ENOENT     2 /* 无文件或目录 */
#define ESRCH      3 /* 无进程 */
#define EINTR      4 /* 中断的系统调用 */
#define EIO        5 /* I/O 错误 */
#define ENOMIO     6 /* 无设备或地址 */
#define EAGAIN     7 /* 参数列表过长 */
#define EINEXEC    8 /* 执行格式错误 */
#define EBADF      9 /* 错误的文件号 */
#define ECHILD     10 /* 无子进程 */
```

```c
#define EMLINK    31 /* 链接过多 */
#define EPIPE     32 /* 管道破 */
#define EDOM      33 /* 数学参数超出范围 */
#define ENRANGE   34 /* 结果无法表示 */
```

处理 Unix 系统调用时常见的“经典”错误另一方面，`errno.h` 包含许多即使对程序员来说也不直观的未使用代码。例如 `EOPS`（代表“传输终端不支持的操作”）和 `ELNG`（意味着“链接数超出范围”）并不被归类为常见错误。更多例子：

```c
/* asm-generic/errno.h *
#define EDEADADLK    35 /* 会发生资源死锁 */
#define ENAMETOOLONG 36 /* 文件名过长 */
#define ENLOCK      37 /* 无记录锁 */
#define ENOSYS      38 /* 函数未实现 */
```

```c
#define EREOKEY     126 /* 需要的密钥不可 */
#define EEKEYPIRED   127 /* 密钥过期 */
#define EEKEYREVOKED 128 /* 密钥已被撤回 */
#define EEKEYREJECTED 129 /* 密钥被服务拒绝 */
```

```c
/* 用于健壮互斥锁 *
#define EOWNERDEAD     130 /* 所有者死亡 */
#define ENOTRECOVERABLE 131 /* 状态不可恢复 */
```
