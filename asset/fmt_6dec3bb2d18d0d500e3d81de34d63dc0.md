
#include <sys/types.h>

#include <sys/ipc.h>

#include <sys/shm.h>

int shmget(key_t key, int size, int shmag);

void *shmat(int shmid, char *shaddr, int shmfl);

void shmctl(int shmid, int cmd, struct shmid_ds *buf);

简而言，`shmget()`调用创建共享内存块，`shmat()`将现有的共享内存块映射到进程的地址空间中，`shmdt()`从进程的地址空间中移除（“取消映射”）共享内存块，而`shmctl()`是一个通用函数（类似于`ioctl`风格），可用于对共享内存块执行所有其他命令。

要创建一个新的内存块，进程调用`shmget()`。如果`shmget`成功创建了新的内存块，它将返回一个类型为`int`的共享内存标识符。该共享内存标识符是内核数据结构的引用（或“句柄”）。如果`shmget`能够创建新的共享内存块，则返回的索引所对应的内核数组将返回一个`struct shmid_kernel`数据结构实例，该结构包含一个字段：

```c
struct shmid_kernel {
    shmid_ds us;
};
```

`shmget()`的参数是`key_t key`、`int size`和`int shmag`。`size`参数用于指定新内存块的字节数。然而，所有的内存分配操作都在内存页中进行。如果进程请求一个字节的内存，内存管理器将分配一个整页（i386机器上的页大小为4096字节）。因此，`size`参数的大小会向上取整到页大小的倍数。1到4096之间的大小将产生一个4K（1页）块；4097到8192将产生一个8K（2页）块；以此此类推。

`key_t`参数可以是现有内存块的键值、0或`IPC_PRIVATE`。如果`key`设置为`IPC_PRIVATE`，则`shmget()`调用将创建一个新的共享内存块。如果在`shmag`中设置了`IPC_CREAT`标志，当`key`为0时，`shmag`标志也可以导致新块的创建。如果进程想要引用一个已知由另一个进程（如父进程或服务器）创建的共享内存块，它将从创建者处获取`struct shmid_kernel`引用。然而，它也可以将`key`参数设置为现有内存块的值。如果设置了`key`的值且`shmf1`设置为`IPC_CREAT | IPC_EXCL`，则`shmget()`将失败。`shmflg`必须通过其最后9位定义用户、组和访问该内存块的权限（使用与文件相同的位模式）。

当共享内存区域被成功创建后，`shmget()`调用返回一个指向`struct shmid_ds`的整数引用：

```c
struct shmid_ds {
    struct ipc_perm shm_perm; /* 操作权限 */
    int shm_gsz;               /* 段的大小（字节） */
    kernel_time_t shm_atime;   /* 最后访问时间 */
    kernel_time_t shm_dtime;   /* 最后脱离时间 */
    kernel_time_t shm_ctime;   /* 最后修改时间 */
    ipc_pid_t shm_cpid;        /* 创建者 pid */
    ipc_pid_t shm_lpid;        /* 最后一次操作者的 pid */
    unsigned short shm_natt;   /* 当前附加次数 */
    unsigned short shm_unused; /* 兼容性 * */
    void shm_unused2;          /* 同上 - 由 DIPC 使用 */
    void shm_unused3;          /* 未使用 */
};
```

`struct ipc_perm shm_perm`字段定义了共享内存块的所有者以及其他进程使用该块的权限。它包含了指定用户ID和组ID、创建者的用户ID和组ID、访问模式（读或写）以及内存块的键值字段（`shmget()`的man页面描述了`shmid_ds`和`ipc_perm`结构）。

`void shmat(int shmid, char *shmaddr, int shmflg)`系统调用将内存块绑定到调用进程的地址空间中。

- `shmid`地址是由创建该块的`shmget()`返回的。
- `shmid`指针是`shmaddr`的抽象地址。

`shmag`是一组单位标志的集合。要在`shmag`中设置多个标志，可以使用逻辑或运算符（"|"）将它们组合并赋值给`shmag`。

## 第十一章 内存管理

```c
/* Create the shared memory */
shm_handle[N_MEM] = ...
/* Map the memory into this process’s address space */
N_ptr = ...
/* Define epsilon, N, A, b, and the initial guess of x */
/* Create worker processes, setup IPC using pipes */
makeWorkers(...);
/* Solve the system of equations */
...
while(check(A, x, b) > epsilon) {
  ...
}
/* System has converged */
yield();
cleanUp();
printResult(x, check(A, x, b, N), N); // Print the results
exit(0);
}
```

最后，考虑求解器子进程的骨架：

```c
void solver(int me) {
  yield();
  while(isConverged()) {
    X_ptr[me] = solveX(A_ptr, X_ptr, B_ptr, *N_ptr, me);
  }
}
int isConverged() {
  if(...)
    return TRUE;
  else
    return FALSE;
}
```
