```
static const struct file_operations proc_file_fops = {
    .read = procfile_read,
};
#endif

static int __init procfs_init(void)
{
    our_proc_file = proc_create(procfs_name, 0644, NULL, &proc_file_fops);
    if (NULL == our_proc_file) {
        pr_alert("Error:Could not initialize /proc/%s\n", procfs_name);
        return -ENOMEM;
    }

    pr_info("/proc/%s created\n", procfs_name);
    return 0;
}

static void __exit procfs_exit(void)
{
    proc_remove(our_proc_file);
    pr_info("/proc/%s removed\n", procfs_name);
}

module_init(procfs_init);
module_exit(procfs_exit);

MODULE_LICENSE("GPL");
```

# 7.1 The proc_ops Structure

The proc_ops structure is defined in include/linux/proc_fs.h in Linux v5.6+. In older kernels, it used file_operations for custom hooks in /proc file system, but it contains some members that are unnecessary in VFS, and every time VFS expands file_operations set, /proc code comes bloated. On the other hand, not only the space, but also some operations were saved by this structure to improve its performance. For example, the file which never disappears in /proc can set the proc_flag as PROC_ENTRY_PERMANENT to save 2 atomic ops, 1 allocation, 1 free in per open/read/close sequence.

# 7.2 Read and Write a /proc File

We have seen a very simple example for a /proc file where we only read the file /proc/helloworld. It is also possible to write to a /proc file. It works the same way as read, a function is called when the /proc file is written. But there is a little difference with read, data comes from user, so you have to import data from user space to kernel space (with copy_from_user or get_user)

The reason for copy_from_user or get_user is that Linux memory (on Intel architecture, it may be different under some other processors) is segmented. This means that a pointer, by itself, does not reference a unique location in memory, only a location in a memory segment, and you need to know which memory