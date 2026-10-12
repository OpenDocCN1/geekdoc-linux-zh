
## 消息长度查找

```c
/* 找到消息的长度 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    get_user(ch, temp);
    for (i=0; ch && i<BUF_LEN; i++, temp++)
        get_user(ch, temp);
#else
    for (i=0; get_user(temp) && i<BUF_LEN; i++, temp++)
    ;
#endif
```

## 设备释放

```c
printk ("device_release(%p,%p)\n", inode, file);
#endif
```

## 设备打开计数递减

```c
/* 我们现在已经准备好处理下一个调用者了 */
Device_Open --;
```

## 模块使用计数递减

```c
MOD_DEC_USE_COUNT;
```

## 设备读函数

```c
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
return 0;
#endif
```

```c
/* 每当已经打开设备文件的进程
* 尝试从其读取数据时，该函数就会被调用。 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t device_read(
    struct file *file,
    char *buffer, /* 用于填充数据的缓冲区 */
    size_t length, /* 缓冲区的长度 */
    loff_t *offset) /* 指向文件的偏移量 */
#else
static int device_read(
    struct inode *inode,
    struct file *file,
    char *buffer, /* 用于填充数据的缓冲区 */
    int length)
    /* 缓冲区的长度 */
    /* (不能写入超出范围!) */
#endif
```

```c
{
    /* 实际写入缓冲区的字节数 */
    int bytes_read = 0;
```

```c
#ifdef DEBUG
printk("device_read,%p,%p)d\n", file, buffer, length);
#endif

/* 如果我们到达消息的末尾，返回 0
* (表示文件结束) */
if (Message_Ptr == 0)
return 0;

/* 实际上将数据放入缓冲区 */
while (length && *Message_Ptr) {

    /* 因为缓冲区位于用户数据段中，
    * 而不是内核数据段，直接赋值将
    * 不起。相反，我们必须使用 put_user，
    * 将数据从内核数据段拷贝到
    * 用户数据段。 */
    put_user(*Message_Ptr++, buffer++);
    length--;
    bytes_read++;
}

#ifdef DEBUG
printk("Read %d bytes, %d left\n", bytes_read, length);
#endif

/* 读取函数应该返回实际插入到
* 缓冲区中的字节数 */
return bytes_read;
}

/* 当有人尝试向我们的设备文件
* 写入时，该函数就会被调用。 */
```

## 设备写函数

```c
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t device_write(struct file *file,
                           const char *buffer,
                           size_t length,
                           loff_t *offset)
#else
static int device_write(struct inode *inode,
                         struct file *file,
                         const char *buffer,
                         int length)
#endif
```

```c
{
    int i;
```

```c
#ifdef DEBUG
printk("device_write%p,%s%d",
       file, buffer, length);
#endif
```

```c
for(i=0; i<length && i<BUF_LEN; i++)
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    get_user(Message[i], buffer+i);
#else
    Message[i] = get_user(buffer+i);
#endif
```

`Message_Ptr = Message;`

```c
/* 再次返回使用的输入字符数 */
return i;
}
```

## 设备 ioctl 函数

- /* 每当进程尝试对我们的设备文件执行 `ioctl` 操作时，该函数就会被调用。我们得到了两个额外的

* 参数（除了 `inode` 和 `file`

* 结构体，所有设备函数都会获取这些结构体）：被调用的

* `ioctl` 数量以及传递给

* `ioctl` 函数的参数。

* 如果 `ioctl` 是写或读/写（意味着输出

* 被返回给调用进程），则 `ioctl` 调用

* 将返回此函数的输出。

*/

```c
int device_ioctl(
    struct inode *inode,
    struct file *file,
    unsigned int ioctl_num, /* ioctl 的数量 */
    unsigned long ioctl_param) /* 传递它的参数 */
{
    int i;
    char *temp;
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    char ch;
#endif
```

/* 根据调用的 `ioctl` 进行分支 */

```c
switch (ioctl_num) {

    case IOCTL_SET_MSG:

        /* 接收指向消息（在用户空间）的指针

        * 并将其设置为设备的消息。 */

        /* 获取进程传递给 `ioctl` 的参数 */

        temp = (char *) ioctl_param;

```

```c
/* 找到消息的长度 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    get_user(ch, temp);
    for (i=0; ch && i<BUF_LEN; i++, temp++)
        get_user(ch, temp);
#else
    for (i=0; get_user(temp) && i<BUF_LEN; i++, temp++)
    ;
#endif
```

```c
/* 不要重复发明轮子 - 调用 `device_write` */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    device_write(file, (char *) temp);
#else
    device_write(file, (char *) temp);
#endif
    break;

```

```c
    case IOCTL_GET_MSG:

        /* 获取一个指向消息（在用户空间）的指针

        * 并将其设置为设备的消息。 */

        /* 获取进程传递给 `ioctl` 的参数 */

        temp = (char *) ioctl_param;

```

```c
/* 找到消息的长度 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    get_user(ch, temp);
    for (i=0; ch && i<BUF_LEN; i++, temp++)
        get_user(ch, temp);
#else
    for (i=0; get_user(temp) && i<BUF_LEN; i++, temp++)
    ;
#endif
```

*注：原文中包含大量重复的 `switch` 和 `case` 块，已根据指令要求处理重复内容。*
