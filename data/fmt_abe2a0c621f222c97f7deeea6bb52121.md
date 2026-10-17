
```c
#include <unistd.h>
#include <sys/mman.h>

void *mmap(void *start, size_t length, int prot, int flags, int fd, off_t offset);
int *munmap(void *start, size_t length, int prot, int flags, int fd, off_t offset);
```

这请求从 `fd` 指定的文件中，从 `offset` 开始映射到内存字节。`offset` 必须是页的整数倍数。

该地址是用于映射的首选地址；如果它是 0（通常情况），`mmap()` 将选择该地址并将其放入返回值：

`prot` 是内存保护。它包含以下位：

这里是一个使用匿名内存映射在父子进程之间共享内存的简单示例：

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <sys/wait.h>
```

| 值 | 含义 |
| --- | --- |
| `PROT_EXEC` | 页面可以执行。 |
| `PROT_READ` | 页面可以读取。 |
| `PROT_WRITE` | 页面可以写入。 |
| `PROT_NONE` | 页面不可被访问。 |

```c
int main (int argc, char **argv) {

    int fd = -1, size = 4096;
    char *args;
    pid_t pid;
    int status;
    void *area;

    area = mmap(NULL, size, PROT_READ | PROT_WRITE,
               MAP_SHARED | MAP_ANONYMOUS, -1, 0);

    pid = fork();
    if (pid == 0) {
        /* 子进程 */
        printf("Child has written: %s\n", args);
        exit(EXIT_SUCCESS);
    }

    if (pid > 0) {
        /* 父进程 */
        wait (&status);
        printf("Parent has read: %s\n", area);
        exit (EXIT_SUCCESS);
    }
    exit (EXIT_FAILURE);
}
```

`munmap` 删除映射并导致对该范围内地址的进一步引用产生无效内存。

绝大部分工作是由函数 `remap_pfn_range()` 完成的。请注意，这允许映射内存跨越 4 KB 的屏障。

参见 `man mmap` 获取更多关于错误代码的信息。

这是一个测试 `mmap()` 入口的程序的简单示例：

## 18.8 mmap() 的驱动入口点

```c
#include <linux.h>
#include <unistd.h>
#include <string.h>
#include <stdlib.h>
#include <errno.h>
#include <sys/mman.h>
```

从内核侧，驱动入口点如下：

```c
int (*mmap)(struct file *file, struct vm_area_struct *vma, unsigned long len);
```

```c
#define DEATH(msg) pperror(msg); exit(errno);
```

`vm_area_struct` 结构定义在 `/usr/include/linux/mm.h` 中，包含了许多重要字段。基本元素是：

```c
int main (int argc, char **argv) {

    int fd, size, rc;
    char *area, *mmap, *nodename = "/dev/cdrom";
    char *info = NULL;

    if (argc > 1)
        nodename = argv[1]; /* 默认使用参数 */
    size = atoi(argv[1]);
    if (argc >= 2)
```

```c
struct vm_area_struct {
    unsigned long start;
    unsigned long end;
    unsigned long vm_flags;
    vm_prot_t prot;
    struct file *vm_file;
    struct vm_operations_struct *vm_ops;
    struct vm_area_struct *vm_page_fault;
    struct vm_area_struct *vm_next;
    struct vm_area_struct *vm_prev;
    struct vm_area_struct *vm_parent;
    struct vm_area_struct *vm_private;
    struct vm_area_struct *vm_child;
    struct vm_area_struct *vm_vm;
    struct vm_area_struct *vm_hash;
    struct vm_area_struct *vm_rb;
    
    ____ *vm_vm_
;
    _ vm_
;
    vm_vm_
;
    struct vm_area_struct *vm_vm;
    
    _____vm_vm;



______vm_vm_




___

___



```

*(注：由于原文中 `vm_area_struct` 的定义部分存在大量碎片化占位符，此处根据上下文逻辑翻译进行了结构化对齐)*

其他非 POSIX 标志可以指定（使用 `mmap()`），`MAP_ANONYMOUS` 标志允许仅在内存中映射，而不与文件关联。

## 18.7 mmap() 的用户空间函数

从用户侧，内存映射通过以下方式完成：

```c
#include <unistd.h>
#include <sys/mman.h>

void *mmap(void *start, size_t length, int prot, int flags, int fd, off_t offset);
int *munmap(void *start, size_t length, int prot, int flags, int fd, off_t offset);
```

这请求从 `fd` 指定的文件中，从 `offset` 开始映射到内存字节。`offset` 必须是页的整数倍数。

该地址是用于映射的首选地址；如果它是 0（通常情况），`mmap()` 将选择该地址并将其放入返回值：

`prot` 是内存保护。它包含以下位：

这里是一个使用匿名内存映射在父子进程之间共享内存的简单示例：

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/types.h>
#include <sys/wait.h>
```

| 值 | 含义 |
| --- | --- |
| `PROT_EXEC` | 页面可以执行。 |
| `PROT_READ` | 页面可以读取。 |
| `PROT_WRITE` | 页面可以写入。 |
| `PROT_NONE` | 页面不可被访问。 |
