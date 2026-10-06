
| | `htcp_port` | Squid 用于从兄弟服务器或代理服务器的缓存中提取内容的端口。默认值为 4287。 |

| 邻居选择算法 | `cache_peer` | 用于建立缓存分级。语法为 `cache_peer host type port icp_port` 选项。例如，如果我想将 fs2 配置为兄弟节点，我会使用 `cache_peer fs2 sibling 3128 3130`。如果我想将 fs2 配置为父节点，我会输入 `cache_peer fs2 parent 3128 3130`。 |

| 缓存大小 | `cache_mem` | 指定用于处理存储在磁盘缓存中的对象的 RAM 数量（字节字节）。默认为 8MB。 |

| | `cache_swap_low` and `cache_swap_high` | 指定磁盘缓存使用的低水位和高水位（百分比）。当达到 `cache_swap_low` 时，Squid 将开始从缓存中转出旧文件。当达到 `cache_swap_high` 数值时，Squid 将真正开始大量清理缓存中的旧内容。默认值：`cache_swap_low: 90` `cache_swap_high: 95` |

| | `maximum_object_size` | 指定存储在磁盘缓存中的文件最大大小（KB）。任何大于此的文件都不会被保存。默认值为 4096KB。 |

| | `minimum_object_size` | 指定存储在磁盘缓存中的文件最小大小（KB）。任何比此小的文件都不会被保存。默认值为 0KB。 |

## 在 SLES 上实现应用层网关

| 章节 | 标签 | 描述 |

| --- | --- | --- |

| | `maximum_object_size_in_memory` | 指定存储在 RAM 缓存中的文件最大大小（KB）。任何大于此的文件都不会保留在 RAM 中。默认值为 8KB。 |

| 日志文件路径和缓存目录 | `cache_dir` | 指定文件系统中用于存储缓存文件的目录。语法如下：`cache_dir type size path L1 L2`。`type` 指定了 Squid 使用的存储格式。默认是 `ufs`。`path` 选项指定缓存所在的目录。默认是 `/var/squid/cache`。`size` 选项指定你想要分配给缓存的空间。默认是 100MB（太小了）。`L1` 选项指定了缓存目录中创建的第一级子目录数量。默认是 16。`L2` 选项指定了缓存目录中创建的二级子目录数量。默认是 256。 |

| | `cache_access_log` | 指定 Squid 访问日志的位置和名称。默认是 `/var/log/squid/access.log`。 |

| | `cache_log` | 指定 Squid 日志文件的位置。默认是 `/var/log/squid/cache.log`。 |

| 管理参数 | `cache_mgr` | 指定管理员的电子邮件。 |

| | `cache_effective_user` | 如果由 root 启动 Squid，此参数定义用户。 |

| | `cache_effective_group` | 如果由 root 启动 Squid，此参数定义组。 |

## 第 10 章：实现数据包过滤防火墙

在配置 Squid 时，你首先需要设置几个基本标签，以控制服务的运行方式。再次，有很多标签；但是，大多数标签的默认值可以满足我们的需求。你可能需要自定义的标签（以及你在 CLE 9 认证中需要了解的标签）如表 10-1：

### Network section (in `/etc/squid/squid.conf`)

`/etc/squid/squid.conf` 中的 Network 部分：

```
NETWORK OPTIONS
  TAG: http_port
    Usage: hostname:port
    1.2.3.4:port
```

Squid 监听 HTTP 客户端请求的套接字地址。可以指定多个套接字地址：

三种形式：仅端口、带端口的主名以及IP 地址。如果你指定了主机名或 IP 地址，Squid 将套接字绑定到特定的地址。这替换了旧的 'tcp, incoming address' 选项。很可能，你不需要绑定到特定的地址，所以你可以仅使用端口号

`/squid.conf` (lines 13-75/360)

好消息是，大多数标签都有与其关联的默认值。这些值中的大多数适用于基本安装。我们将深入使用 `squid.conf` 文件的许多部分。首先，我们需要查看一些基础配置参数。

## 基础配置标签

在配置 Squid 时，你首先需要设置几个基本标签，以控制服务的运行方式。再次，有很多标签；但是，大多数标签的默认值可以满足我们的需求。你可能需要自定义的标签（以及你在 CLE 9 认证中需要了解的标签）如表 10-1：

### 配置 ACLs

Squid 访问控制列表 (ACLs) 也配置在 `squid.conf` 中。此部分显示在 10.42。

`acl` 的语法为：

```
acl name type
```

`name` 选项是你为 acl 定义的名称。你指定的 `type` 取决于 acl。考虑以下 acl 标签：

`acl MySubnet src 192.168.1.0/24`

此标签定义了一个名为 `MySubnet` 的 acl。acl 类型是源系统 IP 地址。条件是任何位于 192.168.1.0 子网且掩码为 255.255.255.0 的系统。注意 acl 并没有说做什么，它只是定义了条件。

要指定对 acl 执行什么，你需要使用 `http_access` 标签。该标签用于定义应用于你定义的 acl 的实际规则。`http_access` 标签的语法如下：

```
http_access allow|deny acl_name
```

本质上，你使用 `acl` 标签定义一个 acl，然后使用 `http_access` 标签指定当引用的 acl 条件满足时该做什么。

### 提示

你可以在条件部分指定多个值。只需在它们之间留空格即可。你可以为同一个 acl 名称使用多个 `acl` 标签，为 acl 的条件部分定义多个值。

## 第 10 章：在 SLES 9 上实现包过滤防火墙

```
acl MySubnet src 192.168.1.0/24
http_access allow MySubnet
```

这将配置 Squid，允许任何 IP 地址为 192.168.1.x 且子网掩码为 255.255.255.0 的系统访问代理服务器。

在使用 `acl` 和 `http_access` 标签时，至关重要的一点是要理解 `squid.conf` 文件中 `acl` 标签的顺序非常重要。你可以按照你喜欢的顺序将它们放在文件的任何位置，只要它们出现在你的 `http_access` 标签之前即可。

然而，`squid.conf` 文件中 `http_access` 标签的顺序是绝对重要的。事实上，它是至关重要的。因为当 Squid 接收来自客户端的入站流量时，它按照标签在文件中出现的顺序来处理 `http_access` 标签。

一旦 Squid 找到匹配的 `http_access` 标签，它就会停止，不再处理文件中剩余的 `http_access` 标签。为了节省处理时间，你应该将最常用的 `http_access` 规则放在前面，将较冷门的 `http_access` 规则放在后面。

### 提示

如果 Squid 处理了所有 `http_access` 规则但没有找到任何匹配项，它将应用文件中最后一个访问规则完全相反的规则。因此，你应该始终在列表末尾包含一个 `deny all`（拒绝所有）或 `allow`（允许）规则，以确保未经授权的流量无法通过。

`squid.conf` 文件包含一组默认的 acl 和规则。在设置初始环境时，你可能应该保持这些设置不变。这些默认设置所示：

```conf
#推荐的最小配置：
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl to_localhost dst 127.0.0.0/8
acl SSL_ports port 463
acl Safe_ports port 80      # http
acl Safe_ports port 21      # ftp
acl Safe_ports port 443 563  # https, sews
acl Safe_ports port 70      # gopher
acl Safe_ports port 210     # wais
acl Safe_ports port 1025-65535 # 未注册
acl Safe_ports port 280     # http-mgmt
acl Safe_ports port 488     # gss-http
acl Safe_ports port 591     # filemaker
acl Safe_ports port 777     # multiling http
acl CONNECT method CONNECT
```

## 在 SLES 上实现应用级网关

```conf
#推荐的最小 cachemgr 配置：
# 仅允许 localhost 访问 cachemgr
http_access allow manager localhost
http_access deny manager
# 拒绝到未知端口的请求
http_access deny !Safe_ports
# 禁止 CONNECT 到非 SSL 端口
http_access deny CONNECT !SSL_ports
http_access allow localhost
# 最后拒绝对此代理的所有其他访问
http_access deny all
```

注意，此配置定义了以下 acl：

- `all`
- `manager`
- `localhost`
- `Safe_ports`
- `CONNECT`

`CONNECT` acl 可能会让人有点困惑。注意它指定了一个名为 `CONNECT` 的方法。Squid 使用此方法直接通过代理服务器连接安全的 HTTP 请求。由于 HTTPS 通信的敏感性，Squid 不缓存它们。相反，它只是直接将它们透通过。

`http_access deny CONNECT SSL_ports` 规则拒绝所有直接通过代理服务器连接的尝试，除非是在 `Safe_ports` acl 中定义的（`acl Safe_ports port 443 563`），该 acl 指定了目标主机上的 443 和 563 端口。

此外，注意为这些 acl 定义的规则按以下顺序执行这些任务：

- 缓存管理员只能从本地主机访问代理。
- 拒绝对未知端口的请求。注意，这是通过在 `http_access` 标签的 `Safe_ports` acl 名称之前放置 `!` 实现的。该字符表示“非”。因此，该规则拒绝任何未包含在 `Safe_ports` acl 中的端口。
- 允许访问 SSL 端口。
- 允许从本地主机访问。
- 拒绝所有其他流量。

## 第 10 章：在 SLES 9 上实现包过滤防火墙

### 提示

记住最后一条规则应该是 `deny all` 或 `allow all`，以确保未经授权的流量不会溜之隙。

如果你仔细阅读这些规则，你会发现开箱即用的情况下 Squid 几乎是完全锁定的。只允许本地机器上的用户访问。因此，为了在网络环境中运行 Squid，你需要在 `squid.conf` 中添加以下 acl：

`acl our_networks src_subnet/your_mask`

例如，如果你想为网络网段 192.168.2.0 提供访问权限，子网掩码为 255.255.255.0/24：

`acl our_networks src 192.168.2.0/24`

这设置了 acl；接下来你需要配置规则。如果你向下滚动 `squid.conf` 到一半处，你会看到一个插入允许访问规则的好位置，如图 10.44 所示。

## 图 10.44

插入允许访问的规则。

```conf
# 拒绝到未知端口的请求
http_access deny !Safe_ports
# 禁止 CONNECT 到非 SSL 端口
http_access deny CONNECT !SSL_ports
# 最后拒绝对此代理的所有其他访问
http_access deny all
```

注意，文件已经包含了一个准备好的 `http_access` 标签。

`http_access allow all`

## 在 SLES 上实现应用级网关

完成后，你可以使用 `squid restart` 命令重启 Squid，基础系统就绪了。然而，注意此配置与我们在本章介绍的通用代理并没有太大。访问是通过 IP 地址和端口号控制的。缺少了什么？认证！

使用 Squid 这种高级代理的关键优势之一是你可以让用户在使用代理之前提供用户名和密码。这让你对谁可以访问代理具有巨大的控制力。

Squid 使用的认证机制在 `squid.conf` 的外部程序选项中进行配置。Squid 可以使用基础认证（使用系统账户存储）、摘要认证（使用其自己的用户账户数据库）或微软的 NTLM 认证过程。`squid.conf` 文件包含了示例代码，你可以取消注释并使用它们来配置用户。这些行如图 10.45 所示

## 图 10.45

认证示例行。

```conf
#推荐的最小配置：
# auth_param basic program (取消注释并完成此行)
# auth_param basic children 5
# auth_param basic realm proxy-caching web server
# auth_param digest realm_interval 7 minutes
# auth_param digest nonce max_duration 30 minutes
# auth_param digest nonce max_count 50
# auth_param ntlm proxy-caching web server
# auth_param ntlm program (取消注释并完成此行以激活)
# auth_param ntlm children 5
# auth_param ntlm max_challenge 0
# auth_param ntlm limit 2 minutes
# auth_param ntlm use statistics off
```

## 配置 Squid 认证

如果 Squid 运行在存储用户账户服务器上，你可以配置基础认证使用主机的 PAM 来认证用户。要实现此操作，你首先需要取消注释行：

```conf
auth_param basic program (取消注释并完成此行)
```

# 第 10 章：使用 SLES 9 实现包过滤防火墙

此行定义了基础认证机制将使用什么程序来验证用户身份。要使用 PAM，你需要指定 Squid 使用 `pam_auth` 程序。你需要编辑前面的行，使其内容如下所示：

`auth_param basic program /usr/sbin/pam_auth`

接下来，你需要指定应该并发运行多少个后台认证进程。通常情况下，五个进程就足够了；但是，如果你的代理服务器被频繁使用，你可能需要增加此值。实现此目的的行位于你的 `squid.conf` 文件中，如下：

`auth_param basic children 5`

接下来，我们必须定义认证将服务的领域（realm）。这听起来很困惑，但其实并非如此。领域仅仅是指提供认证的服务。在这种情况下，它就是 Squid 代理缓存 Web 服务器。实现此目的的行位于你的 `squid.conf` 文件中，并且已经取消了注释。它的内容如下：

`auth_param basic realm Squid proxy-caching web server`

接下来，你需要指定用户提供的凭据在 Squid 系统中有效期多久。实现此目的的行在你的 `squid.conf` 文件中，并且已经取消了注释。它的内容如下：

`auth_param basic credentialsttl 2 hours`

2 小时的默认值通常足够了。

你的工作还没有完成。你刚刚设置的标签仅针对认证系统。它们并没有真正验证用户。为了实现这一点，我们必须回到 `squid.conf` 中的 acls 和规则部分，并配置系统来验证用户。

首先，我们需要创建一个 acl 来列出允许使用代理的用户。这是通过使用 `proxy_auth` 类型完成的。其语法为 `acl name proxy_auth REQUIRED`。例如：

```
acl MyUsers proxy_auth REQUIRED
```

**注意**

`REQUIRED` 条件用于指定使用账户存储器中的所有用户。如果你只想让某些用户能够通过认证并使用代理，可以将 `REQUIRED` 替换为特定用户列表（用空格隔开），例如 `jcorry dcoughanux tux`。

最后，你需要添加一条规则，允许经过身份验证的用户访问代理。这的操作方法与之前讨论的相同。例如，使用上述 acl，你可以输入：

```
http_access allow MyUsers
```

记住，`http_access` 规则是按照它们在文件中出现的顺序进行处理的。你可能想尽早检查认证情况，因此上述规则应该出现在你规则列表的第一位（或接近第一位）。

我们在这里要讨论的 Squid 配置的最后一个元素是如何过滤内容。让我们接下来处理这一部分。

# 使用 SQUID 过滤内容

除了用户认证外，特定协议代理与通用代理相比的另一个显著优势是，它们可以过滤通过代理的内容。这对于 HTTP 代理来说特别有用且重要。

内容过滤在职场中正成为日益日益的问题。在 20 世纪 90 年代初，当桌面首次连接到互联网时，大多数机构的通用可接受策略是告诉员工确保他们只将其用于工作相关目的。基本上，这是一套基于信誉的制度。
