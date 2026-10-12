
`fprintf(stderr, "%s", "unable to register (X, X), udp).\n");`

`exit(1);`

}

```c
transp = svcdpc_create(RPC_ANYSOCK);

if(lsvc_register(transp, RPCPROG, RPCPROGVERS, RP_n, IPPROTO_UDP)) {
    fprintf(stderr, "%s", "unable to register (X, X), udp).\n");
    exit(1);
}
```

```c
/* 将控制权交交给执行调用的库例程 */
svc_run();
    fprintf(stderr, "%s", "svc_run returned");
    exit(1); /* 永远不应到达这里 */
```

在服务器可以注册远程过程之前，它必须打开一个 UDP socket，客户端机器将使用它来寻址服务器。这是通过中间级函数调用实现的

`svcdpc_create(RPC_ANYSOCK)`

此 RPC 库函数在服务器上创建一个 UDP socket，该 socket 将与远程过程名称注册。随后 `svc_register()` 过程可以注册该过程。在此函数中，如果最后一个参数指定了协议号（骨架中的 `IPPROTO_UDP`），则该 socket 将使用服务器端口（称为端口映射器 `portmapper`）注册供外部使用。这允许客户端使用服务器端口映射器以及网络名称（前提是客户端知道名称）发现注册 RPC 所在的端口。如果你研究这个骨架，你会发现它是由系列“模板”组成的，用于使用 `svc_register()` 注册每个远程过程。这里的“模板”意味着你可以复制以 `svcdpc_create()` 开头的行并将其粘贴以创建另一个注册（服务器程序的第二部分是每个服务器中调用 `svc_run()` 且从不从该调用返回的三个行代码块）。`svc_run()` 函数是另一个实现标准服务器循环的库函数：

```c
while(1) {
    /* 阻塞在传输 socket 上 */
    read(...);
    /* 现在我们有了一个 RPC 请求 */
    switch() {
    case 0: /* 产生错误 */
    case RP1: /* 调用 RP1 */
    case RP2: /* 调用 RP2 */
    ...
    case RP1: /* 调用 RP1 */
    svc_run(); /* 循环 */
    svc_reply(); /* 序列化结果 */
    break;
    case RP_n: /* 调用 RP_n */
    default: /* 永远不到达这里 */
};
```

## 外部表示（EXTERNAL REPRESENTATION）

在远程过程调用中，必须允许应用程序（执行在台机器上）能够调用网络上另一个可能的不同类型机器上的过程。例如，使用一种数据表示的机器必须将参数传递给使用另一种表示的机器。这意味着浮点数、字符串、结构体等必须从调用机器的表示转换为服务器。当结果从服务器返回时，必须转换为客户端期望的格式。

这是通过为 RPC 机制增加一个部分——外部表示转换机制（简称 XDR）来处理的。如图 17.14 所示，客户端存根使用 XDR 库将客户端机器使用的表示转换为 RPC 特定的表示。客户端随后以 RPC 特定的格式向服务器发送 RPC 请求。当 RPC 服务器请求该请求时，它会将参数从 XDR 转换为服务器计算机使用的内部格式。这是 `svc_getargs()` 的主要任务。

Sun RPC 包提供了各种参数类型的 XDR 表示。例如，如果远程过程接收一个单个整数参数，内置的 XDR 函数 `xdr_int()` 使用 XDR 转换工具提供了必要的规范。其他内置的 XDR 处理 long、short、char 及其无符号版本，以及其他几个。假设远程过程传递单个字符参数并返回整数结果。上述客户端代码片段将使用此语句调用远程过程：

```c
/* 调用 RP1 */
result = callrpc(rpc_host_name,
    RPCPROGVERS, RPC_1,
    xdr_char, &args, xdr_int, &result);
```

## 图 17.14 XDR 转换

RPC 软件包包含一组例程库，用于将数据从主机表示法与中性表示之间进行转换。这使得 RPC 能够避免诸如数据大端/小端表示等问题。

![](img/65fa32f8b1eb09c8c688a77a880941bf_773_0.png)

也就是说，`callrpc()` 的最后四个参数描述了 XDR 转换规范。调用的通用格式是：第五个参数是参数列表的 XDR 规范名称（它是 `callrpc()` 的第六个参数）；同样地，第七个参数指定返回值的 XDR 规范，第八个参数是指向结果的指针。

假设你想传输多个参数或接收多个结果，或者你的单个参数不是内置类型之一。在这种情况下，你将需要编写自己的 XDR 规范。这里有一个来自 Sun 文档的示例。假设参数类型为：

```c
struct simple {
    int a;
    short b;
};
```

那么，你需要通过定义一个名为 `xdr_simple()` 的 C 函数来定义一个新的 XDR 规范，如下代码段所示：

```c
#include <rpc/rpc.h>
...
xdr_simple(XDR *xdrsp, struct simple *simplep) {
    if(!xdr_int(xdrsp, &simplep->a))
        return(0);
    if(!xdr_short(xdrsp, &simplep->b))
        return(0);
    return(1);
}
```

也就是说，XDR 例程在失败时应返回 0，在成功时返回 1。该 XDR 例程被如下语句使用：

```c
/* Call RPC, */
result = callrpc(rpc_host_name,
```

## 实验题 17.1 使用远程过程调用

（注：此处代码不完整，保持原文）
```c
RPCPROG, RPCPROVERS, RP,
xdr_simple, &arg, ...);
```
