
使用 `memalign()` 或 `posix_memalign()` 分配的内存块应该用 `free()` 释放。

在某些 UNIX 实现中，无法对通过 `memalign()` 分配的内存块调用 `free()`，因为 `memalign()` 的实现使用 `malloc()` 分配内存块，然后返回该块中具有适当对齐地址的指针。glibc 的 `memalign()` 实现不受此限制影响。

## 在栈上分配内存：`alloca()`

与 `malloc` 家族一样，`alloca()` 动态分配内存。然而，`alloca()` 不是从堆上获取内存，而是通过增加栈帧的大小从栈上获取内存。这是可能的，因为调用函数的栈帧根据定义就位于栈的顶端。因此，帧上方有供扩展的空间，这可以通过简单修改栈指针的值来实现。

```c
#include <alloca.h>

void *alloca(size_t size);

// 返回指向分配内存块的指针
```

`size` 参数指定了在栈上分配的字节数。`alloca()` 函数返回指向分配内存的指针作为结果。
事实上，我们不需要也不允许调用 `free()` 来释放通过 `alloca()` 分配的内存。同样，无法使用 `realloc()` 来调整由 `alloca()` 分配的内存块的大小。
尽管 `alloca()` 不是 SUSv3 的，但在大多数 UNIX 实现中都提供，因此具有良好的移植性。

旧版本的 glibc 以及某些 UNIX 实现（主要是 BSD 派系）要求包含 `<stdlib.h>` 而不是 `<alloca.h>` 来获取 `alloca()` 的声明。

如果由于调用 `alloca()` 导致栈溢出，程序的行为将是不可预测的。特别是，我们可能会收到 `SIGGV` 信号。注意我们不能在如下示例中使用 `alloca()`：

```c
func(x, alloca(size));      /* 错误！ */
```

这是因为 `alloca()` 分配的空间会出现在帧的中间（参数空间）。

```c
y = alloca(size);
func(x, y);
```
