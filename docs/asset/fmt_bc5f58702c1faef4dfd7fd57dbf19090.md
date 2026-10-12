
`asmlinkage`

```
int sys_getitimer(int which, struct itimerval *value)
{
    int error;
    struct itimerval get_buffer;

    if (!value)
        return -EFAULT;

    error = _getitimer(which, &get_buffer);

    if (error)
        return error;

    error = verify_area(VERIFY_WRITE, value, sizeof(struct itimerval));

    if (error)
        return error;

    memcpy_tofs(value, &get_buffer, sizeof(get_buffer));

    return 0;
}
```

`void`

```
it_real_fn(unsigned long __data)
{
    struct task_struct * p = (struct task_struct *) __data;
    unsigned long interval;

    send_sig(SIGALRM, p, 1);

    interval = p->it_real_incr;

    if (interval) {
        unsigned long timeout = jiffies + interval;
        /* Check for overflow */
        if (timeout < interval)
            timeout = ULONG_MAX;

        p->real_timer.expires = timeout;
        add_timer(&p->real_timer);
    }
}
```

如列表 6-11 所示，`int_settimer()` 函数设置间隔定时器的值。有三种类型的间隔定时器：`ITIMER_REAL`，它以实际时间倒数；`ITIMER_VIRTUAL`，它在进程运行时倒数；以及 `ITIMER_PROF`，它同时倒数虚拟定时器和用于内核剖析的实时 itimer。

### 列表 6-11：查看 `int_settimer()` 函数

```
int_settimer(int which, struct itimerval *value, struct itimerval *ovalue)
{
    register unsigned long i, j;
    int k;

    i = tvtojiffies(&value->it_interval);
    j = tvtojiffies(&value->it_value);

    if (ovalue && (k = __getitimer(which, ovalue)) < 0)
        return k;

    switch (which) {
    case ITIMER_REAL:
        del_timer(&current->real_timer);
        current->it_real_value = j;
        current->it_real_incr = i;

        if (!j)
            break;

        i = j + jiffies;
        /* check for overflow.. */
        if (i < j)
            i = ULONG_MAX;

        current->real_timer.expires = i;
        add_timer(&current->real_timer);
        break;

    case ITIMER_VIRTUAL:
        if (j)
            j++;

        current->it_virt_value = j;
        current->it_virt_incr = i;
        break;

    case ITIMER_PROF:
        if (j)
            j++;

        current->it_prof_value = j;
        current->it_prof_incr = i;
        break;

    default:
        return -EINVAL;
    }

    return 0;
}
```

`asmlinkage`

```
int sys_settimer(int which, struct itimeral *value, struct itimeral *ovalue)
{
    int error;
    struct itimeral set_buffer, get_buffer;

    if (value) {
        error = verify_area(VERIFY_READ, value, sizeof(*value));
        if (error)
            return error;
        memcpy_fromfs(&set_buffer, value, sizeof(set_buffer));
    } else
        memset((char *) &set_buffer, 0, sizeof(set_buffer));

    if (ovalue) {
        error = verify_area(VERIFY_WRITE, ovalue, sizeof(struct itimeral));
        if (error)
            return error;
    }
```

以下代码用于错误处理。由于可能存在缓冲区溢出问题，错误处理会对此进行检查。

```
error = _settimer(which, &set_buffer, ovalue ? &get_buffer : 0);

if (error || !ovalue)
    return error;

memcpy_tofs(ovalue, &get_buffer, sizeof(get_buffer));

return error;
}
```

> **缓冲区溢出已成为利用 Linux 系统漏洞的一种方式。关于从安全角度对缓冲区溢出的讲解，请参阅第 9 章。**

## 了解你的内核

你可以使用 `uname -a` 命令获取关于内核的大量信息，如下所示：

```
# uname -a

Linux tigerden 2.0.34 #5 Tue Jun 23 14:25:52 PDT 1998 i586 unknown
```

`uname` 命令首先告诉你正在使用哪个 UNIX 操作系统（在此情况下为 Linux），然后是主机名、内核版本、内核编译的日期和时间以及硬件信息。

关于内核的关键信息是版本号。在上面的例子中，内核版本为 2.0.34。由于中间的数字为偶数，这被称为发行版或稳定版内核。如果版本号中间的数为偶数，则你拥有的是稳定版内核。如果版本号中间的数为奇数，则你正在使用的是开发版内核。请记住，开发版内核可能不稳定，因为它被视为“最前沿”技术。

## 重建你的内核

虽然 Linux 附带了用于安装到硬盘的启动内核，但重建内核可以让你拥有合适的驱动程序和硬件支持，从而最大限度地利用 Linux 的功能。在本节中，你将学习如何重建内核以及 Linux 支持的一些硬件。

![](img/8ad518fddafc7f5e73715a2604b61d50_196_0.png)

要了解 Linux 支持哪些硬件的更多信息，请参阅 CD-ROM 中的 `Hardware-HOWTO`。

要重建内核，请执行以下步骤：

1. 检查你的编译器版本
2. 清除旧的编译目标文件
3. 重新配置内核
4. 重新编译内核
5. 备份当前可用的内核
6. 测试新内核

为了获得最佳的内核，请重建你的内核。这使你可以为硬件、网络和文件系统提供合适的驱动程序。这些大部分驱动程序的支持可以是内核的一部分，也可以是可加载模块。

当驱动程序被编译进内核时，Linux 假设硬件存在。另一方面，可加载模块是内核的一部分，只有当内核检测到硬件存在时才会被加载到内核中。当 Linux 检测到硬件时，该模块会被插入内核。一个很好的例子是 PCMCIA 驱动程序，其中模块在卡片插入时加载，在卡片移除时卸载。

在重新编译内核之前，请检查 `gcc` 的版本是否正确（更新版本，确保你正在使用 ELF 格式等）。

要查找你正在运行的 `gcc` 的版本号，请键入以下命令：

```
# gcc -v
```
