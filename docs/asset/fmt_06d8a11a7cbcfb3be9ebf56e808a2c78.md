
```
$ apachectl start
```

有关启动脚本的更多信息，请参见第 3 章。

## 分析日志文件

当你的网站投入运行后，你可能想要收集有关网站使用的统计数据，例如每个页面请求数、每天平均请求数、失败请求百分比以及数据传输量。确保你使用的是“combined”日志格式，`CustomLog`指令末尾是 `combined` 而不是 `common`。`combined`日志格式包含每个请求的引用页（链接到 URL 的页面）和用户代理（客户端浏览器和操作系统）。

你的访问日志和错误日志出现在 Apache 的日志目录中。这些文件是可以读的，但它们包含大量信息，你确实需要一个单独的分析程序从从中提取有用数据。市面上有数百种不同的日志分析工具，免费的都有。

两个值得关注的免费分析工具是 Analog (`analog.cx`) 和 AWStats (`awstats.sourceforge.net`)。它们提供了相当基础的功能。

如果你正在寻找有关网站流量使用模式的信息，请查看 `analytics.google.com` 的 Google Analytics。该服务要求你在想要跟踪的网页上放置一段短代码，但它随后会免费提供所有数据收集和分析基础设施。

## 为静态内容的高性能托管进行优化

托管社区在过去几年中学了，创建高性能托管平台的方法是对某些服务器的静态内容进行优化。

解决这一需求的方法之一是使用内核 Web 服务器或内核页面缓存。由于这些系统在返回请求者之前不会将数据复制到用户空间，它们获得了一些性能提升。然而，由于解决方案在内核空间运行，它们意味着了一些额外的安全风险。我们建议极其谨慎地使用它们。

内核的 Web 服务器 `TUX` 在某些 Linux 发行版中与 Apache 等传统的 Web 服务器配合运行。在可能的情况下，`TUX` 在不离开内核空间的情况下提供静态页面，例如 `rpc.nsfd` 文件。尽管 `TUX` 是由 Red Hat 开发的（Red Hat 现在将其称为 Red Hot Content Accelerator），但它是根据 GPL 发布的，可以与其他 Linux 发行版一起使用。遗憾的是配置 `TUX` 可能是一个挑战。该系统在 2000 年初非常流行，但现在人气已经下降。详情，请参见 `redhat.com/docs/manual/tus`

在 Solaris 平台上，Sun 发布了 Solaris Network Cache (`NCA`) 来提供内核级。

### 23.3 虚拟接口

在早期，一台机器通常作为服务器。随着 Web 的流行，虚拟接口诞生了。这个想法很简单：一台机器响应比其物理接口更多的 IP 地址。因此，一台机器可以为数百个网站。

![](img/9b33263d3e7e36cd43da7756018c8735_1015_0.png)

## 使用基于名的虚拟主机

`HTTP 1.1` 协议定义了一种虚拟接口的功能（正式称为“基于名的虚拟主机”），它消除了为 Web 服务器分配唯一 IP 地址的需求。这种方法保留了 IP 地址并对某些网站（特别是大学）很有用。

遗憾的是，该方案对于商业网站并不实用（移动站点时必须更改 IP 地址）并且可能对安全产生负面影响（如果你根据 IP 访问站点）。此外，基于名的虚拟主机需要浏览器支持使用 SSL。由于基于名的虚拟主机的这些限制，虚拟接口似乎还将存在一段时间。

## 配置虚拟接口

设置虚拟接口涉及两个步骤。首先，要在 TCP/IP 级别创建虚拟接口。具体方法取决于你的 UNIX 版本。其次，你需要告诉 Apache 服务器你安装的虚拟接口。我们从第 971 页开始介绍第二个步骤。

### Linux 虚拟接口

Linux 虚拟接口使用 `接口:实例` 命名。例如，如果你的接口是 `eth0`，与其关联的虚拟可以是 `eth0:0`、`eth0:1` 等。所有接口都通过 `ifconfig` 命令配置。

```
$ sudo ifconfig eth0:0 128.138.243.150 netmask 255.255.255.192
```

配置 `eth0:0` 并分配一个 `128.138.243.128/26` 网络的地址。

# Solaris 虚拟接口

要在 Red Hat 上使虚拟地址分配变为永久性，你需要在 `/etc/sysconfig/network-scripts` 中为每个虚拟接口创建一个单独的文件。例如，对应上述 `ifconfig` 命令的 `ifcfg-eth0:0` 包含以下行：

```
DEVICE=eth0:0

IPADDR=128.138.243.150

NETMASK=255.255.255.192

NETWORK=128.138.243.128

BROADCAST=128.138.243.191

ONBOOT=yes
```

Ubuntu 的处理方法与 Red Hat 类似，但接口定义必须出现在 `/etc/network/interfaces` 文件中。示例中与 `eth0:0` 接口对应的条目位于：

```
eth0:0 inet static
address 128.138.243.150
netmask 255.255.255.192
broadcast 128.138.243.191
```

在 SUSE 系统上，你可以通过 YaST 创建虚拟接口（“别名”），或手动创建接口文件。要使用 YaST 完成，首先在“网络设置”的“全局选项”选项卡上选择“使用 ifup 的传统方法”。

在 ANSI 下，接口的 IP 地址都配置在一个文件中。要手动配置这些文件，请查看 `/etc/sysconfig/network` 中名称以 `ifcfg-name` 开头的文件。

例如，在配置中添加这些行来定义两个虚拟接口：

```
IPADDR_1=128.138.243.149
NETMASK_1=255.255.255.192
STARTMODE_1="auto"
LABEL_1="auto"
IPADDR_2=128.138.243.150
NETMASK_2=255.255.255.192
STARTMODE_2="auto"
LABEL_2=1
```

`IPADDR` 和 `NETMASK` 之后的后缀（此处为 `_1` 和 `_2`）不一定是数字，但为了一致性，这是一个合理的约定。注意，你还需要编辑 `/etc/sysconfig/network/config` 并设置 `NETWORKMANAGER="no"`，以便虚拟接口能够被识别。

# Solaris 虚拟接口

Solaris 通过物理接口和逻辑单元的概念支持虚拟接口（又称为“次级接口”）。例如，如果 `hme0` 是物理接口的名称，那么 `hme0:1`、`hme0:2` 等就是对应虚拟接口的名称。默认情况下，每个物理接口可以挂载最多 256 个虚拟身份。如果你需要更改此限制，请使用 `ndd` 更改参数 `ip_addrs_per_if`（使用 `ndd` 的详情请参见第 498 页）。

要配置虚拟接口，只需在一个虚拟名称上运行 `ifconfig`。（底层物理接口可能已经“接通”（plumbed）。在大多数情况下，你可能希望设置系统，使得虚拟接口的 `ifconfigs` 在启动时完成。

这是一个示例，其中 Solaris 机器在内部虚拟专用网络 (VPN) 的地址空间内有一个地址，在互联网上有一个外部地址，两者都关联同一个物理接口 `hme0`。为了让这些接口在启动时自动配置，管理员可能有两个主机文件：`/etc/hostname.hme0` 和 `/etc/hostname.hme0:1`。

```
$ ls -l /etc/hosts/*
-rw-r--r-- 1 root 10 Nov 4 10:19 /etc/hostname.hme0
-rw-r--r-- 1 root 16 Dec 21 19:34 /etc/hostname.hme0:1
```

主机文件可以包含来自 `/etc/hosts` 文件的主机名，也可以包含 IP 地址。在这种情况下，管理员各用了一个一个：

```
$ cat /etc/hostname.hme0
overkill
$ cat /etc/hostname.hme0:1
206.0.1.133
$ grep overkill /etc/hosts
10.1.2.9 overkill over overkill.domain
```

在启动时，地址会自动配置（带有环回地址，我们在显示的输出中省略了它）：

```
$ ifconfig -a
hme0: flags=863<UP,BROCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 10.1.2.9 netmask ffffffe0 broadcast 10.1.2.255
hme0:1: flags=863<UP,BROCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 206.0.1.133 netmask ffffffe0 broadcast 206.0.1.255
```
