

# 218

# 第 15 章.TCP Wrappers 与 xinetd

- /usr/share/tcp-wrappers-<version>/ — 包含一个 README 文件，讨论了 TCP wrappers 以及存在的主机地址欺骗风险。

- /usr/share/doc/xinetd-<version>/ — 包含一个 README 文件，讨论了访问控制的方面，以及一个 sample.conf 文件，该文件提供了用于修改 /etc/xinetd/ 目录下特定服务配置的各种思路。

- man 5 hosts_access — TCP wrappers 主机访问控制文件的帮助页。

- man hosts_options — TCP wrappers 选项字段的帮助页。

- man xinetd.conf — 列出 xinetd 配置选项的页面。

- man xinetd — xinetd 超服务守护进程的帮助页。

## 15.5.2. 有用的网站

- http://www.xinetd.org — xinetd 的官网，包含示例配置文件、功能完整列表以及详尽的 FAQ。

- http://www.macsecurity.org/resources/xinetd/tutorial.shiml — 一份详尽的教程，讨论了许多调整 xinetd 配置文件以满足特定安全目标的方法。

## 15.5.3. 相关书籍

- Red Hat Linux Security Guide ; Red Hat, Inc. — 提供了工作站、服务器和网络安全的概述，并针对 TCP wrappers 和 xinetd 提供了具体建议。

- Hacking Linux Exposed by Brian Hatch, James Lee, and George Kurtz; Osbourne/McGraw-Hill — 一本优秀的安全资源，包含关于 TCP wrappers 和 xinetd 的信息。

# 第 16 章. iptables

Red Hat Linux 安装了高级的网络数据包过滤工具——该过程是在网络数据包进入和离开内核网络协议栈时对其进行控制。2.4 之前的内核依赖于 ipchains 进行数据包过滤，并使用规则列表在过滤过程的每个步骤将其应用到数据包上。2.4 内核引入了 iptables（也称为 netfilter），它与 ipchains 类似，但极大地扩展了网络数据包过滤的范围和控制能力。

本章将重点介绍数据包过滤的基础，定义 ipchains 和 iptables 之间的区别，解释 iptables 命令中提供的各种选项，以及如何通过系统重启保留过滤规则。

有关构建 iptables 规则或基于这些规则设置防火墙的说明，请参考第 16.5 节附加资源。

> 警告
2.4 内核的默认防火墙机制是 iptables，但如果 ipchains 已经在运行，则无法使用 iptables。如果启动时存在 ipchains，内核将发出错误并无法启动 iptables。

ipchains的功能不受这些错误的影响。

## 16.1. 数据包过滤

流量以数据包的形式在网络中移动。网络数据包是特定大小和格式的数据集合。为了在网络上传输文件，发送计算机必须首先根据网络协议的规则将文件拆分为数据包。每个数据包都持有文件数据的一小部分。接收传输后，目标计算机会将数据包重新组组成文件。

- filter — 处理网络数据包的默认表。
- nat — 用于修改创建新连接的数据包。
- mangle — 用于特定类型的数据包修改。

这些表中的每个表都有组内置链（chains），对应于 netfilter 对数据包执行的操作。
filter 表的内置链如下：

- INPUT — 应用于目标为本机的网络数据包。
- OUTPUT — 应用于本地生成的网络数据包。
- FORWARD — 应用于通过主机的路由网络数据包。

nat 表的内置链如下：

- PRERUTING — 在网络数据包到达之前修改。
- OUTPUT — 在发送之前修改本地生成的网络数据包。
- POSTROUTING — 在发送出去之前修改网络数据包。

mangle 表的内置链如下：

- INPUT — 修改目标为本机的数据包。
- OUTPUT — 在发送之前修改本地生成的网络数据包。
- FORWARD — 修改通过主机的路由网络数据包。
- PREROUTING — 在路由之前修改传入的网络数据包。
- POSTROUTING — 在发送出去之前修改网络数据包。

由 Linux 系统交付或发送的每个网络数据包至少都会接受一个表的处理。
在链结束之前，数据包可能会在每个表内针对多个规则进行检查。规则的结构和目的可能有所不同，但它们通常试图使用特定的协议和网络服务，识别来自或发往特定 IP 地址或一组地址的数据包。

无论目的地何，数据包都会匹配其中一个表中的某条规则，并对其应用目标（target）或操作（action）。如果规则为匹配指定了 ACCEPT 目标，则数据包将跳过剩余检查并允许继续到达目的地。如果规则指定了 DROP 目标，则拒绝该数据包访问系统并返回给发送数据包的主机。如果规则指定了 QUEUE 目标，数据包将传递到用户空间。如果规则指定了可选的 REJECT 目标，数据包将被丢弃，但会向数据包源者发送一个错误包。

每条链都有一个默认策略：ACCEPT、DROP、REJECT 或 QUEUE。如果链中没有规则适用于该数据包，则执行该策略。

## 16.2. ipchains 和 iptables 的区别

从初看，ipchains 和 iptables 看起来很相似。然而，iptables 提供了更大的控制能力。具体来说，ipchains 的用户应该注意以下区别：

在 ipchains 中，规则的顺序并不重要，而 iptables 允许管理员在处理数据包方面具有更大的灵活性。在 ipchains 中，目标选项是有限的，但 iptables 提供了更广泛的操作范围。

## 16.3. iptables 中的选项

### 16.3.1. 表

iptables 的一个强大方面是可以使用多个表来决定数据包的命运。这些表可以创建并存储在 /lib/modules/<kernel-version>/kernel/ipv4/netfilter/ 目录下，其中 <kernel-version> 对应内核版本。

默认表 filter 包含内置的 INPUT、OUTPUT 和 FORWARD 链。这与 ipchains 中使用的标准链相似。但默认情况下，iptables 还包含两个执行特定数据包过滤任务的额外表。nat 表可修改数据包中涉及的源地址和目的地址，mangle 表则以特殊方式修改数据包。

### 16.3.2. 结构

许多 iptables 命令具有以下结构：

```
iptables [-t <table-name>] <command> <chain-name> <parameter-1> <option-1> <parameter-n> <option-n>
```

在此示例中，<table-name> 选项允许用户选择默认 filter 表以外的表来配合命令使用。<command> 选项规定要执行的特定操作，例如添加或删除由 <chain-name> 选项指定的规则。在 <chain-name> 之后是参数和选项的对，定义了当数据包匹配规则时将发生什么。

