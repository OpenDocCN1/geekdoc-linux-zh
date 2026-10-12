
内核执行 `try_module_get` 和 `module_put` 函数来增加或减少引用计数。当调用者确定直到目前为止模块未被卸载时，也可以使用 `__module_get` 来增加引用计数。相比之下，`try_module_get` 确保了情况确实如此。

- `modules_which_me` 用作描述内核中模块依赖的数据结构中的列表。第 7.3.2 节将进行详细介绍。
- `waiter` 是一个指向导致模块卸载的进程的任务结构的指针，该进程现在正在等待激活终止。
- `exit` 是指向 init 的计数器。它是一个指向函数的指针，在模块被移除时执行模块特定的清理工作（例如释放保留的内存区域）。
- `symtab`、`num_symtab` 和 `strtab` 用于记录模块所有符号的信息（不仅是显式导出的符号）。
- `percpu` 指向属于模块的每个 CPU 数据。它在模块加载时初始化。
- `args` 是加载期间传递给模块的命令行参数的指针。

## 7.3.2 依赖与引用

两个模块 A 和 B 之间通过 A 提供的函数存在一种关系。这种关系可以从两个不同的角度来看：

1. B 依赖于 A。除非 A 已经留在内核内存中，否则 B 无法加载。
2. A 引用 B。换句话说，除非 A 已移除，否则 B 不能从内核中移除——除非所有引用 B 的模块都已消失。在内核中，这种关系被描述为 A 使用 B。

为了正确管理这些依赖关系，内核需要引入进一步的数据结构：

```c
kernel/modules.c
struct module_use
{
    struct list_head list;
    struct module *which_uses;
};
```

依赖网络通过模块数据结构中的 `modules_which_use_me` 元素建立。对于每个使用模块 B 中函数的模块 A，都会创建一个新的 `module_use` 实例。该实例被添加到 B 的 `modules_which_use_me` 列表中。`module_which_uses` 指向模块 A 的实例。基于这些信息，内核可以很容易地找到哪些其他模块被某个特定模块所使用。

由于所描述的关系并不直而易见，图 7-3 提供了一个图形示例来说明这种情况。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_520_0.png)

我为这个示例从 Netfilter 软件包中选择了一些模块。当模块编译时，依赖文件 `modules.dep` 包含了以下依赖关系：¹⁰

```
ip_tables.ko  ip_conntrack.ko  ip_tables.ko
iiptable_nat.ko  iptable_nat.ko  ip_conntrack.ko
ip_nat_ftp.ko
ip_conntrack.ko
ip_conntrack_ftp.ko
```

虽然 `ip_nat_ftp` 和 `ip_conntrack_ftp` 依赖于其他几个模块，但没有任何模块依赖于它们，这就是为什么它们实例的 `modules_which_use_me` 是空指针。

`ip_tables` 对其他模块没有任何依赖关系，且有两个依赖 `ip_tables` 的模块：`iptable_nat` 和 `ip_nat_ftp`。为每个模块都创建了一个 `module_use` 实例；这些被放置在 `ip_tables` 的 `modules_which_use_me` 列表中。`module_which_uses` 指向模块实例。基于这些信息，内核可以轻松找到哪些其他模块被使用。

由于所描述的关系并不立即清晰，图 7-3 提供了一个图形示例来说明这种情况。

## 操数据结构

内核提供了 `already_uses` 函数来测试模块 A 是否需要 B：

```c
kernel/modules.c
/* a 使用 b? */
static int already_uses(struct module *a, struct module *b)
```

¹⁰为了提高可读性，我们没有指定出现在 `modules.dep` 中的完整文件名。此外，示例是简化的。

```c
{
  struct module_use *use;
  list_each_entry(use, &b->modules_which_use_me, list) {
    if (use->module_uses == a) {
      return 1;
    }
  }
  return 0;
}
```

如果 A 依赖于 B，B 的 `modules_which_use_me` 列表包含指向模块 A 的指针。这就是为什么内核会逐个检查列表。如果找到了匹配项——换句话说，依赖关系存在——返回 1；否则函数终止并返回 0。

`use_module` 用于建立 A 和 B 之间的关系——A 需要 B 才能运行。它的实现如下：

```c
kernel/modules.c
/* 模块 a b */
static int use_module(struct module *a, struct module *b)
{
  struct module_use *use;

  if (b == NULL || already_uses(a, b)) return 1;

  if (!strong_try_module_get(b)) {
    return 0;
  }
  use = kmalloc(sizeof(*), GFP_ATOMIC);
  if (!use) {
    printf("%s: out of memory loading\n", a->name);
    module_put(b);
    return 0;
  }

  use->module_which_uses = a;
  list_add(&use->list, &b->modules_which_use_me);

  return 1;
}
```

`already_uses` 首先检查关系是否已经建立。如果是，函数可以立即返回（依赖模块的空指针也被解释为关系已经存在）。如果不是，则增加 B 的引用计数以便它不再被移除——毕竟 A 要求它的存在。用于此目的的 `strong_try_module_get` 是上述 `try_module_get` 函数的封装；它处理模块正在加载中的的情况：

```c
static inline int strong_try_module_get(struct module *mod)
{
  if (mod && mod->state == MODULE_STATE_COMING)
```

## 第 7 章：模块 (Modules)

```
return 0;
return try_module_get(mod);
```

建立这种关系并不复杂。会创建一个新的 `module_use` 实例，其 `module_which_uses` 指针指向模块 A 的实例。随后，这个新的 `module_use` 实例会被添加到模块 B 的列表中。

## 7.3 模块的二进制结构

模块使用 ELF 格式，该格式具有几个普通程序或库中不存在的额外节。除了少数与我们目的无关的编译器生成的节（主要是重定位位节）外，模块由以下 ELF 节组成：

- `__ksymtab`、`__ksymtab_gpl` 和 `__ksymtab_gpl_future` 包含一个模块所有导出符号的表。第一个命名节中的符号可以被管理许可（license）的内核部分使用，`__ksymtab_gpl` 中的符号只能被 GPL 兼容部分使用，而 `__ksymtab_gpl_future` 中的符号在未来仅供 GPL 兼容部分使用。
- `__crctab`、`__crctab_gpl` 和 `__crctab_gpl_future` 包含模块导出的 GPL（或未来-GPL）函数的校验和。`__versions` 包含了模块从外部源所用所有引用的校验和。

> 除非在配置内核时启用了内核控制功能，否则这些节不会被创建。

第 7.5 节详细讨论了信息是如何生成和使用的。

- `__param` 存储模块所接受的参数信息。
- `__ex_table` 用于在内核的异常表中定义新条目，当模块代码需要这种机制时使用。
- `modinfo` 存储模块加载之前必须存在内核中的所有其他名称——换句话说，就是该模块所依赖的所有名称。

此外，每个模块还可以包含可以使用 `modinfo` 用户工具查询的特定信息，特别是作者名称、模块描述、许可信息以及参数列表。

- `exit_text` 包含模块从内核中移除时所需的代码（以及可能的数据）。这些信息不会保留在下一个文本段中，以便在内核配置中未启用移除模块选项时，内核不会将其加载到内存中。
- 初始化函数（及数据）存储在 `.init.text` 中。它们被保留在一个单独的节中，因为初始化完成后就不再需要它们，因此可以从内存中移除。
