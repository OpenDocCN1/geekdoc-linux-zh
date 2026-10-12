
```c
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

在服务器注册远程过程之前，它必须打开一个 UDP socket，客户端机器将使用它地址服务器。这是通过中间级函数调用实现的

`svcdpc_create(RPC_ANYSOCK)`

此 RPC 库函数在服务器上创建一个 UDP socket，该 socket 将与远程过程名称注册。随后 `svc_register()` 过程可以注册该过程。在此函数中，如果最后一个参数指定了协议号（骨架中的 `IPPROTO_UDP`），则该 socket 将使用服务器端口（称为端口映射器 `portmapper`）注册供外部使用。这允许客户端使用服务器端口映射器以及网络名称（前提是客户端知道名称）发现注册 RPC 所在的端口。如果你研究这个骨架，你会发现它是由系列“模板”组成的，用于使用 `svc_register()` 注册每个远程过程。这里的“模板”意味着你可以复制以 `svcdpc_create()` 开头的行并将其粘贴以创建另一个注册（服务器程序的第二部分是每个服务器中调用 `svc_run()` 且从不从该调用返回的三个行代码块）。`svc_run()` 函数是另一个实现标准服务器循环（canonical server loop）的库函数：

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

不同的客户端调用 RPC 服务器，服务器接收请求，调用其本地版本的过程，将结果返回给客户端，然后等待另一个请求。如果服务器正在处理上一个客户端的请求，另一个客户端进行了调用，第二个客户端将等待第一个请求完成后才能进入。

服务器代码首先为客户端设置一个命名服务，以便客户端定位可以执行远程过程的服务器；这被称为远程过程注册（`remote_procedure registration`）。一旦注册了远程过程，客户端就可以通过调用命名服务来找到该远程过程服务器。在最简单的情况下，注册仅在服务器机器上完成，要求客户端知道 RPC 服务器的名称。在服务器注册了它的远程可调用过程后，它将开始等待 RPC 请求。当请求到达时，服务器会反序列化调用的详细信息（过程标识和参数），执行本地过程调用，然后序列化结果并返回给客户端（存根/`stub`）。

Sun 设计的 RPC 包允许将多个远程过程封装在单个 RPC 程序中。这使得单个服务器线程可以调用不同的远程过程，允许这些过程在服务器的同一个地址空间内工作。

在支持 RPC 时，还有一个重要的考虑因素。一旦部署了 RPC 程序，预计将运行很长时间。此外，一旦远程过程可用，任何数量的客户端都可能依赖它。假设实现中包含一个微小的 bug，或者程序员创建了具有附加功能的新版本过程。使用现有版本的某些客户端可能不想升级到新版本，因为这可能需要一些客户端编程来利用新功能。而如果新版本确实修复了某个微小的 bug，其他客户端可能需要这个新版本。由于这些可能性，Sun 设计的 RPC 设施使其支持每个远程过程的多个版本。也就是说，可以有不同的远程过程具有相同的 RPC 程序名称和过程名称，但版本号不同。这意味着当客户端查找其远程过程的实现时，它必须知道远程过程名称、RPC 程序名称和版本号。也就是说，RPC 服务器通过 (`远程过程`, `RPC 程序`, `版本号`) 来区分不同的实现。

在实现特定的过程服务器时，设计者首先决定将实现哪些过程。假设服务器要支持一个命名为 `RP1`、`RP2`、... 的 `n` 个远程过程，它们在特定的 RPC 程序 (`RPCPROG`) 中具有相同的版本号 (`RPCPROGVERS`)。小于 `0x4000000` 的 RPC 程序号由系统永久预留。应用程序（包括你对本练习的解答）使用随机选择的大于 `0x4000000` 的程序号。主程序将如下所示：

```c
main(int argc, char *argv[]) {
    register SVXPCFT transp;
```

```c
/* 使用命名服务注册远程过程 */
transp = svcdpc_create(RPC_ANYSOCK);
if(lsvc_register(transp, RPCPROG, RPCPROGVERS, RP1, IPPROTO_UDP)) {
    fprintf(stderr, "%s", "unable to register (X, X), udp).\n");
    exit(1);
}
```

```c
transp = svcdpc_create(RPC_ANYSOCK);
if(lsvc_register(transp, RPCPROG, RPCPROGVERS, RP_2, IPPROTO_UDP)) {
```
