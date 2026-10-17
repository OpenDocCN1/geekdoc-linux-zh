
![](img/b7f4ef3c9bdffc8caed3395478c04bab_29_0.png)

根域域的 DNS 服务器在名称解析中起着至关重要的作用。为了缓解查询带来的服务器负载，每个 DNS 服务器都会将其从其他名称服务器接收到的信息存储在缓存中。当进行查询时，这些信息会被直接发送，而无需重新查询根 DNS 服务器。然而，尽管有这种缓存机制，根 DNS 服务器仍然非常繁忙。每秒数千次的查询并不寻常。

## 目标 2

## 安装并配置 BIND 服务器软件

要运行 DNS 服务器，你需要安装以下软件包：

- `bind`。BIND 服务器软件（SUSE Linux Enterprise Server 10 中的版本为 9.3）
- `bind-chroot`。为 BIND 服务器提供的 chroot 环境
- `bind-utils`。用于查询和测试 BIND 的实用程序（包含在标准安装中）

在启动 DNS 服务器之前，你必须进行一些基础配置更改。完成配置后，可以使用以下命令启动服务器：

```
rcnamed start
```

要停止运行的服务器，使用以下命令：

```
rcnamed stop
```

要让 DNS 服务器在启动时自动启动，使用以下命令：

```
inserver named
```

这会在运行级别目录中创建必要的链接。

默认情况下，名称服务器在 `/etc/sysconfig/named` 中的 chroot 环境中运行（`NAMED_RUN_CHROOTED="yes"`）。

出于安全考虑，应该始终使用 chroot。

![](img/b7f4ef3c9bdffc8caed3395478c04bab_30_0.png)

所有相关文件（如果在 `/etc/sysconfig/named` 中已指定）都会被复制到 `/var/lib/named/` 中相应的子目录中。例如，BIND 配置文件 `/etc/named.conf` 被复制到 `/var/lib/named/etc/named.conf`。要禁用 chroot 环境，请将变量设置为 no。

## 目标 3

## 配置 DNS 服务器

每种类型 DNS 服务器的配置略有不同。在本目标中，将讨论以下内容：

- 配置仅缓存的 DNS 服务器 (Caching-Only DNS Server)
- 为你的域名配置主服务器
- 配置一个或多个从服务器

## 配置仅缓存的 DNS 服务器

仅缓存的 DNS 服务器不管理自己的数据库，而仅仅接受查询并将它们转发到其他 DNS 服务器。回复会被保存在缓存中。

DNS 服务器配置定义在 `/etc/named.conf` 文件中。你可以使用与 DNS 包一起安装的示例文件作为仅缓存服务器的配置文件。

以下示例显示了简单配置的开头：

```
# /etc/named.conf: 名称服务器的配置 (BIND9)
## 全局选项
options
{
## 数据库文件位于哪个目录？
#
    directory "/var/lib/named";
};
```

以井号 (`#`) 开头的行是注释，会被忽略。

全局选项定义在文件开头的 `options` 块中。`directory` 选项指定了数据库文件（或区域文件）所在的目录。通常，这是 `/var/lib/named/`。

使用 `directory` 选项，你可以使用相对路径指定数据库文件的文件名（不需要绝对路径）。

全局选项之后是为 DNS 服务器管理的域配置的数据库文件定义。对于基础 DNS 服务器功能（例如仅缓存服务器提供的功能），需要若干条目。

每个 DNS 服务器需要三个条目：

- 根 DNS 服务器的条目（BIND 9 不需要，因为它在软件中编译了根 DNS 服务器列表）。
- 本地主机 localhost 的正向解析
- 网络 127.0.0.0 (localhost) 的反向解析

以下是这些条目的示例：

```
## 根名称服务器的条目
zone "." in {
    type hint;
    file "root.hint";
};
#
# localhost 的正向解析
#
zone "localhost" in {
    type master;
    file "localhost.zone";
};
#
# localhost 的反向解析
#
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "127.0.0.zone";
};
```

根 DNS 服务器的区域条目包含一个指向根 DNS 服务器地址的文件。`root.hint` 在安装 `bind` 软件包时会在 `/var/lib/named/` 目录中生成。

用于解析 localhost 的两个文件在安装期间也会生成。这些文件的结构将在稍后解释。

从向根服务器查询开始每个名称解析请求可能会非常慢。如果这些请求转发到一个缓存中含有大量信息的名称服务器（例如，你的互联网服务提供商的名称服务器），在大多数情况下处理过程将快得多。

你可以在 `/etc/named.conf` 文件的 `options` 块中定义这些 DNS 服务器，如下：

```
options {
  directory "/var/lib/named";
  forwarders {
    10.0.0.254;
  };
};
```

你可以输入最多三个 DNS 服务器地址。本地 DNS 服务器无法解析的查询将转发到指定的 DNS 服务器之一。

如果无法访问这些 DNS 服务器，查询将直接发送到根 DNS 服务器。

## 为你的域名配置主服务器

为你的域名配置主服务器，需要执行以下任务：

- 调整主配置文件
- 创建区域文件
- 创建额外的资源记录

## 调整主配置文件

你可以调整仅缓存 DNS 服务器的配置以包含自己的信息。

## 使用 BIND 配置 DNS 服务器

该配置已经包含了根服务器的目录和转发器条目（可以省略）。

区域选项后面是该 DNS 服务器服务的域数据库文件（或区域文件）。对于每个域，至少需要两个文件：

- 用于正向解析的文件（将 IP 地址映射到主机名）
- 用于反向解析的文件（将主机名映射到 IP 地址）

如果属于多个子集，则必须为这些网络中的每一个网络创建一个文件。

每个定义都以 `zone` 开头（这就是为什么数据库文件被称为区域文件），随后是该区域的名称。

对于正向解析，这总是域名。对于反向解析，必须反转给出 IP 前缀（`10.0.0.` 变为 `0.0.10.`），加上后缀 `in-addr.arpa`（`0.0.10.in-addr.arpa`）。

区域名称总是跟着一个 `in`。（其他命名空间几乎从未使用。）

括号中的文本定义了该区域的 DNS 服务器类型（例如 `master`）以及区域文件名。

域名 `digitalairlines.com` 和网络 `10.0.0.0/24` 的条目所示：

```
#
# 域名 digitalairlines.com 的正向解析
#
zone "digitalairlines.com" in {
  type master;
  file "master/digitalairlines.com.zone";
}
# 网络 10.0.0.0 的反向解析
zone "0.0.10.in-addr.arpa" in {
  type master;
  file "master/10.0.0.zone"
}
```

## 创建区域文件

用于 localhost 的两个文件和根 DNS 服务器的文件始终包含在安装中。你不需要更改这些文件；但是你必须创建实际域所需的文件。

`/var/lib/named/master/` 子目录用于主服务器的数据库文件。

手动创建区域文件需要以下内容：

- 文件结构
- `/var/lib/named/master/digitalairlines.com.zone`
- `/var/lib/named/master/10.0.0.zone`
- `/var/lib/named/master/localhost.zone`
- `/var/lib/named/master/127.0.0.zone`

### 文件结构

每个数据库文件都由一系列条目（或资源记录）组成。这些记录的语法始终如下：

`reference [TTL] class type value`

以下内容描述了记录的每个部分：

- **reference（引用）**。记录所指引的引用。它可以是一个域名（或子域名）或一台独立的计算机（名称或 IP 地址）。
- **TTL**。记录的生存时间。如果不存在此项，则将使用默认 TTL 值。它决定了其他名称服务器如何在缓存中存储此信息。
- **class（类）**。记录的类别。对于 TCP/IP 网络，类别始终为 `IN`（互联网）。
- **type（类型）**。记录的类型。最重要的类型列在下表中。
- **value（值）**。记录的值。该值取决于后续列出的记录类型：

| 记录类型 | 含义 | 值 |
|---|---|---|
| SOA | 权威机构起始（权威机构的术语） | 域名的参数 |
| NS | 名称服务器 | 该域名一个 DNS 服务器的名称或 IP 地址 |
| MX | 邮件交换器 | 该域名邮件服务器的名称（或 IP 地址）和优先级 |
| A | 地址 | 计算机的 IP 地址 |
| PTR | 指针 | 计算机的名称 |

### 表 1-2（续表）

| 记录类型 | 含义 | 值 |
|---|---|---|
| CNAME | 规范名称 | 计算机的别名 |

单个条目必须从第一列的引用开始。如果条目不是从第一列开始，则引用将从上一个条目获取。

### 文件 `/var/lib/named/master/digitalairlines.com.zone`

与早期版本的 BIND 不同，BIND 9 要求在开头为所有信息指定一个默认 TTL。每当条目没有显式给出 TTL 时，就会使用此值。

你通过以下指令定义 TTL：

```
;
; 定义一个标准的生存时间，这里是：两天
;
$TTL 172800
```

在此文件中，分号 `;` 被用作注释符号。

在此示例中，TTL 以秒为单位给出。也可以以其他单位给出，例如 `2D` 表示两天。其他单位还有 `M`（分钟）、`H`（小时）和 `W`（周）。

随后是 SOA（权威机构起始）条目的定义，它指定了哪个 DNS 服务器拥有该域名的权威：

```
;
; SOA 条目
digitalairlines.com IN SOA dal.digitalairlines.com
hostmaster.digitalairlines.com. (
    2004092601; 序列号
    1D ; 刷新（一天）
    2H ; 重试（两小时）
    1W ; 过期（一周）
    3H ; “负”有效期（三小时）
)
```

该条目所指的域名（示例中为 `digitalairlines.com`）首先列出。如果名称末尾没有点，则会添加域名，这在此处会导致错误。

DNS 服务器的名称列在 SOA 条目之后（示例中为末尾带点的 `da1.digitalairlines.com.`）。或者，你也可以写 `dal`，域名 `digitalairlines.com` 会在名称之后添加。

接下来是负责 DNS 服务器管理的人的电子邮件地址。电子邮件地址中通常使用的 `@` 必须替换为点（因此此示例中的电子邮件地址为 `hostmaster.digitalairlines.com`）。这是必要的，因为 `@` 作为缩写具有特殊含义。

建议在此处使用通用的电子邮件地址（例如 `hostmaster@digitalairlines.com`），而不是个人电子邮件地址。

下一个条目是序列号。可以使用任何数字，通常在此处使用日期和版本号。在对此文件中的数据进行任何更改后，必须增加序列号。

从服务器使用此数字来确定它们是否需要复制此区域文件。如果主服务器上的序列号大于从服务器上的序列号，则复制该文件。

序列号之后是时间信息（这里列出的前三个条目仅对从服务器重要）：

- 第一个条目使从服务器在经过一段时间后查询主服务器，以查看是否有新版本的文件（示例中为 `1D`，即一天）。
- 如果从服务器无法到达主服务器，则下一个条目指定了应以多大的间隔进行新的尝试（示例中为 `2H`，即两小时）。
- 如果较长时间未连接到主服务器，第三个条目指定了从服务器何时应该丢弃关于该区域的信息（示例中为 `1W`，即一周）。
- 这里的基本思想是，不传递任何信息也比传递过时信息要好。

第四个条目定义了 DNS 服务器的负响应的有效时间。每个请求服务器都会将其响应存储在缓存中，即使计算机名称无法解析（示例中为 `3H`，即三小时）。

这些时间定义之后是作为该域名 DNS 服务器的计算机的名称或 IP 地址。在所有情况下，必须在此处输入主服务器。如果使用了从服务器，它们也应该输入在以下位置：

```
; 名称服务器条目
; digitalairlines.com. IN NS da1.digitalairlines.com.
;                 IN NS da2.digitalairlines.com.
```

此处可以省略域名。然后将从 SOA 条目中获取域名。

在该文件的末尾是分配给主机的 IP 地址。

在 `/var/lib/named/master/10.0.zone` 中，分配给主机名称的地址使用 A 条目，如下所示：

```
; 分配给主机名称的 IP 地址
dal10   IN A 10.0.0.10
dal12   IN A 10.0.0.12
dal13   IN A 10.0.0.13
...
14     IN A 10.0.0.14
;
dal254 IN A 10.0.0.254
dal2    IN A 10.0.0.2
```

### `/var/lib/named/master/10.0.zone`

反向解析文件包含与正向解析文件类似的条目。文件的开头是默认 TTL 的定义和 SOA 条目。

在 SOA 和 NS 条目中，网络地址以反序写入：

```
; 域名 digital airlines.com 的数据库文件
; 网络 10.0 的反向解析
;
; 定义默认 TTL，这里是：两天
;
$TTL 172800
;
; SOA 条目
;
0.10.in-addr.arpa. SOA root (d. adams)
      42 ; 刷新
      2D ; 重试
      4H ; 过期
      6W ; 最小
      1W )

; 名称服务器条目
;
IN NS dal.digitalairlines.com.
```

### `/var/lib/named/master/localhost.zone`

对于本地计算机，必须存在以下两个文件。它们在安装期间自动创建，不应修改。

以下是 `/var/lib/named/master/localhost.zone` 的示例：

```
$TTL 1W

@ IN SOA root (d. adams)

      42 ; 刷新

      2D ; 重试

      4H ; 过期

      6W ; 最小

      1W )

@

IN A 127.0.0.1
```
