
回想一下，每个内存通过进程地址空间中的唯一区间进行描述。`vm_start` 字段是区间内的初始（最低）地址，而 `vm_end` 字段是区间内（最高）地址后的第一个字节。也就是说，`vm_start` 是包含的，而 `vm_end`是不包含的。内存区域的字节长度存在于区间 `[vm_start, vm_end)` 之上。同一地址空间中的不同内存区域之间不能重叠。

`vm_mm` 字段指向 VMA 关联的 `mm_struct`。注意，每个 VMA 对于其关联的 `mm_struct` 来说都是唯一的。因此，如果两个进程将同一个文件映射到各自的地址空间，每个进程都有一个唯一的 `vm_area_struct` 来识别其唯一的内存区域。相反，两个共享地址空间的线程也共享所有的 `vm_area_struct` 结构。

## VMA 标志

`vm_flags` 字段包含定义在 `<linux/mm.h>` 中的位标志，这些标志规定了内存区域包含的页的行为并提供了有关这些页的信息。与特定物理页关联的权限不同，VMA 标志规定的是内核负责的行为，而不是硬件。此外，`vm_flags` 包含了关于内存区域中每个页的信息，或者是整个内存区域的信息。表 15.1 是可能的 `vm_flags` 值列表。表 15.1 `vm_flags`

| 标志 | 对 VMA 页的影响 |
| :--- | :--- |
| `VM_READ` | 可以读取。 |
| `VM_WRITE` | 可以写入。 |
| `VM_EXEC` | 可以执行。 |
| `VM_SHARED` | 是共享的。 |
| `VM_MAYREAD` | `VM_READ` 标志可以设置。 |
| `VM_MAYWRITE` | `VM_WRITE` 标志可以设置。 |
| `VM_MAYEXEC` | `VM_EXEC` 标志可以设置。 |
| `VM_MAYHA` | `VM_SHARED` 标志可以向下增长。 |
| `VM_GROWOWN` | 区域向上增长。 |
| `VM_GROSUP` | 区域是共享的。 |
| `VM_DENY` | 禁止。 |
| `VM_LOCKED` | I/O。 |
| `VM_TO` | 顺序。 |
| `VM_RANDOM` | 随机。 |
| `VM_DONTCOPY` | 扩展。 |
| `VM_RESERVED` | 账户。 |
| `VM_HUGETLB` | 非线性。 |

# 第 15 章 进程地址空间

`vm_flags` 字段

让我们深入查看一些最重要的标志。`VM_READ`、`VM_WRITE` 和 `VM_EXEC` 标志规定了该区域的读、写、执行权限。例如，进程的代码可能映射为 `VM_READ` 和 `VM_WRITE`。相反，只读数据只会映射为 `VM_READ`。

`VM_SHARED` 标志指定内存区域是否在多个进程之间共享。如果设置了该标志，直观地称为共享映射。如果未设置，则只有一个进程可以查看此映射，它被称为私有映射。`VM_TO` 标志指定此区域是设备 I/O，由设备驱动程序在调用 `mmap()` 时设置，内存区域不能包含在任何进程的核心中。`VM_RESERVED` 标志指定区域不能被换出。`VM_SEQ` 标志向内核提供了一个提示，应用程序正在执行顺序（即线性且连续的）读取。内核可以选择增加底层文件的预取性能。`VM_READ` 标志则恰恰相反：应用程序正在执行随机（即非顺序的）读取。内核可以选择减少或完全取消底层文件的预取。这些标志分别通过 `madvise()` 系统调用带有 `MADV_SEQUENTIAL` 和 `MADV_RANDOM` 标志设置。预取是顺序请求数据的行为，即额外数据很快就会需要。如果应用程序顺序读取数据，这种行为是有益的。然而，如果访问模式是随机的，预取就是无效的。

### 操作

`vm_area_struct` 中的 `vm_ops` 字段指向与通用内存区域关联的操作表，内核可以调用它来管理 VMA。`vm_area_struct` 作为作为任何类型内存区域的通用对象，而操作描述了可以操作该对象实例的具体方法。

操作由 `struct vm_operations_struct` 表示，并定义在 `<linux/mm.h>` 中：

```c
struct vm_operations_struct {
    void (*open)(struct vm_area_struct *);
    void (*close)(struct vm_area_struct *);
    int (*fault)(struct vm_area_struct *, struct vm_fault *);
    int (*page_mwrite)(struct vm_area_struct *, struct vma *, struct vm_fault *vmf);
    int (*access)(struct vm_area_struct *, unsigned long
            void (*, int, int);
};
```

以下是每个单独方法的描述：

- `void open(struct vm_area_struct *area)`
  当给定的内存区域添加到地址空间时，调用此函数。
- `void close(struct vm_area_struct *area)`
  当给定的内存区域从地址空间中移除时，调用此函数。
- `int fault(struct vm_area_struct *area, struct vm_fault *vmf)`
  当访问不在物理内存中的页时，由页异常处理程序调用此函数。
- `int page_mkwrite(struct vm_area_struct *area, struct vm_fault *vmf)`
  当只读页被设为可写时，由页异常处理程序调用此函数。
- `int access(struct vm_area_struct *vma, unsigned long address, void *buf, int len)`
  当 `get_user_pages()` 失败时，由 `access_process_vm()` 调用此函数。

## 内存区域的列表与树

正如前所述，内存区域是通过内存描述符的 `mmap` 和 `mm_rb` 字段访问的。这两个数据结构指向与内存描述符相关的所有内存区域对象。事实上，它们都包含指向相同 `vm_area_struct` 结构的指针，分别通过单向链表链接了所有的内存对象。

第一个字段 `mmap`，每个 `vm_area_struct` 结构通过其 `vm_next` 字段链接到列表中。这些区域按地址排序。

第二个字段 `mm_rb` 将所有内存对象连接在红黑树（red-tree）中。红黑树的根是 `mm_rb`，地址空间中的每个 `vm_area_struct` 都通过其 `vm_rb` 字段链接到树上。

红黑树是一种平衡二叉树。红黑树中的每个元素都是节点。初始节点称为根。大多数节点有两个孩子：左孩子和右孩子。某些节点只有一个孩子，而末尾节点（叶节点）没有孩子。对于任何节点，左侧的元素值较小，而右侧的元素较大。此外，每个节点根据两个规则分配一种颜色（红色或黑色，这也是这种树的名称）：红色节点的子节点是黑色的，且从节点到叶子节点的每条路径必须包含相同数量的黑色节点。根节点始终是红色的。树的搜索和插入操作复杂度为 `O(log n)`。

当需要遍历特定的内存区域时，使用链表。当需要在地址空间定位特定的内存区域时，使用红黑树。通过这种方式，内核利用冗余的数据结构，无论对内存区域执行什么操作，都能提供优的性能。

## 生活中的内存区域

让我们看看特定进程的地址空间及其内部内存区域。此任务使用了非常有用的 `/proc` 文件系统和 `mmap(1)` 工具。该示例是一个简单的用户空间程序，除了作为示例外，没有做任何有价值：

```c
int main(int argc, char *argv[])
{
    return 0;
}
```

注意此进程地址空间中的几个内存区域。首先，你知道有文本段（`text`）、数据段（`data`）和 `BSS`（`bss`）。假设此进程与 C 库动态链接，这三个内存区域也存在于 `libc.so` 以及 `ld.so` 中。最后，还有进程栈。

`/proc/<pid>/maps` 的输出列出了该进程地址空间中的内存区域：

```
rlove@host $ cat /proc/1426/maps
00e8000-0faf000 r-xp 0000000 01 208530 /lib/tls/libc-2.5.1.so
0faf000-0fb2000 rw-p 0000000 01 208530 /lib/tls/libc-2.5.1.so
0fb2000-0fb4000 rw-p 0000000 00 00 -
08408000-08409000 r-xp 0000000 03 439029 /home/rlove/src/example
08409000-0840a000 rw-p 0000000 03 439029 /home/rlove/src/example
40000000-40015000 rw-p 0000000 01 80276 /lib/ld-2.5.1.so
```
