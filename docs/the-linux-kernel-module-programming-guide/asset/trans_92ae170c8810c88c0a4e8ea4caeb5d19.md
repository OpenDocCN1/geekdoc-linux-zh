

## 11.2 完成

有时在一个具有多个线程的模块中，一件事需要在另一件事之前发生。与其使用 /bin/sleep 命令，内核还有另一种方法可以做到这一点，它允许超时或中断也发生。

作为代码同步机制的完成有三个主要部分，struct completion 同步对象的初始化，通过 wait_for_completion() 的等待或屏障部分，以及通过对 complete() 的调用进行的信号部分。

在随后的示例中，启动了两个线程：crank 和 flywheel。至关重要的是 crank 线程必须在 flywheel 线程之前启动。为这两个线程中的每一个建立了一个完成状态，为 crank 和 flywheel 线程分别定义了不同的完成。在每个线程的退出点，相应的完成状态会被更新，并且 flywheel 线程使用 wait_for_completion 来确保它不会过早开始。crank 线程使用 complete_all() 函数来更新完成，这让 flywheel 线程继续。

因此，即使 flywheel_thread 先启动，你在加载此模块并运行 dmesg 时也应该注意到，摇动曲柄总是先发生，因为 flywheel 线程等待 crank 线程完成。

wait_for_completion 函数还有其他变体，其中包括超时或被中断，但这种基本机制对于许多常见情况来说已经足够，而不会增加太多复杂性。

```
/*
 * completions.c
 */
#include <linux/completion.h>
#include <linux/err.h> /* for IS_ERR() */
#include <linux/init.h>
#include <linux/kthread.h>
#include <linux/module.h>
#include <linux/printk.h>
#include <linux/version.h>

static struct completion crank_comp;
static struct completion flywheel_comp;

static int machine_crank_thread(void *arg)
{
    pr_info("Turn the crank\n");
    complete_all(&crank_comp);
#if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 17, 0)
    kthread_complete_and_exit(&crank_comp, 0);
#else
    complete_and_exit(&crank_comp, 0);
#endif
}

static int machine_flywheel_spinup_thread(void *arg)
{
wait_for_completion(&crank_comp);
pr_info("Flywheel spins up\n");
complete_all(&flywheel_comp);
#if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 17, 0)
 kthread_complete_and_exit(&flywheel_comp, 0);
#else
 complete_and_exit(&flywheel_comp, 0);
#endif
}
static int __init completions_init(void)
{
 struct task_struct *crank_thread;
 struct task_struct *flywheel_thread;

 pr_info("completions example\n");

 init_completion(&crank_comp);
 init_completion(&flywheel_comp);

 crank_thread = kthread_create(machine_crank_thread, NULL, "KThread Crank");
 if (IS_ERR(crank_thread))
  goto ERROR_THREAD_1;

 flywheel_thread = kthread_create(machine_flywheel_spinup_thread, NULL, "KThread Flywheel");
 if (IS_ERR(flywheel_thread))
  goto ERROR_THREAD_2;

 wake_up_process(flywheel_thread);
 wake_up_process(crank_thread);

 return 0;

ERROR_THREAD_2:
 kthread_stop(crank_thread);
ERROR_THREAD_1:
 return -1;
}
static void __exit completions_exit(void)
{
 wait_for_completion(&crank_comp);
 wait_for_completion(&flywheel_comp);
 pr_info("completions exit\n");
}
module_init(completions_init);
module_exit(completions_exit);
MODULE_DESCRIPTION("Completions example");
```

## 12 避免冲突和死锁

如果在不同 CPU 上运行或在不同线程中运行的进程尝试访问相同的内存，那么可能会发生奇怪的事情或你的系统会锁定。为避免这种情况，提供了各种类型的互斥内核函数。这些函数指示代码段是“锁定”还是“解锁”，以便不能同时尝试运行它。

### 12.1 互斥锁

你可以在很大程度上以与在用户空间中部署它们相同的方式使用内核互斥锁（互斥）。这可能是避免大多数情况下冲突所需的一切。

```
/*
 * example_mutex.c
 */
#include <linux/module.h>
#include <linux/mutex.h>
#include <linux/printk.h>

static DEFINE_MUTEX(mymutex);

static int __init example_mutex_init(void)
{
        int ret;

        pr_info("example_mutex init\n");

        ret = mutex_trylock(&mymutex);
        if (ret != 0) {
                pr_info("mutex is locked\n");

                if (mutex_is_locked(&mymutex) == 0)
                        pr_info("The mutex failed to lock!\n");

                mutex_unlock(&mymutex);
                pr_info("Mutex is unlocked\n");
        } else
                pr_info("Failed to lock\n");

        return 0;
}

static void __exit example_mutex_exit(void)
{
        pr_info("example_mutex exit\n");
}

module_init(example_mutex_init);
module_exit(example_mutex_exit);
```

