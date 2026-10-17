
对于 `shmctl` `SHM_LOCK` 操作，`RLIMIT_MEMLOCK` 定义了该进程真实用户 ID 可以锁定的共享内存段字节数的用户级限制。当进程执行 `shmctl` `SHM_LOCK` 操作时，内核会检查 System V 共享内存的字节总数是否已记录为调用进程的真实用户 ID 锁定。如果待锁定段的大小不会超过该进程 `RLIMIT_MEMLOCK` 限制总和，则操作成功。

`RLIMIT_MEMLOCK` 对于 System V 共享内存具有不同的语义，因为共享内存段即使在没有任何进程挂载时也可以继续存在。（它只有在显式调用 `shmctl()` `IPC_RMID` 操作后才被移除，并且在所有进程都从其地址空间中分离后才移除。）

## 锁定和解锁内存区域

进程可以使用 `mlock()` 和 `munlock()` 来锁定和解锁内存区域。

```c
#include <sys/mman.h>

int mlock(void *addr, size_t length);
int munlock(void *addr, size_t length);
```

## 内存锁定的语义细节

在以下段落中，我们注意到了一些内存锁定的语义细节。

内存锁定不会被通过 `fork()` 创建的子进程继承，也不会跨 `exec()` 执行。

当多个进程共享一组页（例如 `MAP_SHARED`），只要至少有一个进程持有锁定，这些页就会保持锁定状态。

内存锁定按页执行的这一事实意味着对同一页上的不同结构独立地应用 `mlock()` 和 `munlock()` 在逻辑上是不正确的。例如，假设我们在同一页内有两个由 `p1` 和 `p2` 指向的数据结构，我们执行了以下调用：

```c
mlock(*pi, len1);
mlock(*p2, len2); /* 实际上没有作用 */
munlock(*pi, len1);
```

上述所有调用将成功，但在该序列结束时，该页被解锁；`p2` 的数据结构未被锁定。

注意 `shmctl` `SHM_LOCK` 操作（第 48.7 节）的语义与 `mlock()` 和 `mlockall()` 不同，如下：

- 在 `SHM_LOCK` 操作后，页只有在发生异常时才被锁定到内存。相比之下，`mlock()` 和 `mlockall()` 在调用返回之前会将所有锁定的页调入内存。
- `SHM_LOCK` 操作设置的是共享内存段的属性，而不是进程的属性。（由于此原因，`proc/pid/status` 文件中的 `Vlock` 字段不包含任何已挂载共享内存段的大小。这意味着，一旦调入内存，即使所有进程都分离了共享内存段，这些页仍将留在内存中。）

`mlockall()` 系统调用根据标志掩码，将进程虚拟地址空间中当前映射的所有页面、未来映射的所有页面，或两者都锁定。该掩码通过按位逻辑或（`OR`）操作将以下常量中的一个或多个组合来指定：

`MCL_CURRENT`

锁定当前映射到调用进程虚拟地址空间的所有页面。这包括当前为程序文本段（text）、数据段、内存映射和栈分配的所有页面。在指定 `MCL_CURRENT` 标志并成功调用后，保证调用进程的所有页面都将驻留在内存中。此标志不会影响随后在进程虚拟地址空间中分配的页面；对于这些页面，必须使用 `MCL_FUTURE`。

`MCL_FUTURE`

锁定随后映射到调用进程虚拟地址空间的所有页面。这些页面例如，可能是通过 `mmap()` 或 `shmat()` 映射的共享内存区域的一部分，也可能是向上增长或向下增长的栈的一部分。由于 `MCL_FUTURE` 标志的存在，如果系统没有足够的 RAM 分配给进程，或者达到了 `RIMIT_MEMLOCK` 限制，稍后的内存分配操作（例如 `mmap()`、`sbrk()` 或 `malloc()`）可能会失败，或者栈增长可能会导致 `SIGSEGV`。

适用于 `lock()` 创建的内存锁的约束、限制和继承的规则，也适用于通过 `munlock()` 创建的内存锁。

> `munlockall()` 系统调用会解锁调用进程的所有页面，并撤销任何之前的 `mlockall(MCL_FUTURE)` 调用的效果。使用 `munlock()` 时，解锁的页面不保证会通过此调用从 RAM 中移除。

在 Linux 2.6.9 之前，调用 `munlock()` 需要权限（`CAP_IPC_LOCK`）（不一致的是，`munlock` get不需要权限）。从 Linux 2.6.9 之后，不再需要该权限。

# 50.3 确定内存驻留：mincore()

`mincore()` 系统调用是内存锁定系统调用的互补。它报告虚拟地址中的页面当前是否驻留在 RAM 中，以及访问时是否会导致页错误（page fault）。

`SUSv3` 未指定 `mincore()`。它在许多但并非所有的 UNIX 实现中都可用。在 Linux 上，`mincore()` 从内核 2.4 版本起一直可用。

```c
#define BSD_SOURCE  /* 或者：#define SVID_SOURCE */
#include <sys/mman.h>

int mincore(void *addr, size_t length, unsigned char *vec);
成功时返回 0，错误时返回 -1
```

`mincore()` 系统返回从 `addr` 开始、长度为 `length` 字节的虚拟地址范围内的页面内存驻留信息。`addr` 中提供的地址必须是页对齐的，由于返回的是整页信息，`length` 实际上会向上取整到系统页大小的下一个倍数。

内存驻留信息在 `vec` 中返回，`vec` 必须是一个长度为 `(length + PAGE_SIZE - 1) / PAGE_SIZE` 字节的数组。（在 Linux 上，`vec` 类型为 `unsigned char *`；某些其他 UNIX 实现类型为 `char *`）；如果相应的页面驻留在内存中，则每个元素的最高位被设置为 1。在某些 UNIX 实现中，其他位的设置是未定义的，因此可移植应用程序应仅测试此。

`mincore()` 返回的信息在调用执行与检查 `vec` 元素之间可能会发生变化。只有通过 `mlock()` 或 `mlockall()` 锁定的页面保证驻留在内存中。

在 Linux 2.6.21 之前，由于各种实现上的问题，`mincore()` 无法正确报告 `MAP_PRIVATE` 映射或非线性映射（使用 `remap_file_pages()` 建立）的内存驻留信息。

列表 50-2 展示了 `mlock()` 和 `mincore()` 的用法。在使用 `mmap()` 分配并映射一个内存区域后，该程序使用 `mlock()` 每隔一段时间锁定该区域或其他组页面。（程序的每个命令行参数都是以页为单位的；程序根据需要将这些转换为字节，以满足 `mmap()`、`mlock()` 和 `mincore()` 用的要求。）在 `mlock()` 调用之前之后，程序使用 `mincore()` 获取该区域页面的内存驻留信息并以图形方式显示。

# 列表 50-2：使用 mlock() 和 mincore()

```c
#define BSD_SOURCE /* 获取 mincore() 声明和 MAP_ANONYMOUS

#include <sys/mman.h>      来自 <sys/mman.h> */
#include "tlpi.h"

/* 显示范围 [addr .. (addr + length - 1)] 内页面的驻留情况 */

static void
displayMincore(char *addr, size_t length)
{
    unsigned char *vec;
    long pageSize, numPages;
    pageSize = sysconf(_SC_PAGESIZE);
    numPages = (length + pageSize - 1) / pageSize;
    vec = malloc(numPages);
    if (vec == NULL)
        Err("malloc");
```

```c
if (mincore(addr, length, vec) == -1)
errExit("mincore");
```

```c
for (j = 0; j < numPages; j++) {
    if (j % 64 == 0) {
        printf("%s%10p: \%s\n", (j == 0) ? "" : "", addr + (j * pageSize));
        printf("%c", vec[j] & 1) ? '*' : '.');
    }
}
```

```c
printf("\n");

free(vec);
}
```
