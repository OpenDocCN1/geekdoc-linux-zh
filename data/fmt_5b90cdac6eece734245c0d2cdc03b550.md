
```c
        /* 在这里放置 module_put(THIS_MODULE) 很重要，因为
         * 对于打开操作被中断的进程，将永远不会有对应的 close。如果我们不在这里递减使用计数，
         * 我们将留下正的使用计数，我们将没有办法将其降到零，给我们一个不朽的模块，只能通过重启机器来杀死它。
         */

        module_put(THIS_MODULE);

        return -EINTR;
    }
}

    return 0; /* 允许访问 */
}

    /* 在 /proc 文件被关闭时调用 */
    static int module_close(struct inode *inode, struct file *file)
    {
        /* 将 already_open 设置为零，以便 waitq 中的其中一个进程可以将 already_open 重新设回为一并打开文件。所有
         * 其他进程将在 already_open 恢复为一时被调用，因此它们会重新休眠。
         */
        atomic_set(&already_open, 0);

        /* 唤醒 waitq 中的所有进程，以便如果有人在等待该文件，他们就可以获得它。 */
        wake_up(&waitq);

        module_put(THIS_MODULE);

        return 0; /* 成功 */
    }

    /* 作为 /proc 文件注册的结构，带有指向所有相关函数的指针。
     */

    /* 我们 proc 文件的文件操作。这里我们放置指向当有人尝试对我们的文件执行某些操作时所调用的所有函数的指针。NULL
     * 表示我们不想处理某件事。
     */
    #ifdef HAVE_PROC_DPS
    static const struct proc_ops file_ops_4our_proc_file = {
        .proc_read = module_output, /* 从文件中“读取” */
        .proc_write = module_input, /* 向文件中“写入” */
        .proc_open = module_open, /* 在 /proc 文件打开时调用 */
        .proc_release = module_close, /* 在关闭时调用 */
```

```c
.proc_lseek = noop_llseek, /* 返回 file->f_pos */
};
#else
static const struct file_operations file_ops_4_our_proc_file = {
    .read = module_output,
    .write = module_input,
    .open = module_open,
    .release = module_close,
    .llseek = noop_llseek,
};
#endif

/* 初始化模块 - 注册 proc 文件 */
static int __init sleep_init(void)
{
    our_proc_file =
        proc_create(PROC_ENTRY_FILENAME, 0644, NULL,
                    &file_ops_4_our_proc_file);
    if (our_proc_file == NULL) {
        pr_debug("Error: Could not initialize /proc/%s\n",
                 PROC_ENTRY_FILENAME);
        return -ENOMEM;
    }
    proc_set_size(our_proc_file, 80);
    proc_set_user(our_proc_file, GLOBAL_ROOT_UID, GLOBAL_ROOT_GID);
    pr_info("/proc/%s created\n", PROC_ENTRY_FILENAME);
    return 0;
}

/* 清理 - 从 /proc 注销我们的文件。如果
 * 仍有进程在 wait_queue 中等待并处于我们的 open 函数内部，这可能会很危险，该模块将被卸载。我将在第 10 章中解释如何在这种情况下避免移除内核模块。
 */
static void __exit sleep_exit(void)
{
    remove_proc_entry(PROC_ENTRY_FILENAME, NULL);
    pr_debug("/proc/%s removed\n", PROC_ENTRY_FILENAME);
}

module_init(sleep_init);
module_exit(sleep_exit);
MODULE_LICENSE("GPL");
```

```c
/*
 * cat_nonblock.c - 打开一个文件并显示其内容，但退出而不是
 * 等待输入。
 */
#include <errno.h> /* for errno */
#include <fcntl.h> /* for open */
#include <stdio.h> /* standard I/O */
#include <stdlib.h> /* for exit */
#include <unistd.h> /* for read */
```

## 11.2 完成

有时在一个具有多个线程的模块中，一件事需要在另一件事之前发生。与其使用 `/bin/sleep` 命令，内核还有另一种方法可以做到这一点，它允许超时或中断也发生。

作为代码同步机制的完成有三个主要部分，`struct completion` 同步对象的初始化，通过 `wait_for_completion()` 的等待或屏障部分，以及通过对 `complete()` 的调用进行的信号部分。

在随后的示例中，启动了两个线程：`crank` 和 `flywheel`。至关重要的是 `crank` 线程必须在 `flywheel` 线程之前启动。为这两个线程中的每一个建立了一个完成状态，为 `crank` 和 `flywheel` 线程分别定义了不同的完成。在每个线程的退出点，相应的完成状态会被更新，并且 `flywheel` 线程使用 `wait_for_completion` 来确保它不会过早开始。`crank` 线程使用 `complete_all()` 函数来更新完成，这让 `flywheel` 线程继续。

因此，即使 `flywheel_thread` 先启动，你在加载此模块并运行 `dmesg` 时也应该注意到，摇动曲柄总是先发生，因为 `flywheel` 线程等待 `crank` 线程完成。

`wait_for_completion` 函数还有其他变体，其中包括超时或被中断，但这种基本机制对于许多常见情况来说已经足够，而不会增加太多复杂性。

```c
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
```
