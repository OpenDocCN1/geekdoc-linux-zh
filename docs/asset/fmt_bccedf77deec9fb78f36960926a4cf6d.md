
# Linux 管理：初学者指南

## dynamic-boot-lease-length
尽管 BOOTP 客户端可能没有机制来让它们收到的地址过期，但有时可以假设它们不再使用该地址，从而将其释放供后续使用。如果已知 BOOTP 应用程序持续时间很短，这就会非常有用。如果是这样，服务器可以相应地设置秒数，并在该时间过后让其过期。

> 注意：使用此选项时要小心，因为如果它在另一个主机停止使用该地址之前就分配了地址，可能会导致问题。

该参数的语法如下：
```
dynamic-boot-lease-length seconds;
```

## filename
在某些应用程序中，DHCP 客户端可能需要知道用于启动的文件名称。这通常会与 `next-server` 结合使用，以检索远程文件进行安装配置或无盘启动。该参数的语法如下：
```
filename filename;
```

## fixed-address
此参数仅出现在主机声明 `host declaration` 项下。它指定了可以分配给客户端的地址集。该参数的语法如下：
```
fixed-address address [, address];
```

## get-lease-hostnames
如果此参数设置为 `true`，服务器将解析声明作用域内的所有地址，并将其用于主机名选项。该参数的语法如下：
```
get-lease-hostnames [true | false];
```

## hardware
为了让 BOOTP 客户端被识别，必须在该语句中使用硬件子句 `hardware clause` 声明其网络硬件地址。在这里，`hardware-type` 必须是物理硬件接口类型的名称。目前，仅识别以太网 `Ethernet` 和令牌环 `Token Ring` 类型。
`hardware-address`（有时称为介质控制 MAC 地址）是接口的物理地址，通常是一组由冒号分隔的十六进制字节。`hardware` 语句也可以用于 DHCP 客户端。该参数的语法如下：
```
hardware hardware-type hardware-address;
```

## max-lease-time
客户端有权请求租约持续时间。只要租约时间不超过此选项指定的秒数，请求就会被授予。否则，它将获得一个等于此处指定秒数最大值的租约。该参数的语法如下：
```
max-lease-time seconds;
```

## next-server
`next-server` 语句用于指定从初始启动文件（在 `filename` 语句中指定）加载的服务器主机地址。在这里，`server-name` 是一个数字 IP 地址或域名。该参数的语法如下：
```
next-server server-name;
```

## server-identifier
DHCP 响应的一部分是对服务器的回答。在多宿主系统，某些接口可能对于服务器或声明作用域的所有客户端都是不可达的。在这些极少数情况下，可以使用此参数发送客户端应与服务器进行通信的正确接口的 IP 地址。该值必须是 DHCP 服务器的 IP 地址，并且对于为特定作用域服务的所有客户端都是可用的。该参数的语法如下：
```
server-identifier hostname;
```

## server-name
`server-name` 语句可以用于告知客户端其启动的服务器的名称。`Name` 应该是提供给客户端的名称。此参数对于远程客户端或网络安装应用程序有时有用。该参数的语法如下：
```
server-name Name;
```

## use-lease-addr-for-default-route
某些网络配置使用一种名为 `ProxyARP`（代理 ARP）的技术，主机可以跟踪其子网之外的其他主机。如果你的网络配置支持 ProxyARP，你可能希望配置客户端使用自身作为默认路由。这将强制它使用 ARP（地址解析协议）来查找所有远程（子网外）的地址。

> 注意：应谨慎使用 `use-lease-addr-for-default-route` 命令，如果它在另一个主机停止使用该地址之前就分配了地址，可能会导致问题。你可能希望配置你的客户端使用自身作为默认路由。

该参数的语法如下：
```
use-lease-addr-for-default-route
```
