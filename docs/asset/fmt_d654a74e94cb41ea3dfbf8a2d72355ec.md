
```c
static int hello_release(struct inode *inode, struct file *file)
{
    printk("hello_release: successful\n");
    return 0;
}

static ssize_t hello_read(struct file *file, char *buf, size_t count,
                          loff_t *ptr)
{
    printk("hello_read: returning zero bytes\n");
    return 0;
}

static ssize_t hello_write(struct file *file, const char *buf,
                           size_t count, loff_t *ppos)
{
    printk("hello_read: accepting zero bytes\n");
    return 0;
}

static int hello_ioctl(struct inode *inode, struct file *file,
                       unsigned int cmd, unsigned long arg)
{
    printk("hello_ioctl: cmd=%ld, arg=%ld\n", cmd, arg);
    return 0;
}

static int __init hello_init(void)
{
    int ret;
    printk("Hello Example Init - debug mode is %s\n",
           debug_enable ? "enabled" : "disabled");
    ret = register_chrdev(HELLO_MAJOR, "hello", &hello_fops);
    if (ret < 0) {
        printk("Error registering hello device\n");
        goto hello_fail1;
    }
    printk("Hello: registered module successfully!\n");
    /* Init processing here... */
    return 0;
hello_fail1:
    return ret;
}

static void _exit hello_exit(void)
{
    printk("Hello Example Exit\n");
}

struct file_operations hello_fops = {
    .owner = THIS_MODULE,
    .read = hello_read,
    .write = hello_write,
    .ioctl = hello_ioctl,
    .open = hello_open,
    .release = hello_release,
};

module_init(hello_init);
module_exit(hello_exit);

MODULE_AUTHOR("Chris Hallinan");
MODULE_DESCRIPTION("Hello World Example");
MODULE_LICENSE("GPL");
```

这个扩展的设备驱动程序示例包含许多新行。从上到下，我们必须添加一个新的内核头文件，以获取文件系统操作的定义。我们还为设备驱动程序定义了一个主设备号。注意给设备驱动程序作者的说明：这不是分配设备驱动程序主设备号的正确方式。请参阅 Linux 内核文档 `…/Documentation/devices.txt` 或有关设备驱动程序的优秀书籍，以获取有关主设备号分配的指导。对于这个简单的示例，我们只是选择一个我们知道在我们的系统上没有使用的编号。

接下来我们看到四个新函数的定义，即我们的 `open`、`close`、`read` 和 `write` 方法。为了符合良好的编码实践，我们采用了一致的命名方案，该方案不会与内核中的任何其他子系统发生冲突。我们的新方法分别称为 `hello_open()`、`hello_release()`、`hello_read()` 和 `hello_write()`。就这个简单练习而言，它们是不执行任何操作的函数，只是向内核日志子系统打印一条消息。

请注意，我们还在 `hello_init()` 例程中添加了一个新的函数调用。这一行将我们的设备驱动程序注册到内核中。通过该注册调用，我们传递了一个包含指向所需方法的指针的结构体。内核使用这个类型为 `struct file_operations` 的结构体，将我们的特定设备功能与文件系统发出的相应请求绑定在一起。当应用程序打开由我们的设备驱动程序表示的设备并请求 `read()` 操作时，文件系统会将通用的 `read()` 请求与我们模块的 `hello_read()` 函数关联起来。以下各节将详细研究此过程。

### 8.3.2 设备节点与 mknod

为了理解应用程序如何将请求绑定到由我们的设备驱动程序表示的特定设备，我们必须理解设备节点的概念。设备节点是 Linux 中的一种特殊文件类型，用于表示一个设备。几乎所有 Linux 发行版都将设备节点保存在一个共同位置，由文件系统层次标准${}^{6}$指定，即名为 `/dev` 的目录中。使用一个专用工具在文件系统中创建设备节点。这个工具叫做 `mknod`。

节点创建的一个示例是说明其功能及其传达信息的最佳方式。与我们简单的设备驱动程序示例保持一致，让我们创建合适的设备节点以对其进行测试：

```bash
$ mknod /dev/hello1 c 234 0
```

在目标嵌入式系统上执行此命令后，我们最终会得到一个新文件 `/dev/hello1`，它代表我们的设备驱动程序模块。如果我们把这个文件列表打印到控制台，它看起来像这样：

```bash
$ ls -l /dev/hello1
crw-rw---- root root 234,0 Jul 14 2005 /dev/hello1
```

我们传递给 `mknod` 的参数包括我们设备驱动程序的主设备号、次设备号和名称。我们选择的名称是 `hello1`。由于我们在演示字符驱动程序的使用，我们使用 `c` 来表示这一点。主设备号是 `234`，这是我们为这个示例选择的编号，次设备号是 `0`。

就其本身而言，设备节点只是我们文件系统中的另一个文件。然而，由于它作为设备节点的特殊地位，我们使用它来绑定到已安装的设备驱动程序。如果应用程序进程发起一个 `open()` 系统调用，并指定我们的设备节点作为路径参数，内核将搜索具有与设备节点匹配的主设备号的有效已注册设备驱动程序——在我们的情况下，是 `234`。这就是内核将我们的特定设备关联到设备节点的机制。

正如大多数 C 程序员所知，`open()` 系统调用或其任何变体返回一个引用，文件描述符，我们的应用程序使用该引用发起后续的文件系统操作，如 `read`、`write` 和 `close`。然后，这个引用被传递给各种文件系统操作，如 `read`、`write` 或其变体。

${}^{6}$ 对此标准的引用可以在本章末尾的“延伸阅读建议”中找到。

对于那些对次设备号目的感到好奇的人来说，它是使用单个设备驱动程序处理多个设备或子设备的机制。它不被操作系统使用；它只是简单地传递给设备驱动程序。设备驱动程序可以按任何它认为合适的方式使用次设备号。例如，在多端口串行卡中，主设备号将指定驱动程序。次设备号可能指定同一驱动程序在多端口卡上处理的多个端口之一。感兴趣的读者建议查阅关于设备驱动程序的优秀文本以获取更多详细信息。

## 8.4 整合所有内容

既然我们有了一个骨架设备驱动程序，我们可以加载它并对其进行测试。列表 8-11 是一个简单的用户空间应用程序，用于测试我们的设备驱动程序。我们已经看过如何加载驱动程序。只需编译它并发出 `make modules_install` 命令将其放置到文件系统中，如前所述。

### 列表 8-11 测试我们的设备驱动程序

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
int main(int argc, char **argv)
{
    /* 我们的文件描述符 */
    int fd;
    int rc = 0;
    char rd_buf[16];
    printf("%s: entered\n", argv[0]);
    /* 打开设备 */
    fd = open("/dev/hello1", O_RDWR);
    if (fd == -1) {
```
