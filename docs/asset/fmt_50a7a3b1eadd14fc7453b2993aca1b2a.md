
这还不够的。想象你有一个连接到调制解调器的串口（即使你有内置调制解调器，从 CPU 的角度来看，它仍然被实现为连接到解调器的串口，所以你不需要太费想象力）。自然的做法是使用设备文件向解调器写入内容（命令或要通过电话线发送的数据），并从解调器读取内容（命令的响应或通过电话线接收的数据）。然而，当你需要与串口通信时（例如发送发送和接收数据的速率），这就留下了一个问题。

Unix 的答案是使用一个特有的函数 `ioctl`（Input Output Control，输入输出控制的缩写）。每个设备都有自己的 `ioctl` 命令，这些命令可以是读 `ioctl`（从进程向内核发送信息）、写 `ioctl`（向进程返回信息）、两者兼具或二者都不具备。调用 `ioctl` 函数时带有三个参数：适当设备文件的文件描述符、`ioctl` 编号以及一个参数（该参数为 `long` 类型，因此你可以使用 `case` 来传递任何内容）。

`ioctl` 编号编码了设备号、`ioctl` 类型、命令以及其类型。这个数字通常在头文件中通过宏调用 `_IO__IOR__OW`（取决于类型）创建。该头文件随后应该被使用 `ioctl` 的程序包含（以便它们可以生成相应的 `ioctl`）以及内核模块包含（以便它能理解它）。在示例中，文件头文件是 `chardev.h`，使用它的程序是 `ioctl.c`。

如果你想在自己的内核模块中使用 `ioctl`，最好获得一个官方的 `ioctl` 分配，否则如果你不小心拿了别人的 `ioctl`，或者他们拿了你的，你就知道出问题了。更多信息请检查内核源码树中的 `Documentation/ioctl-number.txt`。

### 示例 7-1. chardev.c

```c
/*
 * chardev.c - 创建一个输入/输出字符设备
 */

#include <linux/kernel.h>
/* * 我们正在进行内核工作 */
#include <linux/module.h>
/* * 特地，一个模块 */
#include <linux/fs.h>
#include <asm/uaccess.h>

/* * 用于 get_user 和 put_ptr */

#include <chardev.h>
#define SUCCESS 0
#define DEVICE_NAME "chardev"
#define BUF_LEN 80
```

- 设备现在打开着吗？用于防止并发访问同一个设备

```c
static int Device_Open = 0;
```

```c
/*
* 当被询问时设备将给消息
 */
static char Message[BUF_LEN];
```

```c
/*
* 读取消息的进程到了哪里？
* 如果消息大于我们在
* device_read 中填充的
* 缓冲区大小，则很有用。
 */
static char *Message_Ptr;
```

```c
/*
* 当进程尝试打开设备文件时，就会调用此函数
 */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
    printk(KERN_INFO "device_open(%p)\n", file);
#endif

  /*
* 我们不想同时与两个进程通信
 */
 if (Device_Open)
    return -EBUSY;

  Device_Open++;

  /*
* 初始化消息
 */
  Message_Ptr = Message;
  try_module_get(THIS_MODULE);
  return SUCCESS;
}
```

```c
static int device_release(struct inode *inode, struct file *file)
#ifdef DEBUG
    printk(KERN_INFO "device_release(%p,%p)\n", inode, file);
#endif

  /*
* 我们现在准备好接受下一个调用者了
 */
  Device_Open--;

  module_put(THIS_MODULE);
  return SUCCESS;
}
```

```c
/*
* 当进程已经打开设备
* 文件并尝试从中读取时，就会调用此函数。
 */
static ssize_t device_read(struct file *file, 
    /*    /* 查看 include/linux/fs.h */
    char __user *buffer, /* 缓冲区将 */
    /* 填充数据 */
size_t length,           /* 缓冲区长度 */
loff_t * offset);                    */

/*
 * 实际写入缓冲区字节数
 */
int bytes_read = 0;

#ifdef DEBUG
printk(KERN_INFO "device_read(%p,%p,%d)\n", file, buffer, length);
#endif

/*
 * 如果我们在消息的末尾，返回 0
 *（表示文件结束）
 */
if (*Message_Ptr == 0) {
    return 0;
}

/*
 * 填充缓冲区
 */
while (length && *Message_Ptr) {

/*
 * 因为缓冲区在用户空间段，
* 不在内核空间段，赋值将
* 不起。我们必须使用 put_user
* 它将数据从内核空间段拷贝
 * 到用户空间段。
 */
    if (put_user(*(Message_Ptr++), buffer++))
        length--;
    bytes_read++;
}

#ifdef DEBUG
printk(KERN_INFO "Read %d bytes, %d left\n", bytes_read, length);
#endif

/*
 * 填充缓冲区
 */
return bytes_read;
};
```

```c
/*
* 当进程已经打开设备
* 文件并尝试从中读取时，就会调用此函数。
 */
static ssize_t device_write(struct file *file, 
    /*    /* 查看 include/linux/fs.h */
    char __user *buffer, /* 缓冲区将 */
    /* 填充数据 */
size_t length,           /* 缓冲区长度 */
loff_t * offset)                    */

/*
 * 实际写入缓冲区字节数
 */
int bytes_read = 0;

#ifdef DEBUG
printk(KERN_INFO "device_read(%p,%p,%d)\n", file, buffer, length);
#endif

/*
 * 如果我们在消息的末尾，返回 0
 *（表示文件结束）
 */
if (*Message_Ptr == 0) {
    return 0;
}

/*
 * 填充缓冲区
 */
while (length && *Message_Ptr) {

/*
 * 因为缓冲区在用户空间段，
* 不在内核空间段，赋值将
* 不起。我们必须使用 put_user
* 它将数据从内核空间段拷贝
 * 到用户空间段。
 */
    if (put_user(*(Message_Ptr++), buffer++))
        length--;
    bytes_read++;
}

#ifdef DEBUG
printk(KERN_INFO "Read %d bytes, %d left\n", bytes_read, length);
#endif

/*
 * 填充缓冲区
 */
return bytes_read;
};
```

# Linux 内核模块编程指南

```c
return 0;
/*
 * 清理 - 从 /proc 中注销适当的文件
 */
void cleanup_module() {
    int ret;

    /*
     * 取消设备注册
     */
    ret = unregister_chdev(MAJOR_NUM, DEVICE_NAME);

    /*
     * 如果发生错误，则报告错误
     */
    if (ret < 0)
        printk(KERN_ALERT "Error: unregister_chdev: %d\n", ret);
}
```

###### 示例 7–2. chardev.h

```c
/*
 * chardev.h - 包含 ioctl 定义的头文件。
 * 这里的声明必须在头文件中
```

# 第 7 章.与设备文件通信

# Linux 内核模块编程指南
