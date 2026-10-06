
# 2. 循环缓冲区 (Cyclic buffers)

`cycbuff:ONE:/export/cycbuffs/one:512000`

`cycbuff:TWO:/export/cycbuffs/two:512000`

`cycbuff:THREE:/export/cycbuffs/three:512000`

# 2. 元循环缓冲区 (Metacyclic buffers)

`metacyclicbuff:BIGAREA:ONE,TWO`

`metacyclicbuff:SMALLAREA:THREE`

在 `cycbuff.conf` 文件中，所有循环缓冲区（`cycbuff`）条目应该出现在元循环缓冲区（`metacyclicbuff`）之前。`cycbuff` 条目的第二个字段标识缓冲区的名称。例如，这三个缓冲区条目分别命名为 `ONE`、`TWO` 和 `THREE`。（每个缓冲区名称随后会被分配给元循环缓冲区）。每个 `cycbuff` 条目的第三字段是标识缓冲区文件路径的文件名。最后一个字段是以 KB 为单位的缓冲区大小（1K 等于 1024 字节）。

在元循环条目中，第二个字段包含元循环缓冲区的符号名称（用于 `storage.conf` 文件中的 `options` 条目）。每个条目的第三字段将 `cycbuff` 条目分配给每个元循环类别（class）。

你还可以向此文件添加可选条目，如下所示，这些会影响缓冲策略：

- `cycbuffupdate`：反映两次头部更新之间存储了多少文章。默认值为 25。

## 第 22 章：设置新闻服务器 877

- `refreshinterval`：反映读取 `cycbuff` 头部到再次读取之间之间的秒数。默认值为 30。

## 为 cnfs 存储创建缓冲区

你可以使用 `dd` 命令创建一个存在于普通文件系统之上的大文件。现有新闻是 `dd` 命令创建缓冲区文件的示例：

```
dd if=/dev/zero of=/var/spool/news/articles/cycbuff bs=12k count=N
```

在此示例中，`N` 将被替换为你所需的缓冲区大小除以 32。必须为你创建的缓冲区文件分配用户和新闻组所有权。权限模式应为 0664 或 0660。例如：

```
$ chown news /var/spool/news/articles/cycbuff
$ chgrp /var/spool/news/articles/cycbuff
$ chmod 0664 /var/spool/news/articles/cycbuff
```

## 设置过期时间

新闻文章的过期时间设置在 `/etc/news/expire.ctl` 文件中。该文件中的现有条目可以作为默认过期时间。通过 `remember` 条目，文章（即使已过期）也会被保留 10 天。这样一来，如果文章从 `expire.ctl` 提供：你就可以接受它。以下是包含在内的 `remember` 条目：

```
/remember:/10
```

如果你想让 `Expires:` 头部生效，请在你的 `expire.ctl` 文件保留以下条目：

```
*A:1:10:never
```

有些组适合永久保留。`expire.ctl` 中的这些行会让所有位于 `.answers` 中的新闻组以及所有以 `news.announce:` 开头的新闻组保留更久：

```
*answers:M:1:35:90
news.announce:.*M:1:35:90
```

`expire.ctl` 文件中的条目存在三种不同的格式。第一种格式由首先所示的 `/remember` 条目表示。下一种是用于定义与 `storage.conf` 文件中设置的类别相关的过期时间的条目。第三种格式包含五个用冒号分隔的字段，用于为特定组分配过期时间。以下是后两种格式的示例：

```
classnumber:keep:default:purge
newsgroups:modflag:keep:default:purge
```

以下是所有字段的说明：

- `classnumber`。一个数字（0、1 等），对应于 `storage.conf` 文件中标识的类别。
- `newsgroups`。第一个字段指定哪些新闻组被分配到此过期规则。与 usual一样，你可以使用通配符来匹配新闻组。（详情请参阅“理解通配符”侧边栏）。
- `modflag`。你可以使用该字段中的值进一步限制匹配的组。该字段应包含以下内容之一：`M`（仅限审核组）、`U`（仅限未审核组）、`A`（所有组）、`X`（移除组）。
- `keep`。此字段指定了应保留文章的天数。
- `default`。此字段指定在没有其他规则匹配时的过期时间。
- `purge`。此字段指定文章过期时执行的操作。

## 允许用户访问你的服务器

当 INN 服务交付时，你的服务器将允许来自本地计算机的访问。为了实现这一点，`/etc/news/readers.conf` 的内容如下：

```
auth "localhost" {
  hosts: "localhost, 127.0.0.1, stdin"
  default: "<localhost>"
}access "localhost" {
  newsgroups: "*"
  access: RPA
}
```

在上述行中，`auth` 定义了来自不同接口的本地读取器身份。赋予所有新闻组的用户权限包括读取、发布以及向审核组发布。

## 启动新闻服务

在 INN 服务配置完成后，可以通过启动 `innd` 脚本来开启它。要立即启动脚本，你可以输入以下命令（作为 root 用户）：

```
/etc/init.d/innd start
```

如果 INN 服务启动正常，可以通过输入以下命令设置系统每次启动时都启动 INN 服务（作为 root 用户）：

```
chconfig innd on
```

## 检查新闻日志文件

您的新闻服务器活动被记录在 `/var/log/news` 目录的文件中。根据 `/etc/syslog.conf` 文件中的以下设置进行记录：

```
# INN
#
news.crit          /var/log/news/news.crit
news.err           /var/log/news/news.err
news.notice        /var/log/news/news.notice
```

在此示例中，严重错误存储在 `news.crit` 文件中，非严重错误存储在 `news.err` 文件中，反映正常活动的消息记录在 `news.notice` 文件中。你应该定期检查这些文件以发现错误情况。

## 总结

建立新闻服务器是一项非常复杂的任务，对于只有少数用户需要访问新闻的大多数组织来说，应该避免这样做。（在这种情况下，如果可能，请访问您 ISP 的服务器。）但是，如果你决定要自己构建一个新闻服务器，InterNetNews (INN) 软件包随 Red Hat Linux 备箱即用。如果你是新闻服务器管理员，对你来说最重要的配置文件是 `inn.conf` 文件（位于 `/etc/news` 目录）。许多基础 INN 选项都在该文件中设置。你还需要配置从哪些主机获取新闻推送，以及哪些主机向你的用户分发文章。

# 第 23 章

## 设置启动服务器：DHCP 和 NIS

### 本章内容

- 使用动态主机配置协议 (DHCP)
- 设置 DHCP 服务器
- 设置 DHCP 客户端
- 使用网络信息服务 (NIS)
- 将 Red Hat Linux 设置为 NIS 客户端
- 将 Red Hat Linux 设置为 NIS 主服务器
- 将 Red Hat Linux 设置为 NIS 备用服务器

如果你的业务、组织或家庭网络超过几台计算机，单独管理每台计算机可能会很困难。移动你的网络域名服务器可能会导致你必须更改网络上每台计算机的配置文件。组织中的新成员可能意味着要在多台计算机上添加新用户帐户。

Red Hat Linux 提供了几种机制来集中配置和分配与您的网络、服务器以及使用您的计算资源的人相关的关键信息。`DHCP` 提供了一种为本地网络上的计算机动态配置 IP 地址、网络号和服务器位置的方法。`NIS` 提供了一种向网络上的其他 Linux 和 UNIX 系统分发各种配置文件（包含用户帐户、密码和网络地址等信息）的方法。

本章描述了如何将 Red Hat Linux 设置为 DHCP 或 NIS 服务器。然后描述了如何检查这些服务是否正常工作，并介绍了如何设置客户端计算机使用这些服务。

## 使用动态主机配置协议

设置动态主机配置协议 (DHCP) 服务器允许你集中管理私有网络上客户端计算机的地址和其他网络信息。在你的网络上配置了 DHCP 后，客户端计算机只需指示它想要使用 DHCP，DHCP 服务器即可提供其 IP 地址、子网掩码、DNS 服务器、NetBIOS 服务器、路由器（网关）以及在网络上启动运行所需的其他信息。

通过 DHCP，你可以极大地简化网络上每台客户端计算机需要进行的初始网络配置。以后，随着网络的演变，你可以轻松地更新这些信息，客户端在重启网络接口时会自动捕获这些更改。

假设你已经设置了 DHCP 服务器与网络上客户端计算机之间的物理连接（推是以太网局域网），让 DHCP 服务器运行的最少需要是：

- 一个配置好的 `/etc/dhcpcd.conf` 文件
- 一个正在运行的 `dhcpcd` 守护进程（可以在启动时启动）

DHCP 服务器运行后，它会向局域网广播其作为 DHCP 服务器的可用性。客户端只需启动（打开以太网网络接口且 DHCP 识别其获取网络地址的方法），在网络上运行所需的信息将从服务器传输给它。

以下章节描述了如何设置你的 `/etc/dhcpcd.conf` 文件、启动 DHCP 服务器以及配置 DHCP 客户端。

## 设置 DHCP 服务器

在 Red Hat Linux 中配置 DHCP 服务器主要由设置 `/etc/dhcpcd.conf` 文件组成。以下章节描述了如何配置你的 `dhcpcd.conf` 文件。

> 注意：`dhcpcd.conf` 文件允许具有极大的灵活性。要查看可以在该文件中设置的完整选项和参数，请参考 `dhcp-options` 和 `dhcpcd.conf` 的 man 页面（输入 `man dhcpcd-options`）。

### 配置 dhcpcd.conf 文件

假设你有一个 IP 地址池，想要将其分发给一组位于同一子网的计算机。换句话说，所有计算机都连接到一个集线器（或一组链串联的集线器）。这里是一个你可以从这里开始的简单 `dhcpcd.conf` 文件示例：

```
# 一个简单的 /etc/dhcpcd.conf 文件。
default-lease-time 720;
max-lease-time 86400;
option subnet-mask 255.0.0.0;
```

```
option broadcast-address 10.255.255.255;
option routers 10.0.0.254;
option domain-name example.com;
range 10.0.0.10-10.0.0.100;
```

在前面的示例中，租约时间为 720 秒，最大租约时间为 86400 秒。子网掩码是 255.0.0.0。广播地址是 10.255.255.255。路由器是 10.0.0.254。域名是 example.com。范围是 10.0.0.10-10.0.0.100。

DHCP 服务器将向范围内的客户端分配地址。

后续章节描述了如何设置你的 `/etc/dhcpcd.conf` 文件、启动 DHCP 服务器并配置 DHCP 客户端。

### 扩展 dhcpcd.conf 文件

你可以向 `dhcpcd.conf` 文件添加更多选项以向客户端提供更多信息。以下是你可能使用的选项示例：

- 如果你有多个 DNS 服务器，可以在 `domain-name-servers` 选项中列出它们：
`option domain-name-servers 10.0.0.1, 10.0.0.2;`

- 如果你有 WINS 服务器，可以使用 `netbios-servers` 选项：
`option netbios-servers 10.0.0.3;`

- 如果你有时间服务器，可以使用 `time-servers` 选项：
`option time-servers 10.0.0.4;`

- 如果你有多个路由器，你也可以列出它们：
`option routers 10.0.0.254, 10.0.0.253;`

- 如果你想指定默认域名，可以使用 `domain-name` 选项：
`option domain-name example.com;`

这是一个包含其中一些选项的 `dhcpcd.conf` 文件示例：

```
subnet 10.0.0.0 mask 255.255.255.0 {
  range 10.0.0.10-10.0.0.100;
  option routers 10.0.0.254;
  option domain-name-servers 10.0.0.1, 10.0.0.2;
  option netbios-servers 10.0.0.3;
  option time-servers 10.0.0.4;
  option domain-name example.com;
}
```

你还可以为不同的子网定义不同的选项。例如，如果你的网络上有两个不同的子网，你可以这样做：

```
subnet 10.0.0.0 mask 255.255.255.0 {
  range 10.0.0.10-10.0.0.100;
  option routers 10.0.0.254;
  option domain-name example.com;
}
subnet 192.168.1.0 mask 255.255.255.0 {
  range 192.168.1.10-192.168.1.100;
  option routers 192.168.1.254;
}
```
