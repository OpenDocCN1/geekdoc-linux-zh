
`sys_create_module()` 为模块分配内存。所需内存由 `size` 指定。它生成一个模块结构实例，其中 `name` 是模块的名称。该结构的以下值为：名称、大小（页数）、为模块分配的内存的起始地址以及状态（设置为 `MOD_UNINITIALIZED`）。所有其他值均初始化为 `NULL`。

```c
struct module {
    struct module *next; /* 下一个模块 */
    struct module_ref *ref; /* 模块列表 *
    /* * 指向我自己 */
    struct symbol_table *symtab; /* 符号表 * */
    char *name; /* 模块名称 * */
    int size; /* * 以页为单位的模块大小 * */
    void *addr; /* 模块地址 * */
    int state; /* 模块状态标志 * */
    void (*cleanup)(void); /* 清理例程 * */
};
```

如果已存在同名的模块，则返回错误，否则返回值为内核地址空间中分配的内存地址。`sys_init_module()` 加载并激活模块。`code` 是模块加载的地址，`size` 是以字节为单位。它不能超过 `module->size` 中存储的值。如果加载的模块没有在页边界结束，剩余部分将初始化为 0。返回 `mod_routines` 结构的指针是管理模块的接口。它包含两个函数指针，一个指向初始化，另一个指向模块的删除函数。

```c
struct mod_routines {
    int (*init)(void);      /* 初始化 */
    void (*cleanup)(void);  /* 清理 */
};
```

`symtab` 指针指向符号表。该表被加载，其指针通过加上表（在模块中）的地址重新计算。此外，对其他模块的引用会被输入它们的引用列表中。

模块加载后，会调用自身的初始化例程 `init()` 并将状态设置为 `MOD_RUNNING`；现在模块被激活。`sys_delete_module()` 移除模块。如果没有指定名称，则释放该模块。必须没有对该模块的引用，且其使用计数必须为 0。如果模块正在运行 `[MOD_RUNNING]`，则调用自身的清理函数并将状态设置为 `MOD_DELETED`。然后可以通过调用 `free_modules()` 移除模块，该函数搜索模块列表并尝试释放所有不再使用的模块。

`sys_get_kernel_sym()` 指向符号表。该表被加载，其指针通过加上表（在模块中）的地址重新计算。此外，对其他模块的引用会被输入它们的引用列表中。

模块加载后，会调用自身的初始化例程 `init()` 并将状态设置为 `MOD_RUNNING`；现在模块被激活。`sys_delete_module()` 移除模块。如果没有指定名称，则释放该模块。必须没有对该模块的引用，且其使用计数必须为 0。如果模块正在运行 `[MOD_RUNNING]`，则调用自身的清理函数并将状态设置为 `MOD_DELETED`。然后可以通过调用 `free_modules()` 移除模块，该函数搜索模块列表并尝试释放所有不再使用的模块。

`sys_get_kernel_sym()` 指向符号表。该表被加载，其指针通过加上表（在模块中）的地址重新计算。此外，对其他模块的引用会被输入它们的引用列表中。

模块加载后，会调用自身的初始化例程 `init()` 并将状态设置为 `MOD_RUNNING`；现在模块被激活。`sys_delete_module()` 移除模块。如果没有指定名称，则释放该模块。必须没有对该模块的引用，且其使用计数必须为 0。如果模块正在运行 `[MOD_RUNNING]`，则调用自身的清理函数并将状态设置为 `MOD_DELETED`。然后可以通过调用 `free_modules()` 移除模块，该函数搜索模块列表并尝试释放所有不再使用的模块。

`sys_get_kernel_sym()` 指向符号表。该表被加载，其指针通过加上表（在模块中）的地址重新计算。此外，对其他模块的引用会被输入它们的引用列表中。

```c
struct timespec {
  long tv_sec;      /* 秒 */
  long tv_nsec;      /* 纳秒 */
};
```

`timespec` 结构用于指定纳秒级的时间。指针通过加上表（在模块中）的地址重新计算。此外，对其他模块的引用会被输入它们的引用列表中。

`nanosleep()` 系统调用挂起调用线程。如果被信号中断，剩余时间通过 `timespec` 结构返回。`nanosleep()` 返回未睡眠的纳秒数。

## 错误

- `ENOSYS` - `func` 无效。
- `EINVAL` - `ptr` 为 0（读取）或设置错误（写入）。

| 系统 | Create_module | Delete_module | LINUX |
| :--- | :--- | :--- | :--- |
| call | get_kernel_sym | | |

`File`: `kernel/module.c`

```c
unsigned long sys_create_module(char*name, unsigned long size);
int sys_init_module(char *name, char *code, unsigned long codesize,
struct mod_routines *routines, struct symbol_table *symtab);
int sys_delete_module(char *name);
sys_get_kernel_sym(struct kernel_sym *tabelf);
```

`sys_create_module()` 为模块分配内存。所需内存由 `size` 指定。它生成一个模块结构实例，其中 `name` 是模块的名称。该结构的以下值为：名称、大小（页数）、为模块分配的内存的起始地址以及状态（设置为 `MOD_UNINITIALIZED`）。所有其他值均初始化为 `NULL`。

`nanosleep()` 系统调用挂起调用线程。如果被信号中断，剩余时间通过 `timespec` 结构返回。`nanosleep()` 返回未睡眠的纳秒数。

## 错误

- `ENOSYS` - `func` 无效。
- `EINVAL` - `ptr` 为 0（读取）或设置错误（写入）。

| 系统 | Create_module | Delete_module | LINUX |
| :--- | :--- | :--- | :--- |
| call | get_kernel_sym | | |

`File`: `kernel/module.c`

```c
unsigned long sys_create_module(char*name, unsigned long size);
int sys_init_module(char *name, char *code, unsigned long codesize,
struct mod_routines *routines, struct symbol_table *symtab);
int sys_delete_module(char *name);
sys_get_kernel_sym(struct kernel_sym *tabelf);
```

`sys_create_module()` 为模块分配内存。所需内存由 `size` 指定。它生成一个模块结构实例，其中 `name` 是模块的名称。该结构的以下值为：名称、大小（页数）、为模块分配的内存的起始地址以及状态（设置为 `MOD_UNINITIALIZED`）。所有其他值均初始化为 `NULL`。

```c
struct module {
    struct module *next; /* 下一个模块 */
    struct module_ref *ref; /* 模块列表 *
    /* * 指向我自己 */
    struct symbol_table *symtab; /* 符号表 * */
    char *name; /* 模块名称 * */
    int size; /* * 以页为单位的模块大小 * */
    void *addr; /* 模块地址 * */
    int state; /* 模块状态标志 * */
    void (*cleanup)(void); /* 清理例程 * */
};
```

如果已存在同名的模块，则返回错误，否则返回值为内核地址空间中分配的内存地址。`sys_init_module()` 加载并激活模块。`code` 是模块加载的地址，`size` 是以字节为单位。它不能超过 `module->size` 中存储的值。如果加载的模块没有在页边界结束，剩余部分将初始化为 0。返回 `mod_routines` 结构的指针是管理模块的接口。它包含两个函数指针，一个指向初始化，另一个指向模块的删除函数。
