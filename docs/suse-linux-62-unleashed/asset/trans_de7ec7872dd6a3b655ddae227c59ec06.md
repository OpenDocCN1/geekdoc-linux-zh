
一旦运行了启用了别名（aliasing）的内核，创建别名就像执行标准的 `ifconfig` 命令一样简单。你只需要在接口名称后面加上一个冒号和一个别名数字即可。这是一个示例：

```
ifconfig eth0:0 10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
```

这将为以太网接口 eth0 创建一个别名为 eth0:0 的接口，并带有提供的参数。

为了在每次主机启动时自动创建别名，你可以将创建别名的命令添加到 `/etc/init.d/network`。

## 其他 ifconfig 选项

针对某些特殊情况，ifconfig` 还有其他选项：

`ifconfig interface local-address pointpoint remote-address` 将启用点对点接口——该接口仅连接到单个主机，而不是网络。远程主机也必须启用该接口，并交换 `local-address` 和 `remote-address` 参数。

`ifconfig local-address tunnel remote-address` 将会在两个 IPv6 网络之间创建一个 IPv4 隧道。IPv4 是当前互联网的 TCP/IP 标准。IPv6 是下一代 IP。如果有任何需要通过互联网连接的 IPv6 网络，则必须创建一个使用 IPv4 协议的隧道。

## 操控路由表：route

`/sbin/route` 命令用于操作内核的路由表。内核使用此表来查看离开主机需要执行什么——是直接发送到目标主机还是网关，以及通过哪个网络接口发送。

`route` 命令的一般形式如下：

```
route [options] [command parameters]
```

## 查看路由表

该命令最简单的形式（无选项、无命令）直接输出路由表。任何用户都可以使用这种形式的命令：

```
$ /sbin/route
```

```
Kernel IP routing table
```

| IP | Gateway | Netmask | Flags | Metric | Ref | Use |
| --- | --- | --- | --- | --- | --- | --- |
| iface localnet | | 255.255.255.0 | U | 0 | 0 | 16 |
| eth0 | | | | | | |

![](img/cbac72550c7126a22162e94d91a0c360_222_0.png)

## 网络与互联网服务
PART II

| IP | Gateway | Netmask | Flags | Metric | Ref | Use |
| --- | --- | --- | --- | --- | --- | --- |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 2 |
| wlan0 | | | | | | |
| default | router.company.0.0.0.0 | UG | 0 | 0 | 71 |
| eth0 | | | | | | |

输出共有八列：

1. 第一列（Destination 目的）指示路由目的地。如果在 `/etc/hosts` 或 `/etc/networks` 中存在条目，则会替换名称。特殊名称 `default` 表示默认网关。
2. 第二列（Gateway 网关）指示发往此目的地的数据包通过的网关。星号 (\*) 表示数据包将直接发送到目标主机。
3. 第三列（Genmask 通子掩码）指示适用于此路由的子掩码。该掩码应用于 Destination 列中的值。
4. 第四列（Flags 标志）可以有多个值。最常见的标志有：
   - U: 路由已启动。此路由可用。
   - H: 目标是主机。这是到特定主机的静态路由（参见本章的“基于主机的静态路由”）。
   - Gateway: 将使用。
   - G: 使用网关。该数据包不会直接发送到目标主机，而将使用网关。
5. 第五列（Metric 跃）指示到目标的距离。某些路由守护进程用它动态计算到目标主机的最佳路由。
6. 第六列（Ref*）在 Linux 内核中不使用。在其他 UNIX 系统中，它指示此路由的引用次数。
7. 第七列（use）是内核对该路由执行查找的次数。
8. 第八列（iFace 接口）显示发往此路由的数据包通过的接口名称。

系统中至少有一个活动路由——本地回环路由（localhost），它在系统启动时自动设置。每个网络接口也至少有一条路由，指向该接口连接的网络。

`-n` 选项略微修改了显示。它不进行主机或网络名称查找，而是显示数字地址：

```
$ /bin/route -n
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use
```

## TCP/IP 与网络管理
CHAPTER 7 189

（注：后续重复的表格和说明已根据文档工程师原则去重处理，核心内容已与上文一致）

Tip: 如果使用 `route` 命令时挂住了，请按 `Ctrl+C` 中断。
