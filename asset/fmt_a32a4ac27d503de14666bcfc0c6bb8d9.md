
```c
printk(KERN_INFO "Goodbye, world 5\n");
}
module_init(init_hello_5);
module_exit(cleanup_hello_5);
```

我建议尝试一下这段代码：

```bash
satan# insmod hello-5.ko myint=10
myint = 10
satan# insmod hello-5.ko myintarray=10,20
myintarray[0] = 10
myintarray[1] = 20
satan# insmod hello-5.ko myshortarray=1,2,3,4
myshortarray[0] = 1
myshortarray[1] = 2
myshortarray[2] = 3
myshortarray[3] = 4
count = 4
```

## 2.7 跨越多个文件的模块

有时将一个内核模块划分到多个源文件中是有意义的。

这是一个此类内核模块的示例。

### 示例 2–8. start.c

```c
/*
 * start.c - 多文件模块的示例
 */
#include <linux/kernel.h>    /* 我们正在进行内核工作 */
#include <linux/module.h>     /* 特别地，一个模块 */
int init_module(void)
{
    printk(KERN_INFO "Hello, world - this is the kernel speaking\n");
    return 0;
}
```

下一个文件是：

### 示例 2–9. stop.c

```c
/*
 * stop.c - 多文件模块的示例
 */
#include <linux/kernel.h>    /* 我们正在进行内核工作 */
#include <linux/module.h>     /* 特别地，一个模块 */
void cleanup_module()
{
    printk(KERN_INFO "Short is the life of a kernel module\n");
}
```

最后是，编译（make）文件：

### 示例 2–10. Makefile

```makefile
obj-m += hello-1.0
obj-m += hello-2.0
obj-m += hello-3.0
obj-m += hello-4.0
obj-m += hello-5.0
obj-m += startstop.o
startstop-objs := start.o stop.o
all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

这是我们目前为止看到的所有示例的完整 `Makefile`。前几行没什么特殊，但对于最后一个示例，我们需要两行。首先，我们为组合后的模块发明一个对象名称，其次，我们告诉 `make` 哪些对象文件属于该模块。

# 第 2 章. Hello World（你好世界）

## 2.8. 为预编译内核构建模块

显然，我们强烈建议你重新编译内核，这样你就可以启用许多用的调试功能，例如强制卸载（`MODULE_FORCE_UNLOAD`）：当启用此选项时，你可以通过 `rmmod -f module` 在内核认为不安全时强制其卸载模块。此选项可以在开发模块时为你节省大量时间和多次重启。

尽管尽管如此，在某些情况下，你可能想将模块加载到预编译的运行中的内核中，例如与常见 Linux 发行版自带的内核，或者你过去编译过的内核。在某些情况下，你可以编译一个模块并插入到你不允许重新编译的运行内核中，或者插入到一台需要重启的机器上。如果你想不出迫使你为预编译内核使用模块的案例，你可以跳过这里，并将剩余内容视为大麻烦。

现在，如果你安装了内核源码树，用它来编译你的内核模块并尝试将模块插入内核，在大多数情况下，你会得到如下错误：

```
insmod: error inserting 'poet_atkm.ko': -1 Invalid module format
```

不那么异常的情况等于 `/var/log/messages`：

```
Jun 22:07:54 localhost kernel: poet_atkm: version magic '2.6.5-1.358custom 686 REGPARM 4KSTACK gcc-3' should be '2.6.5-1.358 686 REGPARM 4KSTACK gcc-3'
```
