
**图 5.20** 带有完整调试自旋锁

- 88–92 这里的`spinlock_t`最完整的版本。
- 90 `babble`字段（从其用法中可以看出）限制了打印错误消息的次数。
- 91 这是一个指向字符串的指针，该字符串包含声明特定`spinlock_structure`所在的文件名。
- 93 `lock`字段像通常一样被初始化为 0（未锁定）。错误消息最多打印 25 次。`_BASE_FILE`扩展为声明该结构体实例代码的源文件名。
- 97 此宏始终与现有的`spinlock_t`一起使用，并对其传递一个指针。`lock`字段被重新初始化为 0。其他字段均未改变。
- 98 如果`lock`字段的第 0 位被设置，则返回 TRUE；否则返回 FALSE。参见第 5.1.3 节的`test_bit()`。
- 99 `test_and_set_bit()`函数在第 5.1.4.1 节中讨论过。它设置`lock`字段的最低位（第 0 位），如果之前已设置（锁定）则返回 TRUE，否则返回 FALSE（未锁定）。该宏的结果为它的反反：如果之前未锁定则返回 TRUE，否则返回 FALSE。`lock`字段被设置或被测试。
- 101–103 这三个宏由于未知原因被写在同一行。Linux 系统风格通常将宏跨多行编写。为了方便阅读，在第 5.20 节中它们被拆分成了多行。
- 101 `EFLAGS`中的值被保存在锁中断位`_spinflags`中。此举的目的是记住中断位的状态。`save_flags()`函数将在第 12.8.2 节中讨论。中断被禁用，无论它们之前是开启还是禁用。如果已经锁定，且尚未打印最大数量的消息，则正在打印一条消息。该消息由源文件名、行号、"spin_lock"（初始化错误：这是一个指向自旋锁的指针）和 "already locked" 组成。在单处理器情况下，不存在竞争，尝试锁定已锁定的自旋锁意味着设计错误。代码确保此类错误会被报告。然后`babble`减一，这样重复的错误就不会产生大量消息。无论什么情况下，`lock`都被设置为 1（无论是否锁定）。`restore_flags()`函数（第 12.8.2 节）从`_spinflags`恢复`EFLAGS`寄存器，使中断恢复到之前的状态（开启或禁用）。
- 102 这与第 101 行非常相似。在单处理器上，它应该总是发现自旋锁是未锁定的。如果已锁定，会打印类似的消息，但错误被识别为来自 "spin_lock_wait"，并宣布 "deadlock"（死锁）。如果未锁定，则立即返回。此宏不影响`lock`的值。
- 103 尝试解锁一个未锁定的锁意味着设计错误。如果尚未打印最大数量的警告消息，将打印另一条，将其识别为来自 "spin_unlock" 并宣布 "not locked"。无论什么情况下，`lock`的值都被设置为 0（未锁定）。

## 多处理器版本的自旋锁

自旋锁的多处理器实现已在第 5.3 节中介绍过。本节将检查自旋锁在多处理器内核中是如何内核的。

### 5.4.1 数据结构

SMP 内核中`spinlock_t`数据类型的基本结构如图 5.21 所示，源自`<asm-i386/spinlock.h>`。

```c
26     typedef struct {
27         volatile unsigned int lock;
28         #if SPINLOCK_DEBUG
29             unsigned magic;
30         #endif
31     } spinlock_t;
```

图 5.21 表示自旋锁的数据结构

- 27 该结构本质上由一个无符号`int`组成，表示锁。它的值将是 1（表示未锁定）或 0（表示锁定）。这与单处理器情况下使用的惯例相反。注意它是`volatile`的，这在警告编译器：其值可能会被声明它的之外的其他例程修改。
- 28–30 还有一个`magic`字段，用于调试。只有在定义了`SPINLOCK_DEBUG`时才会被编译。
- 31 该数据结构在源码中通常泛称为`spinlock_t`。

### 5.4.2 初始化自旋锁

声明了许多用于初始化自旋锁的宏；见图 5.22，源自`<asm-i386/spinlock.h>`。

```c
33     #define SPINLOCK_MAGIC  0xdead4ead4
34
35     #if SPINLOCK_DEBUG
36     #define SPINLOCK_MAGIC_INIT, SPINLOCK_MAGIC
37     #else
38     #define SPINLOCK_MAGIC_INIT /**/
39     #endif
40
41     #define SPIN_LOCK_UNL(spinlock_t) {1 SPINLOCK_MAGIC_INIT}
```

## 多处理器版本的自旋锁

```c
42 #define spin_lock_init(x) do { (*x) = SPIN_LOCK_UNOCKED; } while(0)
```

图 5.22 初始化自旋锁

- 33 `SPINLOCK_MAGIC`宏仅仅是一个不太可能意外发生的唯一位模式。如果在`magic`字段中发现此值，意味着自旋锁实际上已初始化，且`lock`字段中的值是可以信赖的。
- 36 如果开启了自旋锁调试，则`SPINLOCK_MAGIC_INIT`被赋予`SPINLOCK_MAGIC`的值。注意逗号；这是由预处理器替换的字符串的一部分。
- 38 否则，`SPINLOCK_MAGIC_INIT`为空值，被预处理器简单忽略。
- 41 `spinlock_t`的标准初始化（未锁定状态）是`lock`字段的值为 1，以及`magic`字段为`SPINLOCK_MAGIC_INIT`。注意这可能有它自己的名称。该值要么是`{1, ...}`，取决于`SPINLOCK_DEBUG`是否定义。
- 42 `spin_lock_init(x)`宏将`(*x)`设置为`SPIN_LOCK_UNOCKED`。

- 43 最终，它是对`spinlock_t`指针的引用并操作。

## 5.4.3 自旋锁的操作

在查看了自旋锁的声明和初始化后，我们转向操作这些函数。

### 5.4.3.1 尝试获取自旋锁

`try_lock()`函数在图 5.23 中，源自`<asm-i386/spinlock.h>`，如其名所示。如果锁是空闲的，它将其锁定；否则返回。

```c
116 static int try_lock(spinlock_t *lock)
117 {
118     char oldval;
119     asm __volatile__(
120         "xchg %b,%1"
121     : "=q" (oldval), "m" (lock) : : "memory");
122 
123     return oldval > 0;
124 }
```

图 5.23 测试自旋锁

- 116 参数是要尝试的自旋锁指针。
- 120 `xchg`指令将`oldval`与`lock`交换。
- 121 `oldval`是输出参数。`q`约束意味着它在 A、B、C 或 D 寄存器中。参数`lock`是内存（`m`）。
- 122 `"memory"`指令告诉编译器内存将以不可预测的方式修改。
- 123 在第 120 行后，`lock`拥有之前的值。如果它是正数，说明之前是空闲的，函数返回 TRUE。

### 5.4.3.2 获取自旋锁

`spin_lock()`函数如图 5.24 所示，正如其名。如果锁是空闲的，它获取锁；否则，“忙等待”（自旋）直到锁变得空闲。

```c
126 static inline void spin_lock(spinlock_t lock)
127 {
128 #if SPINLOCK_DEBUG
129     _label_here;
130 here:
131     if (lock->magic != SPINLOCK_MAGIC) {
132         printk("eip: %p\n", &here);
133         BUG();
134     }
135 #endif
136     asm __volatile_(
137         spin_lock_string
138         ="%m" (lock->lock) : : "memory");
139 )
```
