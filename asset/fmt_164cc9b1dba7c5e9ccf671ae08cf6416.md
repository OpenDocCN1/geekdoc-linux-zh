
# 名称服务 (DNS) 第 11 章

## `resolv.conf`

`/etc/resolv.conf` 文件可能包含五种指令：

- `domain`
- `nameserver`
- `sortlist`
- `options`

这些关键字都必须从第一列开始。`domain` 指令用于为机器设置本地或默认域名。在 `/etc/resolv.conf` 中放置 `domain` 指令将覆盖你可能在 `hostname` 中设置的域名。此指令由第一列开始的关键字组成，构造如下：

```
domain eng.umd.edu
```

`search` 指令用于指定要搜索的域名列表和顺序。列表可以包含一到六个域名。搜索列表中的第一个域名成为默认域名，如果它在 `domain` 指令之后，则会覆盖 `domain` 指令。这两个指令中较后出现的那个将覆盖另一个。因此，`search` 和 `domain` 指令是互斥的。这是一个 `search` 指令的示例：

```
search eng.umd.edu comp.umd.edu umd.edu
```

通过该语句，解析器被引导首先在 `eng.umd.edu` 中搜索该主机名。如果没有找到条目，则将搜索 `comp.umd.edu`，然后是 `umd.edu`。

`nameserver` 指令向解析器指定名称服务器的 IP 地址，将所有查询发送到该地址。同样，这通常是您的网络、公司或组织内的名称服务器。如果 `resolv.conf` 中没有 `nameserver` 指令，则解析器将尝试连接到本地运行的名称服务器。你可以指定零到三个 `nameserver` 指令。以下是三个指令的示例：

```
nameserver      10.10.13.100
nameserver      10.10.12.100
nameserver      10.10.11.100
```

只有在完全无法从第一个名称服务器接收到有效响应时，才会查询额外的名称服务器。等待响应的默认时间为五秒。五秒后，查询将超时。只有在查询首次超时或解析器从查询中收到网络错误时，才会查询第二个名称服务器。在第二个名称服务器查询超时五秒后，也会查询第三个名称服务器。如果第三个名称服务器也超时，解析器将返回第一个名称服务器并尝试另一轮查询。Solaris 8 在放弃之前最多可进行四轮。Red Hat 7.1 在两轮后放弃。

如果从第一个名称服务器收到的回答为无主机（no host），则不会查询额外的名称服务器。假设从任何其他名称服务器都会收到相同的回答。指定多个名称服务器严格是为了在主名称服务器发生故障时，提供可以连接的备用名称服务器。

`sortlist` 指令是一种优先选择某些网络而非其他网络的方法。这可以用于系统具有多个网络接口的情况——例如，其中一个是千兆以太网接口，另一个是 FDDI 环网接口。具有多个接口的系统 DNS 条目可以定义为在解析器查询时返回所有地址。如果你想使用千兆以太网，则可以在 `sortlist` 中指定它。该指令可以接受多达 10 个不同的网络或子网。以下是一个示例，表示当名称查找向解析器返回多个地址时，优先选择 `10.10.12.0` 网络：

```
sortlist 10.10.12.0
```

我们将讨论的最后一个指令是 `options` 指令。该指令接受以下任何一个内容作为参数：

```
debug
attempts
timeout
```

还有其他几个，但这些是你最可能想要使用的。
通过此行开启 `debug`：

```
options debug
```

然而，只有当系统上的解析器库在编译时开启了调试功能，此选项才有效。如果你尝试解决解析器或 DNS 的问题，此选项也会很有帮助。

`attempts` 指在放弃之前尝试每个名称服务器的次数。最大值为 5。以下是一个值为 3 的示例：

```
options timeout:3
```

`timeout` 指在发送重试之前，等待名称服务器响应的秒数。此数字只能更改遍历整个名称服务器列表的第一轮的超时时间。后续轮将是每个厂商解析器的典型轮次及。以下是一个示例：

```
options timeout:2
```

最后，这是一个典型的 `/etc/resolv.conf` 内容的示例：

```
search eng.umd.edu comp.umd.edu um.edu
nameserver 10.10.12.100
nameserver 10.10.11.100
```

## `nsswitch.conf`

`/etc/nsswitch.conf` 文件可以确定主机名查找方法的顺序。可以使用关键字 `hosts` 来指定顺序。可能查询主机信息的源（在这种情况下，还包括额外的关键字）包括 `dns`、`files`、`nis` 和 `nisplus`。`files` 条目指的是文件 `/etc/hosts`。如果你希望先进行 DNS 名称解析，然后是解析 `/etc/hosts`，则可以在 `nsswitch.conf` 中放置如下的一行：

```
hosts: dns files
```

关于此配置文件的更多信息，请参阅帮助手册（man page）。

## 名称服务器

DNS 方的服务器端涉及在机器上运行 BIND 以为名称查找提供回答。

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_507_0.png)

为站点提供 DNS 服务最好是使用专用机器。这有几个原因。最重要的之一是，名称服务器需要能够快速地响应许多请求。另一个是名称服务器需要一直在线并可用。如果 DNS 服务器还提供其他应用程序或服务，那么应用程序用户与管理员（他们知道机器不能随时重启）之间发生利益冲突的可能性要大得多。对于 DNS 等基本服务，最好始终在除了提供该服务外没有其他用途的机器上运行。这种哲学也使得故障排除变得更加清晰，因为机器上运行内容的范围被清楚地定义了。

## 主服务器和从服务器

为了协助可用性和冗余问题，要求至少有两个名称服务器可用。这对于系统维护目的尤为重要。硬件故障会发生，系统需要进行补丁和升级。运行多个名称服务器可以防止站点完全离线。

## 配置 BIND

BIND 是我们运行的软件包名称。我们启动时首先检查的配置文件称为 `/etc/named.conf`。出于示例目的，我们将构建 `named.conf`。

### 图 11.2 示例区域 eng.umd.edu

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_509_0.png)

我们示例的 `/etc/named.conf` 如下：

```
# 配置文件

options {
    directory "/var/named";
}

zone "eng.umd.edu" in {
    type master;
    file "forward.eng.umd.edu";
}

zone "11.10.10.in-addr.arpa" in {
  type master;
  file "reverse.10.10.11";
};

zone "12.10.10.in-addr.arpa" in {
  type master;
  file "reverse.10.10.12";
};

zone "0.0.127.in-addr.arpa" in {
  type master;
  file "reverse.127.0.0";
};

zone ".* in {
  type hint;
  file "cache.root";
};
```
