```
static int hello_release(struct inode *inode, struct file *file)
{
    printk("hello_release: successful\\n");
    return 0;
}

static ssize_t hello_read(struct file *file, char *buf, size_t count,
                          loff_t *ptr)
{
    printk("hello_read: returning zero bytes\\n");
    return 0;
}

static ssize_t hello_write(struct file *file, const char *buf,
                           size_t count, loff_t *ppos)
{
    printk("hello_read: accepting zero bytes\\n");
    return 0;
}

static int hello_ioctl(struct inode *inode, struct file *file,
                       unsigned int cmd, unsigned long arg)
{
    printk("hello_ioctl: cmd=%ld, arg=%ld\\n", cmd, arg);
    return 0;
}

static int __init hello_init(void)
{
    int ret;
    printk("Hello Example Init - debug mode is %s\\n",
           debug_enable ? "enabled" : "disabled");
    ret = register_chrdev(HELLO_MAJOR, "hello", &hello_fops);
    if (ret < 0) {
        printk("Error registering hello device\\n");
        goto hello_fail1;
    }
    printk("Hello: registered module successfully!\\n");
    /* Init processing here... */
    return 0;
hello_fail1:
    return ret;
}

static void _exit hello_exit(void)
{
    printk("Hello Example Exit\\n");
}
```