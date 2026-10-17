
### 选项

| `coresize size;` | 如果 `named` 崩溃，Linux 将生成 `coredump`（核心转储），即程序崩溃瞬间内存使用的映像。数据可用于程序员进行“事后”分析。注意：此映像可能相当大；如果你 DNS 系统的磁盘空间不足，请考虑限制核心文件大小。Linux 下的默认值为无限制。`size` 参数可以指定为字节（无后缀）、K、MB 或 GB。例如，以下所有值均为 1 GB：`coresize 1073741824`；`coresize 1048576K`；`coresize 1024M`；以及 `coresize 1G`。 |

| `datasize datasize;` | 指定分配给 `named` 的内存。Linux 下的默认值 = 你拥有的内存量。`datasize` 值遵循与 `coresize` 中 `size` 值相同的约定。因此 `1073741824` 等同于 `1048576K`，等同于 `1024M`，等同于 `1G`。 |

| `files number;` | `named` 可以同时打开的最大文件数。注意：BIND 同时打开的文件越多，其性能受处理所有这些文件句柄的影响越大。（C 程序员因为 `select` 系统调用而对这个问题很熟悉。） |

| `stacksize number;` | `named` 可以从系统栈中分配的最大内存量（用于跟踪程序中的临时变量）。Linux 下的默认值为无限制。对于 `number`，遵循与 `coresize` 和 `datasize` 相同的约定。 |

| `cleaning-interval number;` | 指定服务器从缓存中删除过期记录之间的间隔。默认为每 60 分钟。如果设置为 0，则不会进行定期清理。 |

| `interface-interval number;` | 默认情况下，服务器每 60 分钟扫描一次系统上的接口列表。如果启用了 `listen-on`（在本表中前面定义），`named` 将开始在它发现的任何新接口上监听 DNS 请求。如果接口消失，`named` 将停止监听该接口上的请求。如果将此选项设置为 0，服务器仅在 `named` 启动时检查可用接口。 |

| `statistics-interval number;` | 指定 `named` 服务器生成服务器统计信息并将其记录到日志文件的频率。默认为每 60 分钟。如果设置为 0，则不生成统计信息。 |

| `topology { address-list };` | 当存在多个转发器时，`named` 倾向于假设比其他服务器更近的服务器。默认情况下，`named` 服务器优先选择自身，然后选择同一子网上的服务器。你可以指定另一种优先顺序（`address-list` 的顺序）。你也可以嵌入表示地址组的子列表。例如，在此配置中，`topology { \ 192.168.3.12; \ { 192.168.11.25; 192.168.42/24; } \ 192.168.8.24; \};` 首选 192.168.3.12，对 192.168.11.25 和 192.168.42.0 网络上的所有主机给予同等偏好，最后偏好 192.168.8.24。 |

# 服务器语句

`server` 语句告诉 BIND 关于它可能与之交互的其他名称服务器的特定信息。`server` 语句的格式如下：

```
server ip-address {
    bogus yes/no;
    transfer-format one-answer/many-answers;
};
```

其中 `ip-address` 是相应服务器的 IP 地址。

语句中的第一项 `bogus` 告诉服务器另一个服务器是否正在发送错误信息。当处理可能因配置错误而发送错误信息的另一个站点时，这非常有用。默认值为 "no"。第二项 `transfer-format` 告诉 BIND 该服务器是否可以在单次查询响应中接受多个答案，或者每个答案是否应单独发送。`many-answers` 选项效率高得多，但通常只有运行 BIND 版本 8.x 或更高版本的服务器才能处理此模式。

一个示例 `server` 条目可能如下所示：

```
server 192.168.3.12 {
    bogus no;
    transfer-format many-answers;
};
```

## 区域

`zone` 语句允许你定义一个 DNS 区域，其定义常被混淆。以下是详细说明：`DNS 区域与 DNS 域不是同一回事`。这个区别很微妙，但很重要。

让我们回顾一下：域沿组织边界指定。单个组织可以划分为较小的管理子域。每个子域都有自己的 `zone`。所有区域共同构成整个域。

例如，`bigcompany.com` 是一个域。在其内部有子域 `.engr.bigcompany.com`、`.marketing.bigcompany.com`、`.sales.bigcompany.com` 和 `.admin.bigcompany.com`。这四个子域中的每一个都有自己的 `zone`。并且 `bigcompany.com` 内部有一些主机不属于任何子域；因此它有自己的 `zone`。结果，`bigcompany.com` 实际上由五个 `zones` 组成。

在最简单的模型中，单个域没有子域，`zone` 和 `domain` 的定义在有关主机、配置等方面的信息上是相同的。在 `named.conf` 文件中设置区域的过程在下文中讨论。

![](img/ec2066d370d3af1a767664d36aa7ddfe_343_0.png)

## 配置服务器

是时候来点 `大乐趣` 了：配置名称服务器！哦，你不觉得有趣？好吧，等你了解到人们因知道这些知识而获得多少报酬时再看看吧。

前面，你学习了主要、从属和缓存名称服务器之间的区别。简而言之，主要名称服务器包含具有区域最新 DNS 信息的数据库。当区域管理员想要更新这些数据库时，主要名称服务器

主服务器最先获取更新，世界上的其他设备则向它请求更新。从服务器明确跟踪主服务器，而主服务器在发生变更时通知从服务器。主服务器和从服务器在回答中都被视为同等权威。缓存名称服务器没有权威记录——只有缓存条目。

## 为主区域更新 named.conf 文件

区域条目的最基本语法如下：

```
zone domain-name (
    type master;
    file path-name;
);
```

`path-name` 指的是包含相关区域数据库信息的文件。例如，要为 `example.org` 域创建一个区域，其数据库文件位于 `/var/named/example.org.db`，则使用以下配置：

```
zone "example.org" {
    type master;
    file "example.org.db";
};
```

注意，`named.conf` 文件中 `directory` 选项的值会自动为 `example.org.db` 文件名添加前缀。因此，如果我们指定 `directory` 为 `/var/named`，服务器软件将自动在 `/var/named/example.org.db` 中查找 `example.org` 的信息。

这只是前向解析，即他人查找名称并获取 IP 地址的机制。提供用于 IP 到主机名映射的逆向解析也是正确的网络行为（如果你想向某些站点发送电子邮件，这也是必要的！）。为此，你需要在 `in-addr.arpa` 域中提供一个条目。

正如我们在前面的讨论中提到的，`in-addr.arpa` 条目的格式是你 IP 地址的前三个八位组反转，后跟 `in-addr.arpa`。假设 `example.org` 的网络地址是 `192.168.1`，那么 `in-addr.arpa` 域将是 `1.168.192.in-addr.arpa`。因此，`named.conf` 文件中的区域声明如下：

```
zone "1.168.192.in-addr.arpa" {
    type master;
    file "example.org.rev";
};
```

![](img/ec2066d370d3af1a767664d36aa7ddfe_345_0.png)

此示例假设你正在为包含 255 个 IP 地址的整个 C 类块进行逆向解析。对更大或不同大小的网络块进行逆向映射是可能的，但比我们要涵盖的内容更复杂。BIND 文档和对子网掩码的透彻理解应在你遇到这种情况时提供你所需的信息。

既然你的 `named.conf` 条目已准备就绪，现在是时候实际编写 `example.org.db` 和 `example.org.rev` 文件了。

## 附加选项

主区域也可以从 `options` 语句中使用一些配置选项。这些选项包括

- `check-names`
- `allow-update`
- `allow-query`
- `allow-transfer`
- `notify`
- `also-notify`

在区域配置中使用这些选项中的任何一个将只影响该区域。有关这些选项工作原理的更多信息，请参阅本模块前面关于 `named.conf` 讨论中的“配置选项”小节。
