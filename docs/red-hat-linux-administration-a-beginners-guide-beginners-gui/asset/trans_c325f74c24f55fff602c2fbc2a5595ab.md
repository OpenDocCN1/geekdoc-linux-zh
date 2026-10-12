

这主要用于 BOOTP 客户端。有一些 BOOTP 客户端要求服务器响应完全符合 BOOTP 请求评论（RFC）标准。启用此参数可确保满足此要求。

**authoritative**

此参数的语法如下：

```
authoritative;
not authoritative;
```

**authoritative** 参数用于将特定网络标记为“权威”。默认情况下，服务器会假设自己是权威的。当网络段“不权威”时，服务器会向客户端发送 DHCPNAK 消息以示此情况。届时，客户端可能会重试其请求。

**default-lease-time**

此参数的语法如下：

```
default-lease-time seconds;
```

*seconds* 的值是如果客户端未请求任何时长时分配给发出的 IP 地址的租期时长。租期时长是服务器流量与释放地址以供重用之间的权衡。

**dynamic-bootp-lease-cutoff**

此参数的语法如下：

```
dynamic-bootp-lease-cutoff date;
```

BOOTP 客户端不了解*lease*（租约）概念。默认情况下，DHCP 服务器分配一个永不过期的 IP 地址。在某些情况下，让服务器停止为一组 BOOTP 客户端发放地址可能很有用。在这些情况下，会使用此参数。

*date* 以 *W YYYY/MM/DD HH:MM:SS* 的形式指定，其中 *W* 是以 cron 格式表示的星期几（0=星期日，6=星期六），*YYYY* 是年份，*MM* 是月份（01=一月，12=十二月），*DD* 是两位数的日期，*HH* 是两位数的 24 小时制小时（0=午夜，23=晚上 11 点），*MM* 是两位数的分钟表示；*SS* 是两位数的秒表示。

**dynamic-bootp-lease-length**

此参数的语法如下：

```
dynamic-bootp-lease-length seconds;
```

尽管 BOOTP 客户端没有使所接收地址过期的机制，但有时让服务器假设它们不再使用该地址，从而将其释放以供进一步使用是安全的。如果已知 BOOTP 应用程序持续时间较短，这很有用。在这种情况下，服务器可以相应地设置*seconds* 数量，并在该时间过去后使其过期。

> **CAUTION**
>
> 谨慎使用此选项，因为它可能会在另一个主机停止使用该地址之前发放地址，从而引起问题。

**filename**

此参数的语法如下：

```
filename filename;
```

在某些应用程序中，DHCP 客户端可能需要知道用于启动的文件名。这通常与 **next-server** 结合使用，以检索用于安装配置或无盘启动的远程文件。

**fixed-address**

此参数的语法如下：

```
fixed-address address [ , address ...] ;
```

此参数仅出现在 **host** 声明下。它指定了可分配给客户端的地址集。

**get-lease-hostname**

此参数的语法如下：

```
get-lease-hostname [ true | false ];
```

如果设置为 *true*，服务器将解析声明范围内的所有地址，并用于 **hostname** 选项。

**hardware**

此参数的语法如下：

```
hardware [ ethernet | token-ring ] hardware-address ;
```

为了使服务器能够识别特定主机，必须使用 **hardware** 参数。*hardware-address*（有时称为 MAC 地址）是接口的物理地址，通常是一组以冒号分隔的十六进制字节。此参数用于固定地址 DHCP 客户端，并且对于 BOOTP 客户端是必需的。

**max-lease-time**

此参数的语法如下：

```
max-lease-time seconds;
```

客户端可以选择请求租期时长。只要租期时长不超过此选项指定的秒数，请求就会被授予。否则，授予的租期将为此处指定的秒数最大值。

**next-server**

此参数的语法如下：

```
next-server server-name;
```

在通过网络启动时，客户端可以指定一个文件名（由 **filename** 参数指定）和一个获取启动信息的服务器。该服务器由 **next-server** 参数指定。

**server-identifier**

此参数的语法如下：

```
server-identifier hostname;
```

DHCP 响应的一部分是服务器地址。在多宿主系统上，DHCP 服务器发出第一个接口的地址。不幸的是，该接口可能无法被服务器或声明范围内的所有客户端访问。在这些罕见情况下，可以使用此参数发送客户端应与其通信的正确接口的 IP 地址。

**server-name**

此参数的语法如下：

```
server-name name;
```

其中 *name* 是由远程启动客户端启动的服务器的名称。此参数用于远程客户端或网络安装应用程序。

**use-host-decl-names**

此参数的语法如下：

```
use-host-decl-names [true|false];
```

此参数用于与其他主机声明相同的范围。它将向 **host** 声明添加 **host-name** 选项，使用声明中的主机名作为选项主机名。

**use-lease-addr-for-default-route**

此参数的语法如下：

```
use-lease-addr-for-default-route [true|false];
```

某些网络配置使用一种称为 ProxyARP 的技术，以便主机可以跟踪位于其子网之外的其他主机。如果您的网络配置为支持 ProxyARP，则需要配置客户端以将其自身用作默认路由。这将强制它使用 ARP（地址解析协议）来查找所有远程（子网外）地址。

![](img/ec2066d370d3af1a767664d36aa7ddfe_577_0.png)

应谨慎使用 **use-lease-addr-for-default-route** 命令。并非所有客户端都可以配置为将其自身接口用作默认路由。

## 选项

目前，DHCP 服务器支持超过 60 个选项。选项的一般语法如下：

`option option-name [modifiers]`

表 20-1 总结了最常用的 DHCP 选项。将在项目 20-1 中看到这些选项使用的一些示例。

| 选项名称 | 描述 |
| :--- | :--- |
| **broadcast-address** | 指定为广播地址的客户端子网上的地址 |
| **domain-name** | 客户端执行主机查找时应使用的本地域名 |
| **domain-name-servers** | 客户端用于解析主机名的 DNS 服务器列表 |
| **host-name** | 用于标识客户端名称的字符串 |
| **nis-domains** | 网络信息服务（NIS）域名（参见模块 17） |
| **nis-servers** | 可用于绑定的 NIS 服务器列表 |
| **routers** | 客户端应按优先级顺序使用的路由器列表 |
| **subnet-mask** | 客户端应使用的子网掩码 |

**表 20-1 DHCP 服务器配置中常用的选项**

### 进度检查

- 1. 在配置 DHCP 服务器时，`shared-network` 声明代表什么？
- 2. 什么是 MAC 地址？

**项目 20-1 设置 DHCP 服务器**

现在您已经具备了创建可运行的 DHCP 配置所需的基础，让我们通过一个示例来演练一下。在这个项目中，您将创建一个简单的 `dhcp.conf` 文件，您可以根据自身需求对其进行修改。完成此项目后，您应该对前面部分介绍的选项和参数如何配合使用有更清晰的理解。

### 逐步指南

- 1. 使用您最喜欢的文本编辑器打开 `/etc/dhcpd.conf`。
- 2. 设置您的网络。

```
subnet 192.168.1.0 netmask 255.255.255.0
# Options
option routers 192.168.1.1;
option subnet-mask 255.255.255.0;
```

- 3. 输入您的域名和 DNS 服务器。

```
option domain-name "example.com";
option domain-name-servers delirium.example.com;
```

- 4. 选择您的租期时长。

```
# Parameters
default-lease-time 21600;
max-lease-time 43200;
```

- 5. 创建要发放的地址范围。

```
# Declarations
range dynamic-bootp 192.168.1.25 192.168.1.49;
```

- 1. `shared-network` 声明将同一物理网络的成员地址集分组。这允许将参数和声明分组以用于管理目的。
- 2. MAC 地址是以太网卡的永久硬件地址。

![](img/ec2066d370d3af1a767664d36aa7ddfe_578_0.png)

![](img/ec2066d370d3af1a767664d36aa7ddfe_578_1.png)

![](img/ec2066d370d3af1a767664d36aa7ddfe_578_2.png)

