
`copy_msqid_from_user()` 函数接收的参数包括类型为 `struct msq_subbuf` 的内核消息缓冲区、用户缓冲区，以及指示新 IPC 版本与旧 IPC 版本的版本标志。对于新 IPC 版本的情况，调用 `copy_from_user()` 将用户缓冲区的内容复制到类型为 `msqid64_ds` 的临时缓冲区中。然后，内核缓冲区的 `bytes`、`uid`、`gid` 和 `mode` 字段将被填充为临时缓冲区中对应字段的值。对于旧 IPC 版本的情况，则使用类型为 `struct msqid_ds` 的临时缓冲区。

### 5.3 共享内存

#### 共享内存系统调用接口

##### `sys_shmget()`

整个对 `sys_shmget()` 的调用都受到全局共享内存信号量的保护。

如果需要创建一个新的共享内存段，则调用 `newseg()` 函数来创建并初始化一个新的共享内存段。新段的 ID 将返回给调用者。

如果提供了现有共享内存段的键值，则查找共享内存描述符数组中相应的索引，并在返回共享内存段 ID 之前验证调用者的参数和权限。查找操作和验证是在持有全局共享内存自旋锁期间执行的。

##### `sys_shmctl()`

###### `IPC_INFO`

一个临时的 `shminfo64` 缓冲区加载了系统范围的共享内存参数，并被复制到用户空间以供调用应用程序访问。

###### `SHM_INFO`

在收集共享内存的系统范围统计信息时，持有全局共享内存信号量和全局共享内存自旋锁。调用 `shm_get_stat()` 函数来计算驻留在内存中的共享内存页数和被换出的共享内存页数。其他统计信息包括共享内存总页数和正在使用的共享内存段数量。`swap_attempts` 和 `swap_successes` 的计数被硬编码为零。这些统计信息存储在临时的 `shm_info` 缓冲区中，并复制到用户空间供调用应用程序使用。

###### `SHM_STAT`, `IPC_STAT`

对于 `SHM_STAT` 和 `IPC_STAT`，初始化一个类型为 `struct shmid64_ds` 的临时缓冲区，并锁定全局共享内存自旋锁。

对于 `SHM_STAT` 情况，共享内存段 ID 参数预期是一个直接索引（即 0 到 `n`，其中 `n` 是系统中共享内存 ID 的数量）。在验证索引后，调用 `ipc_buildid()`（通过 `shm_buildid()`）将索引转换为共享内存 ID。在 `SHM_STAT` 成功的情况下，共享内存 ID 将是返回值。请注意，这是一个未记录的特性，但为了 `ipcstat(8)` 程序而保留。

对于 `IPC_STAT` 情况，共享内存段 ID 参数预期是由调用 `shmget()` 生成的 ID。在继续之前会验证该 ID。在 `IPC_STAT` 成功的情况下，0 将是返回值。

对于 `SHM_STAT` 和 `IPC_STAT` 两种情况，都会验证调用者的访问权限。所需的统计信息会被加载到临时缓冲区中，然后复制到调用应用程序。

###### `SHM_LOCK`, `SHM_UNLOCK`

在验证访问权限后，锁定全局共享内存自旋锁，并验证共享内存段 ID。对于 `SHM_LOCK` 和 `SHM_UNLOCK`，都调用 `shm_lock()` 来执行功能。`shm_lock()` 的参数确定要执行的功能。

###### `IPC_RMID`

在 `IPC_RMID` 期间，整个函数持有全局共享内存信号量和全局共享内存自旋锁。验证共享内存 ID，然后如果没有当前附加项，则调用 `shm_destroy()` 销毁共享内存段。否则，设置 `SHM_DEST` 标志以标记其待销毁，并设置 `IPC_PRIVATE` 标志以防止其他进程引用该共享内存 ID。

###### `IPC_SET`

在验证共享内存段 ID 和用户访问权限后，使用用户数据更新共享内存段的 `uid`、`gid` 和 `mode` 标志。同时更新 `shm_ctime` 字段。这些更改是在持有全局共享内存信号量和全局共享内存自旋锁期间进行的。

##### `sys_shmat()`

`sys_shmat()` 接收以下参数：共享内存段 ID、应附加共享内存段的地址（`shmaddr`），以及将在下文描述的标志。

如果 `shmaddr` 非零，且指定了 `SHM_RND` 标志，则 `shmaddr` 会向下舍入为 `SHMLBA` 的倍数。如果 `shmaddr` 不是 `SHMLBA` 的倍数且未指定 `SHM_RND`，则返回 `EINVAL`。

验证调用者的访问权限，并增加共享内存段的 `shm_nattch` 字段。请注意，此增加保证了附加计数非零，并防止在附加到段的过程中销毁该共享内存段。这些操作是在持有全局共享内存自旋锁期间执行的。

调用 `do_mmap()` 函数创建指向共享内存段页面的虚拟内存映射。这是在持有当前任务的 `mmap_sem` 信号量期间完成的。向 `do_mmap()` 传递 `MAP_SHARED` 标志。如果调用者提供了地址，则也向 `do_mmap()` 传递 `MAP_FIXED` 标志。否则，`do_mmap()` 将选择映射共享内存段的虚拟地址。

注意：在 `do_mmap()` 函数调用中，会通过 `shm_file_operations` 结构体调用 `shm_inc()`。调用此函数用于设置 PID、设置当前时间，并增加该共享内存段的附加次数。

在调用 `do_mmap()` 之后，同时获取全局共享内存信号量和全局共享内存自旋锁。然后减少附加计数。由于调用了 `shm_inc()`，`shmat()` 调用对附加计数的净变化为 1。如果减少附加计数后，发现结果计数为零，且该段被标记为待销毁（`SHM_DEST`），则调用 `shm_destroy()` 释放共享内存段资源。

最后，共享内存映射的虚拟地址返回给调用者在用户指定的地址处。如果 `do_mmap()` 返回了错误代码，则该失败代码作为系统调用的返回值传递。

##### `sys_shmdt()`

在执行 `sys_shmdt()` 时，会持有全局共享内存信号量。当前进程的 `mm_struct` 会被搜索，以找到与共享内存地址相关的 `vm_area_struct`。一旦找到，就会调用 `do_munmap()` 来撤销共享内存段的虚拟地址映射。

请注意，`do_munmap()` 会回调 `shm_close()`，该函数执行共享内存的簿记功能，如果不存在其他附加（attachments），则释放共享内存段资源。

`sys_shmdt()` 无条件返回 0。

#### 共享内存支持结构

##### `struct shminfo64`

```c
struct shminfo64 {
    unsigned long shmmax;
    unsigned long shmin;
    unsigned long shmmni;
    unsigned long shmseg;
    unsigned long shmall;
    unsigned long __unused1;
    unsigned long __unused2;
    unsigned long __unused3;
    unsigned long __unused4;
};
```

##### `struct shm_info`

```c
struct shm_info {
    int used_ids;
    unsigned long shm_tot;  /* total allocated shm */
    unsigned long shm_rss;  /* total resident shm */
    unsigned long shm_swp;  /* total swapped shm */
    unsigned long swap_attempts;
    unsigned long swap_successes;
};
```

##### `struct shmid_kernel`

```c
struct shmid_kernel /* private to the kernel */
{
    struct kern_ipc_perm  shm_perm;
    struct file *         shm_file;
    int                   id;
    unsigned long         shm_nattch;
    unsigned long         shm_segsz;
    time_t                shm_atim;
    time_t                shm_dtim;
    time_t shm_ctim;
    pid_t shm_cpid;
    pid_t shm_lpid;
};
```

##### `struct shmid64_ds`
