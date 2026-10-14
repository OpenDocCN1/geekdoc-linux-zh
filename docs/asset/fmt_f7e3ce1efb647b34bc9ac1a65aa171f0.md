
```c
/*
 * chardev.c: Creates a read-only char device that says how many times
 * you have read from the dev file
 */

#include <linux/atomic.h>
#include <linux/cdev.h>
#include <linux/delay.h>
#include <linux/device.h>
#include <linux/fs.h>
#include <linux/init.h>
#include <linux/kernel.h> /* for sprint() */
#include <linux/module.h>
#include <linux/printk.h>
#include <linux/types.h>
#include <linux/uaccess.h> /* for get_user and put_user */
#include <linux/version.h>

#include <asm/errno.h>

/* Prototypes - this would normally go in a .h file */
static int device_open(struct inode *, struct file *);
static int device_release(struct inode *, struct file *);
static ssize_t device_read(struct file *, char __user *, size_t, loff_t *);
static ssize_t device_write(struct file *, const char __user *, size_t,
    loff_t *);

#define SUCCESS 0
#define DEVICE_NAME "chardev" /* Dev name as it appears in /proc/devices */
#define BUF_LEN 80 /* Max length of the message from the device */

/* Global variables are declared as static, so are global within the file. */

static int major; /* major number assigned to our device driver */

enum {
    CDEV_NOT_USED,
    CDEV_EXCLUSIVE_OPEN,
};

/* Is device open? Used to prevent multiple access to device */
static atomic_t already_open = ATOMIC_INIT(CDEV_NOT_USED);

static char msg[BUF_LEN + 1]; /* The msg the device will give when asked */

static struct class *cls;

static struct file_operations chardev_fops = {
    .read = device_read,
    .write = device_write,
    .open = device_open,
    .release = device_release,
};

static int __init chardev_init(void)
{
module_put(THIS_MODULE);

return SUCCESS;
}

/* Called when a process, which already opened the dev file, attempts to
 * read from it.
 */
static ssize_t device_read(struct file *filp, /* see include/linux/fs.h */
			    char __user *buffer, /* buffer to fill with data */
			    size_t length, /* length of the buffer */
			    loff_t *offset)
{
	/* Number of bytes actually written to the buffer */
	int bytes_read = 0;
	const char *msg_ptr = msg;

	if (!(*msg_ptr + *offset)) { /* we are at the end of message */
		*offset = 0; /* reset the offset */
		return 0; /* signify end of file */
	}

	msg_ptr += *offset;

	/* Actually put the data into the buffer */
	while (length && *msg_ptr) {
		/* The buffer is in the user data segment, not the kernel
		 * segment so "*" assignment won't work. We have to use
		 * put_user which copies data from the kernel data segment to
		 * the user data segment.
		 */
		put_user(*(msg_ptr++), buffer++);
		length--;
		bytes_read++;
	}

	*offset += bytes_read;

	/* Most read functions return the number of bytes put into the buffer. */
	return bytes_read;
}

/* Called when a process writes to dev file: echo "hi" > /dev/hello */
static ssize_t device_write(struct file *filp, const char __user *buff,
			    size_t len, loff_t *off)
{
	pr_alert("Sorry, this operation is not supported.\n");
	return -EINVAL;
}

module_init(chardev_init);
module_exit(chardev_exit);

MODULE_LICENSE("GPL");
```

## 6.6 为多个内核版本编写模块

系统调用是内核向进程展示的主要接口，通常在不同版本之间保持不变。可能会添加新的系统调用，但通常旧有的系统调用行为与之前完全一致。这是为了向后兼容——新内核版本不应破坏常规进程。在大多数情况下，设备文件也会保持不变。另一方面，内核内部的接口在不同版本之间可能会且确实会发生变化。

不同内核版本之间存在差异，如果你想要支持多个内核版本，你会发现需要编写条件编译指令。实现方式是将宏 `LINUX_VERSION_CODE` 与宏 `KERNEL_VERSION` 进行比较。在内核版本 `a.b.c` 中，该宏的值为 `2^16 a + 2^8 b + c`。

## 7 /proc 文件系统

在 Linux 中，还有另一种机制让内核和内核模块向进程发送信息——`/proc` 文件系统。它最初的设计目的是允许轻松访问有关进程的信息，因此得名，现在已被内核中每一个有值得报告的内容的部分所使用，例如提供模块列表的 `/proc/modules` 和收集内存使用统计信息的 `/proc/meminfo`。

使用 `proc` 文件系统的方法与设备驱动程序中使用的方法非常相似——创建一个包含 `/proc` 文件所需所有信息的结构体，包括指向任何处理函数的指针，在我们的例子中只有一个，即当有人尝试读取 `/proc` 文件时被调用的那个函数。然后，`init_module` 将该结构体注册到内核，`cleanup_module` 则将其注销。

普通文件系统位于磁盘上，而不仅仅存在于内存中，`/proc` 就是位于内存中，在这种情况下，索引节点编号是指向磁盘上文件 inode 所在位置的指针。`inode` 包含有关文件的信息，例如文件权限，以及指向文件数据所在磁盘位置的一个或多个指针。

由于在文件被打开或关闭时我们不会被调用，因此在这个模块中没有地方放置 `try_module_get` 和 `module_put`，如果文件被打开后模块被移除，就没有办法避免后果。
