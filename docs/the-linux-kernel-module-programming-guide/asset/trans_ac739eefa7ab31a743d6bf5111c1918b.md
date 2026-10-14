
129
130     * 被杀死或停止。
131     */
132     for (i = 0; i < _NSIG_WORDS && !is_sig; i++)
133         is_sig = current->pending.signal.sig[i] &
134             ~current->blocked.sig[i];
135
136     if (is_sig) {
137         /* 在这里放置 module_put(THIS_MODULE) 很重要，因为
138          * 对于打开操作被中断的进程，将永远不会有对应的 close。如果我们不在这里递减使用计数，
139          * 我们将留下正的使用计数，我们将没有办法将其降到零，给我们一个不朽的模块，只能通过重启机器来杀死它。
140          */
141         module_put(THIS_MODULE);
142         return -EINTR;
143     }
144     }
145
146     return 0; /* 允许访问 */
147     }
148
149     /* 在 /proc 文件被关闭时调用 */
150     static int module_close(struct inode *inode, struct file *file)
151     {
152         /* 将 already_open 设置为零，以便 waitq 中的其中一个进程可以将 already_open 重新设回为一并打开文件。所有
153          * 其他进程将在 already_open 恢复为一时被调用，因此它们会重新休眠。
154          */
155         atomic_set(&already_open, 0);
156
157         /* 唤醒 waitq 中的所有进程，以便如果有人在等待该文件，他们就可以获得它。 */
158         wake_up(&waitq);
159
160         module_put(THIS_MODULE);
161
162         return 0; /* 成功 */
163     }
164
165     /* 作为 /proc 文件注册的结构，带有指向所有相关函数的指针。
166      */
167
168     /* 我们 proc 文件的文件操作。这里我们放置指向当有人尝试对我们的文件执行某些操作时所调用的所有函数的指针。NULL
169      * 表示我们不想处理某件事。
170      */
171     #ifdef HAVE_PROC_DPS
172     static const struct proc_ops file_ops_4our_proc_file = {
173         .proc_read = module_output, /* 从文件中“读取” */
174         .proc_write = module_input, /* 向文件中“写入” */
175         .proc_open = module_open, /* 在 /proc 文件打开时调用 */
176         .proc_release = module_close, /* 在关闭时调用 */
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
