

```
39    pr_info("procfile read %s\n", file_pointer->f_path.dentry->d_name.name);
40    -> offset += len;
41    }
42    
43    return ret;
44    }
45    
46    /* This function is called with the /proc file is written. */
47    static ssize_t procfile_write(struct file *file, const char __user *buff,
48                                 size_t len, loff_t *off)
49    {
50        procfs_buffer_size = len;
51        if (procfs_buffer_size >= PROCFS_MAX_SIZE)
52            procfs_buffer_size = PROCFS_MAX_SIZE - 1;
    
54        if (copy_from_user(procfs_buffer, buff, procfs_buffer_size))
55            return -EFAULT;
56    
57        procfs_buffer[procfs_buffer_size] = '\0';
58        *off += procfs_buffer_size;
59        pr_info("procfile write %s\n", procfs_buffer);
60        return procfs_buffer_size;
61    }
62    
63    #ifdef HAVE_PROC_OPS
64    static const struct proc_ops proc_file_fops = {
65        .proc_read = procfile_read,
66        .proc_write = procfile_write,
67    };
68    #else
69    static const struct file_operations proc_file_fops = {
70        .read = procfile_read,
71        .write = procfile_write,
72    };
73    #endif
    
75    static int __init procfs2_init(void)
76    {
77        our_proc_file = proc_create(PROCFS_NAME, 0644, NULL, &proc_file_fops);
78        if (NULL == our_proc_file) {
79            pr_alert("Error:Could not initialize /proc/%s\n", PROCFS_NAME);
80            return -ENOMEM;
81        }
82    
83        pr_info("/proc/%s created\n", PROCFS_NAME);
84        return 0;
85    }
86    
87    static void __exit procfs2_exit(void)
88    {
89        proc_remove(our_proc_file);
90        pr_info("/proc/%s removed\n", PROCFS_NAME);
91    }
92    
93    module_init(procfs2_init);
```
module_exit(procfs2_exit);
MODULE_LICENSE("GPL");

## 7.3 使用标准文件系统管理 /proc 文件

我们已经看到了如何使用 /proc 接口读取和写入一个 /proc 文件。但也可以使用 inode 来管理 /proc 文件。主要关注点是使用高级功能，例如权限。

在 Linux 中，存在一种用于文件系统注册的标准机制。由于每个文件系统都必须拥有自己的函数来处理 inode 和文件操作，因此有一个特殊的结构来保存指向所有这些函数的指针，struct inode_operations，其中包含指向 struct proc_ops 的指针。

文件操作和 inode 操作之间的区别在于，文件操作处理文件本身，而 inode 操作处理引用文件的方式，例如创建指向它的链接。

在 /proc 中，每当我们注册一个新文件时，我们就可以指定将使用哪个 struct inode_operations 来访问它。这就是我们使用的机制，一个包含指向 struct proc_ops 的指针的 struct inode_operations，而 struct proc_ops 包含指向我们的 procfs_read 和 procfs_write 函数的指针。

这里另一个有趣的点是 module_permission 函数。每当一个进程尝试对 /proc 文件执行某些操作时，就会调用此函数，并且它可以决定是否允许访问。目前它仅基于操作和当前用户（在 current 中可用，指向包含有关当前正在运行进程的信息的结构）的 uid，但它可以基于我们喜欢的任何内容，例如其他进程正在对同一文件执行的操作、一天中的时间，或我们收到的最后输入。

需要注意的是，内核中读写角色的标准用法是反转的。读函数用于输出，而写函数用于输入。原因在于读和写指的是用户的观点——如果一个进程从内核读取某些内容，那么内核需要输出它，而如果一个进程向内核写入某些内容，那么内核将其作为输入接收。

```
/*
 * procfs3.c
 */

#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/proc_fs.h>
#include <linux/sched.h>
#include <linux/uaccess.h>
#include <linux/version.h>
#if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 10, 0)
#include <linux/minmax.h>
#endif
```

