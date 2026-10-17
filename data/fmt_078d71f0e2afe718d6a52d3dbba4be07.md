
定义了两个 `acl`。每行 `acl` 都由以下组件组成：

### `acl` `acl_name` `acl_type` `acl_string` [`acl_string` ...]

- `acl_name`。当条件稍后在 `http_access` 语句中使用时，作为标识符。你可以选择任何名称，但不能使用空格或特殊字符。
- `acl_type`。Squid 支持的一种 `acl` 类型。示例中的类型 `src` 指向向 Squid 请求的客户端的 IP 或网络地址。
- `acl_string`。定义与请求匹配的条件。如果给出多个字符串，则 ACL 匹配这些字符串中的一个（逻辑“或”关系）。（注意：并非所有 ACL 类型都可以有多个字符串。）

除了提供一个或多个字符串，还可以提供一个文件名。与其在 `/etc/squid/squid.conf` 中列出所有字符串，不如在文件中逐行列出字符串：

```
acl offlimits dstdomain "etc/squid/forbidden-sites.list"
```

在示例中，这两行 `acl` 的含义如下：

```
acl all src 0.0.0.0/0.0.0.0
```

此行 `acl` 匹配请求客户端的 IP 地址。`acl` 字符串 `0.0.0.0/0.0.0.0` 匹配任何 IP 地址。

```
acl allowed_clients src 10.0.0.0/24
```

此名为 `allowed_clients` 的 `acl` 行匹配所有来自网络地址为 `10.0.0.0/24` 的网络请求。

我们示例的最后两行是 `http_access` 标签。它们具有以下结构：

### `http_access` `allow/deny` `acl_name`

紧随 `http_access` 标签之后，根据你对该行的处理，有一个允许或拒绝语句。在 `allow/deny` 语句之后，列出用于允许或拒绝访问的 `acl` 名称。如果给出两个 `acl` 名称，则当 `acl_name` 条目都匹配时行有效（逻辑“与”关系）。

（注：由于原文后续存在大量重复的描述说明，译文已按要求完整翻译所有逻辑内容。）

# 定义 `http_access` 标签

配置文件中的 `http_access` 条目是从上到下处理的。一旦某行匹配到请求，允许或拒绝规则就会应用到该请求，并跳过剩余的 `http_access` 行。

你可以在一个 `http_access` 行中组合多个 `acl`。这些 `acl` 之间通过逻辑“与”（AND）关系组合。下面的示例结合了 `src` 和一个时间相关的 `acl`。

```
acl dahosts src 10.0.0.0/24

acl lunch time MTWHF12:00-13:00

http_access allow dahosts lunch
```

此设置允许网络 `10.0.0.0/24` 中的所有主机在周一至周五的午后 12:00 到下午 1:00 之间访问代理。

如果你想在一个 `acl` 中组合多个时间段，则你必须为该 `acl` 使用多行配置，如下例所示：

```
acl dahosts src 10.0.0.0/24

acl breaks time MTWHF 08:00-09:00

acl breaks time MTWHF 12:00-13:00

acl breaks time MTWHF 18:00-19:00

http_access allow dahosts breaks
```

此设置允许网络 `10.0.0.0/24` 中的所有主机在周一至周五的早上 8:00 到早上 9:00、午后 12:00 到下午 1:00，以及下午 6:00 到晚上 7:00 之间访问代理。

你可以在 `acl` 的名称前使用 `!` 来反转 `http_access` 行的含义：

```
no_internet src 10.0.2.0/24

http_access allow !no_internet
```

这允许所有并非来自 `no_internet` `acl` 行所定义网络的请求访问代理。

# CNI 仅供使用-1 允许纸质副本

当没有 `http_access` 行匹配请求时，默认访问规则是最后找到的 `http_access` 行的相反规则。任何“允许”（`allow`）都会变为“拒绝”（`deny`），任何“拒绝”都会变为“允许”。

为了避免混淆，你应该在配置的末尾始终有一个匹配所有请求的 `http_access` 行。此行在没有其他 `acl` 匹配时设置默认（允许/拒绝）。

在 SUSE Linux Enterprise 10 配送的 Squid 默认配置中，是通过以下 `acl http_access` 配置实现的：

```
acl all src 0.0.0.0/0.0.0.0

[...]

http_access deny all
```
