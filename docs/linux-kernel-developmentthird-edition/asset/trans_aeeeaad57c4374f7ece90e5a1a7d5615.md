

## VMA 标志

`vm_flags` 字段包含位标志，定义在 `<linux/mm.h>` 中，用于指定内存区域中包含的页面的行为并提供相关信息。与特定物理页面的权限不同，VMA 标志指定的是内核负责的行为，而非硬件负责的行为。此外，`vm_flags` 包含的信息与内存区域中的每个页面或整个内存区域相关，而不是特定单个页面的信息。表 15.1 列出了 `vm_flags` 的可能值。

**表 15.1** `vm_flags`

| 标志 | 对 VMA 及其页面的影响 |
|:---|:---|
| VM_READ | 页面可读。 |
| VM_WRITE | 页面可写。 |
| VM_EXEC | 页面可执行。 |
| VM_SHARED | 页面是共享的。 |
| VM_MAYREAD | 可以设置 `VM_READ` 标志。 |
| VM_MAYWRITE | 可以设置 `VM_WRITE` 标志。 |
| VM_MAYEXEC | 可以设置 `VM_EXEC` 标志。 |
| VM_MAYSHARE | 可以设置 `VM_SHARE` 标志。 |
| VM_GROWSDOWN | 该区域可以向低地址扩展。 |
| VM_GROWSUP | 该区域可以向高地址扩展。 |
| VM_SHM | 该区域用于共享内存。 |
| VM_DENYWRITE | 该区域映射了一个不可写的文件。 |
| VM_EXECTABLE | 该区域映射了一个可执行文件。 |
| VM_LOCKED | 该区域内的页面被锁定。 |
| VM_IO | 该区域映射了设备的 I/O 空间。 |
| VM_SEQ_READ | 页面似乎是被顺序访问的。 |
| VM_RAND_READ | 页面似乎是被随机访问的。 |
| VM_DONTCOPY | 在 `fork()` 时不得复制此区域。 |
| VM_DONTDUMP | 此区域不能通过 `mmap()` 增长。 |
| VM_RESERVED | 此区域不得被换出。 |
| VM_ACCOUNT | 此区域是一个被记账的 VM 对象。 |
| VM_HUGETLB | 此区域使用 hugeTLB 页面。 |
| VM_NONLINEAR | 此区域是一个非线性映射。 |

让我们深入了解一些重要且有趣的标志。`VM_READ`、`VM_WRITE` 和 `VM_EXEC` 标志指定了*此特定内存区域*中页面通常的读、写和执行权限。根据需要组合这些标志，形成进程访问此 VMA 时必须遵守的适当访问权限。例如，进程的目标代码可能映射为 `VM_READ` 和 `VM_EXEC`，但不包括 `VM_WRITE`。另一方面，可执行对象的数据段将映射为 `VM_READ` 和 `VM_WRITE`，但 `VM_EXEC` 没有太大意义。同时，只读的内存映射数据文件仅映射 `VM_READ` 标志。

`VM_SHARED` 标志指定内存区域是否包含在多个进程之间共享的映射。如果设置了该标志，则直观地称为*共享映射*。如果未设置该标志，则只有单个进程可以查看此特定映射，这被称为*私有映射*。

`VM_IO` 标志指定此内存区域是设备 *I/O* 空间的映射。当对设备的 *I/O* 空间调用 `mmap()` 时，通常由设备驱动程序设置此字段。它规定了该内存区域不得包含在任何进程的内存转储中，以及其他内容。`VM_RESERVED` 标志指定内存区域不得被换出。它也用于设备驱动映射。

`VM_SEQ_READ` 标志向内核提供提示，表明应用程序正在此映射中执行*顺序*（即线性且连续）读取。然后内核可以选择增加支持文件上的预读量。`VM_RAND_READ` 标志指定完全相反的情况：应用程序正在此映射中执行*相对随机*（即非顺序）读取。然后内核可以选择减少或完全禁用支持文件上的预读。这些标志分别通过带有 `MADV_SEQUENTIAL` 和 `MADV_RANDOM` 标志的 *madvise()* 系统调用设置。预读是指在请求数据之前顺序读取额外数据的行为，希望这些数据很快会被需要。如果应用程序是顺序读取数据，这种行为是有利的。然而，如果数据访问模式是随机的，预读则无效。

## VMA 操作

`vm_area_struct` 结构体中的 `vm_ops` 字段指向与特定内存区域关联的操作表，内核可以调用这些操作来操纵 VMA。

`vm_area_struct` 充当表示任何类型内存区域的通用对象，而操作表描述的是可以在此对象的特定实例上执行的具体方法。

操作表由 `struct vm_operations_struct` 表示，并定义在 `<linux/mm.h>` 中：

```c
struct vm_operations_struct {
    void (*open)(struct vm_area_struct *);
    void (*close)(struct vm_area_struct *);
    int  (*fault)(struct vm_area_struct *, struct vm_fault *);
    int (*page_mkwrite)(struct vm_area_struct *, struct vm_fault *vmf);
    int (*access)(struct vm_area_struct *, unsigned long ,
                  void *, int, int);
};
```

以下是每个单独方法的描述：

- `void open(struct vm_area_struct *area)`
  - 当给定的内存区域被添加到地址空间时，调用此函数。
- `void close(struct vm_area_struct *area)`
  - 当给定的内存区域从地址空间中移除时，调用此函数。
- `int fault(struct vm_area_struct *area, struct vm_fault *vmf)`
  - 当访问了一个不存在于物理内存中的页面时，由缺页异常处理程序调用此函数。
- `int page_mkwrite(struct vm_area_struct *area, struct vm_fault *vmf)`
  - 当某个原本只读的页面变为可写时，由缺页异常处理程序调用此函数。
- `int access(struct vm_area_struct *vma, unsigned long address, void *buf, int len, int write)`
  - 当 `get_user_pages()` 失败时，由 `access_process_vm()` 调用此函数。

## 内存区域的列表和树

如前所述，内存区域通过内存描述符的 mmap 和 mm_rb 字段进行访问。这两个数据结构独立地指向与内存描述符关联的所有内存区域对象。事实上，它们都包含指向相同 vm_area_struct 结构体的指针，只是表示方式不同。

第一个字段 mmap 将所有内存区域对象链接成一个单链表。每个 vm_area_struct 结构体通过其 vm_next 字段链接到列表中。区域按地址升序排序。第一个内存区域是 mmap 指向的 vm_area_struct 结构体。最后一个结构体指向 NULL。

第二个字段 mm_rb 将所有内存区域对象链接成一棵红黑树。红黑树的根是 mm_rb，该地址空间中的每个 vm_area_struct 结构体都通过其 vm_rb 字段链接到树中。

红黑树是一种平衡二叉树。红黑树中的每个元素称为节点。初始节点称为树的根。大多数节点有两个子节点：左子节点和右子节点。一些节点只有一个子节点，而最终的节点称为叶子，没有子节点。对于任何节点，左侧的元素值较小，而右侧的元素值较大。此外，每个节点根据两条规则分配一种颜色（红色或黑色，因此得名）：红色节点的子节点是黑色的，并且从节点到叶子的任何路径必须包含相同数量的黑色节点。根节点总是红色的。搜索、插入和删除操作的时间复杂度为 O(log(n))。

当需要遍历每个节点时使用链表。当需要在地址空间中定位特定内存区域时使用红黑树。通过这种方式，内核使用冗余数据结构，无论对内存区域执行什么操作，都能提供最佳性能。

## 现实生活中的内存区域

让我们查看特定进程的地址空间及其内部的内存区域。此任务使用了有用的 `/proc` 文件系统和 `pmap(1)` 工具。示例是一个简单的用户空间程序，除了作为一个示例外，完全没有任何价值：

```c
int main(int argc, char *argv[])
{
    return 0;
}
```

注意此进程地址空间中的几个内存区域。首先，你知道有文本段、数据段和 bss。假设此进程与 C 库动态链接，那么 `libc.so` 和 `ld.so` 中也有这三个内存区域。最后，还有进程的栈。

`/proc/<pid>/maps` 的输出列出了此进程地址空间中的内存区域：

```text
rlove@wolf:~$ cat /proc/1426/maps
00080000-00fa0000 r-xp 00000000 03:01 208530          /lib/tls/libc-2.5.1.so
00faf000-00fb2000 rw-p 0012f000 03:01 208530          /lib/tls/libc-2.5.1.so
00fb2000-00fb4000 rw-p 0012f000 00:00 0
00a84000-00a88000 r-xp 00000000 03:03 439029          /home/rlove/src/example
08a49000-08a4a000 rw-p 00000000 03:03 439029          /home/rlove/src/example
40000000-40015000 r-xp 00000000 03:01 80276           /lib/ld-2.5.1.so
40015000-40016000 rw-p 00000000 03:01 80276           /lib/ld-2.5.1.so
4001e000-4001f000 rw-p 00000000 00:00 0
bfff6000-c0000000 rwzp ffffff00 00:00 0
```

数据格式如下：

```text
start-end permission  offset  major:minor  inode  file
```

`pmap(1)` 工具¹ 以更易读的方式格式化此信息：

```text
rlove@wolf:~$ pmap 1426
example(1426)
00e80000 (1212 KB) r-xp  (03:01 208530)   /lib/tls/libc-2.5.1.so
00faf000 (12 KB)    rw-p (03:01 208530)   /lib/tls/libc-2.5.1.so
00fb2000 (8 KB)     rw-p (00:00 0)
08a48000 (4 KB)     r-xp (03:03 439029)   /home/rlove/src/example
```

> ¹ `pmap(1)` 工具显示进程内存区域的格式化列表。它比 `/proc` 输出更易于阅读，但包含相同的信息。它可以在较新版本的 procs 包中找到。

