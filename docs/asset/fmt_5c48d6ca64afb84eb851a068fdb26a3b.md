
```bash
solaris % shmwrite
solaris % shmread
solaris % shmget
solaris % ipcs -b
IPC status from <running system> as of Jun 8 13:18:1998
ID KEY OWNER GROUP SEGS
```

我们运行 `ipcs` 验证共享内存段已被移除。

> 当使用服务器执行文件的名称作为 `ftok` 的参数来标识某种 System V 形式时，通常指定绝对路径，例如 `/usr/bin/myserver`，而不是我们使用的相对路径（`shmget`）。我们在示例中使用相对路径，是因为所有程序都是从包含服务器执行文件的目录运行的。这意味着 `ftok` 使用文件的 inode 来形成 IPC 标识符（如图 3.2），使用绝对路径还是相对路径对 inode 没有影响。

## 14.7 共享内存限制

与 System V 消息队列和 System V 信号一样，System V 共享内存存在某些系统限制（第 3.8 节）。图 14.5 显示了某些实现的值。第一列是包含该限制的传统 System V 变量名。

| 名称 | 说明 | DUNix 4.0 | Solaris 2.6 |
|---|---|---|---|

| `shmax` | 共享内存段的最大字节 | 4,194,304 | 1,048,576 |
| `shmid` | 共享内存段的最大字节 | | 1 |
| `shmni` | 全局共享内存标识符的最大 | 128 | 100 |
| `shmseg` | 每个进程挂载的最大共享内存段 | 32 | 6 |

图 14.5：System V 共享内存的典型系统限制。

### 示例

图 14.6 中的程序确定图 14.5 所示的四个限制。

```c
#include "sys/ipc.h" // shm/limits.c
#define MAX_NIDS 4096

int
main(int argc, char **argv)
{
    int i, j; shmid[MAX_NIDS];
    void *addr[MAX_NIDS];
    unsigned long size;

    /* 查看打开了多少标识符 */
    for (i = 0; i < MAX_NIDS; i++) {
        shmid[i] = shmget(IPC_PRIVATE, 1024, SVSHM_MODE | IPC_CREATE);
        if (shmid[i] == -1) {
            printf("%d open at once\n", i);
            break;
        }
    }
    for (j = 0; j < i; j++) {
        shmctl(shmid[j], IPC_RMID, NULL);
    }

    /* 查看我们挂载了多少 */
    for (i = 0; i < MAX_NIDS; i++) {
        shmid[i] = shmget(IPC_PRIVATE, 1024, SVSHM_MODE | IPC_CREATE);
        addr[i] = shmat(shmid[i], NULL, 0);
        if (addr[i] == (void *) -1) {
            printf("%d shared memory segments attached at once\n", i);
            shmctl(shmid[i], IPC_RMID, NULL);
            break;
        }
    }
    for (j = 0; j < i; j++) {
        shmdt(addr[j]);
        shmctl(shmid[j], IPC_RMID, NULL);
    }

    /* 查看我们能创建多小的共享内存段 */
    for (size = 1; size <= size++) {
        shmid[0] = shmget(IPC_PRIVATE, size, SVSHM_MODE | IPC_CREATE);
        if (shmid[0] == -1) {
            printf("minimum size of shared memory segment = %lu\n", size);
            shmctl(shmid[0], IPC_RMID, NULL);
            break;
        }
    }

    /* 查看我们能创建多大的共享内存段 */
    for (size = 65536; size <= 4096; size++) {
        shmid[0] = shmget(IPC_PRIVATE, size, SVSHM_MODE | IPC_CREATE);
        if (shmid[0] == -1) {
            printf("maximum size of shared memory segment = %lu\n", size - 4096);
            shmctl(shmid[0], IPC_RMID, NULL);
            break;
        }
    }

    exit(0);
}
```

图 14.6 确定共享内存的系统限制。

## 第 14 章

我们在 Digital Unix 4.08 下运行此程序。

`alpha % limits`

同时打开 127 个标识符

同时连接 32 个共享内存段

共享内存段最小大小 = 1

共享内存段最大大小 = 4194304

图 14.5 显示有 128 个标识符但我们的程序只能创建 127 个标识符的原因是系统守护进程已经创建了一个共享内存段。

## 14.8 总结

System V 共享内存在概念上与 Posix 共享内存相似。最常用的函数调用有：

```
shmget 获取标识符，
shmat 将共享内存段附加到进程地址空间，
带有 IPC_STAT 命令的 shmctl 获取现有共享内存段的大小，以及
带有 IPC_RMID 命令的 shmctl 移除内存对象。
```

不同之处在于，Posix 共享内存对象的大小可以通过调用 `ftruncate` 随时更改（如练习 13.1所示），而 System V 共享内存对象的大小由 `shmget` 固定。

## 练习

- 14.1 图 6.8 是图 6.6 的修改，它接受标识符而不是路径名来指定队列。我们证明了访问 System V 消息队列只需要标识符（假设我们有足够的权限）。对图 14.4 进行类似的修改，证明相同的功能也适用于 System V 共享内存。

## 第 5 部分

## 远程过程调用

## 15

## Doors (门)

### 15.1 引言

在讨论客户端-服务器场景和过程调用时，有三种类型的过程调用，我们在图 15.1 中所示。

- 1. 本地过程调用是我们在日常 C 编程中熟悉的调用：被调用的过程（函数）和调用过程都在同一个进程中。通常，会执行某些机器指令将控制权转移到新过程，被调用的过程保存寄存器并在栈上为局部变量分配空间。

- 2. 远程过程调用 (`RPC`) 是被调用的过程和调用过程位于不同的进程中。我们通常将调用者称为客户端，被调用的过程称为服务器。在图 15.1 的中间场景中，我们展示了客户端和服务器在同一主机上执行。这是底部场景的一种自由发生的特例，它赋予我们调用另一主机上过程（函数）的能力。一个进程（服务器）提供一个过程，供其他进程（客户端）通过调用该过程的“门”(`door`)来访问。我们也可以把门视为一种特殊的 IPC（进程间通信），因为信息以参数和返回值的形式在客户端和服务器之间交换。

- 3. 一般来说，`RPC` 允许一个主机上的客户端调用另一个主机上的过程，只要这两个主机通过某种形式的网络连接（图 15.1 中的底部场景）。这是我们在第 16 章中描述的内容。

356 Doors

第 15 章

![](img/1541bd224d292c30573e864db3959d59_362_0.png)

图 15.1 不同类型的过程调用。

从历史上看，门是为 Spring 分布式操作系统开发的，详情见 http://www.sun.com/tech/projects/spring。该操作系统中门 IPC 机制的描述见 [Hamilton and Kouyigaous 1991]。

门随后出现在 Solaris 2.5 中，尽管唯一的手页仅提到门是某些 Sun 应用程序使用的实验性接口。到了 Solaris 2.6，该接口在八页手册中被记录，但这些手册页将接口的稳定性列为演进中。未来 Linux 门版本对在本章中描述的 API 可能发生的更改描述见：http://www.cs.brown.edu/~linux/docs。
