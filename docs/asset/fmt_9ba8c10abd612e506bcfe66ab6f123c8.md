
当给定一个左值（`lvalue`）时，返回值可能是该左值可能具有的最大对齐。例如，结构体内部的左值可能比在结构体外部创建相同类型的实例具有更大的对齐要求，因为结构体对齐的要求。对齐问题将在第 19 章中进一步讨论。

相应的 `free_percpu()` 调用会在所有处理器上释放给定的数据。

对 `alloc_percpu()`（或 `__alloc_percpu()`）的调用返回一个指针，该指针用于间接引用动态创建的每 CPU 数据。内核提供了两个宏来简化这一过程：

```c
get_cpu_var(ptr);      /* 返回指向当前处理器 ptr 副本的 void 指针 */
put_cpu_var(ptr);      /* 完成；重新启用内核抢占 */
```

`get_cpu_var()` 宏返回指向当前处理器数据特定实例的指针。它还禁用内核抢占，随后通过调用 `put_cpu_var()` 重新启用。

让我们看一个使用这些函数的完整示例。当然，这个例子有点可笑，因为你通常只会分配一次内存（也许在某个初始化函数中），在各种地方使用它，然后释放一次（也许在某个关机函数中）。尽管如此，这个例子应该能清楚地说明使用方法：

```c
void *percpu_ptr;
unsigned long foo;

percpu_ptr = alloc_percpu(unsigned long);
if (!ptr)
    /* 内存分配错误 ...*/

foo = get_cpu_var(percpu_ptr);
/* 操作 foo ... */
put_cpu_var(percpu_ptr);
```
