
该结构并没有任何意外：`init`存储一个初始化函数，清理工作由`exit`处理。所有可用的`per_operation`实例都保留在由`per_list`头的列表中；`list`作为列表元素。辅助函数`register_subnet_subsys`和`unregister_subnet_subsys`分别从列表中添加和删除元素。每当创建一个新的网络命名空间时，内核遍历`per_operations`列表，并使用代表命名空间的`net`实例作为参数调用初始化函数。清理新命名空间的操作静默进行。

大多数计算机只需要单个网络命名空间。全局变量`init_net`（在这种情况下，变量实际上是全局的，不包含在另一个命名空间中！）包含了该命名空间的`net`实例。在下文中，为了简化问题，我大多忽略了命名空间。只需记住，网络层的所有全局函数都需要命名空间作为参数，并且网络子系统的所有属性只能通过对所考虑的命名空间的跳转来引用。

## 12.6 套接缓冲区 (Socket Buffers)

当在内核中分析数据包时，底层协议的数据会被传递给高层。在发送数据时，序列将反向对齐。各种协议生成的数据（头部和负载）会连续传递给底层，直到最终被传输。这些操作的速度对网络层性能至关重要，内核使用了一种名为套接缓冲区（socket buffer）的特殊结构，其定义如下：

```c
<sk_buff.h>

struct sk_buff {
    /* 这两个成员必须在前。 */
    struct sk_buff        *next;
    struct sk_buff        *prev;
    struct sock             *sk;
    struct time_t          tstamp;
    struct net_device     *dev;
    struct dst_entry      *dst;
    char                cb[48];
    unsigned int        len;
    __u16               data_len;
    __u16               mac_len;
    __u16               hdr_len;
    union {
        __wsum              csum;
        struct {
            __u16 csum_start;
            __u16 csum_offset;
        };
        __u32;
        __u8 priority;
        local_df:1,
        cloned:1,
        ip_summed:2,
        nohdr:1,
        nfctinfo:3,
        pkt_type:3,
        clone:2,
        ipvs_property:1,
        nf_trace:1,
        protocol;
    };
    __u8 __bel6;
    void (*destructor)(struct sk_buff *skb);
    int ifif;
    sk_buff_data_t transport_header;
    sk_buff_data_t network_header;
    sk_buff_data_t mac_header;
    /* 这些元素必须位于最后，详见 alloc_skb()。 */
    sk_buff_data_t tail;
    sk_buff_data_t end;
    unsigned char *data;
    unsigned int nsize;
    atomic_t users;
};
```

### 12.6.1 使用套接缓冲区管理数据

套接缓冲区用于在协议级之间交换数据，而无需显式复制。套接缓冲区的思想是通过操作指针来添加和删除头部，正如我们稍后看到的。当生成数据包时，TCP层首先在用户空间分配内存来存放数据包数据（头部和负载）。预留空间大于底层层添加头部所需的数据。分配一个套接缓冲区，使得`head`和`end`指向内存中预留空间的开始和结束，而TCP数据区域位于`data`和`tail`之间。当套接缓冲区传递给IP层时，必须添加新层。这可以简单地写入预留空间，除了`data`指针外，所有指针都保持不变，`data`现在指向

## 第12章：网络

到IP头部开始。对于下方的层，重复相同的操作，直到一个完成的数据包准备好发送到网络中。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_784_0.png)

分析数据包采用的方法类似。数据包数据被复制到内核中的预留内存区域，并在整个分析阶段期间保留。带有数据包的socket缓冲区在层之间传递，各种指针被继继赋予正确的值。

内核提供了表12-1所示的标准函数来操作socket缓冲区。

## 表12-1：Socket缓冲区上的操作

| 函数 | 含义 |
| --- | --- |
| `alloc_skb` | 分配一个新的`sk_buff`实例。 |
| `skb_copy` | 创建socket缓冲区及其关联数据的副本。 |
| `skb_clone` | 复制socket缓冲区，但原始数据和副本使用相同的数据包数据。 |
| `skb_tailroom` | 返回数据末尾空空间的大小。 |
| `skb_headroom` | 返回数据开头空空间的大小。 |
| `skb_realloc_headroom` | 在数据开头创建更多空空间。保留现有数据。 |

socket缓冲区需要大量的数字来表示缓冲区内容的不同组件。由于低内存占用和高处理速度对于网络层（因此对于`struct_buff`）来说至关重要，因此该结构尽可能越小越好。在64位CPU上，可以使用一个小技巧来节省一些空间。`sk_buff_data_t`的定义被更改为一个整数变量：

```c
<skbuff.h>

typedef unsigned int sk_buff_data_t;
```

由于在这些架构上，整数所需的内存仅为指针的一半（4字节而不是8字节），该结构缩小了20字节。socket缓冲区中包含的信息仍然相同，

> 8 由于在32位系统上整数和指针使用的位数相同，该技巧对它们无效。

尽管`.data`和`head`仍然是普通指针，并且所有的`sk_buff_data_t`元素现在都被解释为相对于这些指针的偏移量。指向传输头开头的指针计算如下：

```c
<sk_buff.h>

static inline unsigned *sk_transport_header(const struct sk_buff *skb)
{
    return skb->head + skb->transport_header;
}
```
