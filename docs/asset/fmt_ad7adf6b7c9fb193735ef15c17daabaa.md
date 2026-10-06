
注意事项：这个特定调用看起来很老旧了。它与消息队列和信号集对应的操作非常相似。

`shmat()` 的第一个参数是键值（在本例中由 `ftok()` 返回）。该键值随后与内核中存在的键值进行比较。打开或访问操作取决于 `shmfl`。
`IPC_CREAT`: 如果内核中不存在该段，则创建。
`IPC_EXCL`: 与 `IPC_CREAT` 使用时，如果段已存在则失败。

如果使用 `IPC_EXCL`，`shmat()` 要么返回新创建段的标识符，要么返回具有相同键值的段的标识符。如果 `IPC_EXCL` 与 `IPC_CREAT` 使用，则创建一个新段，或者如果段已存在，调用返回 `-1`。`IPC_EXCL` 单独使用没有用，但结合 `IPC_CREAT` 使用，可以作为确保不打开现有段的机制。

再次，可以将可选模式或到掩码中。让我们创建一个用于查找或创建共享内存段的封装函数：

```c
int open_segment( key_t keyval, int segsize )
{
    int shmid;
    if((shmid = shget( keyval, segsize, IPC_CREAT | 0660 )) == -1)
    {
        return(-1);
    }
    return(shmid);
}
```

注意权限 `0660` 的使用。这个小函数返回共享内存段标识符（`int`），或返回错误。键值和请求的大小（字节）作为参数传递。进程一旦给定段的有效 IPC 标识符，下一步是将段附加或映射到自己的地址空间。

## 2.4.4.4 系统调用: shmat()

```c
系统调用: shmat();
原型: int shmat( int shmid, char *shmaddr, int shflg);
返回值: 段附加到进程的地址，或
错误时 -1: errno = EINVAL（传递了无效的 IPC ID 或地址）
ENOMEM（内存不足无法附加段）
EACCESS（权限拒绝）
```

注意事项：
如果参数为零 (`0`)，内核尝试寻找一个未映射的区域。可以指定地址，但通常仅用于辅助硬件或解决与其他参数的冲突。`SHM_RDONLY` 标志可以或入标志参数，以强制传递的地址进行页对齐（向下到最近的页大小）。
此外，如果 `SHM_RDONLY` 标志与标志参数或，则共享内存将被映射并标记为只读。
此调用最易使用。考虑这个封装函数，它传递段的有效 IPC 标识符，并返回段附加的地址：

```c
char *attach_segment( int shmid )
{
    return (shmat(shmid, 0));
}
```

一旦段被正确附加并有了指向该段起始部分的指针，对该段进行读写就变得非常简单，只需引用或解引用指针即可！注意不要丢失原始指针的值！如果发生这种情况，你将无法访问段的基（起始）部分。

## 2.4.4.5 系统调用: shmctl()

```
系统调用: shmctl();
原型: int shmctl(int shmid, int cmd, struct shmid_ds *buf);
返回值: 成功时返回 0
错误时 -1: errno =
    EACCES（无权限且 cmd 为 IPC_STAT）
    EFAULT（在 IPC_SET|IPC_STAT 命令中，buf 指向的地址无效）
    EIDRM（检索期间段已被移除）
    EINVAL（shqid 无效）
```

`EPERM` (发出了 `IPC_SET` 或 `IPC_RMID` 命令，但调用进程没有对该段的写入（修改）访问权限)

注意：
此特定情况直接根据消息队列的 `msgget` 调用进行建模。…… 有效命令值为：

- `IPC_STAT`
获取段的 `shmid.ds` 结构，并将其存储在参数 `buf` 的地址中。

- `IPC_SET`
设置段的 `shmid_ds` 结构中 `ipc_perm` 成员的值。取自 `buf` 参数的值。

- `IPC_RMID`
将段标记为删除。

`IPC_RMID` 命令并不会实际上从内核中删除段。相反，它将该段标记为删除。当当前附加到该段的最后一个进程正确地分离（detach）时，才会发生实际删除。当然，如果当前没有进程附加到该段，该段将立即删除。

要正确地分离共享内存，进程会调用 `shmddt` 系统调用。

## 2.4.4.6 系统调用：shmddt()

```
系统调用：shmddt();
原型：int shmddt ( char *shmaddr )
返回值：错误时返回 -1；errno = EINVAL (传递了无效的附加地址)
```

当进程不再需要某个共享内存时，应该通过调用此系统调用将其分离。如前所述，这与从内核中删除段不是一一的！分离成功后，`shmid_ds` 结构中的 `shm_natch` 成员将减 1。当该值达到 0 (`0`) 时，内核将从物理上移除该段。

## 2.4.4.7 shmtool：一个交互式共享内存管理器

背景：我们 System V IPC 对象的最后一个示例将是 `shmtool`，这是一个用于创建、读取、写入和删除共享内存段的命令行工具。再次，与之前的示例一样，如果该段之前不存在，则会在任何操作期间创建它。

### 命令行语法

向段中写入字符串

```
shmtool w 'text'
```

从段中检索字符串

```
shmtool r
```

更改权限（模式）

```
shmtool m (mode)
```

删除段

```
shmtool d
```

## 2.4. System V IPC

### 示例

```
shmtool w test
shmtool w 'This is a test'
shmtool r
shmtool d
shmtool m 660
```

### 源代码

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
```

```c
#define SEGSZ 100
main(int argc, char *argv[])
{
    key_t key;
    int shmid, cntr;
    char *segptr;
    if(argc == 1)
        usage();
    /* 通过调用 ftok() 创建唯一键 */
    key = ftok(".", 'S');
    /* 打开共享内存段 - 如果必要则创建 - 以客户端身份打开 */
    if((shmid = shmget(key, SEGSZ, IPC_CREAT|IPC_EXCL|0666)) == -1)
    {
        printf("Shared memory segment exists - opening as client\n");
        /* 段可能已经存在 - 尝试作为客户端打开 */
        if(shmid = shmget(key, SEGSZ, 0)) == -1)
        {
            perror("shmget");
            exit(1);
        }
    }
    else
    {
        printf("Creating new shared memory segment\n");
    }
    /* 将共享内存段附加（映射）到当前进程 */
    if((segptr = shmat(shmid, 0, 0)) == -1)
    {
        perror("shmat");
        exit(1);
    }
    switch(tolower(argv[1][0]))
{
case 'w': writeshm(shmid, segptr, argv[2]);
break;
case 'r': readshm(shmid, segptr);
break;
case 'd': removeshm(shmid);
break;
case 'm': changemode(shmid, argv[2]);
break;
default: usage();
}
}
```

```c
writeshm(int shmid, char *text)
{
    strcpy(segptr, text);
    printf('Done...\n');
}
```

```c
readshm(int shmid, char *segptr)
{
    printf('segptr: %s\n', segptr);
}
```

```c
removeshm(int shmid)
{
    shmctl(shmid, IPC_RMID, 0);
    printf('Shared memory segment marked for deletion\n');
}
```

```c
changemode(int shmid, char *mode)
{
    struct shmid_ds myshmids;
    /* 获取内部数据结构的当前值 */
    shmctl(shmid, IPC_STAT, &myshmids);
    /* 显示旧权限 */
    printf('Old permissions: %o\n', myshmids.shm_perm.mode);
    /* 转换并加载模式 */
    sscanf(mode, "%o", &myshmids.shm_perm.mode);
    /* 更新模式 */
    shmctl(shmid, IPC_SET, &myshmids);
    printf('New permissions: %o\n', myshmids.shm_perm.mode);
}
```

```c
usage()
{
    fprintf(stderr, "Usage: shmtool <w|r|d|m> [text|mode]\n");
    exit(1);
}
```

## libc 中的 I/O 函数

## 4.1 I/O 函数

### 4.1.1 格式化输出

`libc` 中的 `printf(...)` 函数提供格式化输出并允许对参数进行转换。

```c
int fprintf(FILE *stream, const char *format, ...)
将转换输出（要填充的参数 ...）并将其写入流中。format 中定义的格式也将写入。该函数返回写入的字符数，或在出错时返回负值。
```
