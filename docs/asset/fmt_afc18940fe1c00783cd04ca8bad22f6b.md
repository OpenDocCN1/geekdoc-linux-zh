
# Linux 内核 IRQ 结构体与 IRQ Domain

```c
struct irq_desc {
    struct irq_common_data      irq_common_data;
    struct irq_data             irq_data;
    unsigned int                __per_cpu     *kstat_irqs;
    irq_handler_t              handle_irq;
#ifdef CONFIG_IRQ_PREFLOW_FASTIRQ
    irq_preflow_handler_t      preflow_handler;
#endif
    struct irq_action           /* IRQ动作列表 */
    unsigned int                status_use_accessors;
    unsigned int                core_internal_state_do_not_mess_with_it;
    unsigned int                depth;              /* 嵌套中断禁用 */
    unsigned int                wake_depth;         /* 嵌套唤醒启用 **/
    unsigned int                
    unsigned int                irq_count;         /* 用于检测故障中断 */
    unsigned long               last_handled;
    unsigned int                irqs_handled;      /* 未处理计数的老化计时器 **/
    atomic_t                    threads;
    int                         threads_handled_last;
    raw_spinlock_t              lock;
    struct cpumask             *per_cpu_enabled;
    const struct cpumask       *per_cpu_affinity;
#ifdef CONFIG_SMP
    const struct cpumask       *affinity_hint;
    const struct cpumask       
#endif
    struct irq_affinity_notify  *affinity_notify;
#ifdef CONFIG_GENERIC_PENDING_IRQ
    cpumask_var_t              pending_mask;
#endif
```

在每个 `struct irq_desc` 内部都有一个 `irq_data` 实例（在上面的 `struct irq_desc` 结构体中已加粗），它包含了与中断管理相关的低层信息，例如 Linux IRQ 编号、hwirq、中断转换域（`struct irq_domain`）以及指向中断控制器操作的指针（`struct irq_chip`）等重要字段。

- `struct irq_data` - 传递给芯片函数的每个中断芯片的数据
- `@mask`: 用于访问芯片寄存器的预计算位掩码
- `@irq`: 中断号
- `@hwirq`: 硬件中断号，局部于中断域
- `@common`: 指向所有 irqchips 共享的数据
- `@chip`: 低层中断硬件访问
- `@domain`: 中断转换域；负责 hwirq 编号与 linux irq 编号之间的映射。
- `@parent_data`: 指向 `struct irq_data` 的指针，用于支持层级 irqdomain
- `@chip_data`: 芯片方法的平台特定私有数据，允许共享芯片实现。

```c
struct irq_data {
  u32 mask;
  unsigned int irq; /* Linux IRQ 编号 */
  unsigned long hwirq; /* hwirq 编号 */
  struct irq_common_data *common;
  struct irq_chip *chip; /* 低层中断控制器硬件访问 */
  struct irq_domain *domain;
};
#ifdef CONFIG_IRQ_DOMAIN_HIERARCHY
  struct irq_data *parent_data;
#endif
  void *chip_data;
};
```

## 用于 GPIO 控制器的 Linux 内核 IRQ Domain

内核内部使用单一空间来表示 IRQ 编号，没有两个 IRQ 具有相同的名称。当系统只有一个中断控制器（IC）时，从硬件角度来看也是如此。然而，当存在两个 IC 时（例如 `irq_chip`、GIC 和 GPIO IC），就需要进行映射。为了解决这个问题，Linux 内核引入了 IRQ 域（domain）的概念，它是硬件 IRQ 编号与内核内部使用的编号之间一个定义良好的接口。

`struct irq_domain` 是中断器的“域”数据结构。它处理给定中断域的硬件与虚拟中断编号之间的映射。

```c
struct irq_domain {
  struct list_head link;
  const char *name;
  const struct irq_domain_ops *ops;
  void *host_data;
  unsigned int flags;

/* 可选数据 */
  struct fnode_handle *fwnode;
  enum irq_domain_bus_token *token;
  struct irq_domain_chip_generic *gc;
};
#ifdef CONFIG_IRQ_DOMAIN_HIERARCHY
  struct irq_domain *parent;
#endif
```

```c
/* 反向映射数据。线性映射会被附加到 irq_domain 中 */
irq_hw_number_t hwirq_max;
unsigned int revmap_max_irq;
unsigned int revmap_size;
struct radix_tree_root revmap_tree;
unsigned int linear_revmap[];
```

中断驱动程序通过调用 `irq_domain` 函数之一来分配并注册 `irq_domain`。该函数在成功时返回一个指向 `struct irq_domain` 的指针。有多种机制可以将 hwirq 映射到 Linux 编号，大多数驱动程序通过 `Documentation/IRQ` 使用线性映射。

```c
/**
 * irq_add_linear() - 分配并注册线性映射
 * @of_node: 指向设备树节点的指针
 * @size: 域中的中断数量
 * @ops: map/umap-domain 回调函数
 * @host_data: 控制器私有数据
 */
struct irq_domain *irq_add_linear(struct device_node *of_node,
                                    unsigned int size,
                                    const struct irq_domain_ops *ops,
                                    void *host_data);
```

中断驱动程序通过调用 `irq_domain` 函数之一来分配并注册 `irq_domain`。该函数在成功时返回一个指向 `struct irq_domain` 的指针。有多种机制可以将 hwirq 映射到 Linux 编号，大多数驱动程序通过 `Documentation/IRQ` 使用线性映射。
