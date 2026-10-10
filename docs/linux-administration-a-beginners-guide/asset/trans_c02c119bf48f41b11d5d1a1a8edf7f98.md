
## 组（GROUP）

我们可能由于多种原因需要对不同的客户端进行分组，例如组织需求、网络布局和管理域。为了协助对这些客户端进行分组，我们引入了以下声明。

对每个主机反复单独列出参数和声明会使配置文件难以管理。**组（group）** 声明允许你将一组参数和声明应用于客户端列表、共享网络或子网。组声明的语法如下：

```
group label {
    [parameters]
    [subdeclarations]
}
```

*标签（label）* 是用于标识该组的用户定义名称。*参数（parameter）* 块包含应用于该组的参数列表。当需要更细粒度的级别来描述可能属于当前声明的额外客户端时，会使用*子声明（subdeclarations）*。

暂时忽略参数字段。我们将在本章后面详细讨论它。

## 主机（HOST）

**主机（host）** 声明用于将一组参数和声明应用于特定主机，此外还应用指定给组的参数。这通常用于固定地址启动或 BOOTP 客户端。主机声明的语法如下：

```
host label {
    [parameters]
    [subdeclarations]
}
```

*标签（label）* 是用于主机组的用户定义名称。*参数（parameters）* 和 *子声明（subdeclarations）* 如组声明中所述。

## 共享网络（SHARED-NETWORK）

**共享网络（shared-network）** 声明将同一物理网络的成员的一组地址分组。这允许出于管理目的将参数和声明进行分组。语法如下：

```
shared-network label {
    [parameters]
    [subdeclarations]
}
```

*标签（label）* 是用于共享网络的用户定义名称。*参数（parameters）* 和 *子声明（subdeclarations）* 如前面的声明中所述。

## 子网（SUBNET）

子网声明用于将一组参数和/或声明应用于匹配该声明描述的一组地址。语法如下：

```
subnet subnet-number netmask netmask {
  [parameters]
  [subdeclarations]
}
```

*标签（label）* 是用于子网的用户定义名称。*参数（parameters）* 和 *子声明（subdeclarations）* 如前面的声明中所述。

## 范围（RANGE）

对于动态启动，范围声明指定了可以颁发给客户端的有效地址范围。语法如下：

```
range [dynamic-bootp] starting-address [ending-address] ;
```

*dynamic-bootp* 关键字用于提醒服务器，接下来的地址范围适用于 BOOTP 协议。*starting-address* 和可选的 *ending-address* 字段是 IP 地址起始块和结束块的实际地址。假设这些块是连续的并且位于同一地址子网中。

# 参数

我们在本章前面简要介绍了这个概念。开启这些参数将改变服务器对相关客户端组的行为。我们将在下一节中讨论这些参数。

## ALWAYS-REPLY-RFC1048

此参数的语法如下：

```
always-reply-rfc1048;
```

这主要用于 BOOTP 客户端。有些 BOOTP 客户端要求服务器的响应完全符合 BOOTP RFC 标准。开启此参数可确保满足该要求。

## AUTHORITATIVE

此参数的语法如下：

```
authoritative;
not authoritative;
```

*authoritative* 参数用于默认将特定网络标记为“权威”；服务器将假设自己是权威的。当网络段被标记为“*非权威（not authoritative）*”时，服务器将向客户端发送 DHCPNAK。届时，客户端可能会重试其请求。

## DEFAULT-LEASE-TIME

此参数的语法如下：

```
default-lease-time seconds;
```

*seconds* 的值是如果客户端未请求任何持续时间，则分配给已颁发 IP 地址的租期。

## DYNAMIC-BOOTP-LEASE-CUTOFF

此参数的语法如下：

```
dynamic-bootp-lease-cutoff date;
```

BOOTP 客户端不了解 *租期（lease）* 的概念。默认情况下，DHCP 服务器分配一个永不到期的 IP 地址。在某些情况下，让服务器停止为一组 BOOTP 客户端颁发地址可能很有用。在这种情况下，使用该参数。

日期以 *YYYY/MM/DD HH:MM:SS* 的形式指定，其中 *W* 是 *cron* 格式中的星期几（0=周日，6=周六）；*YYYY* 是年份；*MM* 是月份（01=一月，12=十二月）；*DD* 是两位数字格式的日期；*HH* 是 24 小时制中的两位数字小时（0=午夜，23=23 点）；*SS* 是两位数字表示的秒数。

## DYNAMIC-BOOTP-LEASE-LENGTH

此参数的语法如下：

```
dynamic-bootp-lease-length seconds;
```

虽然 BOOTP 客户端没有使它们收到的地址过期的机制，但让服务器假设它们不再使用该地址，从而释放地址供进一步使用，有时是安全的。如果已知 BOOTP 应用程序持续时间较短，则很有用。如果是这样，服务器可以相应地设置“*seconds*”的数量，并在该时间过去后使其过期。

> **注意：** 使用此选项时要小心，因为在其他主机停止使用该地址之前颁发地址可能会引入问题。

## FILENAME

此参数的语法如下：

```
filename *filename*;
```

在某些应用程序中，DHCP 客户端可能需要知道用于启动的文件名称。这通常与 **next-server** 结合使用，以检索远程文件用于安装配置或无盘启动。

## FIXED-ADDRESS

此参数的语法如下：

```
fixed-address address [address ...];
```

此参数仅出现在“主机”声明下。它指定了可分配给客户端的地址集。

## GET-LEASE-HOSTNAME

此参数的语法如下：

```
get-lease-hostname [true | false];
```

如果设置为 true，服务器将解析声明范围内的所有地址，并将其用于 **hostname** 选项。

## HARDWARE

此参数的语法如下：

```
hardware [etherent|token-ring] hardware-address;
```

为了使服务器能够识别特定主机，必须使用硬件参数。**hardware-address**（有时称为 MAC 地址）是接口的物理地址，通常是由冒号分隔的一组十六进制八位字节。此参数用于固定地址的 DHCP 客户端，并且是 BOOTP 客户端必需的。

## MAX-LEASE-TIME

此参数的语法如下：

```
max-lease-time seconds;
```

客户端可以选择请求租期的持续时间。只要租期不超过此选项指定的秒数，请求就会被批准。否则，将授予此处指定的最大秒数的租期。

## NEXT-SERVER

此参数的语法如下：

```
next-server server-name;
```

当通过网络启动时，客户端可以给定一个文件名（由 **file-name** 参数指定）和一个用于获取启动信息的服务器。该服务器由 **next-server** 参数指定。

## SERVER-IDENTIFIER

此参数的语法如下：

```
server-identifier hostname;
```

DHCP 响应的一部分是服务器地址。在多宿主系统上，DHCP 服务器颁发第一个接口的地址。不幸的是，该接口可能无法被服务器的所有客户端或声明范围访问。在那些罕见情况下，可以使用此参数来发送客户端应与其通信的服务器的正确接口的 IP。

## SERVER-NAME

此参数的语法如下：

```
server-name name;
```

该名称是由远程启动客户端启动的服务器的宿主名称。此参数用于远程客户端或网络安装应用程序。

## USE-HOST-DECL-NAMES

此参数的语法如下：

```
use-host-decl-names [true|false];
```

此参数与其他主机声明在同一范围内使用。它将使用声明中的主机名将 host-name 选项添加到主机声明中。

## USE-LEASE-ADDR-FOR-DEFAULT-ROUTE

此参数的语法如下：

```
use-lease-addr-for-default-route [true|false];
```

某些网络配置使用一种称为 proxyarp（代理 ARP）的技术，以便主机可以跟踪其子网外其他主机的状态。如果您的网络配置支持 proxyarp，您希望将客户端配置为使用自身作为默认路由。这将强制它使用 arp（地址解析协议）来查找所有远程地址（远程意指子网外）。

> **注：** 应谨慎使用 **use-lease-addr-for-default-route** 命令，因为并非每个客户端都可以配置为使用其自身接口作为默认路由。

## 选项

目前，DHCP 服务器支持超过 60 个选项。选项的通用语法如下：

```
option option-name [modifiers]
```

表 22-1 是最常用选项的摘要。

