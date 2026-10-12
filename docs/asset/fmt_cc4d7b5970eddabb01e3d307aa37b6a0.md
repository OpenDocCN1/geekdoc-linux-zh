
## 第 12 章：网络

可以通过运行时加载到内核的模块来增强 `netfilter` 的功能。一组定义规则集告知内核何时使用各个模块的代码。内核与 `netfilter` 之间的接口保持了尽可能（以及在必要时）将这两个领域相互隔离开来，以防止相互干扰并提高网络稳定性。

正如前面的章节中经常提到的，`netfilter` 钩子（`hooks`）在内核的各个位点被调用，以支持 `netfilter` 代码的执行。这些钩子不仅用于 `IPv4`，还用于 `IPv6` 和 `DECNET` 协议。这里只讨论 `IPv4`，但这些概念同样适用于另外两个协议。

`netfilter` 的实现分为两个领域：

- 内核中的钩子（`Hooks`）用于调用 `netfilter` 代码，并处于网络实现的头部。
- `Netfilter` 模块，其代码从钩子内部调用，或者与剩余的网络代码保持独立。一组标准模块提供了必要的独立函数，而用户特定的函数可以在扩展模块中定义。

管理员使用 `iptables` 来配置防火墙、数据包过滤和类似的功能，它本质上是构建在 `netfilter` 框架之上的模块，提供了一套全面且定义良好的库函数以方便数据包处理。我将不会描述规则如何从用户空间被激活和管理；请参阅大量关于网络管理的文献。

## 调用钩子函数

当执行 `netfilter` 代码时，网络层的函数会被钩子中断。钩子的一个重要特性是，它们将一个函数拆分为两部分——第一部分在调用 `netfilter` 代码之前运行，第二部分在之后运行。为什么要使用两个函数，而不是调用一个执行所有相关任务并返回到调用函数的 `netfilter` 函数呢？这种方法初看似乎很复杂，但可以这样解释：它允许用户（或管理员）决定是否将 `netfilter` 功能编译到内核中，在那种情况下，网络函数可以在不损失任何速度的情况下执行。它还通过预处理器语句解决了网络实现中的谜题，这些语句根据特定选项（启用或禁用选项）在编译时选择适当的代码段。

`netfilter` 钩子通过 `<netfilter.h>` 中的 `NF_HOOK` 宏调用。如果内核中启用了 `netfilter` 支持，该宏定义如下：

```c
<netfilter.h>

static inline int nf_hook_thresh(int pf, unsigned int hook,
	struct sk_buff **buff,
	struct net_device *indev,
	struct net_device *outdev,
	int (*okfn)(struct sk_buff *sk), int thres,
	int cond)
{
	if (!cond)
		return 1;
	return nf_hook_slow(pf, hook, pskb, indev, outdev, okfn, thres);
}
```

```c
<netfilter.h>

#define NF_HOOK_THRESH(fp, hook, skb, indev, outdev, okfn, thresh) \
    ((int[]){ \
        int _ret; \
        if ((_ret=nf_hook_thresh(fp, hook, &skb, indev, outdev, okfn, 1)) == 1) \
            _ret = okfn(skb); \
        return _ret; \
    })()
#define NF_HOOK(fp, hook, skb, indev, outdev, okfn) \
    NF_HOOK_THRESH(fp, hook, skb, indev, outdev, okfn, INT_MIN)
```

该宏具有以下含义：

- `pf` 指向 `netfilter` 钩子源自协议族。`IPv4` 层中的所有调用都使用 `PF_INET`。
- `hook` 是钩子编号；可能的值定义在 `<netfilter-ipv4.h>` 中。如上所述，`IPv4` 中的值具有如 `NF_IP_FORWARD` 和 `NF_IP_LOCAL_OUT` 等名称。
- `skb` 是指向的套接缓冲区（socket buffer）。
- `indev` 和 `outdev` 是指向 `net_device` 实例的指针，数据包通过它们进入和离开内核。

可以传递空指针，因为并不是所有钩子都知道这些值（例如执行路由之前，内核不知道数据包将从哪个设备离开内核）。

- `okfn` 是指向一个函数的指针，其原型为 `(*okfn) (struct sk_buff *)`。它在 `netfilter` 终止时执行。

宏的展开绕过了 `NF_HOOK_THRESH` 和 `nf_hook_thresh`，这两者负责处理 `netfilter` 钩子并继续执行函数。这种看似复杂的方法是必要的，因为内核还提供了可能，即只考虑优先级高于某个阈值的 `netfilter` 钩子并跳过所有其他。在 `NF_HOOK` 的情况下，阈值设置为最小可能的整数值，以便使用 `NF_HOOK_THRESH` 指向特定阈值。只有 `IPv6` 的桥接实现和连接跟踪可能会使用，我不再进一步讨论。

考虑 `NF_HOOK_THRESH` 的实现。首先，如果 `cond` 给出的条件为真，则调用 `nf_hook_thresh`。如果没有，则直接传递给调用者。否则，`nf_hook_slow` 遍历所有注册的 `netfilter` 钩子并调用它们。如果数据包被接受，返回 `1`，否则返回其他值。

如果 `nf_hook_thresh` 返回 `1`，且 `netfilter` 的裁定是接受数据包，则控制权传递给 `okfn` 中指定的后续函数。

`IP` 转发代码包含一个典型的 `NF_HOOK` 宏调用，我们将作为一个示例：

```c
net/ipv4/in_forward.c

int ip_forward(struct sk_buff *skb)
{
    return NF_HOOK(PF_INET, NF_IP_FORWARD, skb, skb->dev, skb->dev_out, ip_forward);
}
```

## 扫描钩子表

如果至少注册了一个钩子函数并需要调用，就会调用 `nf_hook_slow`。所有的钩子都存储在 `nf_hooks` 二维数组中：

```c
net/filter/core.c

struct list_head nf_hooks[NPROTO][NF_MAX_HOOKS] __read_mostly;
```

`NPROTO` 指定了系统支持的协议族最大数量（当前为 `34`）。各个协议族的符号常量定义为 `PF_INET` 和 `PF_DECNet`；它们存储在 `include/linux/socket.h` 中。可以定义包含每个协议钩子（`hooks`）的 `NF_MAX_HOOKS` 列表；默认值为 `8`。

表中的 `list_head` 元素用作双向链表的头，该链表接受 `nf_hook_ops` 实例：

```c
<netfilter.h>

struct nf_hook_ops {
    struct list_head head_list;
    /* User fills in from here. */
    nf_hookfn *hook;
    struct module *owner;
    int pf;
    int hooknum;
    /* Hooks are ordered in ascending priority. */
    int priority;
};
```

除了标准元素（（用于在双向链表中链接列表的列表，以及当钩子实现正确时作为所有者模块数据结构指针的 `owner`）外，还有其他具有以下含义的元素：

- `hook` 是指向钩子的指针，其要求与 `NF_HOOK` 宏相同：

```c
<netfilter.h>

typedef unsigned int nf_hookfn(unsigned int,
    struct sk_buff *skb,
    const struct net_device *dev,
    const struct net_device *out,
    int (*okfn)(struct sk_buff *skb));
```
