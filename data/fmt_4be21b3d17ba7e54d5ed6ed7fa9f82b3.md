
# 第5章 每个开发者都应该了解的内核

## 5.6 用户空间中的内存管理

```
004eb000   4K rw- /lib/ld-2.3.5.so
004e0000 118K r-x /lib/libc-2.3.5.so
00612000   8K r--x /lib/libc-2.3.5.so
00614000   8K r--x /lib/libc-2.3.5.so
00616000   8K r--x [ anon ]
08040000   4K rw- /home/john/examples/mm/pause
08049000   4K rw- /home/john/examples/mm/pause
b7f08000   4K rw- [ anon ]
b7f1a000   4K rw- [ anon ]
bfb05000   88K rw- [ stack ]
ffff0000   4K --- [ anon ]
total      1412K
```

`pmap` 命令列出了虚拟内存各个段的虚拟地址和大小。如你所示，每个内存区域都有一组类似于文件的权限。在每个区域旁边，`pmap` 列出了与映射关联的文件（如果有）。你可以从这个输出中看到，进程什么都没做就消耗了约 1.4MB 的虚拟内存，大部分被 C 标准库（`/lib/libc-2.3.5.so`）消耗了。另一个罪祸是动态链接器（`ld-2.3.5.so`），它消耗了 112K。我的简单代码只占了 4K，这是一个内存页——最小尺寸。我应该指出，虽然 `lib` 消耗了 1MB 的虚拟内存，但只读段在系统中使用的所有进程之间共享——也就是说，该库在整个系统中只消耗了 1MB 的物理存储。这是共享库的主要优势之一。关于映射需要注意的另外一点是，可能存在间隙。

### 5.6.2 内存耗尽

任何系统都在不断变化中，随时都在分配和释放内存。许多进程会在短时间内分配小块内存；而其他进程则分配一次内存后永不释放。即使系统有足够的内存，进程也可能耗尽内存，而在某些进程继续无错误运行的同时，系统也可能耗尽内存。这完全取决于具体情况。

标准库和交换分区（swap partition）在普通程序员试图掌握可用内存量时，往往会合在一起让其感到困惑。交换磁盘让你的系统看起来拥有的物理内存比实际 own。因此，当你想知道有多少可用内存时，答案通常是模糊的。同时，标准库的技巧可能会让进程看起来分配的内存远超系统允许的范围。更令问题复杂的是，进程可能不会崩溃。

#### 5.6.2.1 进程耗尽内存时

进程通过两种方式耗尽内存：它们可能耗尽虚拟地址，也可能耗尽物理存储。耗尽虚拟地址看起来似乎是不可能的。毕竟，如果你只有 1GB 的 DRAM 且没有交换磁盘，那么 `malloc` 会不会在耗尽虚拟地址很久以前就失败了？列表 5-4 中的程序说明情况并非如此。该程序以 1MB 为块持续分配内存，直到 `malloc` 失败。

**列表 5-4 疯狂的 malloc.c：尽可能分配大量内存**

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    void *ptr;
    int n = 0;
    while (1) {
        // 以 1 MB 为块进行分配
        ptr = malloc(0x1000000);
        // 当无法再分配内存时停止
        if (ptr == NULL)
            break;
        n++;
    }
    // 我们获取了多少？
    printf("malloced %d MB\n", n);
    // 停止以便我们可以查看造成的后果
    pause();
}
```

我在一台拥有 160MB RAM 且禁用了交换区的 32 位机器上运行了列表 5-4 中的程序。猜猜发生了什么？`malloc` 一直到进程分配到几乎调用 `pause` 之前都没有失败，你可以查看内存映射：

```
$ ./crazy-malloc &
[1] 2817
malloced 3056 MB
$ jobs -x pmap \
2823: ./crazy-malloc
000c000 412K r---
004d000 104K r-x-- /lib/ld-2.3.5.so
004ea000 4K r---- /lib/ld-2.3.5.so
004eb000 4K r---- /lib/ld-2.3.5.so
004ee000 1168K r-x-- /lib/libc-2.3.5.so
0061200 8K r---- /lib/libc-2.3.5.so
0061400 8K r---- /lib/libc-2.3.5.so
0061600 8K r----
006f060 124388K r---- /home/john/examples/mm/crazy-malloc
0804800 4K r-x--
0804900 4K r---- /home/john/john/mm/crazy-malloc
0805100 2882516K r---
```

##### 虚拟内存与堆

在 `crazy-malloc` 示例中，代码在一个只有 160MB 内存且没有交换分区的系统上分配了几乎所有的用户空间作为动态内存。该映射展示了标准库如何通过 `mmap` 调用在用户空间中创建匿名映射。使用 `strace`，你可以看到 `malloc` 调用会导致如下 `mmap` 调用：

```
mmap2(NULL, 1052672, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0)
```

`mmap2` 系统调用通过设置 `MAP_ANONYMOUS` 标志允许分配内存。这不需要存储设备驱动，因此文件描述符参数为 -1。为了效率，内核推迟到这些页面被使用时再寻找物理空间，因此 `mmap2` 返回了一个并不存在的虚拟内存指针。只有当你尝试使用这个虚拟地址时，物理内存才会被分配。当这种情况发生时，会触发页错误，这是一个非常有效的技术，通过防止不必要的内存访问来提高许多操作的效率。

如果你修改列表 5-4 中的程序来修改它分配的数据，它将强制发生页错误，然后你将看到完全不同的行为，如列表 5-5 所示。

**列表 5-5 crazy-malloc2.c：分配内存并触摸**

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    void *ptr;
    int n = 0;
    while (1) {
        // 按 1MB 块分配
        ptr = malloc(0x1000000);
        // 当无法再分配更多内存时停止
        if (ptr == NULL) {
            break;
        }
        // 修改数据。
        memset(ptr, 1, 0x100000);
        printf("malloc %d MB\n", ++ptr);
    }
    // 停止以便我们可以查看损坏。
    pause();
}
```

当列表 5-5 中的程序运行时，结果可能不是你预期的。程序并没有停下来让你检查损坏，而是在这里被杀了：

```
$ ./crazy-malloc2
malloc 1 MB
malloc 2 MB
malloc 3 MB
...
malloc 74 MB
Killed
$
```
