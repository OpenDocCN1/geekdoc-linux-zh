
```
module_exit(example_mutex_exit);
MODULE_DESCRIPTION("Mutex example");
MODULE_LICENSE("GPL");
```

## 12.2 自旋锁

顾名思义，自旋锁会锁住代码正在运行的 CPU，并占用其 100% 的资源。因此，你应该只在那些运行时间可能不超过几毫秒的代码上使用自旋锁机制，这样从用户的角度来看不会明显拖慢任何操作。

这里的示例是“中断安全”的，如果在加锁期间发生中断，这些中断不会被遗忘，而是在解锁时被激活，使用 `flags` 变量来保持它们的状态。

```
/*
 * example_spinlock.c
 */
#include <linux/init.h>
#include <linux/module.h>
#include <linux/printk.h>
#include <linux/spinlock.h>

static DEFINE_SPINLOCK(sl_static);
static spinlock_t sl_dynamic;

static void example_spinlock_static(void)
{
    unsigned long flags;

    spin_lock_irqsave(&sl_static, flags);
    pr_info("Locked static spinlock\n");

    /* Do something or other safely. Because this uses 100% CPU time, this
     * code should take no more than a few milliseconds to run.
     */

    spin_unlock_irqrestore(&sl_static, flags);
    pr_info("Unlocked static spinlock\n");
}

static void example_spinlock_dynamic(void)
{
    unsigned long flags;

    spin_lock_init(&sl_dynamic);
    spin_lock_irqsave(&sl_dynamic, flags);
    pr_info("Locked dynamic spinlock\n");

    /* Do something or other safely. Because this uses 100% CPU time, this
     * code should take no more than a few milliseconds to run.
     */
```

```
spin_unlock_irqrestore(&sl_dynamic, flags);
pr_info("Unlocked dynamic spinlock\n");
}
static int __init example_spinlock_init(void)
{
    pr_info("example spinlock started\n");
    example_spinlock_static();
    example_spinlock_dynamic();
    return 0;
}
static void __exit example_spinlock_exit(void)
{
    pr_info("example spinlock exit\n");
}
module_init(example_spinlock_init);
module_exit(example_spinlock_exit);
MODULE_DESCRIPTION("Spinlock example");
MODULE_LICENSE("GPL");
```

占用 CPU 100% 的资源也意味着更大的责任。内核代码独占 CPU 的情况被称为原子上下文。持有自旋锁就是其中一种情况。在原子上下文中睡眠可能会导致系统挂起，因为被占用的 CPU 将其 100% 的资源都用在睡眠上，什么也不做。在某些更糟的情况下，系统可能会崩溃。因此，在原子上下文中睡眠被视为内核中的一个 bug。有时在某些资料中，这种情况被称为“原子上下文睡眠”（sleep-in-atomic-context）。

请注意，这里的“睡眠”不仅限于显式调用睡眠函数。如果后续的函数调用最终调用了一个会睡眠的函数，这也被视为睡眠。因此，注意在原子上下文中使用的函数非常重要。虽然没有文档记录所有这类函数，但代码注释可能会有所帮助。有时你可能会在内核源代码中看到注释，说明某个函数“可能睡眠”（may sleep）、“可能会睡眠”（might sleep），或更明确地说明“调用者不应持有自旋锁”（the caller should not hold a spinlock）。这些注释暗示某个函数可能隐式地睡眠，因此绝不能将其用在原子上下文中。

## 12.3 读写锁

读写锁是自旋锁的一种专门类型，使你能够独占读取或写入某个对象。与之前的自旋锁示例类似，下面的示例展示了一种“中断安全”（irq safe）的情况：如果中断触发了其他函数，而这些函数也可能读写你所关心的数据，那么它们不会破坏逻辑。和之前一样，最好让锁内执行的操作尽可能简短，以免系统挂起，导致用户开始反抗你的模块的“暴政”。

```
/*
 * example_rwlock.c
 */
#include <linux/module.h>
#include <linux/printk.h>
#include <linux/rwlock.h>

static DEFINE_RWLOCK(myrwlock);

static void example_read_lock(void)
{
    unsigned long flags;

    read_lock_irqsave(&myrwlock, flags);
    pr_info("Read Locked\n");

    /* Read from something */

    read_unlock_irqrestore(&myrwlock, flags);
    pr_info("Read Unlocked\n");
}

static void example_write_lock(void)
{
    unsigned long flags;

    write_lock_irqsave(&myrwlock, flags);
    pr_info("Write Locked\n");

    /* Write to something */

    write_unlock_irqrestore(&myrwlock, flags);
    pr_info("Write Unlocked\n");
}

static int __init example_rwlock_init(void)
{
    pr_info("example_rwlock started\n");

    example_read_lock();
    example_write_lock();

    return 0;
}

static void __exit example_rwlock_exit(void)
{
    pr_info("example_rwlock exit\n");
}

module_init(example_rwlock_init);
module_exit(example_rwlock_exit);

MODULE_DESCRIPTION("Read/Write locks example");
MODULE_LICENSE("GPL");
```
