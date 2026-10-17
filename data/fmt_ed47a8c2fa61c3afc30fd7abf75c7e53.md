
那么为什么有人会在 Windows 网络上使用 Samba 呢？Samba 与 Linux 结合既快速又稳定，最重要的是，它是免费的。Windows NT 按用户收费，其十用户版本运行在较低的硬件上。仅在旧的 486 或低端 Pentium 上设置 Linux 和 Samba 是不够的。这对于运行一个小型的部门服务器来说绰绰有余，而 Windows NT 服务器则需要更好的计算机才能正常运行。

Samba 也是混合 UNIX 和 Windows 环境的良好选择。由于 Linux 包含了所有标准的 UNIX 网络工具，Linux 上的上的 Samba 可以与 UNIX 和 Windows 进行透明通信。

在完成对 Samba 的介绍后，下一章将介绍如何将 Samba 设置为文件服务器。

## 第 13 章

将 Samba 设置为 Windows NT 服务器

Linux 和 Samba 可以执行 Windows NT 服务器的许多功能。这种组合可以被设置为网络上的独立服务器，也可以作为现有网络的一部分。我们将设置一个 Linux 和 Samba 服务器，然后讨论使用 Linux 和 Samba 的优势和局限性。Windows NT。

### 13.1 将 Samba 设置为独立的 Windows NT 文件服务器

现在我们把把知识付诸实践。首先，我们将在新网络上将 Samba 设置为独立服务器。之后，我们将 Samba 服务器添加到现有网络中。

有一些 IP 地址是预留给私有网络的（不直接连接到互联网的网络）。见下表 13.1 的可在私有网络使用的地址列表。

表 13.1 私有 IP 网络的地址范围

| 类 | IP 地址 | 子网掩码 |
| --- | --- | --- |
| A | 10.X.X.X | 255.0.0.0 |
| B | 172.16.X.X | 255.255.0.0 |
| C | 192.168.X.X | 255.255.255.0 |

接下来，我们需要决定在工作站上使用固定 IP 地址还是动态 IP 地址。固定 IP 地址在每个站点单独设置。动态 IP 地址通过动态主机配置协议（DHCP）从服务器获取。由于在服务器上设置 IP 配置比在每个工作站上更容易，我们将使用 DHCP。然而，如果我们决定使用固定 IP 地址，那么设置 DHCP 就是没必要的。

### 13.1.1 设置 DHCP

在我们在服务器上安装 Linux 后，我们需要设置 DHCP。服务器的 IP 地址将是 10.0.0.2，子网掩码为 255.255.255.0。我们在 10.0.0.1 安装了一个路由器。路由器只是允许网络被划分为若干部分（子网）。DHCP 作为 DHCP 服务器由大多数 Linux 发行版提供安装。如果你的发行版没有带 DHCP，你可以从 Linuxberg http://www.linuxberg.net/ 下载。搜索 DHCP。关于 DHCP 的文档可以在 http://www.linuxdoc.org/doc/ip/howto/dhcp 获取。

安装 DHCP 后，必须创建并编辑配置文件 `/etc/dhcpd.conf`。此文件看起来非常像 `smb.conf`。它包含全局（global）、共享网络（shared network）和组部分。全局部分具有默认值。如果有必要，它可以被其他部分覆盖。注意所有行末尾都有一个分号（`;`）。

```
server identifier none
option subnet mask 255.255.255.0
option broadcast address 10.0.0.255
default lease time 86400
max lease time 259200;
```

有两个参数需要需要解释：`default-lease-time` 和 `max-lease-time`。通过 DHCP，服务器给出的 IP 地址在给定时间后过期。这防止了工作站和其他设备在不再使用地址后继续使用。`default-lease-time` 是设备保留 IP 的时间。在这种情况下，86400 秒等于一天（60 分 x 24 小时）。`max-lease-time` 是设备必须续约的时间。如果在这个时间之前没有续约，设备的 IP 地址将被禁用，且该 IP 可以分配给另一个设备。在这个示例中，`max-lease-time` 是三天（86400 秒 x 3）。

`subnet` 部分配置 DHCP 服务器。子网标识和网络掩码之后是选项：

```
subnet 10.0.0.0 netmask 255.255.255.0
{
  range 10.0.0.5 10.0.0.250;
  option netbios-name-servers 10.0.0.2;
  default lease time 86400
}
```

`range` 指定了用于 DHCP 租约的地址。我们包含了从 5 到 250 的地址。我们使用 251-254 用于服务器、路由器以及需要固定地址的设备的固定地址。在这种情况下，1 是路由器，2 是 Samba 服务器（10.0.0.1 和 10.0.0.2）。`netbios-name-servers` 参数指定 WINS 的 IP 地址。在这种情况下，我们使用 Samba 服务器（10.0.0.2）作为 WINS。

### 将 Samba 设置为独立的 Windows NT 服务器

`default-lease-time` 覆盖了全局部分的值。如果我们留空它，将使用全局值。

如果我们有多个子网，我们将使用 `shared network` 部分。在这个示例中，我们将使用两个子网：10.0.0.0 和 10.0.1.0。

```
shared network
{
  subnet 10.0.0.0 netmask 255.255.255.0
  range 10.0.0.0 10.0.0.250;
  option routers 10.0.0.1;
}
subnet 10.0.1.0 netmask 255.255.255.0
  range 10.0.1.1 10.0.1.250;
  option routers 10.0.1.1;
}
```

`shared network` 部分的选项划分为每个子网。子网中的选项与单个子网设置完全相同。在这种情况下，我们设置了路由器来连接子网，10.0.0.1 和 10.0.1.1。

`group` 部分用于出于特定原因分组。例如，你可以用它将 Windows 98 工作站与 Windows NT 工作站分开。由于我们的网络不需要这个，所以我们不使用 `group` 部分。

所以这就是 `dhcpd.conf` 文件：

```
server identifier none
option subnet mask 255.255.255.0
option broadcast address 10.0.0.255;
option lease time 86400;
max lease time 259200;
shared network
{
  subnet 10.0.0.0 netmask 255.255.255.0
  range 10.0.0.0 10.0.0.250;
  option routers 10.0.0.1;
}
subnet 10.0.1.0 netmask 255.255.255.0
  range 10.0.1.1 10.0.1.250;
  option routers 10.0.1.1;
}
```

接下来我们将设置 `smb.conf` 文件。我们将从默认文件开始并对其修改。以 `#` 开头的行是未使用的选项：

```
# 这是 Samba 的主配置文件。你应该阅读
# smb.conf(5) 手页以理解这里列出的选项。Samba 拥有大量的可配置选项（可能太多了！），其中大多数在示例中并未显示。
```

# 126 第 13 章 · 将 Samba 配置为 Windows NT 服务器
