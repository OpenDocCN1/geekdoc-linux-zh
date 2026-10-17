
```c
<module.h>
struct module {
    enum module_state;

    /* 模块列表成员 */
    struct list_head list;

    /* 此模块的唯一句柄 */
    char name[MODULE_NAME_LEN];

    /* 导出的符号 */
    const struct kernel_symbol *syms;
    unsigned int num_syms;
    const unsigned long *crcs;

    /* GPL 仅限符号 */
    const struct kernel_symbol *gpl_symbols;
    unsigned int num_syms;
    const unsigned long *crcs;

    /* 未来仅限 GPL 的符号 */
    const struct kernel_symbol *gpl_future_syms;
    unsigned int num_gpl_future_syms;
    const unsigned long *gpl_future_crcs;

    /* 异常表 */
    unsigned int num_entries;
    const struct exception_table *extable;

    /* 初始化函数 */
    int (*init)(void);

    /* 如果此非 NULL，在 init(0) 返回后释放 */
    void *module_init;
    void *module_code;

    /* 实际代码 + 数据，卸载时释放 */
    void *module_code;

    /* init 和 core 节的大小 */
    unsigned long init_size, core_size;

    /* 每个节中可执行代码的大小 */
    unsigned long init_text_size, core_text_size;

    /* 体系特定模块值 */
    struct arch_specific arch;
    unsigned int taints; /* 内核污染位 */
#ifndef CONFIG_MODULE_UNLOAD
    /* 引用计数 */
    struct module_ref [NR_CPUS];

    /* 哪些模块依赖我？ */
    struct list_head modules_which_use;

    /* 谁在等待我们卸载 */
    struct task_struct *waiter;

    /* 析构函数 */
    void (*exit)(void);
#endif
#ifndef CONFIG_KALLSYMS
    /* kallsyms 的符号和字符串表 */
    Elf *symtab;
    unsigned long num_symtab;
    char *strtab;

    /* 节属性 */
    struct module_sect_attrs *sect_attrs;

    /* 属性 */
    struct module_notes_attrs *notes_attrs;
#endif

    /* Per CPU 数据 */
    void *percpu;

    /* 命令行参数（可能损坏）。指向此指针 */
    char *args;
```

如此代码所示，结构定义取决于内核配置：

- `KALLSYMS` 配置选项（仅用于开启的系统）在内存中持有内核和已加载模块中定义符号列表（否则只存储导出的函数）。如果内核检测到偏离行为（例如引用了空指针），则 oops 消息不仅输出十六进制数字，还输出函数名称。

- 与 2.5 之前的版本相比，现在必须显式配置卸载模块的能力。除非选择了 `MODULE_UNLOAD` 配置选项，否则额外的信息不会包含在模块数据中。

与其他模块相关的其他影响 `struct module` 定义的配置选项如下：

- `MODVERSIONS` 版本控制；防止接口与当前版本不匹配的旧模块加载到内核中。7.5 节详细讨论了这一点。

- `MODULE_FORCE_UNLOAD` 允许强制从内核移除模块，即使仍有引用或代码被其他模块使用。这种强制方法在正常运行时不需要，但在开发期间有用。

- `KMOD` 允许内核在需要时自动卸载模块。这需要与用户态进行交互，将在下文中描述。

## `struct module` 的元素含义

- `state` 表示模块的当前状态，可以是 `module_state` 的值之一：

```c
<module.h>
enum module_state {
    MODULE_STATE_LIVE,
    MODULE_STATE_COMING,
    MODULE_STATE_GOING,
}
```

在加载期间，状态为 `MODULE_STATE_COMING`。在正常运行期间（完成所有初始化任务后），为 `MODULE_STATE_LIVE`；当模块正在移除时，状态为 `MODULE_STATE_GOING`。

`list` 是内核用于将所有加载的模块放在双向链表中的标准列表。在 `kernel/module.c` 中 `modules` 全局变量作为列表头。

`name` 指定模块的名称。此名称必须是唯一的，因为它会被引用，例如选择要卸载的模块。在这种情况下，二进制文件的名称通常不带 `.ko` 后缀——例如 VFAT 文件系统。

`syms`、`num_syms` 和 `crc` 用于导出模块的符号。`syms` 是一个包含 `num_syms` 个 `kernel_symbol` 类型元素的数组，负责分配标识符（名称）：

```c
<module.h>
struct kernel_symbol {
    unsigned long value;
    const char *name;
};
```

`crcs` 也是一个带有 `num_syms` 个元素的数组，存储导出符号的校验和以实现版本控制（见第 7.5 节）。

当导出符号时，内核不仅考虑可以无视被所有模块使用的符号，还考虑可能被 GPL 兼容许可证使用的符号。第三类模块目前可能由任何许可证使用，但未来将仅限 GPL 许可。`gpl_syms`、`num_gpl_syms` 和 `gpl_crc` 用于 GPL 仅限符号。它们具有上述相同的条，但负责管理现在或未来可能被 GPL 兼容模块使用的符号。

另外两组符号（为了简洁起见从上面的定义中省略）由结构成员 `unused_gpl_syms` 和 `unused_syms` 描述。这些集合用于存储已导出但未被内核内模块使用的（GPL 仅限）符号。当树外模块使用这种类型的符号时，内核会打印警告。

应当发生内核恐慌

> 当发生致命内部错误且无法继续通用操作时，会触发内核恐慌。

## 第 7 章：模块

错误诊断还将包含关于内核被污染（tainted）原因的信息。这有助于开发者区分来自运行正常系统的 bug 报告与那些已经存在可疑情况的报告。

提供了 `__taint_module` 函数来污染 `struct module` 实例。模块可能因为两个原因污染内核：

- 如果向内核加载了具有专有许可证（proprietary license）或与 GPL 不兼容的许可证的模块，将使用 `TAINT_PROPRIETARY_MODULE`。由于专有模块的源代码可能不可用，内核开发人员无法修复出现在可能完全无关区域的 bug。模块可能对内核执行了无法追踪的任意操作，因此 bug 很有可能是该模块引入的。

注意，内核提供了 `license_is_gpl_compatible` 函数来判断许可证是否与 GPL 兼容。

相比之下，所有的许可证并不是通过常量指定的，而是通过 C 字符串指定的。

- `TAINT_FORCED_MODULE` 表示该模块是被强制加载的。如果模块中没有版本信息（称为版本数字 version magic），或者模块和内核对某些符号的版本意见不一致，则可以请求强制加载。

- `license_gplook` 是一个布尔值，指定模块许可证是否与 GPL 兼容；其他系统可能不使用 GPL 兼容系统。该标志在模块插入内核时设置。内核如何判断一个许可证是否与 GPL 兼容将在下文讨论。

- `module_ref` 用于引用计数。系统中的每个 CPU 在数组中有一个条目；该条目指定了系统中有多少点在使用该模块。用于单个数组元素的数据类型 `module_ref` 包含一个条目，它应该在 L1 缓存上对齐。

```c
struct module_ref {
    atomic_t count;
} __cacheline_aligned;
```
