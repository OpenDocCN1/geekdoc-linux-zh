
# 创建区域文件

用于 `localhost` 域的两个文件以及根 DNS 服务器的文件包含在安装包中。你不需要修改这些文件；但是你必须为实际域名创建所需的文件。

`/var/lib/named/master/` 目录用于主服务器的数据库文件。

手动创建区域文件，你需要了解以下内容：

- 区域文件结构
- `/var/lib/named/master/digitalairlines.com.zone` 文件
- `/var/lib/named/master/172.17.8.zone` 文件
- `/var/lib/named/master/localhost.zone` 文件
- `/var/lib/named/127.0.0.zone` 文件

# 区域文件结构

区域文件由一系列资源记录组成，紧跟在全局选项之后。记录的语法如下：

- `reference`：查询引用的部分。
- `TTL`：生存时间（Time To Live）。它决定了本地 DNS 服务器在缓存中存储记录多久。如果未显式给出，将使用默认的 `TTL` 值。
- `class`：类。
- `type`：类型。对于互联网，这总是 `IN`。
- `name`：名称。
- `record`：记录。
- `value`：记录的值。

9 记录类型

| 记录类型 | 含义 | 值 |
| :--- | :--- | :--- |
| SOA | 起始 (Start of Authority) | 域的信息 |
| NS | 名称服务器 | 域的服务器 |
| MX | 邮件交换器 | 优先级和邮件服务器 |
| A | 地址 | 计算机地址 |
| AAAA | IPv6 地址 | IPv6 地址 |
| PTR | 指针 | 计算机名 |
| CNAME | 别名 | 别名 |
| TXT | 文本 | 附加信息 |

注意：单个条目通常以域名开始。如果条目没有以域名开始，则继承前一个条目。

# /var/lib/named/master/digitalairlines.zone 文件

在 SOA（Source of Authority）记录定义之后的是序列号（以下三个条目仅用于从服务器）：

- 第一个条目导致从服务器查询主服务器以检查是否有新版本（示例中为 `1D`，即一天）。
- 如果从服务器无法到达主服务器，下一个条目指定重新尝试的间隔（示例中为 `2H`，即两小时）。
- 如果主服务器长时间无法连接，第三个条目指定从服务器何时丢弃信息（示例中为 `1W`，即一周）。
- 第四个条目定义了 DNS 负响应的有效期（示例中为 `3H`，即三小时）。

这些时间定义之后是负责该域的计算机名称或 IP 地址。在所有情况下，必须输入主服务器。如果使用了从服务器，也应该输入它们，如下：

```
; 名称服务器的条目

;digitalairlines.com.      IN NS      dal.digitalairlines.com.

                        IN NS      da2.digitalairlines.com.
```

在此处可以省略域名。然后取前一个条目（SOA 条目）的名称。文件的其余部分列出了分配给计算机名的 IP 地址。这是通过 `A`（地址）条目完成的，如下：

```
; 分配 IP 地址到主机名

;

dal                        IN A      172.17.8.101

da-host                    IN A      172.17.8.1

...
```

# /var/lib/named/master/172.17.8.zone 文件

反向解析的文件包含与正向解析文件相似的条目。在文件的开头是默认 `TTL` 和 SOA 条目的定义。

在 SOA 和 NS 条目中，网络地址的 IP 地址必须以反序写：

```
; 域名 digitalairirlines.com 的数据库文件：
; 网络 172.17.8.0 的反向解析
;
; 默认 TTL 定义，此处为：两天
```

```
; TTL 172800

; SOA 条目

; 8.17.172.in-addr.arpa. IN SOA dal.digitalairirlines.com. hostmaster.digitalairirlines.com. (

    202309020200;

    86400;

    3600;

    604800;

    3600; )
```

### 名称服务器记录
`IN NS dal.digitalairirlines.com.`
`IN NS ns.digitalairirlines.com.`

该文件的其余部分列出了分配给具有 PTR（指针）条目的 IP 地址的主机名，如下：

```
; 主机名分配

1 PTR host.digitalairirlines.com.

10 PTR host.digitalairirlines.com.
```

本地计算机必须存在这两个文件。它们是 bind 软件包的一部分，不应修改。

### /var/lib/named/master.zone 文件
以下是 `/var/lib/named/master.zone` 的示例：

```
$TTL 86400

SOA dal.digitalairirlines.com. hostmaster.digitalairirlines.com. ( 2023090201 2D 3H 1W 12H )

IN NS ns.digitalairirlines.com.

IN A 172.17.8.1
```

在此示例中，“@” 字符被用作缩写（这就是为什么在电子邮件地址中必须将其替换为点的原因）。使用“@”代替域名会调用系统读取 `/etc/named.conf` 文件，以查看哪个域名是负责解析的。

### 为域名定义邮件服务器
为了能够使用 `user@digitalairirlines.com` 格式的电子邮件地址，必须定义该域名的邮件服务器。这是通过在正向解析数据库文件中 DNS 条目之后添加 MX（邮件交换）条目来实现的

```
digitalairirlines.com.

IN MX 0 mail.digitalairirlines.com

IN MX 10 backup.digitalairirlines.com
```

如果发送到地址 `user@digitalairirlines.com`，发送邮件的计算机会询问 DNS 服务器哪个是邮件服务器，并接收 MX 条目列表。可以列出多个邮件服务器。根据它们的优先级，将决定发送哪封邮件。邮件服务器的优先级由 MX 数字定义；数字越小，优先级越高。在本示例中，`mail.digitalairirlines.com` 的优先级最高。如果无法访问最高优先级的邮件服务器，则使用次高优先级。如果多个邮件服务器的优先级相同，则随机选择其中一个。必须每个邮件服务器都必须创建一个条目。

### 为计算机分配别名
如果你希望通过多个名称访问计算机（例如，通过 `digitalairirlines.com` 和 `www.digitalairirlines.com` 访问某台计算机），则必须提供相应的别名。这些是正向解析数据库文件中的 CNAME（规范名称）条目：

| 名称 | 类型 | 值 |
| :--- | :--- | :--- |
| digitalairirlines.com. | A | 10.0.0.30 |
| www | CNAME | digitalairirlines.com |

注意：域名的邮件服务器名称（MX 条目）不能是别名，因为某些邮件服务器无法正确处理此类情况。

### 从服务器
为了保证可靠运行，除了主服务器外，至少需要一个 DNS 服务器。它从主服务器接收区域信息并可以承担负载。这在 DNS 主服务器不可用时尤为重要。本课程未涵盖从服务器的配置。

### 配置 DNS 客户端
要指示计算机使用特定的 DNS 服务器，必须将信息写入 `/etc/resolv.conf` 文件。可以使用 YaST（在安装期间或之后）或使用任何文本编辑器编辑此文件。`/etc/resolv.conf` 的内容类似于所示：

```
search digitalairirlines.com

nameserver 172.17.8.1
```
