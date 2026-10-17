
## 04 `dig` 实用工具

`dig` 允许你查看与主机相关的 DNS 信息。它的输出比 `host` 更详细。它显示了你所执行的查询的 DNS 服务器，并可以通过执行以下命令帮助你调试问题：

## 05 `$ dig mx`

尝试执行带有详情的 AXFR 查询：

```bash
$ dig 9.8.4 -rr 2005010-P1 << @ localhost.linuxux.com axfr
(2 servers)
; global: options
; Transfer failed.
```

AXFR 用于传输 DNS 数据记录，但它也可用于其他目的。DNS 管理员负责按照协议严格规范回答 AXFR 查询并将其发送到世界其他。

## 06 `/etc/resolv.conf`

查询 DNS 是通过查看 `/etc/resolv.conf` 文件配置的，在该文件中可以看到每个 `nameserver` 键对应的 IP 地址。在进行 DNS 服务器查询时会使用每个条目。通常，管理员在设置 Linux 机器时处理此文件；但如果你的 Linux 机器通过 DHCP 设置它，也是可能的：

## 技巧 | 窍门 | 黑科技 | 应用

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_39_0.png)

```bash
root@mail::/etc/bind cat named.conf.options
options            directory /var/cache/bind;
```

```bind
// 如果你和名称服务器之间有防火墙
// 阻止你通信，你可能需要修复防火墙以允许多个
// 端口通过；参见 http://www.isc.org/wiki/id000813
```

```bind
// 如果所有名称服务器使用 ISP 代理而不是 IP 地址
// 你必须将它们作为转发器（forwards）。
// 在以下块中，插入替换 all-proxy 占位符的地址。
```

```bind
forwarders {
    8.8.8.8;
};
```

```bind
// 如果出现关于密钥已签名的错误消息
// 你需要检查：https://www.isc.org/bind-keys
// validation-method:
```

## 06 `rndc` 实用工具

该目录是名称服务器工具。它通过 TCP 连接控制 `named` 进程的操作。`named` 有一个名为 `named.conf` 的配置文件。你可以输入 `man named-config` 和 `named.conf` 获取更多信息。

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_39_1.png)

```bind
auth-domain any; # 确认符合 RFC 1035
```

## 08 `/etc/bind/directory`

## 10 配置文件

所有与 `/etc/bind/directory` 相关的配置文件位于 `/etc/bind/directory` 内部。你需要 `root` 权限来进行更改，`bind` 将重新加载 `named` 进程以使更改生效。

默认配置几乎准备好支持你的 DNS 服务器。你只需要启用递归（`recursion`）然后允许所有区域。你可以通过在 `named.conf` 内部添加一行确保 `recursion yes;` 语句来实现这一点。

`BIND` 在 `/var/cache/` 中保留了一些其他文件

下一步是按照如下方式运行 `bind` 进程：

```bash
## /etc/init.d/bind start
```

## 07 其他类型的 DNS 服务器

有三种类型的 DNS 服务器：主（primary）、从（secondary）和转发（forwarder）。主 DNS 服务器（primary）是该区域的。

主 DNS 服务器（primary）负责该区域的邮件投递。

从 DNS 服务器（secondary）在主服务器故障时从主服务器复制记录。

转发 DNS 服务器（forwarder）代表客户端查询 DNS 服务器。问题是它不执行递归查询；它将其转发到另一个 DNS 服务器，接收响应并然后缓存结果。

无法发现查询结果是否是从区域主或从服务器回答的。

```text
+ - -1 - /var/cache/bind/
total = -
-r-- - 1 bind 698 Oct 15 09:44
managed-keys.bind
-r-- - 1 bind 512 Oct 15 09:44
named-master.key.bind
```

## 09 `/etc/bind/directory`

下一步是按照如下方式运行 `bind` 进程：

```bash
## /etc/init.d/bind
```

# 11 缓存服务器

缓存 DNS 服务器不包含域名信息；它只包含基于其已执行的 DNS 查询结果的信息。缓存之所以有效，是因为 DNS 数据不会频繁变化。

# 编写客户端-服务器应用程序

每个操作系统都有自己的一套网络 API。

现代计算机网络由多个协议组成。手动创建格式良好的数据包几乎是不可能的 —— 协议栈及其底层网络硬件会影响其形式。

Unix 上的工程师通过引入一个抽象层解决了这个问题——即所谓的套接字（sockets），作为两个或多个应用程序之间的端点。开发者使用标准接口向服务器发送命令，这些命令会被翻译到网络中。

在处理套接字时，对网络有基本的理解是有益的。目前，只需定义消息可以通过高层协议传输即可。

`TCP` - 传输控制协议在数据成功送达时提供确认。这是通过通信过程中的一些开销实现的。然而，某些应用程序需要这种特性。`UDP` 提供了一种不保证交付的无连接通信。在网络上，计算机通过其 IP 地址识别。单个服务通过其端口号识别——将它们想象成高层大楼中的门。

通信软件的开发者发现自己陷入了鸡生蛋的策略困境 —— 如果没有编写服务器，客户端就无法连接。相反，缺乏客户端意味着服务器无法启动。

在实际项目中，你应该从创建一个客户端和服务器将交换的消息的粗略草模型开始。你不需要在第一次尝试就达到 100% 的完善；大多数协议会在实现过程中发生变化。
